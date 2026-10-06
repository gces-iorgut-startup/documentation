# Contrato da API — BE-05: Solicitação e Aprovação de Agendamentos

| | |
| :--- | :--- |
| **Issue do contrato** | [backend#11](https://github.com/gces-iorgut-startup/backend/issues/11) |
| **Issue de implementação** | [backend#13](https://github.com/gces-iorgut-startup/backend/issues/13) |
| **Controle de acesso** | [backend#12](https://github.com/gces-iorgut-startup/backend/issues/12) (SEC04) |
| **Situação** | Implementado na `main` do backend (PR #17 e PR #16) |
| **Consumidores** | Frontend Web (FE-06) e App Mobile |

## Introdução

Até a BE-05, só a clínica criava agendamentos (`POST /appointments`), que já nasciam com status `SCHEDULED`. Este contrato formaliza o fluxo em que o **tutor solicita** um agendamento pelo Portal do Tutor ou pelo App Mobile, e a **clínica aprova** (atribuindo um veterinário) ou **recusa** (com justificativa).

Todos os exemplos JSON deste documento foram **capturados da API real**: as requisições foram executadas contra o backend, com o banco simulado. Eles podem ser usados diretamente como mocks no frontend e no mobile.

## Máquina de estados

```
               [ Tutor solicita ]
                       │
                       ▼
              ┌──────────────────┐
              │ PENDING_APPROVAL │
              └────────┬─────────┘
                       │
         ┌─────────────┴─────────────┐
         │                           │
  [ Clínica aprova ]          [ Clínica recusa ]
  (atribui vetId)             (informa motivo)
         │                           │
         ▼                           ▼
   ┌───────────┐               ┌──────────┐
   │ SCHEDULED │               │ REJECTED │
   └───────────┘               └──────────┘
```

| Transição | Rota | Efeito |
| :--- | :--- | :--- |
| — → `PENDING_APPROVAL` | `POST /portal/appointments/request` | Cria a solicitação sem veterinário (`vetId: null`) e sem horário de fim (`endDateTime: null`). |
| `PENDING_APPROVAL` → `SCHEDULED` | `PATCH /appointments/:id/approve` | Atribui `vetId`, define `endDateTime` e checa conflito na agenda do veterinário. |
| `PENDING_APPROVAL` → `REJECTED` | `PATCH /appointments/:id/reject` | Grava a justificativa em `cancelReason`. Estado final. |

A partir de `SCHEDULED`, o agendamento segue o ciclo já existente (`IN_PROGRESS`, `COMPLETED`, `CANCELLED`).

### Invariantes

- `vetId` é **obrigatório** nos status `SCHEDULED`, `IN_PROGRESS` e `COMPLETED`. Uma CHECK constraint no banco (`check_vet_id_status`) garante isso.
- `vetId` é **`null`** em `PENDING_APPROVAL` e `REJECTED`. Um `CANCELLED` pode ter `vetId: null` quando a clínica cancela uma solicitação ainda pendente.
- **Cálculo de `endDateTime` na aprovação:**
    - Se for informado, precisa ser estritamente posterior a `dateTime` (senão, 400).
    - Se for omitido, assume a duração padrão de **15 minutos** a partir de `dateTime` (`DEFAULT_APPOINTMENT_DURATION_MS`), a mesma convenção do `POST /appointments`.

## Convenções gerais

### Autenticação

Todas as rotas exigem o access token JWT no header:

```
Authorization: Bearer <accessToken>
```

O perfil (`role`) vem do próprio token: `OWNER`, `VET` ou `TUTOR`.

### Formatos

- **Datas:** strings ISO 8601 em UTC (ex.: `2026-10-15T14:30:00.000Z`).
- **IDs:** UUID v4.
- **Envelope de resposta:** os objetos vêm sempre embrulhados: `{ "appointment": { ... } }` para um item e `{ "appointments": [ ... ] }` para listas.
- **`category`:** `VACCINATION`, `OBSERVATION`, `EXAM` ou `SURGICAL`.
- **`status`:** `PENDING_APPROVAL`, `SCHEDULED`, `IN_PROGRESS`, `COMPLETED`, `CANCELLED` ou `REJECTED`.

### Formatos de erro

A API usa **três formatos** de erro. O frontend deve tratar os três:

| Origem | Quando ocorre | Formato |
| :--- | :--- | :--- |
| Middleware de autenticação e perfil | 401 (token ausente ou inválido) e 403 (perfil não autorizado) nas rotas da clínica | `{ "message": "..." }` |
| Regra de negócio (`AppError`) | 400, 403, 404 e 409 vindos dos casos de uso | `{ "statusCode": 400, "error": "..." }` |
| Validação de schema (Zod) | 422 (campo ausente, tipo ou formato inválido) | `{ "statusCode": 422, "error": "Validation Error", "issues": { "<campo>": ["..."] }, "message": "Erros de validação nos campos" }` |

### Ordem de avaliação

A ordem das checagens muda conforme o grupo de rotas. Isso define qual erro aparece quando há mais de um problema na mesma requisição:

| Grupo | Ordem |
| :--- | :--- |
| Portal (`/portal/...`) | autenticação (401) → validação (422) → regras do caso de uso (403, 404, 400) |
| Clínica (`/appointments/...`) | validação (422) → autenticação (401) → perfil (403) → regras do caso de uso (404, 400, 409) |

**Exemplo:** um `PATCH /appointments/:id/approve` **sem token e com body inválido** retorna **422**, não 401.

## Resumo dos endpoints

| # | Método e rota | Perfil | Sucesso |
| :--- | :--- | :--- | :--- |
| 1 | `POST /portal/appointments/request` | `TUTOR` | `201` |
| 2 | `GET /portal/appointments` | `TUTOR` | `200` |
| 3 | `GET /appointments?status=PENDING_APPROVAL` | `OWNER`, `VET` | `200` |
| 4 | `PATCH /appointments/:id/approve` | `OWNER`, `VET` | `200` |
| 5 | `PATCH /appointments/:id/reject` | `OWNER`, `VET` | `200` |

## 1. `POST /portal/appointments/request`

O tutor solicita um agendamento para um dos seus pets. Ele **não escolhe o veterinário**.

- **Perfil:** `TUTOR`.
- **Alias:** `POST /portal/appointments` tem o mesmo comportamento. A rota principal é `/request`.

### Request body

| Campo | Tipo | Obrigatório | Regra |
| :--- | :--- | :--- | :--- |
| `patientId` | UUID | sim | Pet pertencente ao tutor logado. |
| `category` | enum | sim | `VACCINATION`, `OBSERVATION`, `EXAM` ou `SURGICAL`. |
| `dateTime` | data ISO 8601 | sim | Precisa ser no futuro. |
| `observation` | string | não | Observação livre do tutor. |

```json
{
  "patientId": "66666666-6666-6666-6666-666666666666",
  "category": "VACCINATION",
  "dateTime": "2026-10-15T14:30:00.000Z",
  "observation": "Animal tem histórico de reação alérgica"
}
```

### Resposta `201 Created`

```json
{
  "appointment": {
    "id": "77777777-7777-7777-7777-777777777777",
    "patientId": "66666666-6666-6666-6666-666666666666",
    "vetId": null,
    "dateTime": "2026-10-15T14:30:00.000Z",
    "endDateTime": null,
    "category": "VACCINATION",
    "status": "PENDING_APPROVAL",
    "observation": "Animal tem histórico de reação alérgica",
    "cancelReason": null,
    "createdAt": "2026-10-04T15:00:00.000Z",
    "updatedAt": "2026-10-04T15:00:00.000Z",
    "patient": {
      "id": "66666666-6666-6666-6666-666666666666",
      "name": "Rex",
      "species": "Canino"
    }
  }
}
```

### Erros

| Status | Corpo | Causa |
| :--- | :--- | :--- |
| `401` | `{ "message": "Token inválido ou expirado." }` | Token ausente, inválido ou expirado. |
| `422` | Formato de validação (ver [Catálogo de erros](#catalogo-de-erros)) | `patientId` ausente ou inválido, `category` desconhecida, `dateTime` inválido. |
| `403` | `{ "statusCode": 403, "error": "Acesso restrito ao portal do tutor." }` | Token de `OWNER` ou `VET`. |
| `404` | `{ "statusCode": 404, "error": "Conta de tutor não encontrada." }` | Usuário `TUTOR` sem cadastro de tutor vinculado. |
| `404` | `{ "statusCode": 404, "error": "Paciente não encontrado." }` | `patientId` inexistente. |
| `403` | `{ "statusCode": 403, "error": "Você não tem permissão para solicitar agendamento para este animal." }` | O pet pertence a outro tutor. |
| `400` | `{ "statusCode": 400, "error": "A data do agendamento deve ser futura." }` | `dateTime` no passado ou igual ao instante atual. |

## 2. `GET /portal/appointments`

Lista os agendamentos e as solicitações de **todos os pets do tutor logado**, em **qualquer status**, do mais recente para o mais antigo (`dateTime` decrescente). O tutor usa essa rota para acompanhar se o pedido está pendente, foi aprovado ou foi recusado, e por qual motivo (`cancelReason`).

- **Perfil:** `TUTOR`.
- **Parâmetros:** nenhum.

**Atenção:** esta rota **não inclui o objeto `vet`**, só o `vetId`. Para mostrar o nome do veterinário de uma consulta aprovada, o front precisa resolver o `vetId` por conta própria. Incluir o `vet` aqui está registrado como melhoria.

### Resposta `200 OK`

```json
{
  "appointments": [
    {
      "id": "77777777-7777-7777-7777-777777777777",
      "patientId": "66666666-6666-6666-6666-666666666666",
      "vetId": null,
      "dateTime": "2026-10-15T14:30:00.000Z",
      "endDateTime": null,
      "category": "VACCINATION",
      "status": "REJECTED",
      "observation": "Animal tem histórico de reação alérgica",
      "cancelReason": "Sem disponibilidade de profissionais no horário solicitado.",
      "createdAt": "2026-10-04T15:00:00.000Z",
      "updatedAt": "2026-10-04T15:15:00.000Z",
      "patient": {
        "id": "66666666-6666-6666-6666-666666666666",
        "name": "Rex",
        "species": "Canino"
      }
    },
    {
      "id": "bbbbbbbb-bbbb-bbbb-bbbb-bbbbbbbbbbbb",
      "patientId": "66666666-6666-6666-6666-666666666666",
      "vetId": "33333333-3333-3333-3333-333333333333",
      "dateTime": "2026-10-12T09:00:00.000Z",
      "endDateTime": "2026-10-12T09:15:00.000Z",
      "category": "EXAM",
      "status": "SCHEDULED",
      "observation": null,
      "cancelReason": null,
      "createdAt": "2026-10-04T15:00:00.000Z",
      "updatedAt": "2026-10-04T15:00:00.000Z",
      "patient": {
        "id": "66666666-6666-6666-6666-666666666666",
        "name": "Rex",
        "species": "Canino"
      }
    }
  ]
}
```

### Erros

| Status | Corpo | Causa |
| :--- | :--- | :--- |
| `401` | `{ "message": "Token inválido ou expirado." }` | Token ausente, inválido ou expirado. |
| `403` | `{ "statusCode": 403, "error": "Acesso restrito ao portal do tutor." }` | Token de `OWNER` ou `VET`. |
| `404` | `{ "statusCode": 404, "error": "Conta de tutor não encontrada." }` | Usuário `TUTOR` sem cadastro de tutor vinculado. |

## 3. `GET /appointments?status=PENDING_APPROVAL`

Fila de solicitações da clínica. É a **mesma rota da agenda diária** (`GET /appointments?date=YYYY-MM-DD`), agora com o filtro `status`.

- **Perfil:** `OWNER` ou `VET`.

### Query string

| Parâmetro | Tipo | Obrigatório | Regra |
| :--- | :--- | :--- | :--- |
| `status` | enum | condicional | Qualquer valor de `status`. Quando informado, a lista traz só esse status, de todas as datas, em ordem crescente de `dateTime`. |
| `date` | `YYYY-MM-DD` | condicional | Sem `status`, é obrigatório e retorna a agenda do dia. Com `status`, é opcional e restringe a lista àquele dia. |
| `vetId` | UUID | não | Só se aplica à agenda diária (sem `status`). |

É preciso informar **pelo menos um** entre `date` e `status`.

**Agenda diária:** sem `status`, a rota retorna apenas `SCHEDULED`, `IN_PROGRESS` e `COMPLETED`. Solicitações pendentes e recusadas **não aparecem** na agenda.

### Resposta `200 OK`

```json
{
  "appointments": [
    {
      "id": "77777777-7777-7777-7777-777777777777",
      "patientId": "66666666-6666-6666-6666-666666666666",
      "vetId": null,
      "dateTime": "2026-10-15T14:30:00.000Z",
      "endDateTime": null,
      "category": "VACCINATION",
      "status": "PENDING_APPROVAL",
      "observation": "Animal tem histórico de reação alérgica",
      "cancelReason": null,
      "createdAt": "2026-10-04T15:00:00.000Z",
      "updatedAt": "2026-10-04T15:00:00.000Z",
      "patient": {
        "id": "66666666-6666-6666-6666-666666666666",
        "name": "Rex",
        "species": "Canino",
        "clinicId": "11111111-1111-1111-1111-111111111111",
        "photoUrl": null
      },
      "vet": null
    }
  ]
}
```

### Erros

| Status | Corpo | Causa |
| :--- | :--- | :--- |
| `422` | `issues: { "date": ["Informe date ou status"] }` | Nem `date` nem `status` informados. |
| `422` | `issues: { "status": ["Invalid enum value. ..."] }` | `status` desconhecido. |
| `401` | `{ "message": "Token inválido ou expirado." }` | Token ausente, inválido ou expirado. |
| `403` | `{ "message": "Acesso não autorizado para este perfil." }` | Token de `TUTOR`. |

## 4. `PATCH /appointments/:id/approve`

A clínica aprova a solicitação e atribui o veterinário responsável.

- **Perfil:** `OWNER` ou `VET`.
- **Parâmetro de rota:** `id` (UUID do agendamento).

### Request body

| Campo | Tipo | Obrigatório | Regra |
| :--- | :--- | :--- | :--- |
| `vetId` | UUID | sim | Usuário `OWNER` ou `VET` da mesma clínica. |
| `endDateTime` | data ISO 8601 | não | Posterior a `dateTime`. Se omitido, usa `dateTime` + 15 min. |

```json
{
  "vetId": "33333333-3333-3333-3333-333333333333",
  "endDateTime": "2026-10-15T15:00:00.000Z"
}
```

### Regras, na ordem em que são verificadas

1. O agendamento precisa existir e ser da clínica do usuário (senão, 404).
2. O status precisa ser `PENDING_APPROVAL` (senão, 400).
3. O `dateTime` solicitado precisa ser no futuro (senão, 400).
4. O veterinário precisa existir, ser da mesma clínica e não ter perfil `TUTOR` (senão, 404).
5. Se informado, `endDateTime` precisa ser maior que `dateTime` (senão, 400).
6. O veterinário não pode ter consulta `SCHEDULED` ou `IN_PROGRESS` no intervalo (senão, 409). Outras solicitações pendentes no mesmo horário **não** contam como conflito.

### Resposta `200 OK`

```json
{
  "appointment": {
    "id": "77777777-7777-7777-7777-777777777777",
    "patientId": "66666666-6666-6666-6666-666666666666",
    "vetId": "33333333-3333-3333-3333-333333333333",
    "dateTime": "2026-10-15T14:30:00.000Z",
    "endDateTime": "2026-10-15T15:00:00.000Z",
    "category": "VACCINATION",
    "status": "SCHEDULED",
    "observation": "Animal tem histórico de reação alérgica",
    "cancelReason": null,
    "createdAt": "2026-10-04T15:00:00.000Z",
    "updatedAt": "2026-10-04T15:10:00.000Z",
    "patient": {
      "id": "66666666-6666-6666-6666-666666666666",
      "name": "Rex",
      "species": "Canino",
      "clinicId": "11111111-1111-1111-1111-111111111111",
      "photoUrl": null
    },
    "vet": {
      "id": "33333333-3333-3333-3333-333333333333",
      "name": "Dra. Veterinária"
    }
  }
}
```

### Erros

| Status | Corpo | Causa |
| :--- | :--- | :--- |
| `422` | `issues: { "vetId": ["Required"] }` | `vetId` ausente ou inválido, `endDateTime` inválido, `id` não é UUID. |
| `401` | `{ "message": "Token inválido ou expirado." }` | Token ausente, inválido ou expirado. |
| `403` | `{ "message": "Acesso não autorizado para este perfil." }` | Token de `TUTOR`. |
| `404` | `{ "statusCode": 404, "error": "Agendamento não encontrado." }` | Agendamento inexistente ou de outra clínica. |
| `400` | `{ "statusCode": 400, "error": "Apenas agendamentos com status PENDING_APPROVAL podem ser aprovados." }` | O agendamento já foi aprovado, recusado, cancelado etc. |
| `400` | `{ "statusCode": 400, "error": "Não é possível aprovar uma solicitação com data no passado." }` | A data solicitada já passou. |
| `404` | `{ "statusCode": 404, "error": "Veterinário não encontrado" }` | `vetId` inexistente, de outra clínica ou com perfil `TUTOR`. |
| `400` | `{ "statusCode": 400, "error": "O horário de fim deve ser posterior ao horário de início." }` | `endDateTime` menor ou igual a `dateTime`. |
| `409` | `{ "statusCode": 409, "error": "Este horário já está ocupado." }` | Conflito na agenda do veterinário. |

## 5. `PATCH /appointments/:id/reject`

A clínica recusa a solicitação, com justificativa obrigatória. O tutor vê o motivo em `cancelReason` no `GET /portal/appointments`.

- **Perfil:** `OWNER` ou `VET`.
- **Parâmetro de rota:** `id` (UUID do agendamento).

### Request body

| Campo | Tipo | Obrigatório | Regra |
| :--- | :--- | :--- | :--- |
| `reason` | string | sim | Pelo menos 1 caractere após remover os espaços das pontas. É gravado em `cancelReason`. |

```json
{
  "reason": "Sem disponibilidade de profissionais no horário solicitado."
}
```

### Resposta `200 OK`

```json
{
  "appointment": {
    "id": "77777777-7777-7777-7777-777777777777",
    "patientId": "66666666-6666-6666-6666-666666666666",
    "vetId": null,
    "dateTime": "2026-10-15T14:30:00.000Z",
    "endDateTime": null,
    "category": "VACCINATION",
    "status": "REJECTED",
    "observation": "Animal tem histórico de reação alérgica",
    "cancelReason": "Sem disponibilidade de profissionais no horário solicitado.",
    "createdAt": "2026-10-04T15:00:00.000Z",
    "updatedAt": "2026-10-04T15:15:00.000Z",
    "patient": {
      "id": "66666666-6666-6666-6666-666666666666",
      "name": "Rex",
      "species": "Canino",
      "clinicId": "11111111-1111-1111-1111-111111111111",
      "photoUrl": null
    },
    "vet": null
  }
}
```

### Erros

| Status | Corpo | Causa |
| :--- | :--- | :--- |
| `422` | `issues: { "reason": ["Justificativa deve ter ao menos 1 caractere"] }` | `reason` ausente ou em branco, ou `id` não é UUID. |
| `401` | `{ "message": "Token inválido ou expirado." }` | Token ausente, inválido ou expirado. |
| `403` | `{ "message": "Acesso não autorizado para este perfil." }` | Token de `TUTOR`. |
| `404` | `{ "statusCode": 404, "error": "Agendamento não encontrado." }` | Agendamento inexistente ou de outra clínica. |
| `400` | `{ "statusCode": 400, "error": "Apenas agendamentos com status PENDING_APPROVAL podem ser recusados." }` | O agendamento não está pendente. |

## Catálogo de erros

Exemplos completos de cada código de erro, prontos para usar como mock.

### 400 Bad Request — regra de negócio

```json
{
  "statusCode": 400,
  "error": "Apenas agendamentos com status PENDING_APPROVAL podem ser aprovados."
}
```

### 401 Unauthorized — token ausente, inválido ou expirado

```json
{
  "message": "Token inválido ou expirado."
}
```

### 403 Forbidden — perfil não autorizado (rotas da clínica)

```json
{
  "message": "Acesso não autorizado para este perfil."
}
```

### 403 Forbidden — regra de negócio (rotas do portal)

```json
{
  "statusCode": 403,
  "error": "Você não tem permissão para solicitar agendamento para este animal."
}
```

### 404 Not Found

```json
{
  "statusCode": 404,
  "error": "Agendamento não encontrado."
}
```

### 409 Conflict — conflito na agenda do veterinário

```json
{
  "statusCode": 409,
  "error": "Este horário já está ocupado."
}
```

### 422 Unprocessable Entity — validação de schema

Cada campo inválido aparece como uma chave em `issues`, com a lista de mensagens daquele campo.

```json
{
  "statusCode": 422,
  "error": "Validation Error",
  "issues": {
    "patientId": [
      "Required"
    ],
    "category": [
      "Invalid enum value. Expected 'VACCINATION' | 'OBSERVATION' | 'EXAM' | 'SURGICAL', received 'CONSULTA'"
    ]
  },
  "message": "Erros de validação nos campos"
}
```

## Regras de negócio

| # | Regra | Origem |
| :--- | :--- | :--- |
| 1 | O tutor solicita escolhendo pet, `category` e `dateTime`. Não escolhe o veterinário. | Especificação formal |
| 2 | A solicitação nasce `PENDING_APPROVAL`, com `vetId: null`. | Especificação formal |
| 3 | A aprovação exige atribuir um veterinário e leva a `SCHEDULED`. | Especificação formal |
| 4 | A recusa exige justificativa e leva a `REJECTED`. | Especificação formal |
| 5 | O status `REJECTED` é separado de `CANCELLED`, para distinguir a recusa de uma solicitação do cancelamento de uma consulta confirmada. | Decisão do time |
| 6 | O tutor só solicita para pets da própria conta. | Decisão do time |
| 7 | A data solicitada precisa ser no futuro. | Decisão do time |
| 8 | O conflito de agenda é checado **apenas na aprovação**, nunca na solicitação. | Decisão do time |
| 9 | A fila da clínica usa `GET /appointments?status=PENDING_APPROVAL`, sem rota dedicada. | Decisão do time |
| 10 | O tutor acompanha suas solicitações por `GET /portal/appointments`. | Decisão do time |
| 11 | A rota principal da solicitação é `POST /portal/appointments/request`. `POST /portal/appointments` é um alias. | Resolução do conflito documental |
| 12 | Aprovar e recusar são permitidos a `OWNER` e `VET`. | Decisão do time |
| 13 | Não é possível aprovar uma solicitação cuja data já passou. | Decisão de implementação |
| 14 | Um usuário com perfil `TUTOR` não pode ser atribuído como veterinário. | Decisão de implementação |

## Mudanças no modelo de dados

Migration `20261005211500_add_pending_rejected_status_and_optional_vet`:

- O enum `AppointmentStatus` ganha `PENDING_APPROVAL` e `REJECTED`.
- A coluna `appointments.vet_id` passa a aceitar `NULL`.
- Nova CHECK constraint, que garante o invariante de `vetId`:

```sql
ALTER TABLE "appointments"
  ADD CONSTRAINT "check_vet_id_status"
  CHECK (
    ("status" IN ('SCHEDULED', 'IN_PROGRESS', 'COMPLETED') AND "vet_id" IS NOT NULL)
    OR ("status" NOT IN ('SCHEDULED', 'IN_PROGRESS', 'COMPLETED'))
  );
```

**Impacto nos clientes:** `vetId` e `vet` passam a poder ser `null` em qualquer resposta que traga agendamentos. As tipagens do frontend e do mobile (ex.: `vetId: string`) precisam aceitar `null`.

## Impacto em rotas existentes

| Rota ou recurso | Comportamento com os novos status |
| :--- | :--- |
| `GET /appointments?date=` (agenda diária) | Mostra só `SCHEDULED`, `IN_PROGRESS` e `COMPLETED`. |
| `POST /appointments` e `PATCH /appointments/:id/reschedule` | O conflito de agenda considera só consultas `SCHEDULED` e `IN_PROGRESS`. |
| `PATCH /appointments/:id/reschedule` | Continua aceitando só `SCHEDULED`. |
| `DELETE /appointments/:id` | Pode cancelar uma solicitação `PENDING_APPROVAL` (cancelamento administrativo). Ela vira `CANCELLED`. Hoje também aceita `REJECTED`, o que sobrescreve o motivo da recusa (ver [Decisões pendentes](#decisoes-pendentes)). |
| `POST /clinical-records` (iniciar prontuário) | Só para agendamentos `SCHEDULED` ou `IN_PROGRESS`. Pendentes e recusados retornam 400. |
| Dashboards da clínica (`/dashboard`) | Pendências e recusas ficam fora de totais, categorias, tendência e consultas futuras. |
| `GET /portal/dashboard` (consultas recentes) | Mostra só `SCHEDULED`, `IN_PROGRESS` e `COMPLETED`. |

## Decisões pendentes

1. **Cancelamento da solicitação pelo tutor.** Hoje o tutor não consegue desistir de uma solicitação pendente. A proposta, ainda não implementada, é criar `PATCH /portal/appointments/:id/cancel`, restrito ao tutor dono do pet e ao status `PENDING_APPROVAL`.
2. **Incluir `vet` em `GET /portal/appointments`**, para o tutor ver o nome do veterinário depois da aprovação.
3. **Padronizar o `dateTime` do portal** com o mesmo validador ISO 8601 estrito das rotas da clínica. Hoje o portal aceita qualquer formato que o JavaScript consiga converter em data.
4. **Bloquear o cancelamento de solicitações `REJECTED`.** O `DELETE /appointments/:id` bloqueia `COMPLETED`, `CANCELLED` e `IN_PROGRESS`, mas não bloqueia `REJECTED`. Cancelar uma solicitação recusada troca o status para `CANCELLED` e substitui o motivo da recusa pela justificativa do cancelamento. Como `REJECTED` é um estado final, a proposta é retornar 400 nesse caso.

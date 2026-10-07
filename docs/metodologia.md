# Metodologias e Técnicas

## 1. Introdução

Durante o desenvolvimento do projeto **Iougurt**, foram utilizadas diferentes
metodologias, técnicas e práticas com o objetivo de apoiar a descoberta do
produto, o planejamento, o desenvolvimento, o acompanhamento e a validação das
entregas.

O projeto é conduzido em duas disciplinas consecutivas, refletidas na
organização deste site (ver [Início](index.md)):

- **Base Herdada** — concepção inicial da plataforma web para clínicas
  veterinárias, na disciplina anterior, guiada pela **Lean Inception**;
- **Gestão e Evolução** — disciplina atual, focada na evolução do produto
  (incluindo o novo aplicativo mobile do tutor), conduzida em **sprints**
  com backlog técnico próprio.

Este documento apresenta as abordagens utilizadas em ambas as fases,
descrevendo sua finalidade, a forma como foram aplicadas no contexto do
Iougurt e os artefatos produzidos.

---

## 2. Fase de Concepção — Lean Inception

### 2.1 Visão geral

A Lean Inception é uma abordagem colaborativa utilizada para promover o
alinhamento entre os participantes do projeto acerca do produto a ser
desenvolvido e do seu Produto Mínimo Viável (MVP).

Seu objetivo é construir um entendimento compartilhado entre as partes
envolvidas, permitindo discutir objetivos, usuários, funcionalidades, jornadas
e prioridades antes do início do desenvolvimento.

No Iougurt, a Lean Inception foi utilizada na disciplina anterior durante a
etapa inicial de descoberta e definição da plataforma para clínicas
veterinárias, dando origem aos artefatos reunidos na seção **Base Herdada**
deste site.

---

### 2.2 Visão do Produto

A Visão do Produto foi utilizada para alinhar entre equipe e stakeholders qual
produto estava sendo desenvolvido, para quem ele se destina, qual problema
busca resolver e qual é o seu principal diferencial.

#### Finalidade

- Alinhar o entendimento da equipe sobre o produto;
- Identificar o público-alvo;
- Explicitar o problema ou necessidade atendida;
- Registrar os principais benefícios esperados;
- Apoiar decisões posteriores sobre funcionalidades e escopo.

#### Aplicação no Iougurt

A visão consolidada foi registrada na [página inicial da documentação](index.md):
uma plataforma web centralizada para clínicas veterinárias, que otimiza a
operação diária ao unificar o cadastro de pacientes e tutores, a agenda de
consultas/procedimentos e o histórico clínico.

---

### 2.3 Delimitação de Escopo e Perfis de Usuário

Em conjunto com a Visão do Produto, a equipe delimitou o que a plataforma
deveria (e não deveria) resolver na primeira versão, e definiu os perfis de
usuário que utilizariam o sistema — servindo, no contexto do Iougurt, ao mesmo
papel que as técnicas de **"É / Não É / Faz / Não Faz"** e **Personas**
cumprem em uma Lean Inception tradicional.

#### Finalidade

- Reduzir ambiguidades e estabelecer limites iniciais de escopo;
- Identificar os principais usuários do produto e suas necessidades;
- Apoiar decisões de funcionalidades e de experiência do usuário.

#### Aplicação no Iougurt

O resultado foi consolidado em [Requisitos](requirements.md), que define três
perfis de usuário (usuário autenticado da clínica, profissional responsável
pelo atendimento veterinário, e administrador/atendente) e os requisitos
funcionais correspondentes a cada área do sistema (autenticação, dashboard,
gestão de pacientes, cadastro de tutores, entre outros).

---

### 2.4 Brainstorming e Jornadas de Funcionalidades

Após o alinhamento sobre produto, objetivos e usuários, a equipe levantou as
funcionalidades candidatas e as histórias de usuário que descrevem, sob a
perspectiva de cada perfil, como a interação com o sistema deveria ocorrer —
cumprindo o papel do **Brainstorming de Funcionalidades** e das **Jornadas de
Usuário** da Lean Inception.

#### Finalidade

- Identificar possíveis funcionalidades e soluções para as necessidades dos
  usuários;
- Descrever, por perfil, como o usuário interage com o produto;
- Criar uma base para priorização e para a definição do MVP.

#### Aplicação no Iougurt

O levantamento foi formalizado em [Histórias de Usuário](us_stories.md), com
16 histórias (US01 a US16) organizadas por épicos (Autenticação e Segurança,
Dashboard e Navegação, Gestão de Pacientes, Atendimento Clínico, Portal do
Tutor, entre outros), cada uma no formato *Como/Quero/Para que* acompanhada de
critérios de aceite.

---

### 2.5 Protótipo de Alta Fidelidade

Para validar fluxos e telas antes do desenvolvimento, a equipe produziu
protótipos navegáveis de alta fidelidade no Figma.

#### Finalidade

- Validar a experiência de uso antes da implementação;
- Servir de referência visual para o desenvolvimento de frontend e mobile.

#### Aplicação no Iougurt

O protótipo do aplicativo mobile do tutor está disponível em
[Protótipo](prototipo.md) e embutido diretamente na documentação via Figma
Embed. Sua elaboração está rastreada no backlog técnico como **PROT-01** e
**PROT-02** (ver [Backlog do Produto](backlog.md)).

---

### 2.6 Priorização e Definição do MVP

Em vez do Sequenciador de Funcionalidades e do Canvas MVP tradicionais da
Lean Inception, a equipe adotou o método **ICE Scoring (Impact, Confidence,
Ease)** para priorizar objetivamente as histórias de usuário e planejar as
entregas de forma incremental.

#### Finalidade

- Equilibrar valor de negócio e viabilidade técnica na priorização;
- Organizar a evolução incremental do produto;
- Identificar o conjunto mínimo de funcionalidades de cada entrega (MVP);
- Validar hipóteses e reduzir o risco de desenvolver funcionalidades sem
  valor.

#### Aplicação no Iougurt

Cada história recebeu uma pontuação `Score = Impacto × Confiança × Facilidade`
e foi classificada como **Estratégica**, **Operacional** ou **Complementar**.
A partir dessa priorização, o desenvolvimento foi dividido em **3 MVPs
incrementais** ao longo de 12 semanas:

| MVP | Foco | Período |
|-----|------|---------|
| MVP 1 | Base operacional da clínica (acesso, pacientes, agenda) | Semanas 1–4 |
| MVP 2 | Atendimento clínico e histórico | Semanas 5–8 |
| MVP 3 | Portal do tutor e funcionalidades complementares | Semanas 9–12 |

Detalhes completos da matriz de priorização e do escopo de cada MVP estão em
[Planejamento MVP](mvp.md).

---

## 3. Fase de Execução — Gestão e Evolução

A disciplina atual aplica um processo iterativo inspirado em **Scrum**, com
o trabalho organizado em sprints, equipes fixas (trios) e um backlog técnico
próprio. Cada tarefa vira uma issue no GitHub, é desenvolvida em uma branch
própria e entra no produto por Pull Request, validada por pipelines de
**Integração e Entrega Contínua (CI/CD)**.

### 3.1 Sprints e Trios de Desenvolvedores

O trabalho é dividido em sprints de aproximadamente duas semanas, com tarefas
distribuídas entre trios de desenvolvedores responsáveis por conjuntos
específicos de entregas (ex.: protótipo e desenvolvimento mobile, segurança,
correções de bugs).

No aplicativo mobile, cada história de usuário é desdobrada em três etapas —
**Protótipo**, **Desenvolvimento** e **Testes** —, de modo que a tela é
validada no Figma antes de ser implementada.

#### Finalidade

- Entregar valor de forma incremental e mensurável a cada ciclo;
- Distribuir responsabilidades de forma clara entre os trios;
- Manter rastreabilidade entre tarefas, issues e responsáveis.

#### Artefato resultante

- [Atividades da Sprint](atividades_sprint.md), com o detalhamento das
  entregas, responsáveis e códigos de rastreabilidade por sprint.

---

### 3.2 Reuniões de Acompanhamento (Weeklies)

Cada sprint conta com ao menos duas reuniões semanais (*weeklies*) e
reuniões extras de alinhamento quando necessário, usadas para levantar
requisitos, refinar histórias e revisar o andamento das entregas.

#### Finalidade

- Manter a equipe alinhada quanto ao progresso e aos próximos passos;
- Registrar decisões, presenças e pendências de cada encontro.

#### Artefato resultante

- [Registro de Reuniões da Sprint](registro_reunioes_sprint.md).

---

### 3.3 Backlog Técnico e Kanban

As demandas da disciplina atual — engenharia, refatoração, documentação,
segurança e novas funcionalidades — são organizadas em um backlog técnico
categorizado por frente de trabalho (Mobile, Frontend, Backend, Segurança,
QA/CI-CD, Infraestrutura), e visualizadas em quadros Kanban no GitHub
Projects, um por equipe.

#### Finalidade

- Dar visibilidade ao fluxo de trabalho de cada frente;
- Categorizar e rastrear itens técnicos que não são histórias de usuário
  (bugs, segurança, CI/CD, infraestrutura);
- Apoiar a priorização contínua ao longo das sprints.

#### Artefato resultante

- [Backlog do Produto](backlog.md);
- Quadros Kanban: [Mobile](https://github.com/orgs/gces-iorgut-startup/projects/5),
  [Frontend](https://github.com/orgs/gces-iorgut-startup/projects/7) e
  [Backend](https://github.com/orgs/gces-iorgut-startup/projects/6).

---

### 3.4 Fluxo de Trabalho no GitHub (Issues, Branches e Pull Requests)

Toda tarefa do backlog é registrada como issue e associada ao quadro Kanban
da sua frente. O desenvolvimento acontece em uma branch própria, criada a
partir da `main` — no mobile, com o nome gerado pela própria issue (ex.:
`43-us12-visualizar-recomendacoes-veterinarias`); na documentação, com o
prefixo `docs/`. A entrega é integrada por Pull Request, e a issue é fechada
automaticamente quando o commit ou o PR traz `Closes #<número>`.

Os commits seguem, em geral, o padrão *Conventional Commits* (`feat:`,
`fix:`, `docs:`, `refactor:`, `style:`), citando o código da tarefa (ex.:
`(US12)`, `(BE-05)`); quando o trabalho é feito em trio, os demais
integrantes são registrados com `Co-authored-by`.

#### Finalidade

- Rastrear cada entrega até a tarefa e os responsáveis que a originaram;
- Isolar mudanças em andamento da versão estável na `main`;
- Validar cada mudança no CI antes de integrá-la à `main`.

#### Artefato resultante

- Issues, branches e Pull Requests dos repositórios da organização
  [gces-iorgut-startup](https://github.com/gces-iorgut-startup).

---

### 3.5 Contratos de API

Para funcionalidades que envolvem mais de uma frente (backend, frontend e
mobile), a equipe passou a definir e documentar o contrato da API **antes**
da implementação, em uma issue própria — prática adotada a partir da BE-05.
Os exemplos do contrato são capturados da API real e servem de mock para
quem consome o endpoint.

#### Finalidade

- Permitir que backend, frontend e mobile trabalhem em paralelo;
- Reduzir retrabalho por divergência de formato entre as frentes;
- Documentar regras de acesso e erros esperados de cada rota.

#### Artefato resultante

- [Contrato BE-05 — Solicitação e Aprovação de Agendamentos](api_contract_be05.md).

---

### 3.6 Integração e Entrega Contínua (CI/CD)

Backend, frontend e mobile possuem pipelines próprios no GitHub Actions,
executados a cada push e Pull Request para a branch `main`.

#### Finalidade

- Garantir qualidade de código antes da integração (lint e checagem de
  tipos);
- Executar testes automatizados de forma consistente e reprodutível;
- Automatizar o empacotamento e a publicação da aplicação.

#### Aplicação no Iougurt

- **Backend:** lint, checagem de tipos, migrações e testes com cobertura
  executados contra um container PostgreSQL de teste, seguidos de build e
  push da imagem Docker (`iougurt-api`) para o Docker Hub;
- **Frontend:** lint (ESLint), checagem de tipos e build de verificação,
  seguidos de build e push da imagem Docker (`iougurt-frontend`);
- **Mobile:** formatação (Prettier), lint (ESLint), checagem de tipos e
  validação da configuração do Expo; ao publicar uma tag de versão (`v*`),
  ou sob demanda, um segundo pipeline gera o build Android pelo EAS;
- **Documentação:** publicada no GitHub Pages com `mkdocs gh-deploy`;
  automatizar essa publicação é o item **CI-03** do backlog.

---

## 4. Resumo da aplicação

| Metodologia/Técnica | Objetivo | Artefato |
|---|---|---|
| Lean Inception | Alinhar equipe e stakeholders acerca do MVP | Artefatos da seção Base Herdada |
| Visão do Produto | Estabelecer propósito e direção do produto | [Início](index.md) |
| Delimitação de escopo e perfis de usuário | Delimitar entendimento, escopo e público-alvo | [Requisitos](requirements.md) |
| Brainstorming e jornadas | Identificar funcionalidades e fluxos de uso | [Histórias de Usuário](us_stories.md) |
| Protótipo de alta fidelidade | Validar experiência antes da implementação | [Protótipo](prototipo.md) |
| ICE Scoring | Priorizar histórias com critérios objetivos | [Planejamento MVP](mvp.md) |
| MVPs incrementais | Planejar entregas de valor validável | [Planejamento MVP](mvp.md) |
| Sprints e trios | Organizar e distribuir o trabalho de desenvolvimento | [Atividades da Sprint](atividades_sprint.md) |
| Weeklies | Acompanhar progresso e alinhar a equipe | [Registro de Reuniões](registro_reunioes_sprint.md) |
| Backlog técnico e Kanban | Rastrear e priorizar demandas técnicas | [Backlog do Produto](backlog.md) |
| Issues, branches e Pull Requests | Rastrear cada entrega e proteger a `main` | Repositórios no GitHub |
| Contratos de API | Alinhar as frentes antes da implementação | [Contrato BE-05](api_contract_be05.md) |
| CI/CD | Garantir qualidade e automatizar entrega | Pipelines GitHub Actions (backend, frontend e mobile) |

---

## 5. Referências

- CAROLI, Paulo. *Lean Inception: como alinhar pessoas e construir o produto
  certo*.
- ProductPlan. *ICE Scoring Model | Definition and Overview*.
- Savio. *What is the ICE Scoring Framework? Guide and Template*.
- Imaginary Cloud. *Build your MVP efficiently with agile methodology*.

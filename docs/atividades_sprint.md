# Atividades Realizadas por Sprint

Este documento consolida o andamento técnico da equipe ao longo do projeto, detalhando cada atividade entregue com base em seu código de rastreabilidade. Os trios e os responsáveis por cada atividade são indicados individualmente.

## Sprint 1

**Período:** 31/08/2026 a 14/09/2026
**Objetivo da Sprint:** Preparação de fundações, segurança inicial, limpeza de dependências, Setup Mobile e primeiras User Stories do fluxo do tutor.

### MOB-01: Setup inicial React Native
- **Frente:** Mobile (Infraestrutura)
- **Trio / Responsáveis:** [Taynara Vitorino](https://github.com/taybalau), [Luiza Pugas](https://github.com/Luizaxx) e [João Marcos](https://github.com/JJOAOMARCOSS)
- **Descrição:** Configuração da arquitetura base do aplicativo e do ecossistema inicial em React Native.
- **Status:** Em Andamento
- **Issue:** [#16](https://github.com/gces-iorgut-startup/android-mobile/issues/16) · [Quadro do Projeto](https://github.com/orgs/gces-iorgut-startup/projects/5)

---

### PROT-01: Protótipos Mobile (US01 a US08)
- **Frente:** Mobile (Design e Prototipação)
- **Trio / Responsáveis:** [Taynara Vitorino](https://github.com/taybalau), [Luiza Pugas](https://github.com/Luizaxx) e [João Marcos](https://github.com/JJOAOMARCOSS)
- **Descrição:** Elaboração dos protótipos navegáveis referentes às histórias de usuário de 01 a 08 (Acesso e Meu Pet).
- **Status:** Em Andamento
- **Issues:** [US01 a US08](https://github.com/gces-iorgut-startup/android-mobile/issues?q=is%3Aissue+PROT-01+in%3Atitle) · [Quadro do Projeto](https://github.com/orgs/gces-iorgut-startup/projects/5)

---

### PROT-02: Protótipos Mobile (US09 a US15)
- **Frente:** Mobile (Design e Prototipação)
- **Trio / Responsáveis:** Manoela, Victor e Thales
- **Descrição:** Elaboração dos protótipos navegáveis referentes às histórias de usuário de 09 a 15 (Saúde e Agenda).
- **Status:** Em Andamento
- **Issues:** [US09 a US15](https://github.com/gces-iorgut-startup/android-mobile/issues?q=is%3Aissue+PROT-02+in%3Atitle) · [Quadro do Projeto](https://github.com/orgs/gces-iorgut-startup/projects/5)

---

### BUG-01: Correção do cadastro de senhas do tutor
- **Frente:** Bug fix
- **Trio / Responsáveis:** Wallyson, Pedro e Artur
- **Descrição:** Análise e correção das falhas e inconsistências relacionadas ao fluxo de cadastro de senhas do tutor.
- **Status:** Em Andamento
- **Issue:** [#1](https://github.com/gces-iorgut-startup/backend/issues/1)

---

### SEC-01: Proteger ou remover rotas backdoor
- **Frente:** Segurança
- **Trio / Responsáveis:** Paola, Lara e Magno
- **Descrição:** Resolução de questões de segurança críticas apontadas no backend, com foco na proteção ou exclusão de rotas backdoor.
- **Status:** Concluído
- **Issue:** [#2](https://github.com/gces-iorgut-startup/backend/issues/2)

---

### SEC-02: Atualizar dependências vulneráveis
- **Frente:** Segurança
- **Trio / Responsáveis:** Paola, Lara e Magno
- **Descrição:** Atualização de bibliotecas vulneráveis do backend (como fastify e fastify-jwt) para mitigar falhas de segurança.
- **Status:** Concluído
- **Issue:** [#3](https://github.com/gces-iorgut-startup/backend/issues/3)

---

### SEC-03: Migrar armazenamento de sessão do localStorage para Cookies HttpOnly com proteção CSRF
- **Frente:** Segurança
- **Trio / Responsáveis:** Paola, Lara e Magno
- **Descrição:** Migração da arquitetura de autenticação do sistema, removendo a persistência de tokens do localStorage no frontend (mitigando ataques XSS) e implementando o envio de credenciais via Cookies HttpOnly, aliados a uma camada de proteção com tokens Anti-CSRF no backend (Fastify) e Axios.
- **Status:** Em Andamento
- **Issue:** [#4](https://github.com/gces-iorgut-startup/backend/issues/4)

---

### CI-04: Ajustes de CI/CD do aplicativo mobile
- **Frente:** CI/CD
- **Trio / Responsáveis:** Paola, Lara e Magno
- **Descrição:** Correção e aprimoramento dos pipelines de integração e entrega (CI/CD) focados na esteira do aplicativo mobile.
- **Status:** Em Andamento
- **Kanban:** [Quadro do Projeto](https://github.com/orgs/gces-iorgut-startup/projects/5)

---

## Sprint 2

**Período:** [Data de Início] a [Data de Fim]
**Objetivo da Sprint:** Entregas de melhoria em agendamento, refatorações cruciais em páginas pesadas, definição de regra de negócios central e avanços no login mobile.

### BE-01: Prontuário Universal para Perfil Owner
- **Frente:** Backend / Regra de Negócio
- **Trio / Responsáveis:** _A definir_
- **Descrição:** Quebra de trava funcional que impedia donos da clínica de gerenciarem os prontuários gerais sob sua própria responsabilidade.
- **Status:** Homologado

---

### FE-02: Redesign Institucional
- **Frente:** Frontend Web
- **Trio / Responsáveis:** _A definir_
- **Descrição:** Criação e integração de uma nova Landing Page para alinhar o visual à realidade atual do aplicativo.
- **Status:** Homologado

---

### MOB-02: Implementar Onboarding e Login seguro
- **Frente:** Mobile
- **Trio / Responsáveis:** [Taynara Vitorino](https://github.com/taybalau), [João Marcos](https://github.com/JJOAOMARCOSS) e [Luiza Pugas](https://github.com/Luizaxx)
- **Descrição:** Implementação prática das US01 e US02, consumindo endpoints de login e persistindo as credenciais com segurança (SecureStore).
- **Status:** Homologado
- **Issues:** [#17](https://github.com/gces-iorgut-startup/android-mobile/issues/17) e [#18](https://github.com/gces-iorgut-startup/android-mobile/issues/18)

---

### CI-02: Configurar Automação Headless
- **Frente:** CI/CD
- **Trio / Responsáveis:** _A definir_
- **Descrição:** Garantir a execução invisível e performática do ChromeDriver no fluxo E2E das Actions no repositório Web.
- **Status:** Homologado

---

### BE-02: Modelagem e Implementação de Soft Delete
- **Frente:** Backend / Modelagem
- **Trio / Responsáveis:** _A definir_
- **Descrição:** Adaptação do schema Prisma para evitar perdas irreversíveis de dados, ativando inativação lógica.
- **Status:** Homologado

---

*(Os demais itens como FE-03, FE-04, MOB-03 e adjacentes serão mapeados e atualizados conforme as Sprints 3 e 4 se consolidarem.)*

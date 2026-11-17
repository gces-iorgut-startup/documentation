# Atividades Realizadas por Sprint

Este documento consolida o andamento tecnico da equipe ao longo do projeto, detalhando cada atividade entregue baseada no seu codigo de rastreabilidade. Os trios e os responsaveis por cada atividade sao indicados individualmente.

## Kanbans do Projeto

- **Mobile:** [GitHub Projects - Mobile](https://github.com/orgs/gces-iorgut-startup/projects/5)
- **Frontend:** [GitHub Projects - Frontend](https://github.com/orgs/gces-iorgut-startup/projects/7)
- **Backend:** [GitHub Projects - Backend](https://github.com/orgs/gces-iorgut-startup/projects/6)

# Sprint 01
 
*Período:* 31/08/2026 a 14/09/2026
 
## Entregas da Sprint
 
| Trio de Desenvolvedores | Qtd. de Tarefas | Tarefas (Issues) | Assunto das Tarefas |
|---|---:|---|---|
| Taynara, Luiza e Joao | 11 | MOB-01 (#16), PROT-01 (#1 ao #8), DEV-01 (#17, #18) | Setup inicial, Protótipos e Desenvolvimento Mobile (Acesso e Meu Pet) |
| Manoela, Victor e Thales | 9 | PROT-02 (#9 ao #15), DEV-02 (#20, #21) | Protótipos e Desenvolvimento Mobile (Saúde e Agenda) |
| Wallyson, Pedro e Artur | 1 | BUG-01 (#1) | Correção do cadastro de senhas do tutor |
| Paola, Lara e Magno | 3 | SEC-01 (#2), SEC-02 (#3), SEC-03 (#4) | Segurança (rotas backdoor, dependências vulneráveis e sessão) |
 
---
 
## Resumo
 
- *Líder da Apresentação*: Taynara Vitorino
- *Total de Tarefas:* 24
- *Início da Sprint:* 31/08/2026
- *Fim da Sprint:* 14/09/2026

---

# Sprint 02
 
*Período:* 28/09/2026 a 05/10/2026
 
## Entregas da Sprint
 
| Trio de Desenvolvedores | Qtd. de Tarefas | Tarefas (Issues) | Assunto das Tarefas |
|---|---:|---|---|
| Taynara, Luiza e João Marcos | 9 | US-02[(#18)](https://github.com/gces-iorgut-startup/android-mobile/issues/18), US03[(#24)](https://github.com/gces-iorgut-startup/android-mobile/issues/24), US04[(#25)](https://github.com/gces-iorgut-startup/android-mobile/issues/25), US05[(#26)](https://github.com/gces-iorgut-startup/android-mobile/issues/26), US06[(#27)](https://github.com/gces-iorgut-startup/android-mobile/issues/27), US07[(#28)](https://github.com/gces-iorgut-startup/android-mobile/issues/28), US08[(#29)](https://github.com/gces-iorgut-startup/android-mobile/issues/29), MOB-02[(#31)](https://github.com/gces-iorgut-startup/android-mobile/issues/31), MOB-04[(#48)](https://github.com/gces-iorgut-startup/android-mobile/issues/48) | Desenvolvimento Mobile (Recuperação de Acesso, Autenticação, Gestão de Pets, Home, Suporte Expo Web e Geração/Deploy do APK) |
| Manoela, Thales e Victor | 3 | US11[(#42)](https://github.com/gces-iorgut-startup/android-mobile/issues/42), US12[(#43)](https://github.com/gces-iorgut-startup/android-mobile/issues/43), US13[(#44)](https://github.com/gces-iorgut-startup/android-mobile/issues/44) | Desenvolvimento Mobile (Exames, Recomendações Veterinárias e Consultas) |
| Artur, Wallyson e Pedro | 7 | BE-05[(#11)](https://github.com/gces-iorgut-startup/backend/issues/11), SEC04[(#12)](https://github.com/gces-iorgut-startup/backend/issues/12), BE-05[(#13)](https://github.com/gces-iorgut-startup/backend/issues/13), BE-01[(#14)](https://github.com/gces-iorgut-startup/backend/issues/14), BUG-01[(#1)](https://github.com/gces-iorgut-startup/frontend/issues/1), BUG-03[(#8)](https://github.com/gces-iorgut-startup/frontend/issues/8), BE-07[(#27)](https://github.com/gces-iorgut-startup/backend/issues/27) | Backend (Validação CRMV, Migration Appointments, Esteira de Agendamento, Status de Ativação da Conta do Tutor) e Frontend (Cadastro de Senha do Tutor, Tela de Primeiro Acesso e Reenvio de Convite) |
| Lara, Magno e Paola | 4 | BE[(#19)](https://github.com/gces-iorgut-startup/backend/issues/19) BE-02[(#21)](https://github.com/gces-iorgut-startup/backend/issues/21), QA[(#20)](https://github.com/gces-iorgut-startup/backend/issues/20), FE (Limpeza de Código) | Backend (Uptime/Timestamp no Health Check, Soft Delete para Pacientes e Tutores), QA (Cobertura real de PostgreSQL) e Frontend (Remoção de código morto - TutorDevPage) |
 
---
 
## Resumo
 
- *Líder da Apresentação*: Artur Fernandes Galdino
- *Total de Tarefas:* 23
- *Início da Sprint:* 28/09/2026
- *Fim da Sprint:* 05/10/2026

### Deploy do Aplicativo Mobile (v1)

Como parte da entrega da **MOB-04 (#48)**, foi disponibilizada a primeira versão standalone do aplicativo para Android:

- **Artefato:** `v1.apk` (*Iougurt Tutor*)
- **Versão:** `1.0.0`
- **API em Produção:** `https://backend-tlpu.onrender.com`
- **Download Direto do APK:** [Baixar v1.apk](https://github.com/gces-iorgut-startup/android-mobile/releases/download/v1.0.0/v1.apk)

---

# Sprint 03
 
*Período:* 12/10/2026 a 26/10/2026
 
## Entregas da Sprint
 
| Trio de Desenvolvedores | Qtd. de Tarefas | Tarefas (Issues) | Assunto das Tarefas |
|---|---:|---|---|
| Taynara, Luiza e João Marcos | 8 | TEST-01: US01[(#49)](https://github.com/gces-iorgut-startup/android-mobile/issues/49), US02[(#50)](https://github.com/gces-iorgut-startup/android-mobile/issues/50), US03[(#51)](https://github.com/gces-iorgut-startup/android-mobile/issues/51), US04[(#52)](https://github.com/gces-iorgut-startup/android-mobile/issues/52), US05[(#53)](https://github.com/gces-iorgut-startup/android-mobile/issues/53), US06[(#54)](https://github.com/gces-iorgut-startup/android-mobile/issues/54), US07[(#55)](https://github.com/gces-iorgut-startup/android-mobile/issues/55), US08[(#56)](https://github.com/gces-iorgut-startup/android-mobile/issues/56) | Testes Automatizados do App Mobile (Unitários, de Widget e E2E das US01 a US08) |
| Manoela, Thales e Victor | 9 | DEV-02: US14[(#57)](https://github.com/gces-iorgut-startup/android-mobile/issues/57) (inclui BE-06[(#18)](https://github.com/gces-iorgut-startup/backend/issues/18) e MOB-03[(#40)](https://github.com/gces-iorgut-startup/android-mobile/issues/40)), US15[(#58)](https://github.com/gces-iorgut-startup/android-mobile/issues/58); TEST-02: US09[(#59)](https://github.com/gces-iorgut-startup/android-mobile/issues/59), US10[(#60)](https://github.com/gces-iorgut-startup/android-mobile/issues/60), US11[(#61)](https://github.com/gces-iorgut-startup/android-mobile/issues/61), US12[(#62)](https://github.com/gces-iorgut-startup/android-mobile/issues/62), US13[(#63)](https://github.com/gces-iorgut-startup/android-mobile/issues/63), US14[(#64)](https://github.com/gces-iorgut-startup/android-mobile/issues/64), US15[(#65)](https://github.com/gces-iorgut-startup/android-mobile/issues/65) | Desenvolvimento Mobile (Detalhes da Consulta com o Veterinário e Agendamento de Consulta) e Testes Automatizados do App (US09 a US15) |
| Artur, Wallyson e Pedro | 8 | BE-08[(#29)](https://github.com/gces-iorgut-startup/backend/issues/29), BE-09[(#30)](https://github.com/gces-iorgut-startup/backend/issues/30), BE-10[(#31)](https://github.com/gces-iorgut-startup/backend/issues/31), QA-04[(#32)](https://github.com/gces-iorgut-startup/backend/issues/32), FE-06[(#13)](https://github.com/gces-iorgut-startup/frontend/issues/13), FE-07[(#14)](https://github.com/gces-iorgut-startup/frontend/issues/14), FE-08[(#15)](https://github.com/gces-iorgut-startup/frontend/issues/15), QA-05[(#16)](https://github.com/gces-iorgut-startup/frontend/issues/16) | Backend (Sigla Única da Clínica, Validação Pública por Sigla e Autocadastro de Veterinário), Frontend (Cadastro com Alternância Dono/Veterinário, Validação da Sigla em Tempo Real e Sigla da Clínica no Perfil do Dono) e Testes Automatizados |
| Lara, Magno e Paola | 6 | QA-01[(#11)](https://github.com/gces-iorgut-startup/frontend/issues/11), QA-02[(#12)](https://github.com/gces-iorgut-startup/frontend/issues/12), QA-03[(#19)](https://github.com/gces-iorgut-startup/frontend/issues/19), QA-04[(#18)](https://github.com/gces-iorgut-startup/frontend/issues/18), SEC-03[(#4)](https://github.com/gces-iorgut-startup/backend/issues/4), BE-04[(#28)](https://github.com/gces-iorgut-startup/backend/issues/28) | Testes do Frontend (Autenticação, Zustand, Máscaras e Formulários), Testes Unitários na CI, Testes E2E do Primeiro Acesso do Tutor, Segurança (Sessão Web com Cookies HttpOnly e CSRF) e Backend (Lembrete de Consulta por E-mail 24h Antes) |
 
---
 
## Resumo
 
- *Líder da Apresentação*: Thales Germano
- *Total de Tarefas:* 31
- *Início da Sprint:* 12/10/2026
- *Fim da Sprint:* 26/10/2026

### Deploy do Aplicativo Mobile (v2)

Como parte das entregas da **Sprint 03** (com inclusão do fluxo de agendamento de consultas, visualização do veterinário responsável e suíte completa de testes automatizados), foi disponibilizada a segunda versão standalone do aplicativo para Android:

- **Artefato:** `v2.apk` (*Iougurt Tutor*)
- **Versão:** `2.0.0`
- **API em Produção:** `https://backend-tlpu.onrender.com`
- **Download Direto do APK:** [Baixar v2.apk](https://github.com/gces-iorgut-startup/android-mobile/releases/download/v2.0.0/v2.apk)

---

# Sprint 04

*Período:* 29/10/2026 a 17/11/2026

## Entregas da Sprint

| Trio de Desenvolvedores | Qtd. de Tarefas | Tarefas (Issues) | Assunto das Tarefas |
|---|---:|---|---|
| Luiza, João Marcos e Taynara | 6 | MOB-01[(#71)](https://github.com/gces-iorgut-startup/android-mobile/issues/71), MOB-02[(#72)](https://github.com/gces-iorgut-startup/android-mobile/issues/72), MOB-03[(#73)](https://github.com/gces-iorgut-startup/android-mobile/issues/73), MOB-06[(#78)](https://github.com/gces-iorgut-startup/android-mobile/issues/78), MOB-07[(#79)](https://github.com/gces-iorgut-startup/android-mobile/issues/79), MOB-09[(#85)](https://github.com/gces-iorgut-startup/android-mobile/issues/85) | Estabilização do aplicativo mobile, correção de bugs, validação da integração com a API e melhorias de paridade com o portal web, incluindo pesquisa no histórico, compartilhamento de atendimentos, tipos de consulta e avisos vacinais. |
| Paola, Lara e Magno | 5 | WEB-01 Frontend[(#35)](https://github.com/gces-iorgut-startup/frontend/issues/35), WEB-03 Backend[(#68)](https://github.com/gces-iorgut-startup/backend/issues/68), WEB-03 Backend[(#69)](https://github.com/gces-iorgut-startup/backend/issues/69), WEB-04 Frontend[(#64)](https://github.com/gces-iorgut-startup/frontend/issues/64), WEB-04/WEB-05 Backend[(#77)](https://github.com/gces-iorgut-startup/backend/issues/77) | Estabilização da aplicação web, correção das validações de cadastro, ajustes de segurança e datas da agenda, além da configuração e validação do frontend e backend no ambiente de produção. |
| Manoela, Thales e Victor | 12 | CAD-01 Backend[(#50)](https://github.com/gces-iorgut-startup/backend/issues/50) e Frontend[(#37)](https://github.com/gces-iorgut-startup/frontend/issues/37), CAD-02 Backend[(#51)](https://github.com/gces-iorgut-startup/backend/issues/51) e Frontend[(#38)](https://github.com/gces-iorgut-startup/frontend/issues/38), CAD-03 Backend[(#52)](https://github.com/gces-iorgut-startup/backend/issues/52) e Frontend[(#39)](https://github.com/gces-iorgut-startup/frontend/issues/39), CAD-04 Backend[(#53)](https://github.com/gces-iorgut-startup/backend/issues/53) e Frontend[(#40)](https://github.com/gces-iorgut-startup/frontend/issues/40), CAD-05 Backend[(#54)](https://github.com/gces-iorgut-startup/backend/issues/54) e Frontend[(#41)](https://github.com/gces-iorgut-startup/frontend/issues/41), CAD-06 Backend[(#55)](https://github.com/gces-iorgut-startup/backend/issues/55) e Frontend[(#42)](https://github.com/gces-iorgut-startup/frontend/issues/42) | Evolução dos cadastros e da navegação web, incluindo novos campos de pacientes, contatos alternativos dos tutores, pesquisa avançada, tipos e edição de atendimentos e atividades recentes no dashboard. |
| Artur, Pedro Henrique e Wallyson | 18 | CLI-00 Backend[(#41)](https://github.com/gces-iorgut-startup/backend/issues/41), CLI-01 Backend[(#46)](https://github.com/gces-iorgut-startup/backend/issues/46) e Frontend[(#32)](https://github.com/gces-iorgut-startup/frontend/issues/32), CLI-02 Backend[(#42)](https://github.com/gces-iorgut-startup/backend/issues/42) e Frontend[(#27)](https://github.com/gces-iorgut-startup/frontend/issues/27), CLI-03 Backend[(#44)](https://github.com/gces-iorgut-startup/backend/issues/44) e Frontend[(#29)](https://github.com/gces-iorgut-startup/frontend/issues/29), CLI-04 Frontend[(#31)](https://github.com/gces-iorgut-startup/frontend/issues/31), CLI-05 Backend[(#45)](https://github.com/gces-iorgut-startup/backend/issues/45) e Frontend[(#30)](https://github.com/gces-iorgut-startup/frontend/issues/30), CLI-06 Backend[(#43)](https://github.com/gces-iorgut-startup/backend/issues/43) e Frontend[(#28)](https://github.com/gces-iorgut-startup/frontend/issues/28), EVO-01 Backend[(#70)](https://github.com/gces-iorgut-startup/backend/issues/70) e Frontend[(#57)](https://github.com/gces-iorgut-startup/frontend/issues/57), EVO-05 Backend[(#71)](https://github.com/gces-iorgut-startup/backend/issues/71) e Frontend[(#58)](https://github.com/gces-iorgut-startup/frontend/issues/58), EVO-06 Backend[(#72)](https://github.com/gces-iorgut-startup/backend/issues/72) e Frontend[(#59)](https://github.com/gces-iorgut-startup/frontend/issues/59) | Evolução do prontuário clínico com observações, patologias crônicas, tipos de exames, gráfico de peso, acompanhamento fotográfico e vacinação. Também foram antecipadas as evoluções de orçamentos, internações e alertas automáticos de vacinação. |

### Deploy do Aplicativo Mobile (v3)

Como parte das entregas da **Sprint 04** (com estabilização do aplicativo, correção de bugs, validação da integração com a API e melhorias de paridade com o portal web), foi disponibilizada a terceira versão standalone do aplicativo para Android:

- **Artefato:** `v3.apk` (*Iougurt Tutor*)
- **Versão:** `3.0.0`
- **API em Produção:** `https://backend-tlpu.onrender.com`
- **Download Direto do APK:** [Baixar v3.apk](https://github.com/gces-iorgut-startup/android-mobile/releases/download/v3.0.0/v3.apk)

---

## Resumo

- *Líder da Apresentação*: Victor Hugo Bernardes
- *Total de Tarefas:* 41
- *Início da Sprint:* 29/10/2026
- *Fim da Sprint:* 17/11/2026

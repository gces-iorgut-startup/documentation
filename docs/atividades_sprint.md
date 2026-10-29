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

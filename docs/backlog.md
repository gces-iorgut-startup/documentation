# Backlog Geral do Produto

O backlog a seguir contempla as atividades de engenharia, refatoracao, documentacao e desenvolvimento focadas na evolucao do Iougurt e separadas por categorias técnicas.

## Mobile (Prototipo e App)

- **MOB-01**: Setup inicial Reactive Native.
- **MOB-02**: Cache persistente offline e Pull-to-Refresh.
- **MOB-03**: Geracao de build Android (.apk).
- **DEV E TEST US01 a US15**: Historias de usuario focadas na experiencia do tutor (Acessar aplicativo, visualizar animais, consultar resumo de saude, alternar pets, logout, detalhes de consulta, entre outras).

## Seguranca

- **SEC-01**: Remover ou proteger com secret a rota backdoor de delecao de clinicas e restringir a ambiente de testes.
- **SEC-02**: Atualizar dependencias vulneraveis do backend (fastify, fastify-jwt).
- **SEC-03**: Migrar armazenamento de sessao do localStorage para Cookies HttpOnly com protecao CSRF.

## Frontend Web e Usabilidade

- **FE-01**: Excluir codigo morto de paginas de desenvolvimento e atualizar dependencias vulneraveis.
- **FE-02**: Redesign e implementacao da nova Landing Page institucional, removendo dados ficticios.
- **FE-03**: Refatorar paginas monoliticas de Paciente, extraindo componentes reutilizaveis.
- **FE-04**: Refatorar a pagina de cuidados clinicos, dividindo as secoes em abas acessiveis e isoladas.
- **FE-05**: Implementar funcionalidade de solicitacao de agendamento e retorno diretamente pelo Portal do Tutor.

## Backend e Regras de Negocio

- **BE-01**: Permitir que o perfil OWNER possa iniciar o prontuario de qualquer consulta vinculada a sua clinica.
- **BE-02**: Modelar e implementar exclusao logica (Soft Delete) em Pacientes e Tutores no Prisma.
- **BE-03**: Criar endpoint de listagem e gerenciamento de veterinarios da clinica focado no perfil OWNER.
- **BE-04**: Implementar envio de e-mails automaticos via Resend para lembretes de consultas (24h antes).
- **BE-05**: Criar endpoints dedicados para solicitacao e aprovacao de agendamentos solicitados pelo tutor.
- **FIN-01**: Modulo Financeiro Basico com registros de valores e metodos de pagamento no encerramento da consulta.

## Design e Prototipacao (UX/UI)

- **PROT-01**: Elaboracao de prototipos de alta fidelidade referentes as funcionalidades de Acesso e Meu Pet (US01 a US08).
- **PROT-02**: Elaboracao de prototipos de alta fidelidade referentes as funcionalidades de Saude e Agenda (US09 a US15).

## Bug Fixes e Manutencao

- **BUG-01**: Analise e correcao das falhas e inconsistencias relacionadas ao fluxo de cadastro de senhas do tutor.

## Testes, CI/CD e Infraestrutura

- **QA-01**: Criar suite de testes unitarios no Frontend para os componentes de autenticacao e stores de estado.
- **QA-02**: Adicionar testes unitarios em formularios e validacoes de mascaras do Frontend (CPF, Telefone, CEP).
- **QA-03**: Criar testes E2E para o fluxo completo do Portal do Tutor e App Mobile usando emuladores.
- **CI-01**: Corrigir timeouts de integracao nas pipelines do Vitest e adicionar verificacao de seguranca npm audit.
- **CI-02**: Configurar ChromeDriver em modo headless nas GitHub Actions do Frontend para testes E2E.
- **CI-03**: Implementar pipeline de build e deploy continuo da documentacao (MkDocs) via GitHub Pages.
- **CI-04**: Implementar pipeline de build e deploy continuo da documentacao (MkDocs) via GitHub Pages.
- **INFRA-01**: Definir o provisionamento de infraestrutura em nuvem, decidindo entre Docker em VPS padrao ou migracao AWS/GCP.

## Detalhamento das Historias de Usuario (Mobile)

### Objetivo do Projeto

Criar um prototipo navegavel de um aplicativo mobile do Iougurt voltado para o **tutor do animal**, permitindo acompanhar seus pets, informacoes de saude e consultas.

**Escopo:** Prototipo mobile    
**Ferramenta:** Figma  
**Entregavel:** Prototipo navegavel de alta fidelidade

---

### US01 - Acessar o aplicativo

**Historia de Usuario**
> Como tutor, quero acessar o aplicativo utilizando minhas credenciais, para consultar as informacoes dos meus animais.

**Criterios de Aceite**
- [ ] Exibir campo de e-mail.
- [ ] Exibir campo de senha.
- [ ] Disponibilizar botao de login.
- [ ] Disponibilizar opcao de recuperacao de senha.
- [ ] Login com sucesso direciona para a Home.
- [ ] Representar visualmente o cenario de credenciais invalidas.

---

### US02 - Recuperar acesso

**Historia de Usuario**
> Como tutor, quero recuperar minha senha, para voltar a acessar o aplicativo caso eu esqueca minhas credenciais.

**Criterios de Aceite**
- [ ] Permitir informar e-mail.
- [ ] Disponibilizar opcao de solicitar recuperacao.
- [ ] Exibir confirmacao da solicitacao.
- [ ] Representar erro para e-mail invalido.

---

### US03 - Visualizar meus pets

**Historia de Usuario**
> Como tutor, quero visualizar os animais vinculados a minha conta, para escolher qual pet desejo consultar.

**Criterios de Aceite**
- [ ] Exibir pets vinculados ao tutor.
- [ ] Exibir nome do pet.
- [ ] Exibir foto do pet.
- [ ] Permitir selecionar um pet.

---

### US04 - Visualizar informacoes do pet

**Historia de Usuario**
> Como tutor, quero visualizar os dados do meu pet, para consultar suas principais informacoes.

**Criterios de Aceite**
- [ ] Exibir nome.
- [ ] Exibir foto.
- [ ] Exibir especie.
- [ ] Exibir raca.
- [ ] Exibir idade ou data de nascimento.
- [ ] Exibir sexo.
- [ ] Exibir peso.

---

### US05 - Alternar entre pets

**Historia de Usuario**
> Como tutor, quero alternar entre meus animais, para consultar as informacoes de cada um deles.

**Criterios de Aceite**
- [ ] Exibir os pets vinculados a conta.
- [ ] Permitir selecionar outro pet.
- [ ] Atualizar as informacoes conforme o pet selecionado.

---

### US06 - Visualizar resumo de saude

**Historia de Usuario**
> Como tutor, quero visualizar um resumo da saude do meu pet, para acompanhar rapidamente sua situacao.

**Criterios de Aceite**
- [ ] Exibir resumo das informacoes de saude.
- [ ] Exibir situacao das vacinas.
- [ ] Exibir informacoes recentes.
- [ ] Exibir recomendacoes ou alertas relevantes.
- [ ] Permitir acessar informacoes detalhadas.

---

### US07 - Navegar pela Home

**Historia de Usuario**
> Como tutor, quero acessar as principais areas do aplicativo pela Home, para encontrar rapidamente as informacoes do meu pet.

**Criterios de Aceite**
- [ ] Home deve apresentar acesso aos pets.
- [ ] Home deve apresentar acesso a saude.
- [ ] Home deve apresentar acesso a agenda.
- [ ] Navegacao deve ser consistente entre as telas.
- [ ] Deve existir uma forma clara de retornar a Home.

---

### US08 - Logout

**Historia de Usuario**
> Como tutor, quero sair da minha conta, para impedir que outra pessoa acesse meus dados.

**Criterios de Aceite**
- [ ] Disponibilizar opcao de sair.
- [ ] Solicitar confirmacao antes do logout.
- [ ] Apos sair, retornar a tela de login.

---

### US09 - Visualizar historico clinico

**Historia de Usuario**
> Como tutor, quero visualizar o historico clinico do meu pet, para acompanhar os atendimentos realizados.

**Criterios de Aceite**
- [ ] Exibir lista de atendimentos.
- [ ] Exibir data do atendimento.
- [ ] Exibir tipo de atendimento.
- [ ] Permitir acessar os detalhes do atendimento.
- [ ] Representar historico vazio.

---

### US10 - Visualizar vacinas

**Historia de Usuario**
> Como tutor, quero visualizar as vacinas do meu pet, para saber quais estao em dia e quais precisam de atencao.

**Criterios de Aceite**
- [ ] Exibir nome da vacina.
- [ ] Exibir data da aplicacao.
- [ ] Exibir proxima dose.
- [ ] Exibir status da vacina.
- [ ] Diferenciar visualmente situacoes pendentes.

---

### US11 - Visualizar exames

**Historia de Usuario**
> Como tutor, quero visualizar os exames realizados pelo meu pet, para acompanhar seus registros medicos.

**Criterios de Aceite**
- [ ] Exibir exames disponiveis.
- [ ] Exibir data.
- [ ] Exibir tipo de exame.
- [ ] Permitir acessar detalhes do exame.
- [ ] Representar ausencia de exames.

---

### US12 - Visualizar recomendacoes veterinarias

**Historia de Usuario**
> Como tutor, quero visualizar recomendacoes relacionadas ao meu pet, para saber quais cuidados devo realizar.

**Criterios de Aceite**
- [ ] Exibir recomendacoes.
- [ ] Exibir informacoes importantes sobre o cuidado.
- [ ] Exibir prazo ou data quando aplicavel.
- [ ] Diferenciar recomendacoes importantes ou urgentes.

---

### US13 - Visualizar proximas consultas

**Historia de Usuario**
> Como tutor, quero visualizar as proximas consultas do meu pet, para acompanhar meus compromissos com a clinica.

**Criterios de Aceite**
- [ ] Exibir data.
- [ ] Exibir horario.
- [ ] Exibir pet.
- [ ] Exibir tipo de atendimento.
- [ ] Permitir acessar os detalhes da consulta.
- [ ] Representar ausencia de consultas futuras.

---

### US14 - Visualizar detalhes da consulta

**Historia de Usuario**
> Como tutor, quero visualizar os detalhes de uma consulta, para saber quando e onde o atendimento acontecera.

**Criterios de Aceite**
- [ ] Exibir pet.
- [ ] Exibir data.
- [ ] Exibir horario.
- [ ] Exibir profissional.
- [ ] Exibir tipo de atendimento.
- [ ] Exibir informacoes adicionais quando disponiveis.

---

### US15 - Agendar consulta

**Historia de Usuario**
> Como tutor, quero solicitar um agendamento para meu pet, para marcar uma consulta com a clinica.

**Criterios de Aceite**
- [ ] Permitir selecionar o pet.
- [ ] Permitir selecionar o tipo de atendimento.
- [ ] Permitir selecionar uma data.
- [ ] Permitir selecionar um horario.
- [ ] Exibir resumo antes da confirmacao.
- [ ] Exibir confirmacao do agendamento.

---

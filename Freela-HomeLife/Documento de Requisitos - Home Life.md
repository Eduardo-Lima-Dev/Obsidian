## Informações sobre o Cliente
**Nome do Cliente:** João Henrique  
**Nome da Empresa:** Home Life  
**Contato:** (89) 99437-0939  

## Descrição do Projeto
**Título do Projeto:** Home Life  

**Resumo do Projeto:**  
Prestação de serviços de saúde domiciliar, democratizando o mesmo, levando para as pessoas uma saúde e um padrão de vida melhor, onde mesmo os que não podem sair de casa para buscar esses atendimentos possam usufruir disso.  

**Objetivo do Projeto:**  
Democratizar a prestação de serviços de saúde domiciliar.  

**Público-alvo:**  
Pessoas que não podem ou preferem não sair de casa para um atendimento.

---

## Personas

### 1. João Silva (Paciente)
- **Idade:** 68 anos
- **Ocupação:** Aposentado
- **Necessidade:** João tem dificuldade de locomoção e precisa de serviços de saúde em casa.
- **Objetivo:** Conseguir marcar consultas médicas e procedimentos sem precisar sair de casa.
- **Frustrações:** A dificuldade de encontrar um profissional disponível em horários acessíveis.

### 2. Maria Oliveira (Cuidadora)
- **Idade:** 45 anos
- **Ocupação:** Cuidadora de idosos
- **Necessidade:** Maria precisa agendar atendimentos médicos para a mãe idosa.
- **Objetivo:** Facilitar o acesso a profissionais de saúde para seus familiares e dependentes.
- **Frustrações:** O processo de agendamento complexo e a falta de opções de pagamento.

### 3. Dr. Ricardo Santos (Médico)
- **Idade:** 42 anos
- **Ocupação:** Médico clínico geral
- **Necessidade:** Dr. Ricardo deseja gerenciar seu horário de atendimento domiciliar e receber por suas consultas.
- **Objetivo:** Organizar sua agenda de forma que possa atender pacientes de forma eficiente.
- **Frustrações:** Dificuldade em gerenciar múltiplos agendamentos sem uma plataforma adequada.

---

## Histórias de Usuário

### História 1: Cadastro de Paciente
**Como** um usuário,  
**Eu quero** poder criar um cadastro pessoal e de paciente,  
**Para que** eu consiga solicitar atendimentos para mim ou para familiares.

### História 2: Agendamento de Consulta
**Como** um paciente,  
**Eu quero** selecionar o horário e o profissional de saúde disponível,  
**Para que** eu possa receber o atendimento no melhor momento para mim.

### História 3: Sistema de Pagamento
**Como** um paciente,  
**Eu quero** ter a opção de pagar online (cartão ou PIX) ou na hora do atendimento,  
**Para que** eu possa concluir o pagamento da forma mais conveniente.

### História 4: Cadastro de Médicos
**Como** um administrador,  
**Eu quero** cadastrar médicos e enfermeiros com e-mail e senha,  
**Para que** eles possam ter acesso ao sistema e gerenciar seus horários.

### História 5: Aviso de Agendamento
**Como** um médico ou enfermeiro,  
**Eu quero** ser notificado quando um paciente marcar um atendimento comigo,  
**Para que** eu possa me organizar para a consulta.

---

## Requisitos Funcionais

1. **Sistema Duplo:**
   - Um sistema para os usuários finais (pacientes).
   - Um sistema para administradores (médicos e gestores).

2. **Sistema dos Pacientes:**
   - Cadastro pessoal com nome, contato e cidade.
   - Cadastro de atendimento para terceiros (ex.: avós, pais).
   - Seleção de horário e profissional para atendimento.
   - Preenchimento de ficha de anamnese com:
     - Nome do paciente
     - Idade
     - Diagnóstico
     - Alergias
     - Principais necessidades
     - Medicações contínuas
   - Opções de pagamento via cartão, PIX ou presencial.

3. **Sistema dos Administradores:**
   - Cadastro de médicos e enfermeiros.
   - Cadastro de horários de disponibilidade dos profissionais.
   - Cadastro de informações de pagamento (cartão de recebimento para profissionais).

4. **Integração de Pagamento:**
   - Pagamento via PagBank ou outra plataforma de pagamento.

5. **Notificações:**
   - Notificar médicos e enfermeiros sobre novos agendamentos.

---

## Requisitos Não Funcionais

1. **Segurança:**
   - O sistema deve criptografar todas as transações financeiras e dados pessoais dos usuários.
   - Autenticação de dois fatores para acesso de médicos e administradores.

2. **Usabilidade:**
   - Interface intuitiva e simples para os usuários, com foco em acessibilidade.
   - Opção de contato direto via WhatsApp.

3. **Desempenho:**
   - O sistema deve suportar múltiplos usuários simultâneos sem perder desempenho.
   - Tempo de resposta para agendamento e pagamento deve ser inferior a 2 segundos.

4. **Disponibilidade:**
   - Sistema deve estar disponível 99,9% do tempo, com exceção de manutenções programadas.

5. **Compatibilidade:**
   - Deve funcionar em navegadores modernos e dispositivos móveis.

---

## Integrações com Outras Plataformas

- Integração com sistemas de pagamento como PagBank.
- Possibilidade de integração com plataformas futuras para notificações (WhatsApp Business API).

---

## Cronograma e Prazos

- **Data de início:** 03 de junho de 2024
- **Reuniões:** Uma vez por mês, apresentando o progresso e coletando feedback.
- **Prazo final:** Conforme a evolução das etapas e aprovação nas reuniões mensais.

---

## Orçamento

- **Hospedagem:** Inicialmente na Vercel.
  
---

## Comunicação e Aprovação

- **Canal de Comunicação:** Preferencialmente via WhatsApp.
- **Processo de Aprovação:** Reuniões mensais via Meet para apresentação do progresso e coleta de aprovação.

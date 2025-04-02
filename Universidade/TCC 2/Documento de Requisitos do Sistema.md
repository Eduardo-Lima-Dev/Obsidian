---
tags:
  - Universidade
materia: TCC
tipo: Atividade
---
# 1. Introdução

Este documento tem como objetivo apresentar os requisitos do sistema de gerenciamento acadêmico, que auxiliará os alunos a acompanhar seu progresso no curso, cadastrando informações, visualizando desempenho e utilizando funcionalidades adicionais para melhorar a experiência de estudo.

## 2. Escopo do Sistema

O sistema permitirá que o aluno:
- Realize o cadastro e login;
- Consulte a lista de matérias, com distinção entre as já concluídas e as pendentes;
- Cadastre matérias optativas, diferenciando entre livres e obrigatórias;
- Acompanhe seu desempenho por meio de um dashboard interativo;
- Visualize gráficos detalhados dos períodos de cada matéria;
- Consulte informações detalhadas de cada disciplina (incluindo pré-requisitos);
- Marque o estado de cada matéria (Concluída, Em Progresso ou Reprovada);
- Escolha entre temas claro e escuro para a interface;
- Leia uma explicação sobre o funcionamento do sistema (não integrado ao SIGAA);
- (Opcionalmente) Utilize um módulo de estudo com temporizador Pomodoro.

## 3. Requisitos Funcionais

### 3.1. Cadastro e Login
- **RF001:** O sistema deverá permitir o cadastro de novos usuários, solicitando Nome, Curso, Semestre, Email e Senha.
- **RF002:** O sistema deverá possibilitar o login do usuário com email e senha.

### 3.2. Visualização de Matérias Concluídas
- **RF003:** Ao iniciar, se o usuário não estiver no 1° semestre, o sistema deverá exibir a lista de matérias do curso, destacando aquelas já concluídas.

### 3.3. Cadastro de Matérias Optativas
- **RF004:** O sistema deverá oferecer um campo para cadastro de matérias optativas, diferenciando entre matérias livres e obrigatórias.

### 3.4. Dashboard Interativo
- **RF005:** O dashboard deverá exibir cards que informem a quantidade de matérias concluídas e as que faltam.
- **RF006:** O dashboard deverá incluir um diagrama que evidencie, com cores diferenciadas, as matérias ainda não concluídas.

### 3.5. Visualização dos Gráficos
- **RF007:** O sistema deverá permitir a alteração do tipo de visualização dos gráficos, que exibirão os períodos de cada matéria.

### 3.6. Gestão de Pré-Requisitos
- **RF008:** As matérias que possuírem pré-requisitos deverão apresentar, de forma clara, as relações e dependências entre elas.

### 3.7. Detalhamento da Matéria (Card de Matéria)
- **RF009:** Ao clicar em uma matéria, o sistema deverá exibir um card com:
  - Código da matéria;
  - Nome;
  - Período;
  - Carga horária;
  - Pré-requisitos;
  - Botão para marcar a matéria como concluída.

### 3.8. Atualização do Estado da Matéria
- **RF010:** O usuário deverá poder atualizar o estado de cada matéria (Concluída, Em Progresso, Reprovada) ao final de cada semestre.

### 3.9. Temas da Interface
- **RF011:** O sistema deverá oferecer suporte a temas claro e escuro, permitindo ao usuário alternar conforme sua preferência.

### 3.10. Explicação do Sistema
- **RF012:** Deverá ser disponibilizada uma breve explicação do funcionamento do sistema, esclarecendo que o mesmo não é integrado ao SIGAA.

### 3.11. Interface Responsiva
- **RF013:** A interface deverá ser simples, intuitiva e responsiva, garantindo boa visualização em dispositivos móveis.

### 3.12. Funcionalidade Adicional (Caso de Tempo)
- **RF014 (Opcional):** Caso haja tempo disponível, implementar um módulo de estudo com:
  - Temporizador Pomodoro;
  - Opção para o usuário selecionar a matéria que está estudando.

## 4. Requisitos Não Funcionais

- **RNF001 – Usabilidade:** A interface deve ser intuitiva e de fácil navegação, com foco na experiência do usuário.
- **RNF002 – Performance:** O sistema deve carregar de forma rápida, mesmo com a exibição de gráficos e dashboards.
- **RNF003 – Segurança:** Os dados dos usuários (especialmente senhas) devem ser armazenados de forma segura, utilizando técnicas de criptografia.
- **RNF004 – Compatibilidade:** O sistema deverá funcionar corretamente em navegadores modernos e ser compatível com dispositivos móveis.
- **RNF005 – Manutenibilidade:** O código deverá ser modular e bem documentado para facilitar manutenções e futuras atualizações.
- **RNF006 – Escalabilidade:** O sistema deve suportar um aumento no número de usuários sem perda de desempenho.
- **RNF007 – Acessibilidade:** A interface deverá seguir as diretrizes de acessibilidade para atender usuários com diferentes necessidades.

## 5. Histórias de Usuário

- **HU001 – Cadastro e Login:**
  - *Como aluno, desejo me cadastrar utilizando nome, curso, semestre, email e senha, para acessar minhas informações acadêmicas.*

- **HU002 – Visualização de Matérias:**
  - *Como aluno, desejo visualizar a lista de matérias do meu curso, com destaque para as já concluídas, para acompanhar meu progresso.*

- **HU003 – Cadastro de Matérias Optativas:**
  - *Como aluno, desejo cadastrar matérias optativas (livres e obrigatórias), para personalizar meu percurso acadêmico.*

- **HU004 – Dashboard Interativo:**
  - *Como aluno, desejo acessar um dashboard que mostre, por meio de cards e gráficos, quantas matérias já concluí e quantas ainda faltam, para ter uma visão geral do meu desempenho.*

- **HU005 – Visualização de Gráficos:**
  - *Como aluno, desejo alterar o tipo de visualização dos gráficos que indicam os períodos das matérias, para ter diferentes perspectivas sobre meu planejamento.*

- **HU006 – Gestão de Pré-Requisitos:**
  - *Como aluno, desejo visualizar as relações de pré-requisitos entre as matérias, para planejar adequadamente minha trajetória acadêmica.*

- **HU007 – Detalhamento da Matéria:**
  - *Como aluno, desejo clicar em uma matéria e visualizar suas informações detalhadas (código, nome, período, carga horária, pré-requisitos e opção de marcar como concluída), para obter mais detalhes sobre ela.*

- **HU008 – Atualização do Estado da Matéria:**
  - *Como aluno, desejo atualizar o estado de cada matéria (concluída, em progresso ou reprovada) ao final de cada semestre, para manter meus registros atualizados.*

- **HU009 – Alternância de Temas:**
  - *Como aluno, desejo alternar entre os temas claro e escuro, para adequar a interface à minha preferência visual.*

- **HU010 – Explicação do Sistema:**
  - *Como aluno, desejo ler uma breve explicação sobre o funcionamento do sistema e a não integração com o SIGAA, para entender suas funcionalidades e limitações.*

- **HU011 – Módulo de Pomodoro (Opcional):**
  - *Como aluno, desejo utilizar um módulo de estudo com temporizador Pomodoro e a opção de selecionar a matéria que estou estudando, para gerenciar melhor meu tempo de estudo.*

## 6. Considerações Finais

Este documento de requisitos estabelece a base para o desenvolvimento do sistema, assegurando que as necessidades dos alunos sejam atendidas e que a aplicação seja intuitiva, segura e responsiva. Futuras revisões poderão incluir ajustes e novos requisitos com base no feedback dos usuários e nas demandas do mercado.


> [!Camada Aplicação] Próximos Assuntos 
> [[Lista de Exercı́cios 1|Lista de Exercı́cios 1]]
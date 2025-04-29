
## 1. Objetivo do Sistema
O sistema será um aplicativo de organização de tarefas baseado no conceito de Bullet Journal, onde os usuários poderão adicionar atividades, atribuir pesos a essas atividades, ganhar pontos por atividades concluídas e participar de um ranking semanal. O foco é na gamificação para engajar os usuários.

## 2. Descrição do Problema
O aplicativo visa ajudar os usuários a se manterem organizados e motivados através de uma estrutura gamificada, onde cada tarefa possui um peso específico e uma pontuação associada, e os usuários são recompensados por completarem suas atividades. O ranking permitirá que os usuários vejam seu progresso em comparação com os outros.

## 3. Requisitos Funcionais

### 3.1 Cadastro/Login de Usuários
- O usuário deverá criar uma conta ou fazer login usando email e senha.
- O login pode ser feito por redes sociais ou através de contas Google.
- O sistema deve permitir recuperação de senha.

### 3.2 Criação e Organização de Tarefas
- O usuário deve poder criar tarefas (atividades) e atribuir um peso (em pontos) a cada uma.
- A tarefa pode ter um prazo de conclusão e uma categoria (ex: trabalho, pessoal, saúde, etc.).
- O usuário poderá marcar tarefas como concluídas.

### 3.3 Sistema de Pontuação
- O sistema deve atribuir uma pontuação a cada tarefa concluída.
- A pontuação será baseada no peso de cada tarefa.
- A pontuação deve ser acumulada ao longo da semana para formar um total de pontos.
  
### 3.4 Ranking Semanal
- O sistema deve calcular o total de pontos de cada usuário ao longo da semana.
- O ranking será atualizado automaticamente a cada vez que o usuário concluir uma tarefa.
- O ranking deve ser visível para todos os usuários.
- Os 10 melhores do ranking semanal devem ser destacados.
  
### 3.5 Gamificação
- O sistema deve recompensar o usuário com badges ou conquistas por marcos, como:
  - Número de tarefas concluídas em um dia.
  - Conseguir completar tarefas durante toda a semana.
  - Superar o próprio recorde de pontos.
  
### 3.6 Dashboard do Usuário
- O usuário deve ter uma visão geral do seu progresso, incluindo:
  - Tarefas pendentes e concluídas.
  - Total de pontos conquistados na semana.
  - Posicionamento no ranking.
  - Histórico de conquistas e badges.

### 3.7 Notificações
- O sistema deverá enviar notificações ao usuário quando ele tiver tarefas a completar.
- Notificações de lembrete de tarefas pendentes ou para o ranking semanal.

## 4. Requisitos Não Funcionais

- **Segurança**: O login e dados do usuário devem ser protegidos com criptografia (ex: criptografia de senha).
- **Escalabilidade**: O sistema deve ser capaz de suportar um grande número de usuários simultâneos.
- **Desempenho**: O sistema deve ter uma resposta rápida ao criar tarefas, atribuir pontuação e atualizar o ranking.
- **Interface de usuário (UI)**: A interface deve ser simples, intuitiva e responsiva para funcionar bem em dispositivos móveis.

## 5. Prioridades

- **Alta prioridade**: Cadastro e login de usuário, criação e organização de tarefas, sistema de pontuação e ranking.
- **Média prioridade**: Gamificação (badges e conquistas).
- **Baixa prioridade**: Notificações e histórico detalhado de tarefas.

## 6. Critérios de Aceitação

### Cadastro/Login de Usuário
- O usuário pode criar uma conta e fazer login com sucesso.
- O sistema valida o login com informações corretas.
- O sistema envia uma notificação de sucesso ou erro ao tentar recuperar senha.

### Criação de Tarefas
- O usuário pode criar uma tarefa e atribuir um peso corretamente.
- O sistema permite que o usuário marque tarefas como concluídas.
- O usuário consegue visualizar todas as tarefas criadas, com prazos e pesos.

### Ranking Semanal
- O ranking deve ser calculado corretamente com base nos pontos.
- O ranking exibe corretamente a posição de todos os usuários.
- Os melhores colocados são destacados.

### Gamificação (Badges e Conquistas)
- O sistema atribui badges conforme o usuário atinge os marcos de atividades concluídas.
- O usuário pode visualizar os badges conquistados no seu perfil.

## 7. Restrições

- **Acessibilidade**: O app deve ser acessível, com suporte para deficientes visuais (por exemplo, compatibilidade com leitores de tela).
- **Multiplataforma**: O app deve ser desenvolvido para iOS e Android.
- **Armazenamento**: O armazenamento de dados pode ser feito em banco de dados na nuvem (ex: Firebase, AWS).

## 8. Necessidade de Exemplos Visuais

- Mockups da tela inicial (login, painel do usuário).
- Layout da tela de ranking com destaque para os melhores colocados.
- Exemplo de como a tarefa será exibida (com peso e prazo).

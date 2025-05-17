# 1. Introdução

Este documento apresenta os requisitos do **BulletQuest**, um aplicativo móvel e web de organização de tarefas inspirado no método _Bullet Journal_. Seu propósito é ajudar os usuários a planejar e acompanhar atividades diárias, enquanto mantém um sistema de pontuação leve — gamificando a experiência sem comprometer o foco em produtividade.

---

## 2. Escopo do Sistema

O sistema permitirá que o usuário:

- Criar conta e autenticar‐se (e‑mail/senha ou redes sociais);
    
- Registrar, editar e excluir tarefas com pesos, prazos e categorias;
    
- Marcar tarefas como concluídas ou reabri‑las;
    
- Acompanhar pontuação semanal acumulada;
    
- Visualizar ranking semanal com destaque para o _Top 10_;
    
- Receber badges por marcos de produtividade;
    
- Consultar um **dashboard** com progresso, ranking e conquistas;
    
- Receber notificações de prazos e fechamento de ranking;
    
- Sincronizar dados em tempo real entre dispositivos;
    
- (Opcional) Gerenciar categorias, badges e usuários via painel administrativo.
    

---

## 3. Requisitos Funcionais

### 3.1 Cadastro e Autenticação

- **RF001:** Permitir criação de conta via e‑mail e senha.
    
- **RF002:** Permitir login social (Google, Apple, GitHub).
    
- **RF003:** Disponibilizar recuperação de senha por e‑mail.
    

### 3.2 Gestão de Tarefas

- **RF004:** Criar tarefas contendo título, descrição opcional, peso (pontos), prazo e categoria.
    
- **RF005:** Editar ou excluir tarefas existentes.
    
- **RF006:** Marcar e desmarcar tarefas como concluídas.
    
- **RF007:** Listar tarefas com filtros (pendentes, concluídas, categoria, prazo).
    

### 3.3 Pontuação

- **RF008:** Atribuir pontos conforme o peso da tarefa ao marcá‑la como concluída.
    
- **RF009:** Atualizar saldo de pontos semanal em tempo real.
    

### 3.4 Ranking Semanal

- **RF010:** Gerar ranking automático com base no total de pontos semanais.
    
- **RF011:** Exibir posição do usuário e destacar os 10 primeiros colocados.
    
- **RF012:** Reiniciar o ranking toda segunda‑feira 00:00 UTC‑3.
    

### 3.5 Gamificação

- **RF013:** Conceder badges ao atingir marcos pré‑definidos (ex.: 20 tarefas em 7 dias).
    
- **RF014:** Disponibilizar tela de conquistas no perfil do usuário.
    

### 3.6 Dashboard

- **RF015:** Mostrar visão geral de tarefas pendentes/concluídas, pontos, ranking e badges.
    

### 3.7 Notificações

- **RF016:** Enviar lembretes push/e‑mail de tarefas próximas do prazo.
    
- **RF017:** Notificar encerramento do ranking semanal e início de nova contagem.
    

### 3.8 Administração (Opcional)

- **RF018:** Permitir a administradores gerenciar categorias padrão, metas de badges e usuários.
    

### 3.9 Sincronização

- **RF019:** Sincronizar dados de tarefas e pontos entre dispositivos em tempo real (WebSockets).
    

---

## 4. Requisitos Não Funcionais

- **RNF001 – Usabilidade:** Interface limpa, responsiva e baseada em componentes reutilizáveis para facilitar o trabalho de design.
    
- **RNF002 – Performance:** Ações de CRUD devem responder em até 300 ms na média.
    
- **RNF003 – Segurança:** Autenticação via JWT; senhas criptografadas com _bcrypt_; comunicação HTTPS/TLS 1.3.
    
- **RNF004 – Compatibilidade:** PWA responsivo nos principais navegadores; apps nativos via _wrapper_ (Capacitor/Ionic).
    
- **RNF005 – Manutenibilidade:** Código modular em TypeScript, testes unitários/integração (>80 % cobertura).
    
- **RNF006 – Escalabilidade:** Backend _stateless_ com _horizontal scaling_ (Docker/Kubernetes) e banco PostgreSQL.
    
- **RNF007 – Acessibilidade:** Conformidade WCAG 2.1 AA; compatível com leitores de tela e contraste adequado.
    

---

## 5. Histórias de Usuário

- **HU001 – Cadastro Rápido:**
    
    - _Como visitante_, desejo criar uma conta em poucos passos, para começar a organizar minhas tarefas sem dificuldades.
        
- **HU002 – Concluir Tarefa:**
    
    - _Como usuário_, desejo marcar uma tarefa como concluída, para receber meus pontos automaticamente.
        
- **HU003 – Consultar Ranking:**
    
    - _Como usuário_, desejo ver minha posição no ranking semanal, para me motivar a completar mais tarefas.
        
- **HU004 – Receber Lembrete:**
    
    - _Como usuário_, desejo receber uma notificação quando o prazo de uma tarefa estiver próximo, para não perder prazos importantes.
        

---

## 6. Considerações Finais

Este documento de requisitos estabelece a base para o desenvolvimento do **BulletQuest**, garantindo que as necessidades de usuários, desenvolvedores (frontend em _Next.js + React_, backend em _Express/Node.js_ + PostgreSQL) e designers sejam atendidas. O projeto adota sprints de 2 semanas gerenciadas no Trello e será ajustado continuamente com base em feedback de uso e métricas de engajamento.
# 1. Introdução

Este documento descreve os requisitos do **BulletQuest**, um aplicativo **web** de organização de tarefas inspirado no método *Bullet Journal*. Seu objetivo é ajudar usuários a planejar e acompanhar suas atividades diárias enquanto se mantêm motivados por meio de um sistema de pontuação leve (gamificação).

---

## 2. Escopo do Sistema

O sistema permitirá que o usuário:

- Criar conta e autenticar‐se (e‑mail/senha ou contas sociais);
- Registrar, editar e excluir tarefas com pesos, prazos e categorias;
- Marcar tarefas como concluídas ou reabri‑las;
- Acompanhar pontuação semanal acumulada;
- Visualizar ranking semanal com destaque para o *Top 10*;
- Receber badges por marcos de produtividade;
- Consultar um **dashboard** com progresso, ranking e conquistas;
- Receber notificações de prazos e fechamento de ranking;
- Sincronizar dados em tempo real entre dispositivos (sessões do navegador).

---

## 3. Requisitos Funcionais

### 3.1 Cadastro e Autenticação
- **RF001:** Permitir criação de conta via e‑mail e senha;  
- **RF002:** Permitir login social (Google, GitHub, Apple);  
- **RF003:** Disponibilizar recuperação de senha por e‑mail.  

### 3.2 Gestão de Tarefas
- **RF004:** Criar tarefas contendo título, descrição opcional, peso (pontos), prazo e categoria;  
- **RF005:** Editar ou excluir tarefas existentes;  
- **RF006:** Marcar e desmarcar tarefas como concluídas;  
- **RF007:** Listar tarefas com filtros (pendentes, concluídas, categoria, prazo).  

### 3.3 Pontuação
- **RF008:** Atribuir pontos conforme o peso da tarefa ao marcá‑la como concluída;  
- **RF009:** Atualizar saldo de pontos semanal em tempo real.  

### 3.4 Ranking Semanal
- **RF010:** Gerar ranking automático com base no total de pontos semanais;  
- **RF011:** Exibir posição do usuário e destacar os 10 primeiros colocados;  
- **RF012:** Reiniciar o ranking toda segunda‑feira 00:00 (UTC‑3).  

### 3.5 Gamificação
- **RF013:** Conceder badges ao atingir marcos pré‑definidos (ex.: 20 tarefas em 7 dias);  
- **RF014:** Disponibilizar tela de conquistas no perfil do usuário.  

### 3.6 Dashboard
- **RF015:** Mostrar visão geral de tarefas pendentes/concluídas, pontos, ranking e badges.  

### 3.7 Notificações
- **RF016:** Enviar lembretes (push ou e‑mail) de tarefas próximas do prazo;  
- **RF017:** Notificar encerramento do ranking semanal e início de nova contagem.  

### 3.8 Administração (Opcional)
- **RF018:** Permitir a administradores gerenciar categorias padrão, metas de badges e usuários.  

### 3.9 Sincronização
- **RF019:** Sincronizar dados de tarefas e pontos entre sessões do navegador em tempo real (WebSockets).  

---

## 4. Requisitos Não Funcionais

| Código | Descrição |
|--------|-----------|
| **RNF001 – Usabilidade** | Interface limpa, responsiva e baseada em componentes reutilizáveis, facilitando o trabalho de design. |
| **RNF002 – Performance** | Operações de CRUD devem responder em até **300 ms** na média. |
| **RNF003 – Segurança** | Autenticação via **JWT**; senhas criptografadas com *bcrypt*; comunicação HTTPS/TLS 1.3. |
| **RNF004 – Compatibilidade** | Aplicação **web responsiva** compatível com os principais navegadores desktop e mobile; não serão fornecidos aplicativos nativos. |
| **RNF005 – Manutenibilidade** | Código modular em **TypeScript**, testes unitários e de integração (> 80 % de cobertura). |
| **RNF006 – Escalabilidade** | Backend *stateless* com escalonamento horizontal (Docker/Kubernetes) e banco **PostgreSQL**. |
| **RNF007 – Acessibilidade** | Conformidade **WCAG 2.1 AA**; compatível com leitores de tela e contraste adequado. |

---

## 5. Histórias de Usuário

| ID | História | Critérios de Aceitação |
|----|----------|------------------------|
| **HU001** | *Como visitante*, quero criar uma conta rapidamente para começar a organizar minhas tarefas. | Conta criada com e‑mail ou login social em ≤ 2 min. |
| **HU002** | *Como usuário*, quero marcar uma tarefa como concluída para receber meus pontos. | Pontos atualizados instantaneamente após check‑off. |
| **HU003** | *Como usuário*, quero ver minha posição no ranking semanal para me motivar. | Ranking exibe posição, pontos e top 10. |
| **HU004** | *Como usuário*, quero receber uma notificação próximo ao prazo de uma tarefa para não me atrasar. | Notificação enviada T‑30 min do prazo configurado. |

---

## 6. Restrições

- **Acessibilidade:** Deve atender WCAG 2.1 AA.  
- **Plataforma:** O BulletQuest será disponibilizado **exclusivamente como aplicação web responsiva**; não haverá desenvolvimento de apps nativos para iOS ou Android.  
- **Armazenamento:** Dados persistidos em banco **PostgreSQL** em nuvem (ex.: Supabase, AWS RDS).  

---

## 7. Sprints e Ferramentas

- **Tecnologias Front‑end:** Next.js + React + TailwindCSS;  
- **Tecnologias Back‑end:** Express (Node.js) + Prisma ORM + PostgreSQL;  
- **Controle de Versão:** Git & GitHub;  
- **Metodologia:** Sprints de 2 semanas gerenciadas no **Trello**.  

---

## 8. Considerações Finais

Este documento de requisitos define a base para o desenvolvimento do **BulletQuest** como uma aplicação web responsiva. Ele garante alinhamento entre times de back‑end, front‑end e design, fornecendo um guia único e de fácil leitura. Alterações e melhorias serão avaliadas a cada sprint com base no feedback dos usuários e nas métricas de engajamento.
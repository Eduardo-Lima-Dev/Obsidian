# 1. Introdução

Este documento tem como objetivo apresentar os requisitos do sistema **Despesas Compartilhadas**, que tem como propósito facilitar o controle de despesas domésticas entre moradores de uma mesma residência por meio de funcionalidades colaborativas, como convites por link, visualização compartilhada e divisão de valores.

## 2. Escopo do Sistema

O sistema permitirá que o usuário:
- Crie uma conta;
- Faça login em sua conta;
- Registre despesas domésticas;
- Classifique as despesas como compartilhadas ou individuais;
- Marque despesas como recorrentes;
- Visualize o status de pagamento de cada despesa;
- Compartilhe despesas com outras pessoas por meio de link de convite;
- Visualize despesas de outros usuários da mesma casa;
- Adicione novas despesas em uma casa compartilhada;
- Visualize o valor total das despesas da casa;
- Visualize o total gasto por pessoa;
- Visualize a divisão das despesas por igual entre os moradores;
- Cadastre e visualize a chave Pix de cada usuário;
- Acesse histórico de despesas por mês;
- Aplique filtros por categoria, pessoa, recorrência e pagamento;
- (Opcional) Receba notificações sobre vencimentos e despesas recorrentes.

## 3. Requisitos Funcionais

### 3.1. Autenticação e Conta de Usuário
- **RF001:** O sistema deve permitir a criação de contas com e-mail e senha.
- **RF002:** O sistema deve permitir login com autenticação segura.
- **RF003:** O sistema deve permitir que cada usuário cadastre sua chave Pix no perfil.

### 3.2. Gerenciamento de Despesas
- **RF004:** O sistema deve permitir o registro de despesas com descrição, valor, data, recorrência e status de pagamento.
- **RF005:** O sistema deve permitir marcar uma despesa como "paga" ou "não paga".
- **RF006:** O sistema deve replicar automaticamente despesas recorrentes a cada mês.

### 3.3. Compartilhamento de Casas
- **RF007:** O sistema deve permitir classificar uma despesa como compartilhada.
- **RF008:** O sistema deve permitir que o usuário gere um link de convite para compartilhar sua casa.
- **RF009:** O sistema deve permitir que usuários aceitem convites e participem da mesma casa.

### 3.4. Visualização e Análise
- **RF010:** O sistema deve permitir visualizar a lista de despesas de uma casa.
- **RF011:** O sistema deve exibir o valor total das despesas da casa.
- **RF012:** O sistema deve exibir o valor total de despesas atribuídas a cada usuário.
- **RF013:** O sistema deve exibir a divisão igualitária do total (ex: valor total ÷ número de moradores).
- **RF014:** O sistema deve permitir filtros por: categoria, status de pagamento, usuário e recorrência.
- **RF015:** O sistema deve exibir a chave Pix dos participantes da casa compartilhada.

## 4. Requisitos Não Funcionais

- **RNF001 – Usabilidade:** Interface simples e responsiva, com foco na clareza das informações financeiras.
- **RNF002 – Performance:** O sistema deve responder em até 2 segundos para ações comuns.
- **RNF003 – Segurança:** Dados sensíveis (ex: senha e chave Pix) devem ser criptografados.
- **RNF004 – Compatibilidade:** Suporte a navegadores modernos e dispositivos móveis.
- **RNF005 – Manutenibilidade:** Código modular e documentado para facilitar futuras atualizações.
- **RNF006 – Escalabilidade:** Capacidade de gerenciar múltiplos usuários e casas simultaneamente.
- **RNF007 – Acessibilidade:** Interface compatível com leitores de tela e navegação por teclado.

## 5. Histórias de Usuário

- **HU001 – Criar conta e login:**
  - *Como usuário, desejo criar uma conta e fazer login, para acessar minhas despesas e casas compartilhadas.*

- **HU002 – Registrar despesa:**
  - *Como usuário autenticado, desejo registrar uma nova despesa, para controlar os gastos da casa.*

- **HU003 – Marcar pagamento de despesa:**
  - *Como usuário, desejo marcar se uma despesa foi paga ou não, para manter o controle financeiro.*

- **HU004 – Dividir despesas e ver valores por pessoa:**
  - *Como usuário, desejo ver o valor total das despesas, o que cabe a cada pessoa, e o que cada um gastou, para facilitar a divisão dos custos.*

- **HU005 – Chave Pix:**
  - *Como usuário, desejo cadastrar e visualizar a chave Pix dos participantes, para realizar transferências.*

- **HU006 – Compartilhar casa:**
  - *Como usuário, desejo compartilhar minha casa via link, para que outras pessoas possam contribuir com as despesas.*

## 6. Considerações Finais

Este documento define os requisitos do sistema **Despesas Compartilhadas**, voltado à organização colaborativa de finanças domésticas. A clareza, segurança e usabilidade são os pilares da aplicação. Requisitos poderão ser refinados conforme surgirem novas demandas.
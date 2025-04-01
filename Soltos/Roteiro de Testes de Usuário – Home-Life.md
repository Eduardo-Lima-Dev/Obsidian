
---

Este documento descreve o roteiro para a execução dos testes de usabilidade do sistema **Home-Life**. O objetivo é validar a experiência do usuário, identificar pontos de melhoria e garantir que as funcionalidades atendam às necessidades dos usuários finais.

## Objetivos dos Testes

- **Avaliar a Usabilidade:** Verificar a facilidade de navegação e utilização das funcionalidades.
- **Identificar Problemas:** Detectar erros, inconsistências e áreas de melhoria na interface.
- **Coletar Feedback:** Obter sugestões e opiniões dos usuários para aprimorar a experiência.

## Perfil dos Usuários

- Usuários com conhecimentos básicos em tecnologia.
- Proprietários de residências interessados em automação e gerenciamento de dispositivos.
- Profissionais da área de manutenção ou TI que implementam soluções residenciais.

## Cenários de Teste

### Cenário 1: Cadastro e Login

**Objetivo:** Verificar se o fluxo de cadastro e login está funcionando sem erros.

**Passos:**
1. Acessar a página de cadastro.
2. Preencher os dados obrigatórios (nome, email, senha) e submeter.
3. Verificar o recebimento de e-mail de confirmação (se aplicável).
4. Realizar o login com as credenciais criadas.
5. Validar que o usuário é redirecionado para o dashboard.

**Critérios de Aceitação:**
- Cadastro realizado com sucesso.
- Redirecionamento para o dashboard após o login.
- Mensagens de erro adequadas em caso de dados inválidos.

### Cenário 2: Gerenciamento de Dispositivos

**Objetivo:** Testar a funcionalidade de adicionar, editar e remover dispositivos.

**Passos:**
1. No dashboard, acessar a seção “Dispositivos”.
2. Adicionar um novo dispositivo preenchendo os dados necessários (nome, tipo, status).
3. Editar o dispositivo recém-adicionado, alterando informações como nome e status.
4. Remover o dispositivo e confirmar a exclusão.

**Critérios de Aceitação:**
- Dispositivo adicionado com sucesso e listado corretamente.
- Edição salva e refletida na interface.
- Remoção efetivada sem erros e com feedback visual adequado.

### Cenário 3: Configuração de Alertas e Notificações

**Objetivo:** Validar a configuração e o funcionamento das notificações.

**Passos:**
1. Acessar a área de configurações.
2. Configurar alertas para eventos específicos (ex.: queda de energia, invasão).
3. Simular a ocorrência de um evento para verificar se a notificação é disparada.
4. Confirmar o recebimento da notificação (via email, SMS ou na própria interface).

**Critérios de Aceitação:**
- Configuração salva corretamente.
- Notificações disparadas de acordo com as regras configuradas.
- Mensagens de alerta claras e informativas.

### Cenário 4: Geração e Visualização de Relatórios

**Objetivo:** Testar a funcionalidade de geração e exibição de relatórios.

**Passos:**
1. Navegar até a seção “Relatórios”.
2. Selecionar um período para geração do relatório (ex.: últimos 7 dias).
3. Gerar e visualizar o relatório.
4. Exportar o relatório em formato PDF ou CSV.

**Critérios de Aceitação:**
- Relatório gerado sem erros.
- Dados apresentados de forma clara e organizada.
- Funcionalidade de exportação funcionando conforme o esperado.

## Coleta de Feedback

Após a realização dos testes, aplique um questionário breve para coletar feedback dos usuários:
- **Facilidade de uso:** Em uma escala de 1 a 5, como você avaliaria a usabilidade do sistema?
- **Clareza das informações:** As informações e alertas são apresentados de forma clara?
- **Sugestões:** O que poderia ser melhorado para facilitar a utilização do sistema?

## Considerações Finais

- Documente todos os problemas encontrados com capturas de tela e descrições detalhadas.
- Agende uma reunião de revisão com a equipe para discutir as melhorias e priorizar as correções.


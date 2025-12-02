
## Sistema Turbo Tickets

**Versão:** 1.0  
**Data:** Dezembro 2025  
**Projeto:** Turbo Tickets – Monorepo com Backend (NestJS) + Frontend (React + Zendesk Garden)

---

## 1. Introdução

### 1.1 Objetivo
Este documento especifica os requisitos funcionais do sistema **Turbo Tickets**, uma aplicação web para consulta, visualização e exportação de tickets de suporte através de uma interface intuitiva.

### 1.2 Escopo
O sistema é composto por:
- Um backend que fornece dados de tickets via API REST
- Um frontend web que exibe e permite interação com esses dados
- Um pacote de tipos compartilhados garantindo consistência entre camadas

### 1.3 Definições e Abreviações

| Termo | Definição |
|-------|-----------|
| **Ticket** | Registro de solicitação ou problema de suporte |
| **API** | Interface de comunicação entre backend e frontend |
| **Exportação** | Extração de dados para formato de arquivo (CSV) |
| **Paginação** | Divisão de dados em páginas para melhor visualização |
| **Status** | Estado do ticket (aberto ou fechado) |

---

## 2. Requisitos Funcionais

### 2.1 Consulta de Tickets

#### RF-001: Listar todos os tickets

**Descrição:**  
O sistema deve permitir que o usuário visualize uma lista completa de tickets cadastrados, com opção de navegação entre páginas.

**Atores:**  
- Usuário final (agente de suporte)
- Sistema (API)

**Pré-condições:**
- Backend está operacional
- Frontend está carregado
- Há tickets cadastrados no sistema

**Fluxo Principal:**
1. Usuário acessa a aplicação web
2. Sistema carrega automaticamente a primeira página de tickets
3. Sistema exibe tabela com tickets listados
4. Usuário visualiza informações: ID, Assunto, Status

**Fluxo Alternativo (Paginação):**
1. Usuário clica em "Próxima Página"
2. Sistema carrega próxima página de tickets
3. Tabela é atualizada com novos registros

**Pós-condições:**
- Lista de tickets é exibida na tela
- Usuário pode navegar entre páginas

**Critérios de Aceitação:**
- Tabela exibe mínimo 10 tickets por página
- Cada ticket mostra ID, Assunto e Status
- Botões de paginação (Anterior/Próxima) funcionam
- Transição entre páginas é suave e sem erros

**Regras de Negócio:**
- Padrão: 10 tickets por página
- Status "Aberto" é destacado em vermelho
- Status "Fechado" é destacado em verde

---

#### RF-002: Filtrar tickets por status

**Descrição:**  
O sistema deve permitir que o usuário visualize apenas tickets com um status específico (aberto ou fechado).

**Atores:**  
- Usuário final

**Pré-condições:**
- Página de listagem de tickets está carregada

**Fluxo Principal:**
1. Usuário seleciona filtro de status (ex: "Apenas Abertos")
2. Sistema filtra a lista de tickets
3. Tabela é atualizada mostrando apenas tickets do status selecionado

**Pós-condições:**
- Apenas tickets do status selecionado são exibidos
- Contador indica quantidade de resultados

**Critérios de Aceitação:**
- Filtro por "Abertos" mostra apenas tickets com status open
- Filtro por "Fechados" mostra apenas tickets com status closed
- Opção "Todos" remove o filtro e mostra todos os tickets
- Filtro é persistido ao navegar entre páginas

---

#### RF-003: Buscar tickets por assunto

**Descrição:**  
O sistema deve permitir que o usuário pesquise tickets digitando palavras-chave no campo de busca.

**Atores:**  
- Usuário final

**Pré-condições:**
- Página de listagem está carregada
- Campo de busca está visível

**Fluxo Principal:**
1. Usuário digita palavra-chave no campo "Pesquisar"
2. Sistema busca por tickets com palavra-chave no assunto
3. Tabela é atualizada com resultados da busca
4. Quantidade de resultados é exibida

**Fluxo Alternativo (Sem Resultados):**
1. Usuário digita palavra-chave
2. Sistema não encontra matches
3. Mensagem "Nenhum ticket encontrado" é exibida

**Pós-condições:**
- Apenas tickets que correspondem à busca são exibidos
- Se nenhum resultado, mensagem clara é mostrada

**Critérios de Aceitação:**
- Busca é case-insensitive (maiúsculas/minúsculas não importam)
- Resultados aparecem instantaneamente (debounce de 300ms)
- Botão "Limpar" reseta a busca
- Campo mantém o texto digitado

---

### 2.2 Visualização de Tickets

#### RF-004: Exibir detalhes de um ticket

**Descrição:**  
O sistema deve permitir que o usuário clique em um ticket para visualizar seus detalhes completos.

**Atores:**  
- Usuário final

**Pré-condições:**
- Página de listagem está carregada
- Ticket está na lista

**Fluxo Principal:**
1. Usuário clica em uma linha da tabela (ticket)
2. Sistema abre modal ou página com detalhes do ticket
3. Detalhes exibidos: ID, Assunto, Status, Data de criação (se aplicável)

**Pós-condições:**
- Modal com detalhes é aberto
- Usuário pode fechar modal (botão X ou clicando fora)

**Critérios de Aceitação:**
- Modal exibe todos os campos do ticket
- Botão "Fechar" está visível e funcional
- Pressionando ESC também fecha o modal

---

#### RF-005: Indicar carregamento de dados

**Descrição:**  
O sistema deve mostrar indicador visual enquanto os dados estão sendo carregados.

**Atores:**  
- Sistema
- Usuário final

**Pré-condições:**
- Requisição HTTP foi enviada
- Resposta ainda não foi recebida

**Fluxo Principal:**
1. Usuário acessa página ou muda de página
2. Requisição é enviada ao backend
3. Spinner de loading aparece no centro da tabela
4. Mensagem "Carregando tickets..." é exibida

**Pós-condições:**
- Quando dados chegam, spinner desaparece e tabela é renderizada

**Critérios de Aceitação:**
- Spinner é animado e visível
- Mensagem de loading é clara
- Spinner desaparece quando dados carregam
- Máximo 5 segundos para carregar (timeout)

---

#### RF-006: Exibir mensagem de erro

**Descrição:**  
O sistema deve exibir mensagem clara quando há falha ao carregar os dados.

**Atores:**  
- Sistema
- Usuário final

**Pré-condições:**
- Requisição ao backend falhou
- Conexão está indisponível ou erro de servidor

**Fluxo Principal:**
1. Usuário tenta carregar tickets
2. Sistema tenta fazer requisição e falha
3. Alerta em vermelho é exibido com mensagem de erro
4. Botão "Tentar Novamente" está disponível

**Pós-condições:**
- Mensagem de erro é clara e orientadora
- Usuário pode tentar novamente

**Critérios de Aceitação:**
- Mensagem descreve o erro (ex: "Erro de conexão com servidor")
- Botão "Tentar Novamente" recarrega os dados
- Alerta é facilmente visível (contraste adequado)

---

### 2.3 Exportação de Dados

#### RF-007: Exportar tickets em formato CSV

**Descrição:**  
O sistema deve permitir que o usuário baixe todos os tickets em formato CSV (arquivo de planilha).

**Atores:**  
- Usuário final

**Pré-condições:**
- Página de listagem está carregada
- Botão "Exportar" está visível

**Fluxo Principal:**
1. Usuário clica em botão "Exportar"
2. Sistema inicia download de arquivo CSV
3. Arquivo é salvo no computador do usuário (ex: tickets-export.csv)
4. Arquivo contém: ID, Assunto, Status em colunas

**Fluxo Alternativo (Filtro Aplicado):**
1. Usuário aplica filtro (ex: apenas "Abertos")
2. Usuário clica "Exportar"
3. Apenas tickets filtrados são incluídos no arquivo

**Pós-condições:**
- Arquivo CSV é disponibilizado para download
- Arquivo pode ser aberto em Excel, Google Sheets, etc.

**Critérios de Aceitação:**
- Arquivo é gerado sem erros
- Nome do arquivo é descriptivo (tickets-YYYY-MM-DD.csv)
- Arquivo contém cabeçalho (ID, Assunto, Status)
- Arquivo pode ser aberto em Excel
- Largos volumes (1000+ tickets) não causam travamento

**Regras de Negócio:**
- Exportação respeita filtros aplicados
- Se nenhum ticket, arquivo vazio é criado com cabeçalho

---

### 2.4 Experiência de Usuário

#### RF-008: Interface responsiva

**Descrição:**  
O sistema deve funcionar corretamente em diferentes tamanhos de tela (desktop, tablet, mobile).

**Atores:**  
- Usuário final (em diferentes dispositivos)

**Pré-condições:**
- Sistema está acessível

**Fluxo Principal:**
1. Usuário acessa em desktop
2. Tabela exibe com todas as colunas
3. Usuário acessa em tablet
4. Tabela se adapta, colunas podem encolher ou rolar
5. Usuário acessa em mobile
6. Tabela fica empilhada ou em formato adaptado

**Critérios de Aceitação:**
- Em desktop (1920px): todas as colunas visíveis
- Em tablet (768px): layout se adapta, sem perda de funcionalidade
- Em mobile (375px): layout é adaptado, tabela é scrollável horizontalmente
- Botões e links têm tamanho mínimo de 44px (toque)
- Sem necessidade de zoom para ler conteúdo

---

#### RF-009: Tema visual consistente

**Descrição:**  
O sistema deve aplicar tema visual profissional e consistente em toda a interface.

**Atores:**  
- Usuário final

**Pré-condições:**
- Aplicação está carregada

**Fluxo Principal:**
1. Usuário acessa qualquer página
2. Componentes visuais (botões, tabelas, alerts) seguem mesmo estilo
3. Cores, fontes e espaçamento são consistentes

**Critérios de Aceitação:**
- Todos os botões têm mesmo estilo
- Tabela usa componentes Zendesk Garden
- Cores seguem paleta definida (Zendesk Garden)
- Fontes são legíveis e consistentes
- Sem discrepâncias visuais entre páginas

---

#### RF-010: Tema claro/escuro (Opcional)

**Descrição:**  
O sistema pode oferecer opção de alternar entre tema claro e escuro.

**Atores:**  
- Usuário final

**Pré-condições:**
- Selector de tema está visível

**Fluxo Principal:**
1. Usuário clica em ícone de lua/sol (tema)
2. Interface muda para tema escuro/claro
3. Preferência é salva localmente

**Critérios de Aceitação:**
- Tema escuro tem contraste adequado
- Tema claro é legível
- Preferência persiste ao recarregar página
- Todos os componentes mudam de tema

---

### 2.5 Performance e Confiabilidade

#### RF-011: Carregamento rápido de dados

**Descrição:**  
O sistema deve carregar tickets em tempo razoável para boa experiência de usuário.

**Atores:**  
- Sistema
- Usuário final

**Critérios de Aceitação:**
- Primeira página carrega em < 1 segundo
- Mudança de página carrega em < 500ms
- Busca retorna resultados em < 1 segundo
- Exportação inicia em < 2 segundos

**Regras de Negócio:**
- Se carregamento ultrapassa 5 segundos, timeout é acionado
- Cache local pode ser usado para melhorar performance

---

#### RF-012: Tratamento de erros

**Descrição:**  
O sistema deve tratar e exibir erros de forma clara.

**Atores:**  
- Sistema

**Cenários:**
- Backend indisponível: Mensagem "Servidor indisponível"
- Erro de rede: Mensagem "Verifique sua conexão"
- Erro desconhecido: Mensagem "Ocorreu um erro, tente novamente"

**Critérios de Aceitação:**
- Mensagens são amigáveis, não técnicas
- Cada erro tem ação sugerida (tentar novamente, recarregar página, etc.)
- Erro não quebranta aplicação (usuário pode continuar usando)

---

## 3. Casos de Uso

### Caso de Uso 1: Listar e Filtrar Tickets

**Ator Principal:** Agente de Suporte

**Objetivo:** Visualizar todos os tickets abertos para priorizar respostas

**Fluxo:**
1. Agente acessa sistema
2. Lista completa de tickets é carregada
3. Agente clica em filtro "Apenas Abertos"
4. Tabela mostra apenas 45 tickets abertos
5. Agente navega entre páginas para revisar todos
6. Agente identifica ticket urgente e clica para ver detalhes

---

### Caso de Uso 2: Exportar Relatório

**Ator Principal:** Gerente de Suporte

**Objetivo:** Gerar relatório mensal de tickets para análise

**Fluxo:**
1. Gerente acessa sistema
2. Aplica filtro de data (ex: mês de Dezembro)
3. Clica em "Exportar"
4. Arquivo CSV é baixado (tickets-2025-12.csv)
5. Gerente abre em Excel para análise

---

### Caso de Uso 3: Buscar Ticket Específico

**Ator Principal:** Agente de Suporte

**Objetivo:** Encontrar rapidamente um ticket sobre um assunto específico

**Fluxo:**
1. Agente digita "login" na busca
2. Sistema exibe 12 tickets contendo "login"
3. Agente encontra ticket desejado
4. Clica para ver detalhes completos

---

## 4. Prototipagem de Telas

### Tela 1: Lista de Tickets

┌─────────────────────────────────────────┐
│  Turbo Tickets                  🔍 Buscar│
├─────────────────────────────────────────┤
│ Filtro: [Todos ▼]   [Exportar] [Atualiz]│
├─────────────────────────────────────────┤
│ ID   │ Assunto                │ Status  │
├──────┼────────────────────────┼─────────┤
│ 001  │ Login não funciona     │ 🔴 Aberto
│ 002  │ Dashboard lento        │ 🔴 Aberto
│ 003  │ Erro de integração     │ 🟢 Fechado
│ 004  │ Bug em relatório       │ 🔴 Aberto
│ 005  │ Paginação duplica      │ 🟢 Fechado
├─────────────────────────────────────────┤
│ Página 1 de 10  [Anterior] [Próxima]    │
└─────────────────────────────────────────┘

---

### Tela 2: Modal de Detalhes

┌────────────────────────────────┐
│ Detalhes do Ticket         [X] │
├────────────────────────────────┤
│ ID:       001                  │
│ Assunto:  Login não funciona   │
│ Status:   🔴 Aberto            │
│                                │
│           [Fechar]             │
└────────────────────────────────┘

---

## 5. Requisitos Não-Funcionais Relacionados

| Aspecto | Requisito |
|---------|-----------|
| Performance | Carregar 100 tickets em < 500ms |
| Segurança | CORS habilitado apenas para localhost |
| Compatibilidade | Chrome, Firefox, Safari, Edge versões recentes |
| Escalabilidade | Suportar até 10.000 tickets sem degradação |
| Acessibilidade | Contraste WCAG AA, navegação por teclado |

---

## 6. Critérios de Aceitação Global

- ✅ Todos os RF implementados conforme especificado
- ✅ Interface responsiva funciona em 3+ resoluções
- ✅ Mensagens de erro são claras e acionáveis
- ✅ Não há console errors ao usar funcionalidades
- ✅ Backend responde todas requisições em < 1s
- ✅ Frontend renderiza em < 2s após dados recebidos
- ✅ Usuário consegue usar sistema sem documentação técnica

---

## 7. Glossário de Termos

| Termo | Significado |
|-------|-----------|
| **Ticket** | Registro de problema/solicitação de suporte |
| **Status** | Estado do ticket (aberto, fechado) |
| **Assunto** | Título ou descrição breve do ticket |
| **Paginação** | Divisão de dados em páginas |
| **Filtro** | Restrição de dados por critério |
| **Busca** | Pesquisa por texto/palavra-chave |
| **Modal** | Janela sobreposta à página |
| **CSV** | Formato de arquivo de planilha (comma-separated values) |
| **API** | Interface de comunicação entre sistemas |

---

**Documento de Requisitos Funcionais - Turbo Tickets**  
**Versão 1.0 | Dezembro 2025**
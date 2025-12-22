# Fluxo de Teste - Cadastro de Projetos para 2026

  

Este documento descreve o fluxo completo para testar a funcionalidade de inclusão de projetos para o ano de 2026 no frontend do sistema PROPAG.

  

## Pré-requisitos

  

1. **Login no sistema**: É necessário estar autenticado no sistema

2. **Edital para 2026**:

- Deve existir um edital cadastrado para o ano de 2026 no sistema

- ⚠️ **O edital deve estar com status "aberto" = true** para permitir cadastro de novos projetos

- O nome do edital geralmente contém o ano (ex: "Edital PROPAG 2026")

3. **Usuário adequado**: O usuário deve ser do tipo "professor" ou "coordenador" (não administrador)

- Administradores não têm acesso à opção "Cadastrar projeto" no menu

  

## Fluxo de Navegação

  

### 1. Acessar o Menu Principal

- **Rota**: `/menu` ou `/` (após login)

- **Como acessar**: Após fazer login, você será redirecionado para o menu

  

### 2. Iniciar Cadastro de Projeto

- **Rota**: `/cadastro_projeto`

- **Como acessar**: No menu, na seção de dados do usuário (painel direito), clique em **"Cadastrar projeto"**

  

**⚠️ Validações Automáticas ao Clicar em "Cadastrar projeto":**

1. O sistema verifica se existe pelo menos um edital **aberto** no momento

- Se não houver edital aberto, será exibido o alerta: "Não existe edital aberto no momento"

- Para testar projetos de 2026, é necessário que exista um edital de 2026 com status "aberto" = true

2. O sistema verifica se você possui rascunhos salvos

- Se houver rascunhos, será exibido o alerta: "você tem rascunhos salvos!" e você será redirecionado para `/rascunhos_salvos`

- Se não houver rascunhos, os dados serão limpos e você será redirecionado para `/cadastro_projeto`

  

- **Descrição**: Esta é a primeira etapa do cadastro

  

#### Tela 1: Dados do Coordenador (`/cadastro_projeto`)

  

**Campos obrigatórios:**

- **Coordenador**: Preenchido automaticamente com o nome do usuário logado (não editável)

- **CPF**: Preenchido automaticamente com o CPF do usuário logado (não editável)

- **Programa de Pós-Graduação**: Preenchido automaticamente (não editável)

- **Edital**: ⚠️ **SELECIONE O EDITAL PARA 2026** (campo obrigatório)

- No dropdown, procure pelo edital que contenha "2026" no nome

- Exemplo: "Edital PROPAG 2026" ou similar

- **Quantidade de Professores Colaboradores**: Selecione a quantidade (opcional)

- **Adicionar Professores Colaboradores**: (opcional)

- Se selecionar "Sim", você pode adicionar professores cadastrados ou não cadastrados

  

**Ação**: Clique em **"Salvar"** para avançar

  

**⚠️ IMPORTANTE**: Se você não selecionar um edital, verá a mensagem de erro: "selecione o edital"

  

---

  

### 3. Especificações do Projeto

- **Rota**: `/especificacoes_projeto`

- **Navegação automática**: Após salvar na tela anterior

  

#### Tela 2: Especificações (`/especificacoes_projeto`)

  

**Campos obrigatórios:**

- **Título do Projeto**: Digite o título do projeto

- **Número de Vagas Remuneradas**:

- Máximo: 2 vagas

- Digite o número (0 a 2)

- **Número de Vagas Voluntárias**:

- Máximo total de instrutores (remunerados + voluntários): 5

- Digite o número conforme as regras:

- Se 0 remunerados → máximo 3 voluntários

- Se 1 remunerado → máximo 2 voluntários

- Se 2 remunerados → máximo 1 voluntário

- **Regime de Trabalho**: Selecione o regime (campo obrigatório)

- **Tipo**: Sempre será "TIPO I" (automático)

  

**Ação**: Clique em **"Salvar"** para avançar

  

**Observação**: Você pode clicar em **"Cancelar"** para salvar como rascunho ou voltar ao menu

  

---

  

### 4. Cadastro de Disciplinas

- **Rota**: `/cadastro_disciplina`

- **Navegação automática**: Após salvar na tela anterior

  

#### Tela 3: Cadastro de Disciplinas (`/cadastro_disciplina`)

  

**Passos:**

1. **Adicionar Disciplinas**:

- Preencha os campos para cada disciplina:

- Nome da Disciplina

- Código

- Semestre

- Tipo de Disciplina

- É Obrigatória? (Sim/Não)

- Unidade de Oferta (selecione do dropdown)

- Cursos Contemplados na Oferta (adicione cada curso)

- TSD (Tipo de Suporte Didático)

- Carga Horária

- Clique em **"Adicionar Disciplina"** para adicionar à lista

- Você pode adicionar múltiplas disciplinas

- Você pode editar ou excluir disciplinas da lista

  

2. **Upload do Comprovante**:

- Faça o upload de um arquivo PDF ou imagem com o comprovante das disciplinas

  

**Ação**: Após adicionar pelo menos uma disciplina e fazer o upload do comprovante, clique em **"Salvar Todas as Disciplinas"** para avançar

  

**Observação**: Você pode clicar em **"Cancelar"** para salvar como rascunho ou voltar ao menu

  

---

  

### 5. Dados das Disciplinas

- **Rota**: `/dados_disciplinas`

- **Navegação automática**: Após salvar na tela anterior

  

#### Tela 4: Dados das Disciplinas (`/dados_disciplinas`)

  

Esta tela exibe um resumo das disciplinas cadastradas.

  

**Ação**: Revise os dados e avance para a próxima etapa

  

---

  

### 6. Identificação do Projeto

- **Rota**: `/identificacao_projeto`

- **Navegação automática**: Após revisar os dados das disciplinas

  

#### Tela 5: Identificação (`/identificacao_projeto`)

  

**Campos obrigatórios:**

- **Palavra-chave 1**: Digite uma palavra-chave

- **Palavra-chave 2**: Digite uma palavra-chave

- **Palavra-chave 3**: Digite uma palavra-chave

- **Palavra-chave 4**: Digite uma palavra-chave

- **Quantidade de Bolsas**: Digite o número de bolsas

  

**Informações exibidas:**

- Dados do edital selecionado (nome, data de início, data de fim)

  

**Ação**: Clique em **"Salvar"** para avançar

  

**Observação**: Você pode clicar em **"Cancelar"** para salvar como rascunho

  

---

  

### 7. Resumo do Projeto

- **Rota**: `/resumo_projeto`

- **Navegação automática**: Após salvar na tela anterior

  

#### Tela 6: Resumo (`/resumo_projeto`)

  

**Campo obrigatório:**

- **Resumo**: Digite o resumo do projeto (editor de texto rico - Quill)

  

**Ação**: Clique em **"Salvar"** para avançar

  

**Observação**: Você pode clicar em **"Cancelar"** para salvar como rascunho

  

---

  

### 8. Introdução do Projeto

- **Rota**: `/introducao_projeto` ou `/introducao_projeto_upload`

- **Navegação automática**: Após salvar na tela anterior

  

#### Tela 7: Introdução (`/introducao_projeto`)

  

**Opções disponíveis:**

- **Digitar**: Você pode digitar a introdução diretamente no editor de texto rico

- **Upload de Arquivo**: Você pode fazer upload de um arquivo (PDF) contendo a introdução

  

**Campo obrigatório:**

- **Introdução**: Conteúdo da introdução (texto ou arquivo)

  

**Ação**: Clique em **"Salvar"** para avançar

  

**Observação**: Você pode clicar em **"Cancelar"** para salvar como rascunho

  

---

  

### 9. Metodologia do Projeto

- **Rota**: `/metodologia_projeto` ou `/metodologia_projeto_upload`

- **Navegação automática**: Após salvar na tela anterior

  

#### Tela 8: Metodologia (`/metodologia_projeto`)

  

**Opções disponíveis:**

- **Digitar**: Você pode digitar a metodologia diretamente no editor de texto rico

- **Upload de Arquivo**: Você pode fazer upload de um arquivo (PDF) contendo a metodologia

  

**Campo obrigatório:**

- **Metodologia**: Conteúdo da metodologia (texto ou arquivo)

  

**Ação**: Clique em **"Salvar"** para avançar

  

**Observação**: Você pode clicar em **"Cancelar"** para salvar como rascunho

  

---

  

### 10. Resultados Esperados

- **Rota**: `/resultados_projeto` ou `/resultados_projeto_upload`

- **Navegação automática**: Após salvar na tela anterior

  

#### Tela 9: Resultados Esperados (`/resultados_projeto`)

  

**Opções disponíveis:**

- **Digitar**: Você pode digitar os resultados esperados diretamente no editor de texto rico

- **Upload de Arquivo**: Você pode fazer upload de um arquivo (PDF) contendo os resultados esperados

  

**Campo obrigatório:**

- **Resultados Esperados**: Conteúdo dos resultados esperados (texto ou arquivo)

  

**Ação**: Clique em **"Salvar"** para avançar

  

**Observação**: Você pode clicar em **"Cancelar"** para salvar como rascunho

  

---

  

### 11. Cronograma do Projeto

- **Rota**: `/cronograma_projeto`

- **Navegação automática**: Após salvar na tela anterior

  

#### Tela 10: Cronograma (`/cronograma_projeto`)

  

**Campos obrigatórios:**

- **Cronograma**: Preencha pelo menos 10 meses de atividades

- Para cada mês:

- Selecione o Mês/Ano (formato: MM/AAAA)

- Digite a Atividade correspondente

  

**Estrutura do cronograma:**

- Mês/Ano 1 até Mês/Ano 10 (obrigatórios)

- Mês/Ano 11 e Mês/Ano 12 (opcionais)

  

**Ação**: Clique em **"Salvar"** para avançar

  

**Observação**: Você pode clicar em **"Cancelar"** para salvar como rascunho

  

---

  

### 12. Referências

- **Rota**: `/referencia_projeto`

- **Navegação automática**: Após salvar na tela anterior

  

#### Tela 11: Referências (`/referencia_projeto`)

  

**Campo obrigatório:**

- **Referências**: Digite as referências bibliográficas

- Mínimo: 10 caracteres

- Máximo: 2000 caracteres

  

**Ação**: Clique em **"Salvar"** para finalizar o cadastro

  

**⚠️ IMPORTANTE**: Esta é a última etapa. Ao clicar em "Salvar", o projeto será cadastrado no sistema e você será redirecionado para a página de detalhes do projeto (`/detalhes_projeto/:id`)

  

**Observação**: Você pode clicar em **"Cancelar"** para salvar como rascunho

  

---

  

## Fluxo Visual Resumido

  

```

Login → Menu → Cadastrar Projeto

↓

1. Dados do Coordenador (/cadastro_projeto)

→ Selecionar Edital 2026 ⚠️

↓

2. Especificações (/especificacoes_projeto)

→ Título, Vagas, Regime

↓

3. Cadastro de Disciplinas (/cadastro_disciplina)

→ Adicionar disciplinas + Upload comprovante

↓

4. Dados das Disciplinas (/dados_disciplinas)

→ Revisão

↓

5. Identificação (/identificacao_projeto)

→ Palavras-chave + Quantidade de bolsas

↓

6. Resumo (/resumo_projeto)

→ Resumo do projeto

↓

7. Introdução (/introducao_projeto)

→ Introdução (texto ou upload)

↓

8. Metodologia (/metodologia_projeto)

→ Metodologia (texto ou upload)

↓

9. Resultados Esperados (/resultados_projeto)

→ Resultados (texto ou upload)

↓

10. Cronograma (/cronograma_projeto)

→ 10 meses de atividades

↓

11. Referências (/referencia_projeto)

→ Referências bibliográficas

↓

✅ Projeto Cadastrado → Detalhes do Projeto

```

  

## Pontos de Atenção para Teste de 2026

  

1. **Edital 2026 Aberto**:

- ⚠️ **IMPORTANTE**: O edital para 2026 deve estar cadastrado no sistema E deve ter o status "aberto" = true

- Se o edital não estiver aberto, você não conseguirá iniciar o cadastro de projeto

- Certifique-se de selecionar o edital correto na primeira tela (`/cadastro_projeto`)

- O sistema busca editais abertos através da API: `GET /api/edital`

  

2. **Validações**: Preste atenção nas mensagens de erro e validações em cada etapa

  

3. **Rascunhos**:

- Você pode salvar como rascunho em qualquer etapa usando "Cancelar"

- Ao clicar em "Cancelar", será perguntado: "deseja salvar como rascunho?"

- Se confirmar, o projeto será salvo como rascunho e você será redirecionado para o menu

  

4. **Rascunhos Salvos**:

- Para continuar um rascunho, acesse "Rascunhos salvos" no menu (`/rascunhos_salvos`)

- Se você tiver rascunhos salvos e tentar criar um novo projeto, o sistema alertará e redirecionará para a página de rascunhos

  

5. **Upload de Arquivos**:

- Algumas etapas permitem upload de PDF ao invés de digitação (Introdução, Metodologia, Resultados Esperados)

- Para Disciplinas, é obrigatório fazer upload do comprovante

  

6. **Dados Persistem no LocalStorage**:

- Os dados do formulário são salvos no localStorage durante o preenchimento

- Se você sair e voltar antes de finalizar, poderá perder os dados (exceto se salvar como rascunho)

  

## Verificação Pós-Cadastro

  

Após finalizar o cadastro na última etapa (Referências), o sistema:

  

1. **Salva o Projeto**: O projeto é salvo no banco de dados através da API `POST /api/projeto`

2. **Associa Cronogramas**: Os cronogramas são associados ao projeto através da API `POST /api/cronograma`

3. **Redireciona**: Você será redirecionado automaticamente para `/detalhes_projeto/:id` (onde `:id` é o ID do projeto criado)

  

**Após o cadastro, você pode:**

  

1. **Visualizar o Projeto**: Visualizar todos os detalhes do projeto cadastrado

2. **Listar Projetos**: Acesse "Projetos submetidos" no menu (`/projetos_submetidos`) para ver todos os seus projetos

3. **Editar (se permitido)**: Alguns dados podem ser editáveis dependendo do status do projeto e do edital

4. **Verificar Status**: O projeto estará associado ao edital selecionado (2026)

  

## Solução de Problemas

  

### Problema: "Não existe edital aberto no momento"

**Solução**:

- Verifique se existe um edital cadastrado para 2026 no sistema

- Verifique se o edital está com status "aberto" = true

- Um administrador precisa cadastrar/abrir o edital no backend

  

### Problema: "você tem rascunhos salvos!"

**Solução**:

- Você será redirecionado para `/rascunhos_salvos`

- Você pode continuar um rascunho existente ou criar um novo projeto após finalizar/excluir os rascunhos

  

### Problema: Não consigo ver a opção "Cadastrar projeto" no menu

**Solução**:

- Verifique se você está logado como professor/coordenador (não administrador)

- Administradores não têm acesso a essa funcionalidade

  

## Rotas Resumidas

  

| Etapa | Rota | Descrição |

|-------|------|-----------|

| 1 | `/cadastro_projeto` | Dados do Coordenador + Seleção de Edital |

| 2 | `/especificacoes_projeto` | Título, Vagas, Regime |

| 3 | `/cadastro_disciplina` | Cadastro de Disciplinas |

| 4 | `/dados_disciplinas` | Revisão das Disciplinas |

| 5 | `/identificacao_projeto` | Palavras-chave e Bolsas |

| 6 | `/resumo_projeto` | Resumo do Projeto |

| 7 | `/introducao_projeto` | Introdução |

| 8 | `/metodologia_projeto` | Metodologia |

| 9 | `/resultados_projeto` | Resultados Esperados |

| 10 | `/cronograma_projeto` | Cronograma |

| 11 | `/referencia_projeto` | Referências (Finalização) |

  

---

  

**Data de Criação**: Janeiro 2025

**Sistema**: PROPAG - Sistema de Gerenciamento de Projetos
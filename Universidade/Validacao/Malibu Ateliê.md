## Equipe

- **Luiz Eduardo Borges de Lima**
    

## Descrição do Sistema

O **Malibu Ateliê** é um hub digital para uma loja de crochê sob medida. O sistema centraliza catálogo, portfólio e redes sociais em uma interface pública personalizada, responsiva e acessível, além de oferecer um painel administrativo protegido por autenticação para cadastro e gerenciamento de produtos. O objetivo é facilitar a divulgação das peças exclusivas do ateliê, mantendo identidade visual sofisticada e processos internos simples para a equipe administradora. 

---

## Histórias de Usuário e Cenários BDD

> Abaixo, cada história segue o formato **Como [ator] quero [objetivo] para [benefício]**. Em seguida, derivamos cenários de teste em estilo **Given/When/Then (Gherkin)**.

### US01 – Cadastrar Produto

**Como** administrador,  
**Quero** cadastrar um novo produto informando nome, descrição e imagem,  
**Para** que ele apareça no catálogo público.

```gherkin
Scenario: Cadastro válido
  Given que o administrador está autenticado
  And acessa a página "Cadastrar produto"
  When preenche "Nome", "Descrição" e faz upload de "Imagem" válidos
  And clica em "Salvar"
  Then o sistema armazena o produto
  And exibe a mensagem "Produto cadastrado com sucesso"
  And o produto aparece na listagem

Scenario: Campo obrigatório ausente
  Given que o administrador está autenticado
  And acessa a página "Cadastrar produto"
  When deixa o campo "Nome" vazio e clica em "Salvar"
  Then o sistema exibe mensagem de erro "Nome é obrigatório"
  And o produto **não** é salvo
```

---

### US02 – Editar Produto

**Como** administrador,  
**Quero** alterar informações de um produto já cadastrado,  
**Para** corrigi‑las ou atualizá‑las.

```gherkin
Scenario: Edição bem‑sucedida
  Given que o administrador está autenticado
  And visualiza um produto existente
  When clica em "Editar", altera a descrição e salva
  Then o sistema atualiza o produto
  And exibe "Produto atualizado com sucesso"

Scenario: Produto inexistente
  Given que o administrador está autenticado
  When tenta acessar a URL de edição de um ID inexistente
  Then o sistema retorna erro 404
```

---

### US03 – Excluir Produto

**Como** administrador,  
**Quero** remover produtos do catálogo,  
**Para** que itens obsoletos ou incorretos não apareçam para os clientes.

```gherkin
Scenario: Exclusão confirmada
  Given que o administrador está autenticado
  And está na listagem de produtos
  When clica em "Excluir" no produto X
  And confirma a ação
  Then o sistema remove o produto X
  And exibe "Produto excluído com sucesso"
  And o produto X deixa de aparecer na listagem

Scenario: Exclusão cancelada
  Given que o administrador está autenticado
  And inicia a exclusão do produto Y
  When clica em "Cancelar" no modal de confirmação
  Then o sistema **não** remove o produto Y
```

---

### US04 – Buscar Produto

**Como** visitante,  
**Quero** pesquisar produtos por palavra‑chave,  
**Para** encontrar itens específicos rapidamente.

```gherkin
Scenario: Resultados encontrados
  Given que o visitante está na página inicial
  When digita "biquíni" no campo de busca
  Then o sistema exibe produtos cujo nome ou descrição contenha "biquíni"

Scenario: Nenhum resultado
  Given que o visitante está na página inicial
  When busca por "xyz123"
  Then o sistema exibe a mensagem "Nenhum produto encontrado"
```

---

### US05 – Visualizar Detalhes do Produto

**Como** visitante,  
**Quero** ver detalhes completos de um produto,  
**Para** avaliar se ele atende às minhas expectativas.

```gherkin
Scenario: Visualização de produto existente
  Given que o visitante vê a listagem de produtos
  When clica no produto Z
  Then o sistema exibe página com nome, descrição e imagem do produto Z

Scenario: Produto não encontrado
  Given que o visitante acessa diretamente a URL /produto/9999
  When o produto 9999 não existe
  Then o sistema retorna erro 404 com mensagem "Produto não encontrado"
```

---

### US06 – Login no Painel Administrativo

**Como** administrador,  
**Quero** autenticar‑me com e‑mail e senha,  
**Para** acessar o painel administrativo com segurança.

```gherkin
Scenario: Login bem‑sucedido
  Given que o administrador está na tela de login
  When informa credenciais válidas
  Then o sistema concede acesso
  And redireciona para o dashboard

Scenario: Credenciais inválidas
  Given que o administrador está na tela de login
  When informa senha incorreta
  Then o sistema exibe "E‑mail ou senha inválidos"
  And permanece na tela de login
```

---

## Glossário de Termos

|Termo|Definição|
|---|---|
|Administrador|Usuário interno responsável por gerenciar produtos no painel administrativo.|
|Visitante/Usuário|Qualquer pessoa que acessa a interface pública da loja.|
|Produto|Peça de crochê oferecida pelo Malibu Ateliê, contendo nome, descrição e imagem.|

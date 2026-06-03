

> **Carga máxima:** 4 dias × 3h por dia = **12 horas**
>
> **Objetivo realista:** não tentar dominar tudo profundamente, mas conseguir **defender o projeto**, cobrir as principais lacunas da vaga e responder com segurança às perguntas mais prováveis.
>
> **Fonte base:** plano original enviado pelo usuário: `Plano-de-Estudos.md`.  
> As fontes externas usadas como apoio estão listadas no fim deste arquivo, com indicação de onde cada uma foi aplicada.

---

## 1. Estratégia principal

O plano original estava organizado para aproximadamente **6 dias intensivos**, com prioridade em dois pontos:

1. **Defender com profundidade o projeto Teste-Eteg**, porque é o que você já construiu e pode explicar com exemplos reais.
2. **Cobrir em alto nível as lacunas da vaga**, como React Native/Expo, Redis, pagamentos, Firebase FCM, AWS, MongoDB, streams, ERP e LGPD.

Como agora o prazo é de **4 dias com no máximo 3h por dia**, a estratégia muda para:

- **Dia 1:** Backend, autenticação, NestJS, Prisma e PostgreSQL.
- **Dia 2:** Frontend React, TypeScript, Zod, hooks e testes.
- **Dia 3:** React Native/Expo, Redis, filas, pagamentos, FCM e ERP.
- **Dia 4:** Docker, CI/CD, AWS, MongoDB, streams, LGPD e simulado final.

Você não precisa fingir domínio completo de todos os diferenciais. O ideal é responder com honestidade técnica:

> “No meu projeto eu implementei X com profundidade. Sobre Y, ainda não implementei neste projeto, mas entendo o fluxo e aplicaria da seguinte forma...”

---

# 2. Cronograma de 4 dias

---

## Dia 1 — Backend, Auth, NestJS, PostgreSQL e Prisma

**Objetivo do dia:** conseguir explicar o backend como uma arquitetura profissional.

### 0h00–0h40 — Fluxo de autenticação

Estude e explique em voz alta:

- `POST /auth/login`
- `bcrypt.compare`
- geração do JWT
- armazenamento do token em cookie `httpOnly`
- `sameSite: lax`
- `secure` em produção
- `JwtStrategy`
- `JwtAuthGuard`
- diferença entre autenticação e autorização

**Conceitos que você precisa dominar:**

- **Autenticação:** confirma quem o usuário é.
- **Autorização:** define o que esse usuário pode acessar.
- **Cookie httpOnly:** protege o token contra acesso direto por JavaScript em ataques XSS.
- **CSRF:** risco associado a cookies; mitigação inicial com `sameSite: lax`, mas em sistemas mais críticos pode exigir token CSRF.

**Resposta pronta para entrevista:**

> “No projeto, eu optei por armazenar o JWT em cookie httpOnly para reduzir exposição do token a XSS. O backend valida o token via JwtStrategy e protege rotas com Guard. Como melhoria, eu adicionaria RBAC com roles e refresh token.”

**Fontes aplicadas:** [F1], [F2]

---

### 0h40–1h20 — Ciclo de request no NestJS

Domine a ordem mental:

```txt
Request → Guard → Pipe → Controller → Service → Prisma/Database → Response
```

Estude:

- Guard
- Pipe
- Controller
- Service
- Provider
- Exception handling
- Injeção de dependência

**O que explicar:**

- O **Guard** decide se a requisição pode prosseguir.
- O **Pipe** valida ou transforma dados.
- O **Controller** recebe a requisição.
- O **Service** concentra regra de negócio.
- O Prisma acessa o banco.

**Resposta pronta:**

> “No NestJS, a requisição passa por camadas. Primeiro posso barrar com Guard, depois validar ou transformar dados com Pipe, então o Controller recebe a chamada e delega a regra de negócio para o Service.”

**Fontes aplicadas:** [F2], [F3]

---

### 1h20–2h10 — Prisma, PostgreSQL e modelagem

Estude no projeto:

- `schema.prisma`
- modelos `Customer`, `Color`, `AdminUser`
- relação `Customer.color`
- `@unique`
- `onDelete: Restrict`
- migrations
- `P2002`
- `$transaction([findMany, count])`
- `include: { color: true }`
- paginação com `skip` e `take`
- busca case-insensitive
- problema de N+1

**Pontos que você precisa saber defender:**

- Por que usar migrations.
- Por que CPF/email únicos já geram índices.
- Por que usar `include` para evitar múltiplas consultas manuais.
- Por que retornar erro `409 Conflict` em duplicidade.
- Por que fazer `findMany` e `count` juntos na listagem paginada.

**Resposta pronta:**

> “Usei Prisma para ter queries tipadas, migrations versionadas e integração limpa com o NestJS. Na listagem, uso `findMany` com `count` dentro de uma transação para retornar os dados paginados e o total de registros de forma consistente.”

**Fontes aplicadas:** [F0]

---

### 2h10–2h40 — Bug do `colors.service`

O plano original aponta um bug importante no delete de cores:

```ts
customer.count({ where: { id } })
```

O correto seria verificar clientes usando a cor:

```ts
customer.count({ where: { colorId: id } })
```

**Por que isso importa:**

- O sistema deveria impedir deletar uma cor ainda usada por clientes.
- O bug verifica o `id` do cliente, não o `colorId`.
- Isso é um ótimo exemplo para falar de code review e testes.

**Resposta pronta:**

> “Durante a revisão eu identifiquei um bug no delete de cores: o código contava clientes por `id`, mas deveria contar por `colorId`. Isso poderia permitir deletar uma cor ainda vinculada a clientes. Corrigiria a query e adicionaria teste unitário para esse caso.”

**Fontes aplicadas:** [F0]

---

### 2h40–3h00 — Simulado rápido do Dia 1

Responda sem olhar:

1. Como funciona o login?
2. Por que cookie httpOnly?
3. Qual a diferença entre autenticação e autorização?
4. Como o Guard protege rotas?
5. O que o Pipe faz?
6. O que é migration?
7. Como você trata CPF/email duplicado?
8. Onde entraria RBAC?

---

## Dia 2 — Frontend React, TypeScript, Zod, hooks e testes

**Objetivo do dia:** defender o frontend e reduzir o ponto fraco de testes.

---

### 0h00–0h40 — React SPA e estado

Estude:

- React Router
- rotas públicas/admin
- `useState`
- `useEffect`
- `useCallback`
- `useMemo`
- custom hooks
- Context API
- Zustand

**Pontos importantes:**

- O projeto usa mais estado local.
- Isso é aceitável para escopo pequeno.
- Para autenticação global, carrinho, tema, sessão e dados compartilhados, Context ou Zustand fazem mais sentido.
- O projeto ainda não tem uma rota protegida real, apenas redirecionamento após erro `401`.

**Resposta pronta:**

> “No projeto, `useState` foi suficiente porque o escopo é pequeno. Se tivesse autenticação global, carrinho, tema ou sessão persistente, eu usaria Context ou Zustand para evitar prop drilling e centralizar estado.”

**Fontes aplicadas:** [F5], [F6], [F7], [F8]

---

### 0h40–1h20 — TypeScript profissional

Estude:

- `type` vs `interface`
- generics
- `unknown` vs `any`
- `strict`
- `tsconfig`
- ESLint
- Prettier
- organização de tipos compartilhados

**Pontos que você precisa saber:**

- `any` desativa segurança de tipo.
- `unknown` exige validação antes de uso.
- `strict` aumenta a segurança do projeto.
- `tsconfig` define como o TypeScript compila e valida o projeto.

**Resposta pronta:**

> “Eu evito `any` porque ele desliga a segurança do TypeScript. Prefiro `unknown` quando realmente não sei o tipo, porque ele me obriga a validar antes de usar.”

**Fontes aplicadas:** [F9], [F10]

---

### 1h20–1h50 — Zod compartilhado entre front e back

Estude no projeto:

- `packages/shared`
- schemas Zod
- uso no frontend com `react-hook-form`
- uso no backend com pipe de validação
- validação de CPF
- fonte única de verdade

**Resposta pronta:**

> “Coloquei os schemas Zod em um pacote shared para evitar divergência entre frontend e backend. Assim, a regra de validação do formulário é a mesma regra validada pela API.”

**Fontes aplicadas:** [F0]

---

### 1h50–2h40 — Testes automatizados

O plano original alerta que a cobertura de testes do projeto é mínima. Por isso, este bloco é prioridade.

**Faça pelo menos 2 testes reais:**

1. **Back-end:** teste unitário do `isValidCpf`.
2. **Back-end ou front-end:** teste do `CustomersService` com Prisma mockado ou teste de componente do formulário.

**Testes recomendados:**

- Validação de CPF válido.
- Validação de CPF inválido.
- Erro de CPF/email duplicado.
- Delete de cor bloqueado quando há cliente vinculado.
- Formulário exibindo erro para campos obrigatórios.
- Login com credenciais inválidas.

**Resposta pronta:**

> “A cobertura atual ainda é mínima, mas eu priorizaria testes unitários para regras de negócio, como validação de CPF e tratamento de duplicidade, e testes de componente para o fluxo de cadastro. Também adicionaria testes de integração para endpoints críticos com Supertest.”

**Fontes aplicadas:** [F4]

---

### 2h40–3h00 — Simulado rápido do Dia 2

Responda:

1. Quando usar `useState`, Context ou Zustand?
2. O que é custom hook?
3. Para que serve `useEffect`?
4. Quando usar `useCallback`?
5. Quando usar `useMemo`?
6. Por que Zod no shared?
7. O que o TypeScript `strict` melhora?
8. Quais testes você escreveria primeiro?

---

## Dia 3 — React Native/Expo, Redis, filas, pagamentos, FCM e ERP

**Objetivo do dia:** cobrir as lacunas mais prováveis da vaga.

---

### 0h00–0h50 — React Native + Expo

Estude:

- diferença entre React Web e React Native
- Expo
- React Navigation
- Stack navigation
- Tab navigation
- deep linking
- AsyncStorage
- Zustand
- NativeWind
- EAS Build
- OTA updates

**Pontos que você precisa saber:**

- Expo acelera o desenvolvimento mobile.
- React Navigation organiza navegação em telas.
- AsyncStorage é persistência local simples.
- AsyncStorage não deve guardar dados sensíveis sem camada adicional de segurança.
- Zustand pode centralizar estado global no app.
- NativeWind permite uma experiência parecida com Tailwind no React Native.

**Resposta pronta:**

> “No mobile, eu usaria Expo para acelerar o ciclo de desenvolvimento e React Navigation para organizar stack/tabs. Para estado global, usaria Zustand, e para persistência simples, AsyncStorage, lembrando que ele não é criptografado, então não guardaria dados sensíveis nele.”

**Fontes aplicadas:** [F11], [F12], [F13]

---

### 0h50–1h40 — Redis: cache e filas

Estude:

- cache-aside
- TTL
- invalidação
- cache de estoque
- cache de preços
- sessão
- BullMQ
- workers
- retry
- filas assíncronas

**Onde Redis entraria no projeto/vaga:**

- Cache de cores/listagens com TTL curto.
- Cache de estoque e preço vindos do ERP.
- Sessões ou tokens de curta duração.
- Fila para processar pedido.
- Fila para envio de push notification.
- Fila para sincronizar catálogo.

**Resposta pronta:**

> “Eu usaria Redis para cache de dados de alta frequência, como estoque e preços, com TTL curto. Para tarefas assíncronas, como sincronização com ERP, envio de push ou processamento de pedidos, usaria BullMQ com workers.”

**Fontes aplicadas:** [F14], [F15]

---

### 1h40–2h20 — Pagamentos: Cielo/Braspag, PIX, webhook e tokenização

Estude:

- autorização
- captura
- tokenização
- cartão tokenizado
- PIX com QR Code
- webhook de confirmação
- idempotência
- validação da origem do webhook
- nunca armazenar cartão cru

**Pontos que você precisa saber:**

- Em cartão, o gateway pode autorizar e capturar.
- Em PIX, normalmente o sistema gera uma cobrança e aguarda confirmação assíncrona.
- Webhooks podem chegar repetidos.
- Por isso, o processamento precisa ser idempotente.
- Tokenização evita armazenar dados sensíveis de cartão diretamente no seu sistema.

**Resposta pronta:**

> “Eu nunca armazenaria dados crus de cartão. Usaria tokenização do gateway. Para PIX, eu geraria a cobrança, exibiria o QR Code e aguardaria confirmação via webhook. O webhook precisa ser idempotente para evitar processar o mesmo pagamento mais de uma vez.”

**Fontes aplicadas:** [F16], [F17], [F18]

---

### 2h20–2h45 — Firebase FCM

Estude:

- push notification
- device token
- token por dispositivo
- tópicos
- remoção de tokens antigos
- payload sem dados sensíveis

**Fluxo básico:**

```txt
App abre → Firebase gera device token → App envia token ao backend
→ Backend salva token do usuário → Backend envia push via FCM
```

**Resposta pronta:**

> “No FCM, o app registra um device token e envia esse token para o backend. O backend guarda o token associado ao usuário e usa isso para enviar notificações. Também é importante limpar tokens antigos e evitar dados sensíveis no payload.”

**Fontes aplicadas:** [F19], [F20]

---

### 2h45–3h00 — Integração ERP/TOTVS

Estude só o suficiente:

- catálogo
- estoque
- preços
- pedidos
- jobs de sincronização
- filas
- cache
- logs
- retry
- idempotência

**Resposta pronta:**

> “Eu integraria o ERP por uma camada de sincronização: jobs periódicos para catálogo/preço/estoque, fila para processar grandes volumes, Redis para cache de leitura e logs para auditoria. Pedidos enviados ao ERP precisariam de idempotência e retry controlado.”

**Fontes aplicadas:** [F23]

---

## Dia 4 — Docker, CI/CD, AWS, MongoDB, streams, LGPD e simulado final

**Objetivo do dia:** fechar arquitetura, produção e revisão geral.

---

### 0h00–0h40 — Docker e produção

Estude:

- Dockerfile multi-stage
- imagem final menor
- usuário não-root
- docker-compose
- Nginx reverse proxy
- variáveis de ambiente
- diferença entre build e runtime

**Resposta pronta:**

> “Usei Docker multi-stage para separar instalação de dependências, build e runtime. Isso reduz a imagem final, melhora segurança e evita levar dependências desnecessárias para produção.”

**Fontes aplicadas:** [F0]

---

### 0h40–1h10 — CI/CD e GitHub Actions

Estude:

- build
- testes
- lint
- push para registry
- ECR
- deploy em EC2
- secrets
- rollback básico

**Resposta pronta:**

> “O pipeline ideal roda lint, testes, build, cria imagem Docker, envia para um registry como ECR e atualiza o ambiente de produção via deploy automatizado. Secrets ficam no GitHub Actions ou no provedor, nunca commitados.”

**Fontes aplicadas:** [F0]

---

### 1h10–1h40 — AWS: EC2, S3 e Lambda

Estude:

- EC2: servidor/VM para rodar aplicação/container
- S3: armazenamento de objetos/arquivos
- Lambda: funções event-driven/serverless
- quando usar cada um

**Exemplos conectados à vaga:**

- EC2 para hospedar backend e painel.
- S3 para imagens de produtos, notas ou arquivos.
- Lambda para processar eventos, webhooks ou rotinas assíncronas.

**Resposta pronta:**

> “Eu usaria EC2 para hospedar a aplicação/container, S3 para imagens e arquivos, e Lambda para tarefas event-driven, como processamento assíncrono, webhooks ou rotinas disparadas por eventos.”

**Fontes aplicadas:** [F21], [F22]

---

### 1h40–2h05 — MongoDB e PostgreSQL

Estude:

- banco relacional
- banco orientado a documentos
- schema rígido vs flexível
- consistência
- relacionamentos
- quando escolher cada um

**Resposta pronta:**

> “Eu manteria pedidos, pagamentos e usuários no PostgreSQL por causa de relacionamento e consistência. MongoDB faria sentido para dados mais flexíveis, como atributos variáveis de catálogo, logs ou documentos com estrutura dinâmica.”

**Fontes aplicadas:** [F0]

---

### 2h05–2h25 — Streams no Node.js

Estude:

- Readable
- Writable
- Transform
- pipeline
- backpressure
- processamento em partes
- importação de catálogo grande

**Exemplo conectado à vaga:**

```txt
Arquivo grande do ERP → stream de leitura → transformação → validação → gravação em lotes
```

**Resposta pronta:**

> “Para processar um arquivo grande vindo do ERP, eu não carregaria tudo em memória. Usaria streams com pipeline, processando em partes e respeitando backpressure.”

**Fontes aplicadas:** [F0]

---

### 2h25–2h45 — LGPD

Estude:

- CPF e email como dados pessoais
- minimização
- consentimento/base legal
- HTTPS
- controle de acesso
- logs sem dados sensíveis
- direito de exclusão
- anonimização
- criptografia em trânsito

**Resposta pronta:**

> “O projeto lida com dados pessoais como CPF e email. Eu aplicaria minimização, HTTPS obrigatório, controle de acesso, logs sem PII, política de retenção e suporte à exclusão/anonimização quando aplicável.”

**Fontes aplicadas:** [F0]

---

### 2h45–3h00 — Simulado final

Responda em voz alta, em até 1 minuto cada:

1. Explique o projeto em alto nível.
2. Explique o login.
3. Explique o banco.
4. Explique o frontend.
5. Onde entraria Redis?
6. Como integraria pagamento?
7. Como integraria FCM?
8. Como subiria isso em produção?
9. Quais pontos fracos você reconhece?
10. Que testes você escreveria?

---

# 3. Ordem de prioridade dos estudos

## Prioridade 1 — Obrigatório

Estude primeiro:

- Auth JWT + cookie httpOnly
- NestJS Guard/Pipe/Service
- Prisma/PostgreSQL/migrations
- React hooks
- Zod shared
- Docker/CI/CD
- Testes
- Redis básico
- React Native/Expo básico

---

## Prioridade 2 — Saber conversar

- Pagamentos
- PIX
- Webhooks
- FCM
- AWS EC2/S3/Lambda
- MongoDB
- Streams

---

## Prioridade 3 — Visão geral

- OpenSearch/Elasticsearch
- TOTVS Consinco em detalhes
- EAS OTA updates avançado
- Redundância/fault tolerance avançada

---

# 4. Perguntas prováveis da entrevista

## Possíveis perguntas da entrevista técnica — versão ajustada para nível pleno

> Foco: perguntas mais prováveis para uma entrevista de nível pleno, considerando que o teste exigia uma aplicação com TypeScript, React, Node.js, PostgreSQL, Docker e repositório único. A ideia não é só explicar o que foi feito, mas defender decisões, apontar limitações e propor evolução profissional do projeto.

---

## 1. Entendimento do problema e decisões de produto

1. Quais requisitos funcionais e não funcionais você identificou a partir do enunciado do teste?
2. O enunciado dizia que o cliente deveria preencher o formulário uma única vez. Como você garantiu isso tecnicamente?
    
3. Você tratou CPF e e-mail como únicos. Por que essa decisão faz sentido para esse caso?
    
4. Como você lidaria se o cliente depois pedisse para permitir atualização dos dados cadastrados?
    
5. A cor preferida foi limitada às cores do arco-íris, mas o enunciado dizia que isso poderia mudar posteriormente. Como sua modelagem facilita ou dificulta essa mudança?
    
6. O campo “observações” deveria ter algum limite de tamanho? Onde essa regra deveria ser validada?
    
7. O que você faria diferente se esse formulário fosse usado por milhares de usuários por dia?
    
8. Quais decisões você tomou pensando em uma futura equipe mantendo o projeto?
    
9. Que partes do projeto estão mais preparadas para evolução e quais ainda precisam melhorar?
    
10. Se esse sistema virasse um produto real, quais seriam as primeiras features que você adicionaria?
    

---

## 2. Arquitetura e organização do projeto

11. Por que você escolheu organizar o código em um único repositório?
    
12. Quais são as vantagens e desvantagens de usar monorepo nesse cenário?
    
13. O que você separou entre frontend, backend e pacote compartilhado?
    
14. Que tipo de código faz sentido ficar em um pacote `shared`?
    
15. Que tipo de código não deveria ficar no `shared`?
    
16. Como você evitaria acoplamento excessivo entre frontend e backend dentro de um monorepo?
    
17. Como você organizaria esse projeto se ele crescesse para ter aplicativo mobile, painel admin e API pública?
    
18. Como você garantiria padronização de código em uma equipe maior?
    
19. Quais decisões do projeto mostram preocupação com manutenção?
    
20. O que você considera débito técnico no projeto atual?
    

---

## 3. Backend, API e regras de negócio

21. Como você estruturou as responsabilidades entre controller, service e camada de banco?
    
22. Que validações acontecem antes de salvar um cliente?
    
23. Você valida os dados apenas no frontend ou também no backend? Por quê?
    
24. Como sua API responde quando o CPF ou e-mail já existe?
    
25. Como você diferencia erro de validação, erro de conflito e erro interno?
    
26. Como você garantiria respostas padronizadas de erro em toda a API?
    
27. Como você versionaria essa API se futuramente surgisse um app mobile consumindo os mesmos endpoints?
    
28. Como você lidaria com uma alteração de contrato entre frontend e backend?
    
29. Como você implementaria paginação, busca e filtros no painel administrativo?
    
30. Como você protegeria endpoints administrativos?
    
31. Como você adicionaria autenticação para administradores?
    
32. Como você implementaria autorização por perfis, por exemplo admin e operador?
    
33. Como você evitaria abuso de requisições no endpoint de cadastro?
    
34. Como você lidaria com logs de erro sem expor dados pessoais?
    
35. Que pontos da API você considera mais críticos para testar?
    

---

## 4. Banco de dados, PostgreSQL e modelagem

36. Por que PostgreSQL é uma boa escolha para esse teste?
    
37. Como você modelou cliente e cor preferida?
    
38. Por que deixar cor em uma tabela separada pode ser melhor do que usar um enum fixo?
    
39. Quais campos deveriam ter índice nesse sistema?
    
40. Qual a diferença entre validar CPF único na aplicação e garantir unicidade no banco?
    
41. Como você lidaria com concorrência se dois cadastros com o mesmo CPF chegassem ao mesmo tempo?
    
42. O que é uma migration e por que ela é importante em produção?
    
43. Como você faria rollback de uma migration problemática?
    
44. Como você lidaria com alteração futura no modelo, por exemplo adicionar telefone ou endereço?
    
45. O campo CPF deveria ser armazenado formatado ou apenas com números? Por quê?
    
46. Como você trataria dados sensíveis nesse banco?
    
47. Quando você usaria transação nesse projeto?
    
48. Como você investigaria uma query lenta?
    
49. Como evitaria problema de N+1 caso o painel começasse a listar mais dados relacionados?
    
50. O que mudaria se o projeto precisasse suportar múltiplos clientes/empresas, ou seja, multi-tenant?
    

---

## 5. Frontend React e experiência do usuário

51. Como você organizou os componentes da tela de cadastro?
    
52. Como você garantiu que o usuário sabe que o cadastro foi bem-sucedido?
    
53. Como você evita múltiplos envios do mesmo formulário?
    
54. Como você trata estados de loading, erro e sucesso?
    
55. Como você garante que o formulário seja responsivo?
    
56. Como você lidaria com acessibilidade nesse formulário?
    
57. Quais validações devem aparecer imediatamente para o usuário?
    
58. Quais validações só podem ser confirmadas pelo backend?
    
59. Por que usar uma biblioteca de formulário em vez de controlar tudo manualmente com `useState`?
    
60. Quando você usaria `useState`, `useReducer`, Context API ou Zustand?
    
61. O que seria um bom custom hook nesse projeto?
    
62. Como você lidaria com internacionalização se o sistema precisasse suportar outro idioma?
    
63. Como você protegeria uma rota administrativa no frontend?
    
64. Como você evitaria duplicação de regras de validação entre front e back?
    
65. Que testes de interface você escreveria para esse formulário?
    

---

## 6. TypeScript, validação e qualidade de código

66. Como TypeScript ajudou nesse projeto?
    
67. Qual a diferença entre `type` e `interface`?
    
68. Quando você usaria `unknown` em vez de `any`?
    
69. O que o modo `strict` do TypeScript ajuda a prevenir?
    
70. Como você tiparia corretamente o payload de criação de cliente?
    
71. Como você garantiria que o tipo usado no frontend é compatível com o backend?
    
72. Qual o papel do Zod, Joi ou bibliotecas semelhantes em uma aplicação profissional?
    
73. O que pode dar errado se a aplicação confiar apenas nos tipos do TypeScript?
    
74. Como você organizaria ESLint e Prettier em um monorepo?
    
75. Como você revisaria um PR para garantir qualidade em TypeScript?
    

---

## 7. Docker, deploy e ambiente de produção

76. Por que o enunciado menciona Docker como requisito importante?
    
77. O que é uma imagem Docker?
    
78. Qual a diferença entre Dockerfile e docker-compose?
    
79. Como você estruturaria um Dockerfile para frontend e backend?
    
80. Por que usar build multi-stage?
    
81. Como você lidaria com variáveis de ambiente em produção?
    
82. O que não deve ir para dentro da imagem Docker?
    
83. Como você subiria banco, API e frontend em ambiente de homologação?
    
84. Como você faria deploy desse projeto em uma EC2?
    
85. Como você configuraria HTTPS para essa aplicação?
    
86. Como você monitoraria se a aplicação caiu?
    
87. Como você faria rollback de uma versão com bug?
    
88. Como você lidaria com logs em containers?
    
89. Como você separaria ambiente de desenvolvimento, homologação e produção?
    
90. Que melhorias você faria no pipeline de deploy?
    

---

## 8. Segurança Web e LGPD

91. Quais dados pessoais o sistema armazena?
    
92. CPF e e-mail exigem quais cuidados de segurança?
    
93. Como você evitaria vazamento de dados pessoais em logs?
    
94. Como você protegeria a API contra envio automatizado ou abuso?
    
95. Como você lidaria com CORS nesse projeto?
    
96. Qual a diferença entre autenticação e autorização?
    
97. Se fosse adicionado login administrativo, você usaria localStorage ou cookie httpOnly? Por quê?
    
98. Como você lidaria com CSRF em uma aplicação com cookie?
    
99. Como você aplicaria princípios da LGPD nesse sistema?
    
100. Como você implementaria exclusão ou anonimização de dados de um cliente?
    

---

## 9. Testes automatizados

101. Que testes você escreveu ou escreveria primeiro nesse projeto?
    
102. Como você testaria a validação de CPF?
    
103. Como você testaria o caso de CPF duplicado?
    
104. Como você testaria o formulário no frontend?
    
105. Qual a diferença entre teste unitário, teste de integração e teste end-to-end?
    
106. Como você mockaria a camada de banco em um teste unitário?
    
107. Quando vale a pena testar com banco real?
    
108. Como você testaria a API de cadastro com Supertest?
    
109. Que cenários de erro são importantes nesse projeto?
    
110. Como você mediria cobertura de testes?
    
111. Cobertura alta garante qualidade? Por quê?
    
112. O que você colocaria em um pipeline de CI antes do deploy?
    

---

## 10. Escalabilidade, performance e evolução para a vaga

113. Se esse sistema tivesse muitos acessos, onde poderiam surgir gargalos?
    
114. Como Redis poderia ser usado nesse projeto?
    
115. Que dados fariam sentido cachear?
    
116. Como você invalidaria cache quando uma cor fosse alterada?
    
117. Como você processaria uma importação grande de clientes sem carregar tudo em memória?
    
118. Onde streams do Node poderiam ser úteis?
    
119. Se o sistema virasse um e-commerce, como você modelaria catálogo, estoque e pedidos?
    
120. Como você integraria esse sistema a um ERP externo?
    
121. Como você lidaria com falhas temporárias de uma API externa?
    
122. Quando usaria fila em vez de processar tudo na requisição HTTP?
    
123. Como você garantiria idempotência em integrações?
    
124. Como você lidaria com webhooks de pagamento?
    
125. Como você adicionaria notificações push com Firebase FCM?
    
126. Como você adaptaria esse backend para ser consumido por um app React Native?
    
127. O que muda no armazenamento de dados entre web e mobile?
    
128. O que você guardaria em AsyncStorage e o que não guardaria?
    
129. Quando usaria AWS S3 nesse projeto?
    
130. Quando usaria Lambda em vez de colocar tudo dentro da API?
    

---

## 11. Code review e postura de nível pleno

131. Se você fosse revisar esse projeto como tech lead, o que observaria primeiro?
    
132. Que decisões você defenderia com segurança?
    
133. Que decisões você mudaria se tivesse mais tempo?
    
134. Qual foi o maior trade-off técnico do projeto?
    
135. Qual parte do projeto você considera mais madura?
    
136. Qual parte está mais frágil?
    
137. Que bug você acha que poderia passar despercebido nesse sistema?
    
138. Como você priorizaria melhorias pós-entrega?
    
139. Como você comunicaria limitações técnicas para um PO ou cliente?
    
140. Como você equilibraria prazo curto com qualidade?
    
141. O que você faria se recebesse uma regra ambígua do cliente?
    
142. Como você documentaria decisões técnicas para a próxima equipe?
    
143. Como você lidaria com feedback negativo em code review?
    
144. Como você garantiria que outro dev consiga rodar o projeto localmente?
    
145. Qual seria seu plano para transformar esse teste em um MVP real?
    

---

## Perguntas mais prováveis de cair

Se o tempo for curto, priorize treinar estas:

1. Quais requisitos você identificou no enunciado e como traduziu isso em solução técnica?
    
2. Por que você escolheu PostgreSQL e como modelou cliente/cor?
    
3. Como você garantiu que o cliente só consiga se cadastrar uma vez?
    
4. Por que validar dados no frontend e também no backend?
    
5. Por que usar TypeScript nesse projeto?
    
6. Como você organizou o monorepo e por quê?
    
7. Como Docker ajuda na entrega e deploy desse projeto?
    
8. Como você protegeria uma área administrativa?
    
9. Quais dados pessoais existem e como aplicaria LGPD?
    
10. Que testes você escreveu ou escreveria primeiro?
    
11. Qual ponto fraco do seu projeto você melhoraria primeiro?
    
12. Como você evoluiria esse projeto para suportar mobile?
    
13. Onde Redis entraria nesse sistema?
    
14. Como você prepararia o projeto para uma equipe continuar o desenvolvimento?
    
15. Se tivesse mais uma semana, quais melhorias faria e em qual ordem?

---

# 5. Checklist final

Antes da entrevista, marque:

- [ ] Consigo explicar o projeto em 2 minutos.
- [ ] Explico `POST /auth/login` até o cookie no navegador.
- [ ] Sei defender cookie httpOnly vs localStorage.
- [ ] Sei explicar autenticação vs autorização.
- [ ] Sei explicar Guard, Pipe, Controller e Service.
- [ ] Sei explicar Zod compartilhado front/back.
- [ ] Sei explicar Prisma, migrations, `P2002`, `include` e `$transaction`.
- [ ] Sei falar do bug no delete de cor e como corrigiria.
- [ ] Tenho pelo menos 2 testes ou sei exatamente quais escreveria.
- [ ] Sei explicar React Native/Expo em alto nível.
- [ ] Sei dizer onde Redis entraria.
- [ ] Sei explicar PIX, webhook e tokenização.
- [ ] Sei explicar FCM com device token.
- [ ] Sei comparar PostgreSQL e MongoDB.
- [ ] Sei explicar EC2, S3 e Lambda.
- [ ] Tenho 3 pontos fracos do projeto e melhorias claras.

---

# 6. Resumo direto para usar na entrevista

## Pitch técnico do projeto

> “O projeto é um monorepo TypeScript com frontend em React/Vite, backend em NestJS, banco PostgreSQL com Prisma e validações compartilhadas com Zod. O backend possui autenticação JWT com cookie httpOnly, guards, rate limiting e tratamento de erros. O frontend consome a API com credenciais via cookie, usa formulários validados e uma interface responsiva. O deploy usa Docker, Nginx e pipeline CI/CD para ambiente em EC2.”

---

## Pontos fortes para destacar

- Monorepo TypeScript.
- Validação compartilhada com Zod.
- Backend NestJS organizado em módulos.
- JWT em cookie httpOnly.
- PostgreSQL + Prisma + migrations.
- Docker multi-stage.
- CI/CD com GitHub Actions.
- Uso de boas práticas de tratamento de erro.
- Autocrítica técnica sobre testes e rota protegida.

---

## Pontos fracos para admitir com maturidade

1. **Cobertura de testes ainda baixa.**
   - Melhoria: adicionar testes unitários, integração e e2e.
2. **Rota admin ainda não tem ProtectedRoute real.**
   - Melhoria: criar proteção no React Router.
3. **Bug no delete de cor.**
   - Melhoria: trocar `where: { id }` por `where: { colorId: id }`.
4. **Sem Redis.**
   - Melhoria: cache de listagens, estoque e preços.
5. **Sem refresh token.**
   - Melhoria: access token curto + refresh token seguro.
6. **Produção precisa de HTTPS.**
   - Melhoria: TLS com Nginx, ALB ou Let's Encrypt.

---

# 7. Fontes e onde foram aplicadas

| ID | Fonte | Link | Onde foi aplicada |
|---|---|---|---|
| F0 | Plano original enviado pelo usuário | `Plano-de-Estudos.md` | Base do cronograma, priorização dos 4 dias, pontos fortes/fracos do projeto, perguntas prováveis, bug do `colors.service`, lacunas da vaga e checklist final. |
| F1 | NestJS — Authentication | https://docs.nestjs.com/security/authentication | Dia 1: fluxo de autenticação, JWT, estratégia de autenticação e resposta pronta sobre login. |
| F2 | NestJS — Guards | https://docs.nestjs.com/guards | Dia 1: explicação de Guard, proteção de rotas e ciclo de request. |
| F3 | NestJS — Pipes | https://docs.nestjs.com/pipes | Dia 1: validação/transformação de dados antes do Controller. |
| F4 | NestJS — Testing | https://docs.nestjs.com/fundamentals/testing | Dia 2: bloco de testes automatizados no backend, mocks de providers e estrutura de testes. |
| F5 | React — Built-in Hooks | https://react.dev/reference/react/hooks | Dia 2: revisão geral de hooks e estado em React. |
| F6 | React — useEffect | https://react.dev/reference/react/useEffect | Dia 2: explicação de sincronização com APIs e efeitos colaterais. |
| F7 | React — useCallback | https://react.dev/reference/react/useCallback | Dia 2: explicação de cache de função e otimização de callbacks. |
| F8 | React — useMemo | https://react.dev/reference/react/useMemo | Dia 2: explicação de cache de cálculos e otimização. |
| F9 | TypeScript — strict | https://www.typescriptlang.org/tsconfig/strict.html | Dia 2: explicação do modo `strict` e segurança de tipos. |
| F10 | TypeScript — tsconfig.json | https://www.typescriptlang.org/docs/handbook/tsconfig-json.html | Dia 2: explicação de configuração de projeto TypeScript. |
| F11 | Expo Documentation | https://docs.expo.dev/ | Dia 3: visão geral de Expo e desenvolvimento React Native com Expo. |
| F12 | React Navigation — Getting started | https://reactnavigation.org/docs/getting-started/ | Dia 3: React Navigation, stack, tabs e navegação mobile. |
| F13 | Expo — AsyncStorage | https://docs.expo.dev/versions/latest/sdk/async-storage/ | Dia 3: persistência local no mobile e alerta sobre não armazenar dados sensíveis. |
| F14 | NestJS — Queues | https://docs.nestjs.com/techniques/queues | Dia 3: filas no NestJS, Redis e processamento assíncrono. |
| F15 | BullMQ Documentation | https://docs.bullmq.io/ | Dia 3: uso de BullMQ com Redis para filas, workers e jobs. |
| F16 | Cielo — API E-commerce | https://docs.cielo.com.br/ecommerce-cielo/docs/sobre-api-ecommerce | Dia 3: visão geral de integração com gateway de pagamento. |
| F17 | Cielo — Webhook/Post de Notificação | https://docs.cielo.com.br/ecommerce-cielo/docs/webhook | Dia 3: confirmação assíncrona de transações e importância de webhooks. |
| F18 | Cielo — Tipos de tokenização | https://docs.cielo.com.br/ecommerce-cielo/docs/tokenization-types | Dia 3: tokenização de cartão e motivo para não armazenar cartão cru. |
| F19 | Firebase — Cloud Messaging | https://firebase.google.com/docs/cloud-messaging | Dia 3: funcionamento geral do Firebase FCM e push notifications. |
| F20 | Firebase — Manage registration tokens | https://firebase.google.com/docs/cloud-messaging/manage-tokens | Dia 3: gerenciamento de device tokens e limpeza de tokens antigos. |
| F21 | AWS — Getting started with Amazon S3 | https://docs.aws.amazon.com/AmazonS3/latest/userguide/GetStartedWithS3.html | Dia 4: uso de S3 para armazenamento de arquivos/objetos. |
| F22 | AWS — What is AWS Lambda? | https://docs.aws.amazon.com/lambda/latest/dg/welcome.html | Dia 4: uso de Lambda para funções event-driven/serverless. |
| F23 | TOTVS — Varejo Supermercados API | https://centraldeatendimento.totvs.com/hc/pt-br/articles/5097492575767-Varejo-Supermercados-API-Listagem-de-APIs-dispon%C3%ADveis | Dia 3: referência geral para integração com APIs TOTVS/Consinco e sincronização ERP. |

---

# 8. Observação final

A melhor preparação, considerando o tempo curto, é:

1. **Defender o que você fez.**
2. **Reconhecer pontos fracos com maturidade.**
3. **Conectar cada lacuna da vaga com uma solução prática.**
4. **Responder com exemplos reais do projeto.**

Não tente passar a impressão de domínio profundo em tudo. Para uma entrevista de pleno, pesa muito mais mostrar raciocínio técnico, consciência de trade-offs e capacidade de evoluir o sistema.
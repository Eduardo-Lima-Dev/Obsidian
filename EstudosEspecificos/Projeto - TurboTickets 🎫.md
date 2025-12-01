**O Desafio:** Criar um monorepo onde o Backend serve dados de tickets e processa um fluxo de dados (streams), e o Frontend consome isso usando a interface visual da Zendesk.

### Roadmap de Execução (Passo a Passo)

#### Passo 1: O Chão de Fábrica (Setup do Turborepo)

Não crie as pastas na mão. Vamos usar o gerador para criar a estrutura monorepo.

1. Rode no terminal: `npx create-turbo@latest`
2. Dê o nome de `turbo-tickets`.
3. Escolha `npm` ou `pnpm` (pnpm é mais rápido para monorepos).
4. Isso criará pastas `docs` e `web` (Next.js) por padrão. **Apague** o conteúdo da pasta `apps` para começarmos do zero com as tecnologias que você quer (Vite e Nest).
#### Passo 2: O Backend (NestJS + Streams)

Vamos criar a API dentro da pasta `apps`.

1. Entre na pasta `apps`: `cd apps`.
2. Instale o NestJS CLI (se não tiver): `npm i -g @nestjs/cli`.
3. Crie o projeto: `nest new api` (escolha o mesmo gerenciador de pacotes, ex: pnpm).
4. **A Missão do Backend:**
    - Crie um módulo `TicketsModule`.
    - Crie um endpoint `GET /tickets` que retorna um array de objetos (use TypeScript!).
    - **Desafio Node Streams:** Crie um endpoint `GET /tickets/export`. Ao invés de retornar um JSON normal, use `StreamableFile` do NestJS para simular o envio de um relatório "pesado" linha por linha para o cliente.
#### Passo 3: O Frontend (React + Zendesk Garden)

Ainda na pasta `apps`, vamos criar o frontend.

1. Crie o projeto React com Vite: `npm create vite@latest web -- --template react-ts`.
2. Instale as dependências visuais:
	
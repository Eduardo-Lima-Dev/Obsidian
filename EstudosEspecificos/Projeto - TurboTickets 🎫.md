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
```Bash
	npm install styled-components @zendeskgarden/react-components@zendeskgarden/react-theming react-icons react-router-dom
```
3. **A Missão do Frontend:**
    - Configure o `ThemeProvider` do Zendesk Garden no `App.tsx`.
    - Crie uma rota `/` que lista os tickets.
    - Use o componente `Table` do Zendesk Garden para mostrar os dados vindos da API.

#### Passo 4: O "Pulo do Gato" (Compartilhamento de Tipos)

Aqui é onde o Turborepo brilha e você domina o TypeScript.
1. Na pasta `packages`, crie uma pasta `types`.
2. Crie um `index.ts` exportando uma interface, por exemplo:
```TypeScript
export interface Ticket { 
	id: string; 
	subject: string; 
	status: 'open' | 'closed'; 
}
```
3. No `package.json` da `api` e da `web`, adicione essa dependência local.
4. **Resultado:** Se você mudar o tipo no pacote `types`, o Backend (que envia) e o Frontend (que recebe) vão acusar erro se não estiverem alinhados. Isso é o poder do monorepo.

#### Passo 5: Rodando tudo junto

Na raiz do projeto `turbo-tickets`:

1. Rode `npx turbo dev`.
2. O Turborepo vai iniciar o NestJS (porta 3000, por exemplo) e o Vite (porta 5173) ao mesmo tempo, em um único terminal.
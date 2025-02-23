---
tags:
  - Videos
materia: Livre
tipo: Hobbie
estado: Nao Gravado
---
## Ato 1: Introdução e Contextualização

### Apresentação Pessoal e do Projeto
- **Saudação e Boas-Vindas:**  
  "Fala, pessoal! Eu sou **Eduardo** e, depois de criar conteúdos para Instagram e TikTok, decidi trazer para o YouTube um conteúdo mais técnico e aprofundado. Esse vídeo marca o começo de algo novo por aqui, onde vou compartilhar experiências reais do meu dia a dia como desenvolvedor, sempre trazendo aprendizados práticos que podem ajudar vocês."

- **Introdução ao Assunto do Vídeo:**
  "E pra começar com o pé direito, vou contar pra vocês sobre um problema real que enfrentei em um dos meus projetos e como resolvi de forma eficiente. Se você já programou alguma aplicação web, sabe que a segurança é um dos pontos mais críticos. Um simples descuido pode abrir brechas para acessos indevidos – e foi exatamente isso que aconteceu comigo."

- **Sobre o Meu Racha:**  
  "Eu desenvolvi um sistema chamado **Meu Racha**, que ajuda a organizar times no futebol amador de forma mais equilibrada. Ele foi criado inicialmente para o meu grupo de amigos, mas logo percebi que poderia ser útil para muitas outras pessoas."

### O Papel do Tabnews
- **O que é o Tabnews:**  
  "Recentemente, publiquei um artigo no Tabnews – uma plataforma colaborativa de publicação de conteúdos, onde qualquer pessoa pode compartilhar textos, notícias e opiniões de forma democrática."

- **Quem é o Criador:**  
  "O Tabnews foi criado por um desenvolvedor brasileiro que buscava oferecer um espaço livre e descentralizado para a disseminação de informações. Essa iniciativa tem contribuído para uma comunidade ativa e colaborativa, permitindo que ideias e debates ganhem visibilidade."

### O Problema Identificado
- **A Falha de Segurança:**  
  "Após a publicação do meu artigo no Tabnews, recebi uma mensagem informando sobre um erro crítico: uma rota sem autenticação, que permitia acesso administrativo a qualquer pessoa sem login. Esse bug comprometia a segurança do sistema."

- **Gancho para a Solução:**  
  "No vídeo de hoje, vou explicar como identifiquei esse problema e, principalmente, como o corrigi utilizando um middleware. Vou detalhar o que é um middleware, como ele foi implementado e por que essa abordagem é a mais adequada para proteger o Meu Racha."

---

## Ato 2: Desenvolvimento e Explicação Técnica

### 1. Conceito de Middleware
- **Definição e Importância:**  
  "Um middleware é uma camada intermediária que intercepta as requisições antes que elas cheguem à rota final, permitindo a aplicação de verificações de autenticação e autorização de maneira centralizada. Isso garante que apenas usuários devidamente autenticados e autorizados possam acessar áreas restritas do sistema."

### 2. Análise do Código do Middleware

#### Código do Middleware
```js
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function middleware(req: NextRequest) {
  const token = req.cookies.get("token")?.value;
  const userRole = req.cookies.get("role")?.value;

  if (!token) {
    return NextResponse.redirect(new URL("/admin", req.url));
  }

  if (!userRole || userRole !== "admin") {
    return NextResponse.redirect(new URL("/acesso-negado", req.url));
  }

  return NextResponse.next();
}

export const config = {
  matcher: ["/dashboard", "/times", "/notas"],
};
```

- **Explicação:**  
  - **Verificação do Token:**  
    "O middleware verifica se há um token armazenado nos cookies. Se não encontrar, redireciona o usuário para a página de login (`/admin`)."
  - **Verificação do Papel do Usuário:**  
    "Em seguida, ele confere o cookie que contém a role do usuário. Caso a role não exista ou não seja 'admin', o usuário é redirecionado para a página de acesso negado (`/acesso-negado`)."
  - **Fluxo de Acesso Permitido:**  
    "Se ambas as condições forem satisfeitas, o middleware permite que a requisição prossiga normalmente com `NextResponse.next()`."

### 3. Integração com a Aplicação

#### Página de Login (AdminLogin)
- **Autenticação e Configuração dos Cookies:**  
  "No componente de login, o usuário insere suas credenciais, o Firebase autentica e, após a verificação, os cookies (`token`, `role`, entre outros) são configurados. Esses cookies serão posteriormente validados pelo middleware para controlar o acesso às áreas restritas."
  
*Trecho de código relevante:*
```js
Cookies.set("role", role, { path: "/", sameSite: "strict", secure: true });
Cookies.set("token", await userCredential.user.getIdToken(), { path: "/", sameSite: "strict", secure: true });
```

#### Página Protegida (AdminDashboard)
- **Verificação Adicional:**  
  "Na página do dashboard, há uma verificação local (utilizando um hook `useEffect`) que redireciona o usuário para a página de acesso negado se os cookies não estiverem corretos. Essa redundância reforça a segurança do sistema."

*Exemplo de verificação:*
```js
useEffect(() => {
  const checkAuth = () => {
    const role = Cookies.get("role");
    const token = Cookies.get("token");

    if (!token || role !== "admin") {
      router.push("/acesso-negado");
    }
  };

  checkAuth();
}, [router]);
```

### 4. Racional da Solução
- **Centralização das Verificações:**  
  "A utilização de um middleware permite centralizar as verificações de autenticação e autorização, evitando a repetição de código em cada rota protegida."
- **Robustez e Escalabilidade:**  
  "Essa abordagem não só corrigiu a vulnerabilidade reportada, como também fortaleceu o sistema para futuras implementações e melhorias, garantindo um ambiente mais seguro para todos os usuários."

---

## Ato 3: Conclusão e Chamadas para Ação

### Recapitulação
- **Resumo da Solução:**  
  "Identifiquei uma falha de segurança que permitia o acesso indevido à área administrativa. Ao implementar um middleware que verifica a presença de um token e a role do usuário, garanti que somente administradores possam acessar as rotas protegidas."

### Lições Aprendidas e Dicas Técnicas
- **Importância da Segurança:**  
  "Esse processo reforçou a importância de implementar boas práticas de segurança, como a centralização de verificações com middlewares, para proteger aplicações web."
- **Conselhos para Desenvolvedores:**  
  "Sempre revise e teste as rotas sensíveis do seu sistema e utilize abordagens centralizadas para garantir que as verificações de autenticação sejam aplicadas de forma consistente."

### Chamadas para Ação
- **Engajamento com o Público:**  
  "Se você gostou deste conteúdo, deixe seu like, se inscreva no canal e compartilhe suas dúvidas ou experiências nos comentários!"
- **Agradecimento e Encerramento:**  
  "Esse foi meu primeiro vídeo aqui no YouTube, e espero que as dicas tenham sido úteis. Muito obrigado por assistir e até o próximo vídeo!"

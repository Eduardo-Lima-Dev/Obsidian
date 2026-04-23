
Substitui `BASE_URL` pela URL da API (ex.: `http://localhost:3000`).
Todos os corpos são `Content-Type: application/json`.

---
## 1. Aluno — autocadastro com convite (público)

Não envia cabeçalho `Authorization`.

**`POST {BASE_URL}/usuarios/registro/aluno`**

```json

{

"nome": "Maria Silva",

"email": "maria@example.com",

"senha": "senhaSegura12",

"conviteToken": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",

"cursoId": "00000000-0000-4000-8000-000000000000"

}

```


- `conviteToken`: UUID devolvido ao gerar convite tipo `CADASTRO_ALUNO`.
- `cursoId`: opcional (omitir a chave ou não enviar se não aplicável).

**Exemplo com `fetch`:**


```javascript

await fetch(`${BASE_URL}/usuarios/registro/aluno`, {

method: 'POST',

headers: { 'Content-Type': 'application/json' },

body: JSON.stringify({

nome: 'Maria Silva',

email: 'maria@example.com',

senha: 'senhaSegura12',

conviteToken: tokenDaUrlOuRespostaDoConvite,

}),

});

```

---
## 2. Professor — autocadastro com convite (público)

**`POST {BASE_URL}/usuarios/registro/professor`**

```json

{

"nome": "João Professor",

"email": "joao@example.com",

"senha": "outraSenha8chars",

"conviteToken": "uuid-do-convite-CADASTRO_PROFESSOR",

"cursoId": "00000000-0000-4000-8000-000000000000"

}

```

- `conviteToken`: convite tipo `CADASTRO_PROFESSOR` (emitido por coordenador).
- `cursoId`: opcional.

---
## 3. Coordenador cria professor ou aluno (autenticado)
Requer JWT de utilizador com role **COORDENADOR** (`POST /auth/login` antes).

**Professor — `POST {BASE_URL}/usuarios/coordenador/professores`**

```http

Authorization: Bearer <access_token>

```

```json

{

"nome": "Ana Costa",

"email": "ana@example.com",

"cursoId": "uuid-do-curso-do-coordenador"

}

```

**Aluno — `POST {BASE_URL}/usuarios/coordenador/alunos`**

  

Mesmo corpo JSON. A resposta inclui `senhaTemporaria` (mostrar uma vez ou enviar por canal seguro).

  

**Exemplo com `fetch`:**

  

```javascript

await fetch(`${BASE_URL}/usuarios/coordenador/alunos`, {

method: 'POST',

headers: {

'Content-Type': 'application/json',

Authorization: `Bearer ${accessToken}`,

},

body: JSON.stringify({

nome: 'Ana Costa',

email: 'ana@example.com',

cursoId: cursoIdDoCoordenador,

}),

});

```

  

---

  

## 4. Clínica cria coordenador (autenticado)

  

Requer JWT com role **CLINICA**.

  

**`POST {BASE_URL}/clinica/{clinicaId}/coordenadores`**

  

```http

Authorization: Bearer <access_token>

```

  

```json

{

"nome": "Carlos Coordenador",

"email": "carlos@example.com",

"cursoId": "uuid-do-curso"

}

```

  

A resposta inclui `senhaTemporaria` para o novo coordenador.

  

---

  

## 5. Gerar convite (antes do registo público)

  

Requer JWT de **PROFESSOR** ou **COORDENADOR**.

  

**`POST {BASE_URL}/convites`**

  

```http

Authorization: Bearer <access_token>

```

  

Convite para aluno (professor ou coordenador):

  

```json

{ "tipo": "CADASTRO_ALUNO" }

```

  

Convite para professor (apenas coordenador):

  

```json

{ "tipo": "CADASTRO_PROFESSOR" }

```

  

Usa o `token` devolvido na resposta como `conviteToken` nos endpoints de registo das secções 1 e 2.

  

---

  

## 6. Login (após existir utilizador)

  

**`POST {BASE_URL}/auth/login`**

  

```json

{

"email": "maria@example.com",

"senha": "senhaSegura12"

}

```

  

Resposta típica: `access_token`, `token_type` (`Bearer`). Usar o token nos endpoints autenticados acima.

  

---

  

## Notas

  

- `senha` nos registos públicos tem comprimento mínimo de **8** caracteres (validação do backend).

- Valores de `tipo` em convites correspondem ao enum `TipoConvite` no Prisma (`CADASTRO_ALUNO`, `CADASTRO_PROFESSOR`).

- Documentação interativa: Swagger em `/api/docs` (em produção pode exigir HTTP Basic, conforme configuração do ambiente).
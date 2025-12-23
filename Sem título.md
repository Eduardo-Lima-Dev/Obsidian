### **Ato 1 – Contexto e problema (0:00 – 0:50)**  
- **Cena 1 – Apresentação**  
  “Olá, neste vídeo eu vou mostrar uma pequena migração que fizemos no Propag para melhorar a identificação dos projetos, sem quebrar nada do que já existe hoje.”  

- **Cena 2 – Como é hoje**  
  “Atualmente, cada projeto no sistema é identificado apenas por um `id` numérico sequencial, gerado automaticamente pelo banco.  
  Isso funciona bem internamente, mas para o usuário ou para a secretaria, olhar só para ‘id 57’ não diz nada sobre o ano ou o contexto daquele projeto.”  

- **Cena 3 – Problema**  
  “Na prática, isso dificulta organização, filtragem manual, comunicação entre equipe e até a emissão de relatórios, porque o identificador não traz nenhuma informação semântica, como o ano do projeto.”  

---

### **Ato 2 – Solução e funcionamento (0:50 – 2:10)**  
- **Cena 4 – Ideia da migração**  
  “A solução foi criar um novo identificador amigável para cada projeto, chamado `codigo`, formado por `ano do projeto + id`.  
  Por exemplo, um projeto de 2026 com id 23 passaria a ter o código `202600023`.”  

- **Cena 5 – Preservando o que já existe**  
  “É importante: o `id` numérico continua exatamente igual. Ele ainda é a chave primária, usado em todos os relacionamentos e endpoints atuais.  
  O que fizemos foi adicionar um novo campo `codigo` na entidade `Projeto` e na tabela do banco, sem alterar os dados existentes.”  

- **Cena 6 – Como o código é gerado**  
  “Quando um novo projeto é salvo, o fluxo é assim:  
  1. O backend salva o projeto normalmente, o banco gera o `id`.  
  2. Depois disso, o serviço calcula o `codigo` usando o ano atual + o `id` com zero à esquerda.  
  3. Em seguida, atualiza o registro com esse `codigo` e devolve para o frontend tanto o `id` quanto o `codigo`.”  

- **Cena 7 – Exemplos de uso**  
  “No frontend, continuamos usando `id` para tudo que é interno, mas passamos a exibir o `codigo` sempre que o usuário precisa identificar um projeto: em listagens, detalhes e comunicação.  
  Opcionalmente, podemos expor um endpoint de busca por `codigo`, além da busca tradicional por `id`.”  

---

### **Ato 3 – Benefícios e fechamento (2:10 – 3:00)**  
- **Cena 8 – Benefícios**  
  “Com isso, ganhamos um identificador mais rico, que traz o ano embutido, facilita a organização, ajuda na comunicação entre coordenação, secretaria e avaliadores, e melhora relatórios — tudo isso sem impactar a compatibilidade com o que já estava em produção.”  

- **Cena 9 – Conclusão**  
  “Resumindo: mantivemos a segurança e a integridade do sistema, adicionando apenas uma camada de clareza para quem usa o Propag no dia a dia.  
  Essa é a essência da migração: evoluir o modelo de projetos sem quebrar o passado. Obrigado por assistir.”
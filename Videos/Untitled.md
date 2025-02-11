---
tags:
  - Videos
materia: Livre
tipo: Hobbie
estado: Nao Gravado
---
---
### **Ato 1 - O Orgulho do Criador**

Eu estava empolgado. Depois de semanas desenvolvendo o **Meu Racha**, um sistema para organizar partidas e rachas entre amigos, finalmente publiquei um artigo no **Tabnews** falando sobre o projeto. Expliquei como ele funcionava, as tecnologias usadas e até compartilhei algumas decisões de design que tomei ao longo do caminho.

A recepção foi melhor do que eu esperava! Algumas pessoas comentaram elogiando o projeto, outras fizeram sugestões interessantes. Mas então, no meio das mensagens, apareceu um comentário diferente:

> "Tem uma falha de segurança no sistema. Uma rota que deveria estar autenticada não está."

Aquilo acendeu um alerta. Resolvi parar tudo e ir checar.

---

### **Ato 2 - O Desastre Anunciado**

Ao abrir o projeto, comecei a investigar. O código estava funcionando como esperado… até que resolvi dar uma olhada no banco de dados.

Nada.

Zero registros.

O **banco inteiro** tinha sido apagado.

Na hora, meu cérebro deu um curto-circuito. Como assim? Eu não tinha deixado nenhum comando que pudesse apagar tudo assim do nada.

Foi aí que percebi o erro.

Eu tinha implementado um botão **"Limpar Jogadores"**, que era para resetar a lista de jogadores cadastrados. O problema? Esse botão **simplesmente deletava todo o banco de dados**. E o pior: estava exposto sem nenhuma autenticação. Ou seja, qualquer pessoa que descobrisse a rota poderia apagar tudo com um simples request.

Foi exatamente o que aconteceu.

---

### **Ato 3 - O Aprendizado (E A Dor)**

Depois de uma mistura de choque, frustração e um pouco de riso nervoso, comecei a corrigir o problema. A primeira coisa foi adicionar autenticação nas rotas sensíveis e restringir os comandos perigosos. Também revisei toda a segurança do sistema para evitar que algo assim acontecesse de novo.

Mas a maior lição veio depois: **nunca subestime o impacto de uma única funcionalidade mal planejada**. Um simples botão, que parecia inofensivo, se transformou em uma armadilha capaz de derrubar o projeto inteiro.

No fim, aprendi da pior forma que **segurança nunca é opcional**. Mas agora, pelo menos, o **Meu Racha** está mais forte do que antes – e eu também.

---


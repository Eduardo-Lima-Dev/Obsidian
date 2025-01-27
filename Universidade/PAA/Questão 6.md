---
tags:
  - Universidade
materia: PAA
tipo: Atividade
estado: Concluído
---

![[{B7267974-41CF-49DE-AAB6-912240E3ED74}.png]]

## Resposta

- O **Kruskal** não precisa de muitas mudanças, porque ele já lida com grafos desconexos. Só precisamos ordenar as arestas por peso e usar o Union-Find pra garantir que não terá ciclos. Ele automaticamente cria árvores geradoras mínimas para cada componente.
- o **Prim** já precisa rodar um algoritmo separado para cada componente do grafo. Primeiro vamos identificar as componentes conexas com BFS ou DFS, depois executamos o Prim em cada uma delas, criando as árvores mínimas. 


> [!Camada Aplicação] Próximo Assunto 
> [[Questão 4]]
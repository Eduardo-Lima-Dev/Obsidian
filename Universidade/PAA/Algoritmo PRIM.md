---
tags:
  - Universidade
materia: PAA
tipo: Revisão
---
O algoritmo PRIM constrói a arvore geradora mínima adicionando um vértice de cada vez. Ele baseia em expandir uma arvore a partir de um vértice inicial, escolhendo sempre a arvore de menor peso que conecta um vértice de uma arvore a um vértice fora dela.

> Cuidado para não fechar um ciclo, pois deixa de ser uma arvore, como no exemplo abaixo se conectarmos **(1 -> 4 -> 3 -> 1)** deixa de ser uma arvore 
### **Exemplo:**
![[{547526B9-AC16-49B8-BFB8-5ED7F922F1FE}.png]]


| De -> Para | Custo  |
| ---------- | ------ |
| 1 -> 4     | 4      |
| 4 -> 3     | 2      |
| 4 -> 6     | 4      |
| 3 -> 5     | 4      |
| 5 -> 2     | 3      |
| 6 -> 7     | 6      |
| **Total**  | **23** |


> [!Camada Aplicação] Próximo Assunto 
> [[Lista de Exercı́cios 1|Lista de Exercı́cios 1]]
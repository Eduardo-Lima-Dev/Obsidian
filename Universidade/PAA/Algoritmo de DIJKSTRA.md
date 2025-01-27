---
tags:
  - Universidade
materia: PAA
tipo: Revisão
---
Ele é um dos mais famosos algoritmos para a resolução do problema dos caminhos mínimos de única fonte. Ele determina a menor distancia de um vértice de origem para todos os outros vértices do grafo.
### **Exemplo:**

![[{927D037F-5898-44B6-BAC9-AD6486A3447F}.png]]

| Vértice     | A   | B     | C     | D     | E     |
| ----------- | --- | ----- | ----- | ----- | ----- |
| Distancia   | 0   | **∞** | **∞** | **∞** | **∞** |
| Predecessor |     |       |       |       |       |

| Vértice     | A*  | B   | C   | D     | E     |
| ----------- | --- | --- | --- | ----- | ----- |
| Distancia   | 0   | 4   | 3   | **∞** | **∞** |
| Predecessor |     | A   | A   |       |       |

| Vértice     | A*  | B   | C*  | D   | E   |
| ----------- | --- | --- | --- | --- | --- |
| Distancia   | 0   | 4   | 3   | 4   | 6   |
| Predecessor |     | A   | A   | C   | C   |

| Vértice     | A*  | B*  | C*  | D   | E   |
| ----------- | --- | --- | --- | --- | --- |
| Distancia   | 0   | 4   | 3   | 4   | 6   |
| Predecessor |     | A   | A   | C   | C   |

| Vértice     | A*  | B*  | C*  | D*  | E   |
| ----------- | --- | --- | --- | --- | --- |
| Distancia   | 0   | 4   | 3   | 4   | 6   |
| Predecessor |     | A   | A   | C   | C   |

#### **Qual menor caminho entre A -> D?**

A -> C -> D, com custo total de 4


> [!Camada Aplicação] Próximo Assunto 
> [[Algoritmo PRIM]]
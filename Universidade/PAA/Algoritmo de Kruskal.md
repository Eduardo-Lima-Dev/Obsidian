---
tags:
  - Universidade
materia: PAA
tipo: Revisão
---
## Implementação com  Union-Find

``` Kruskal(G, w)
1  Crie um vetor C[1..e(G)] e copie as arestas de G para C
2  Ordene C de modo não-decrescente de pesos das arestas
3  Seja F = ∅
4  para todo vértice v ∈ V(G) faça
5      MAKESET(v)
6  para i = 1 até e(G) faça
7      Seja uv a aresta em C[i]
8      se FINDSET(u) ≠ FINDSET(v) então
9          F = F ∪ {C[i]}
10         UNION(u, v)
11 retorna F
```

![[{B6BE9F8C-8D82-41B8-A43F-EB76BAB604C4}.png]]

![[{B25F4FD2-AA4D-4026-A9DD-68A260C20646}.png]]


> [!Camada Aplicação] Próximo Assunto 
> [[Lista de Exercı́cios 1|Lista de Exercı́cios 1]]
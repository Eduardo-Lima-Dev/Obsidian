---
tags:
  - Universidade
materia: PAA
---
## Notação Assintótica
É uma abstração que permite focar no que ocorre com $f(n)$ quando $n$ cresce indefinidamente.
> - Termos de menor ordem não importam
> - Constantes não importam
> - **Ex:** $f(n) = 2n³ + 400n² + 10000n - 47$
> - $n³$ é o termo de maior ordem nesse exemplo

## 3 Notações Básicas

### Notação $O$
- Notação que limita funções superiormente
Seja $n$ um inteiro positivo e sejam $f(n)$ e $g(n)$ funções positivas
- Dizemos que: $$f(n) = O(g(n))$$ou $$(f(n)  é  O(g(n))$$
- Se existem Constantes positivas $C$ e $N_0$ tais que: $$f(n) \leq C * g(n)$$
- Para todo $$n \geq N_0$$
### Exemplo $$f(n) \leq 5tn + 3t$$
- $g_1(n)=n$
- $g_2(n) = n²$
- $g3(n) = \sqrt{n}$

### $G_1$
$$
5tn + 3t \leq 5tn + 3tn
$$
$$
5tn + 3tn = 8tn
$$
$$
f(n) \leq Cn
$$
- Significa que **$f(n) \ é \ O(g(n))$**
### $G_2$
$$
5tn + 3t \leq 5tn + 3tn
$$
$$
5tn + 3tn = 8tn \leq 8tn²
$$
-  Significa que **$f(n) \ é \ O(g(n))$**

### $G_3$



> [!Camada Aplicação] Próximo Assunto 
> [[Lista de Exercı́cios 2]]
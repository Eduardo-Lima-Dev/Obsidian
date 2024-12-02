---
tags:
  - Universidade
materia: PAA
estado: Concluído
tipo: Atividade
---
9. **É verdade que $2^{n+1} = O(2^n)$? E $2^{2n} = O(2^n)$?**
=> Analisando as afirmações
-  Para $2^{n+1} = O(2^n)$: **Verdadeira**
	Sabemos que $2^{n+1} = 2 * 2^n$. Quando dizemos que $f(n) = O(g(n))$, significa que $f(n)$ cresce no máximo tão rápido quanto $g(n)$ multiplicado por uma constante. Nesse caso, $2^{n+1}$ é proporcional a $2^n$, já que $2^{n+1} = 2 * 2^n$, que é a constante multiplicada por $2^n$
- Para $2^{2n} = O(2^n)$: **Falsa** 
	Nesse caso, $2^{2n} = (2^n)²$, ou seja, $2^{2n}$ cresce muito mais rápido que $2^n$. A relação $2^{2n} = O(2^n)$ seria verdadeira se $2^{2n}$ fosse no máximo proporcional a $2^n$, o que não é o caso. De fato, $2^{2n}$ cresce exponencialmente mais rápido que $2^n$.
=> **Conclusão:**
- $2^{n+1} = O(2^n)$: **Verdadeira**
- $2^{2n} = O(2^n)$: **Falsa**
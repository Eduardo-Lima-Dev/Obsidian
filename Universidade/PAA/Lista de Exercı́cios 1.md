---
tags:
  - Universidade
materia: PAA
estado: Concluído
---
1. **Escreva um algoritmo que testa se uma vetor de tamanho n esta ordenado. Depois determine a complexidade desse seu algoritmo em relação ao melhor e pior caso.**

``` C
bool is_sorted(int vetor[], int n) {
    for (int i = 1; i < n; i++) {
        if (vetor[i] < vetor[i - 1]) {
            return false;
        }
    }
    return true;
}
```

- O laço `for` percorre o vetor, começando de `i = 1` até `i = n - 1`, realizando ***`n - 1`*** iterações no total.
- Em cada iteração, é feita uma comparação `vetor[i] < vetor[i - 1]`.

Equação para o número total de operações:
$$
T(n)=n−1
$$
Simplificação:
$$
T(n)=O(n)
$$
2. **Escreva um algoritmo para inserir um elemento em um vetor ordenado contendo n elementos (supondo o tamanho máximo do vetor m >> n), de tal modo que após a inserção ele continue ordenado. Depois determine a complexidade desse seu algoritmo em relação ao melhor e pior caso.**

```C
void insert_in_sorted_array(int vetor[], int *n, int elemento) {
    int i = *n - 1;

    while (i >= 0 && vetor[i] > elemento) {
        vetor[i + 1] = vetor[i];
        i--;
    }

    vetor[i + 1] = elemento;
    (*n)++;
}

```

- O `while` move elementos maiores que o novo elemento para a direita até encontrar a posição correta para inseri-lo.
- No **pior caso**, o elemento é menor que todos os elementos do vetor, então o laço `while` percorre todos os ***n*** elementos.

Equação para o número total de operações no pior caso:

$$
T(n)=n
$$
Simplificação:

$$
T(n)=O(n)
$$

> [!Camada Aplicação] Próximo Assunto 
> [[Lista de Exercı́cios 2]]
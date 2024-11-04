---
tags:
  - Universidade
materia: PAA
---
### 1. **Objetivo da Análise de Algoritmos**

A análise de algoritmos é essencial para prever o comportamento de um algoritmo em termos de eficiência antes de sua implementação. A ideia é estimar o tempo que ele levará para executar e determinar a "pior entrada" possível – aquela que fará o algoritmo consumir o maior tempo para concluir sua tarefa. Esses insights ajudam na escolha de algoritmos adequados para problemas específicos, principalmente quando lidamos com grandes volumes de dados.

### 2. **Tipos de Problemas Computacionais**

Problemas computacionais podem ser categorizados como:

- **Problemas de Decisão**: Responder com um “sim” ou “não” para uma pergunta específica, como verificar se um número é primo.
- **Problemas de Busca**: Envolve encontrar uma solução específica em um conjunto de dados, como localizar um item em uma lista.
- **Problemas de Otimização**: Determinar a melhor solução dentro de várias possibilidades, como o problema da mochila, onde a meta é maximizar o valor transportado respeitando restrições de peso.

**Exemplos práticos**:

- **Primalidade**: Dado um número, o problema é verificar se ele é primo. A resposta é "sim" ou "não".
- **Ordenação**: Consiste em ordenar os elementos de um vetor de inteiros.
- **Problema da Mochila**: Maximizar o valor dos itens transportados por um ladrão com uma mochila de capacidade limitada.
- **Caixeiro Viajante**: Encontrar o caminho mais curto que permite visitar todas as cidades uma única vez e retornar ao ponto de partida.

### 3. **Conceito de Algoritmo e Tamanho da Entrada**

Um **algoritmo** é uma sequência de passos bem definidos que recebe uma entrada e devolve uma saída correspondente. Na análise de algoritmos, o **tamanho da entrada** é um fator crucial, pois muitos algoritmos aumentam seu tempo de execução conforme o tamanho da entrada aumenta. Por exemplo:

- Em um problema de ordenação, o tamanho da entrada é o número de elementos no vetor.
- No problema da mochila, o número de itens é o tamanho da entrada.

### 4. **Complexidade de Algoritmos**

A **complexidade de um algoritmo** expressa o número de operações elementares que ele executa em função do tamanho da entrada. A função `T(n)` é usada para representar o tempo de execução em função de `n`, onde `n` é o tamanho da entrada. Cada operação fundamental do algoritmo é considerada um "passo" com tempo constante, como:

- **Atribuição** (definir um valor para uma variável)
- **Soma** e **multiplicação**
- **Comparação** (para avaliar uma condição)

A **quantidade de passos** que um algoritmo precisa executar define sua complexidade.

### 5. **Medição da Complexidade**

A complexidade de um algoritmo pode ser **analisada de três maneiras**:

- **Melhor Caso**: O cenário ideal, onde a configuração da entrada permite que o algoritmo termine rapidamente. Por exemplo, em uma busca sequencial, se o item buscado é o primeiro da lista.
- **Pior Caso**: O cenário onde o algoritmo consome o máximo tempo possível. Em uma busca sequencial, isso ocorre quando o item buscado está no final da lista ou não existe.
- **Caso Médio**: Uma média de tempos que representa o comportamento do algoritmo em condições variadas. O caso médio é mais complexo de calcular porque exige suposições probabilísticas sobre a distribuição da entrada.

### 6. **Exemplos de Análise de Complexidade**

- **Soma de um Vetor**: Um algoritmo que percorre um vetor para somar todos os elementos. Neste caso:
    
    - O tempo para somar o vetor cresce linearmente com `n` (o tamanho do vetor).
    - A função de complexidade para este caso é linear, representada como `T(n) = 2n + 3`, indicando que o tempo de execução aumenta proporcionalmente com o tamanho do vetor.
- **Busca Sequencial**:
    
    - **Melhor caso:** o elemento buscado está na primeira posição, então o algoritmo realiza poucas comparações.
    - **Pior caso:** o elemento está na última posição ou não está no vetor, fazendo o algoritmo percorrer todos os elementos.
    - **Caso médio:** requer uma análise probabilística para determinar o tempo médio esperado, considerando que o elemento pode estar em qualquer posição.

### 7. **Por Que Analisar Algoritmos?**

A análise de algoritmos permite escolher o mais eficiente para um determinado problema, especialmente em sistemas com restrições de tempo e espaço. A análise fornece uma visão independente do ambiente em que o algoritmo será executado (hardware, linguagem, etc.), tornando a comparação entre diferentes algoritmos mais justa e precisa.

> [!Camada Aplicação] Próximo Assunto 
> [[Atividade PAA|Atividade PAA]]
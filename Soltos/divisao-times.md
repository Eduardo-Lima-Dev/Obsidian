# Algoritmo de Divisão de Times

Este documento explica como funciona o algoritmo de divisão de times implementado no sistema.

## 1. Pesos e Complementaridade

O sistema utiliza pesos e complementaridade para avaliar os jogadores:

```typescript
const P1 = 0.4; // Peso para média
const P2 = 0.4; // Peso para gols
const P3 = 0.2; // Peso para assistências

const complementaridade = {
  media: { assistencias: 0.7, gols: 0.6 },
  gols: { media: 0.6, assistencias: 0.8 },
  assistencias: { media: 0.7, gols: 0.8 },
};
```

- Cada jogador tem um peso calculado baseado em sua média, gols e assistências
- A complementaridade define como diferentes habilidades se complementam entre si

## 2. Cálculo de Peso Individual

```typescript
const calcularPeso = (jogador: Jogador) => {
  return (
    jogador.media * P1 +
    jogador.gols * P2 +
    jogador.assistencias * P3
  );
};
```

- Calcula o peso total de um jogador usando os pesos P1, P2 e P3
- Exemplo: Se um jogador tem média 8, 5 gols e 3 assistências:
  - Peso = (8 * 0.4) + (5 * 0.4) + (3 * 0.2) = 3.2 + 2 + 0.6 = 5.8

## 3. Cálculo de Complementaridade

```typescript
const calcularComplementaridade = (jogadorA: Jogador, jogadorB: Jogador) => {
  return (
    Math.abs(jogadorA.media - jogadorB.media) * complementaridade.media.assistencias +
    Math.abs(jogadorA.gols - jogadorB.gols) * complementaridade.gols.assistencias +
    Math.abs(jogadorA.assistencias - jogadorB.assistencias) * complementaridade.assistencias.gols
  );
};
```

- Calcula quão bem dois jogadores se complementam
- Quanto maior a diferença em habilidades complementares, melhor a complementaridade

## 4. Algoritmo Genético

O sistema usa um algoritmo genético para otimizar a divisão dos times:

### a) Geração Inicial

```typescript
const gerarTimesIniciais = (jogadores: Jogador[], numTimes: number) => {
  const times: Jogador[][] = Array.from({ length: numTimes }, () => []);
  const shuffle = [...jogadores].sort(() => Math.random() - 0.5);
  shuffle.forEach((jogador, index) => {
    times[index % numTimes].push(jogador);
  });
  return times;
};
```

- Cria uma divisão inicial aleatória dos times

### b) Avaliação

```typescript
const avaliarTimes = (times: Jogador[][]) => {
  return times.map((time) => {
    const totalPeso = time.reduce((acc, jogador) => acc + calcularPeso(jogador), 0);
    const complementaridadeTotal = time.reduce((acc, jogador, i, arr) => {
      if (i === 0) return acc;
      return acc + calcularComplementaridade(jogador, arr[i - 1]);
    }, 0);
    return { peso: totalPeso, complementaridade: complementaridadeTotal };
  });
};
```

- Avalia a qualidade de cada time baseado no peso total e complementaridade

### c) Crossover e Mutação

```typescript
const crossover = (times: Jogador[][]) => {
  // Troca jogadores entre times
};

const mutacao = (times: Jogador[][], taxaMutacao: number) => {
  // Faz trocas aleatórias de jogadores
};
```

- Crossover: Troca jogadores entre times
- Mutação: Faz trocas aleatórias para evitar estagnação

## 5. Otimização

```typescript
const dividirTimesOtimizado = (jogadores: Jogador[], numTimes: number, maxIteracoes: number) => {
  let times = gerarTimesIniciais(jogadores, numTimes);
  let melhorTime = avaliarTimes(times);
  let melhorPontuacao = melhorTime.reduce((acc, t) => acc + t.peso, 0);

  for (let i = 0; i < maxIteracoes; i++) {
    let novosTimes = crossover(times);
    novosTimes = mutacao(novosTimes, 0.3);
    
    const novaAvaliacao = avaliarTimes(novosTimes);
    const novaPontuacao = novaAvaliacao.reduce((acc, t) => acc + t.peso, 0);

    if (novaPontuacao > melhorPontuacao) {
      melhorTime = novaAvaliacao;
      melhorPontuacao = novaPontuacao;
      times = novosTimes;
    }
  }

  return times;
};
```

- Executa o algoritmo genético por um número máximo de iterações
- Mantém a melhor divisão encontrada
- Tenta melhorar a divisão através de crossover e mutação

## Resultado Final

O resultado final é uma divisão de times que:
1. Tenta equilibrar o nível geral dos times (através do peso)
2. Busca complementaridade entre os jogadores de cada time
3. É otimizada através de um algoritmo genético
4. Pode ser ajustada através dos parâmetros (número de times, jogadores por time) 
---
tags:
  - Universidade
materia: PAA
tipo: Atividade
estado: Concluído
---
![[{83751182-BD95-4252-B1A2-604D053FD45D}.png]]
## Resposta

``` C
#include <stdio.h>

typedef struct {
    int id;
    int inicio;
    int fim;
} Atividade;

int compara(const void *a, const void *b) {
    Atividade *atividadeA = (Atividade *)a;
    Atividade *atividadeB = (Atividade *)b;
    return atividadeA->fim - atividadeB->fim;
}

void selecaoAtividades(Atividade atividades[], int n) {

    qsort(atividades, n, sizeof(Atividade), compara);

    printf("Atividades selecionadas:\n");

    int ultimaFim = atividades[0].fim;
    printf("Atividade %d (Início: %d, Fim: %d)\n", atividades[0].id, atividades[0].inicio, atividades[0].fim);

    for (int i = 1; i < n; i++) {
        if (atividades[i].inicio >= ultimaFim) {

            printf("Atividade %d (Início: %d, Fim: %d)\n", atividades[i].id, atividades[i].inicio, atividades[i].fim);
            ultimaFim = atividades[i].fim;
        }
    }
}

int main() {

    Atividade atividades[] = {
        {1, 1, 4}, {2, 3, 5}, {3, 0, 6}, {4, 5, 7}, {5, 3, 8},
        {6, 5, 9}, {7, 6, 10}, {8, 8, 11}, {9, 8, 12}, {10, 2, 13}, {11, 12, 14}
    };
    int n = sizeof(atividades) / sizeof(atividades[0]);

    selecaoAtividades(atividades, n);

    return 0;
}
```

### **Aplicando a Instancia do Problema**

#### Entrada:
Atividades com $s_i$ (início) e $f_i$ (fim):
- \{ (1,4), (3,5), (0,6), (5,7), (3,8), (5,9), (6,10), (8,11), (8,12), (2,13), (12,14) \} 

#### Saída:
Atividades selecionadas (maximizando o número de atividades compatíveis):
- Atividade 1:  (1, 4) 
- Atividade 4:  (5, 7) 
- Atividade 8: (8, 11) 
- Atividade 11:  (12, 14) 


> [!Camada Aplicação] Próximo Assunto 
> [[Questão 6]]
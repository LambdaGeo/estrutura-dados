# Lista - Pilhas

---

## 1. O que será impresso na tela

Considerando a implementação do TAD Pilha baseada em ponteiros e alocação dinâmica vista em aula, analise o código abaixo:

```
#include <stdio.h>

// Supondo que os TADs Pilha e Fila já estejam implementados com as funções:
// criaPilha(), criaFila(), empilha(), desempilha(), enfileira(), desenfileira().

int main() {
    // Criação das estruturas dinâmicas
    Pilha *s = criaPilha(10);
    Fila *q = criaFila(10);
    int temp_val;

    empilha(85, s);
    empilha(34, s);

    temp_val = desempilha(s);
    enfileira(temp_val, q);

    temp_val = desempilha(s);
    enfileira(temp_val, q);

    empilha(92, s);

    temp_val = desenfileira(q);
    empilha(temp_val, s);

    printf("%d\n", desempilha(s));
    printf("%d\n", desempilha(s));

    return 0;
}
```

**Pergunta:** Qual será a saída impressa no console ao final da execução?

---

## 2. Verificação de expressão balanceada

No material da disciplina, a **Pilha** foi apresentada como a estrutura ideal para avaliar expressões. Um exemplo clássico é o código que verifica se uma expressão formada por parênteses está balanceada.

Agora teste a implementação passando a seguinte expressão:

```
( 1 + 2 ) * (4 + (3 + 5) )
```

O algoritmo irá funcionar corretamente?
Caso contrário, corrija o algoritmo para analisar **apenas o balanceamento dos parênteses**, ignorando os números e operadores.

---

## 3. Simulação da avaliação de uma expressão pós-fixa

A avaliação de expressões em notação pós-fixa (polonesa reversa) é uma das principais aplicações práticas do conceito LIFO (*Last In, First Out*) de uma Pilha.

Simule a avaliação da seguinte expressão:

```
a b + c * d /
```

Onde:

```
a = 2, b = 4, c = 3, d = 36
```

Preencha a tabela de rastreio mostrando o estado da pilha passo a passo:

| Expressão | Elemento | Ação (empilha / desempilha) | Pilha (Estado atual) |
| --- | --- | --- | --- |
|  |  |  |  |

---

## 4. Avaliação pós-fixa com números de múltiplos dígitos

Modifique a implementação em C da **avaliação pós-fixa** para suportar:

- números com **vários dígitos**;
- **valores em ponto flutuante** (lembre-se de adaptar a sua `struct pilha` e o vetor interno `valores` para armazenar o tipo `float` ao invés de `int`, conforme sugerido no material).

Teste com a expressão:

```
45.5 83 + 75.4 *
```
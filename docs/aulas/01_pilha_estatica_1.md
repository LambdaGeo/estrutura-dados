# Pilha Estática I: Implementação Básica com Vetores Globais

Este capítulo introduz o conceito de Tipo Abstrato de Dados (TAD) através do exemplo mais simples possível: a pilha. O objetivo é compreender a lógica LIFO da pilha e, em seguida, vivenciar na prática as limitações de uma implementação sem encapsulamento — o que motivará, no próximo capítulo, a introdução de `struct` e funções.

## 1. Tipo Abstrato de Dados (TAD)

Um Tipo Abstrato de Dados (TAD) é uma forma de organizar uma coleção de dados junto com um conjunto de operações bem definidas, escondendo como essa coleção é realmente armazenada na memória. Dito de forma mais direta: um TAD é como um "container" de dados — ele define que tipo de dado você pode colocar dentro e quais operações fazem sentido nesse container, sem que quem o usa precise saber os detalhes de implementação.

Três ideias sustentam esse conceito:

1. **Abstração:** quem usa o TAD conhece a interface ("o que ela faz"), não o "como".
2. **Encapsulamento:** o estado interno (por exemplo, o vetor e o topo de uma pilha) fica protegido; o acesso só acontece através das operações previstas.
3. **Reusabilidade:** o mesmo TAD pode ser usado em vários contextos diferentes.

Pilha, fila, lista e árvore são todos exemplos de TADs — cada um com uma lógica própria de organização e acesso.

## 2. A Pilha como TAD

A ideia por trás de uma pilha é intuitiva: imagine uma pilha de pratos, de livros ou de caixas. Os elementos são colocados uns sobre os outros, e apenas o elemento do topo está diretamente acessível. Na pilha, o primeiro elemento a entrar pode ficar "sepultado" por muito tempo; o último a entrar é sempre o primeiro a sair.

Essa política de acesso é chamada de **LIFO** — *Last In, First Out* (último a entrar, primeiro a sair) — e se resume a três regras: a inserção sempre acontece no topo da pilha, a remoção só pode remover o topo, e o acesso de leitura também se limita ao topo. As três operações conceituais que implementam essa política são `push` (empilhar, insere um elemento no topo), `pop` (desempilhar, remove o elemento do topo) e `peek`/`top` (consulta o valor do topo sem removê-lo).

Essa estrutura aparece com frequência fora da sala de aula: em uma pilha de pratos, tudo que é lavado é colocado em cima, e ao retirar um prato sempre se retira o de cima; no navegador web, cada página visitada é empilhada, e o botão "Voltar" desempilha a última página visitada; em um editor de texto, cada ação é empilhada, e `Ctrl+Z` desfaz desempilhando a ação mais recente.

## 3. Aplicações de Pilha em Programação

A pilha não é apenas um exercício didático — ela está presente em mecanismos que você já usa no dia a dia da programação. A **pilha de chamadas** (*call stack*) gerencia as funções em execução e suas variáveis locais. A avaliação de expressões em notação pós-fixa (polonesa reversa) depende de uma pilha para armazenar operandos intermediários. Algoritmos de exploração como busca em profundidade (DFS) e *backtracking* usam pilhas — explícitas ou implícitas, via recursão — para acompanhar o caminho percorrido. E funcionalidades de "desfazer"/"voltar" em sistemas em geral são, no fundo, uma pilha de estados anteriores.

## 4. Implementação Estática Simples em C

Antes de construir uma pilha bem projetada, vale a pena implementar uma versão deliberadamente "nua": apenas variáveis globais, sem funções, sem ponteiros e sem `struct`. Isso torna visíveis os problemas que um TAD bem feito resolve.

O núcleo dessa versão são duas variáveis globais:

```c
int pilha[MAX];
int topo = -1;
```

O vetor `pilha` guarda os elementos, e a variável `topo` indica o índice do último elemento inserido — quando `topo == -1`, a pilha está vazia.

Um exemplo completo, empilhando e desempilhando alguns valores:

```c
#include <stdio.h>

#define MAX 10

int pilha[MAX];   // Container de dados da pilha
int topo = -1;    // Topo aponta para o índice do último elemento (vazia: topo == -1)

int main() {
    // 1. Exemplo: empilhar alguns valores

    // Empilha 10
    if (topo < MAX - 1) {
        topo++;
        pilha[topo] = 10;
    } else {
        printf("Pilha cheia!\n");
    }

    // Empilha 20
    if (topo < MAX - 1) {
        topo++;
        pilha[topo] = 20;
    } else {
        printf("Pilha cheia!\n");
    }

    // Empilha 30
    if (topo < MAX - 1) {
        topo++;
        pilha[topo] = 30;
    } else {
        printf("Pilha cheia!\n");
    }

    // 2. Ver o topo (sem remover)
    if (topo == -1) {
        printf("Pilha vazia!\n");
    } else {
        printf("Topo: %d\n", pilha[topo]);
    }

    // 3. Desempilha (pop)
    if (topo == -1) {
        printf("Pilha vazia!\n");
    } else {
        int valor = pilha[topo];
        topo--;
        printf("Desempilhado: %d\n", valor);
    }

    // 4. Empilha novamente um valor
    if (topo < MAX - 1) {
        topo++;
        pilha[topo] = 40;
    } else {
        printf("Pilha cheia!\n");
    }

    // 5. Desempilha até ficar vazia (simples)
    while (topo != -1) {
        int valor = pilha[topo];
        topo--;
        printf("Desempilhando %d\n", valor);
    }

    return 0;
}
```

`#define MAX 10` fixa o tamanho do vetor em tempo de compilação, e `int topo = -1` guarda o índice do último elemento inserido: `topo == -1` significa pilha vazia, `topo == 0` significa que existe um elemento em `pilha[0]`, e `topo == MAX - 1` significa pilha cheia.

A lógica de empilhar sempre incrementa `topo` antes de gravar o valor — justamente porque `topo` começa em -1:

```c
if (topo < MAX - 1) {
    topo++;           // 1. Avança o indicador
    pilha[topo] = x;  // 2. Guarda o valor na nova posição
} else {
    printf("Pilha cheia!\n");
}
```

A lógica de desempilhar faz o caminho inverso: lê o valor no topo antes de decrementar o indicador.

```c
if (topo == -1) {
    printf("Pilha vazia!\n");
} else {
    int valor = pilha[topo]; // 1. Salva o valor atual
    topo--;                  // 2. Decrementa o indicador (esquece o elemento)
    printf("Desempilhado: %d\n", valor);
}
```

A tabela a seguir mostra como `topo` e o conteúdo do vetor evoluem ao longo de uma sequência de operações:

| Comando | `topo` | `pilha` (índices 0, 1, 2, 3…) |
| --- | --- | --- |
| `topo = -1` | -1 | `[?, ?, ?, …]` |
| `empilha 10` | 0 | `[10, ?, ?, …]` |
| `empilha 20` | 1 | `[10, 20, ?, …]` |
| `empilha 30` | 2 | `[10, 20, 30, …]` |
| `desempilha` | 1 | `[10, 20, 30, …]` (30 já foi lido) |
| `empilha 40` | 2 | `[10, 20, 40, …]` (sobrescreve a posição 2) |

## 5. Limitações desta Implementação

O código funciona, mas viola os princípios de um TAD robusto de três formas.

Primeiro, **falta reuso**: toda a lógica está dentro do `main`, então usá-la em outro lugar exige copiar e colar o código — não existe um "módulo de pilha" importável.

Segundo, **falta controle sobre `topo`**: nada impede que qualquer parte do programa escreva diretamente

```c
topo = 1000;        // Quebra a lógica
pilha[9999] = 42;   // Acesso indevido à memória
```

já que o `main` (e qualquer outra função) tem acesso direto ao vetor e à variável de controle. Isso quebra o encapsulamento que um TAD deveria garantir.

Terceiro, há **poluição de escopo**: por serem variáveis globais, `pilha` e `topo` podem ser alteradas acidentalmente por qualquer parte do programa, sem qualquer aviso.

Esses três problemas motivam o próximo passo: agrupar `pilha` e `topo` dentro de uma `struct`, e definir funções como `empilha()`, `desempilha()` e `pilhaVazia()` para transformar este código "não-TAD" em um TAD de verdade — reutilizável e com controle sobre seu próprio estado.

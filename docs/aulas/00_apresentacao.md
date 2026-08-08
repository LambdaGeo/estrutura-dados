# Apresentação da Disciplina

**Professor:** Sérgio Souza Costa · **Unidade I:** Memória e Estruturas Lineares

Este capítulo apresenta o programa da disciplina de Estrutura de Dados e faz uma introdução prática à linguagem C, que será usada como ferramenta principal ao longo de todo o livro.

## 1. Visão Geral da Disciplina

A ementa cobre recursividade e Tipos Abstratos de Dados (TAD); estruturas lineares — pilhas, filas e listas encadeadas; estruturas hierárquicas — árvores de busca, árvores balanceadas e heaps; e algoritmos de ordenação e complexidade.

O conteúdo está organizado em três unidades.

**Unidade I — Memória e Estruturas Lineares.** Foco em ponteiros, alocação e na base das estruturas de dados.

1. Apresentação da disciplina.
2. Pilha Estática I: implementação básica com vetores globais.
3. Pilha Estática II: funções, ponteiros e structs.
4. Pilha Estática III: alocação dinâmica.
5. Lista Estática: inserção/remoção em vetor e complexidade (melhor vs. pior caso).
6. Lista Encadeada Dinâmica: nós, ponteiros e encadeamento físico.
7. Fila I: o conceito FIFO em vetor.
8. Fila II: fila circular (resolvendo o problema do deslocamento no vetor).
9. Revisão da Unidade I: consolidação de ponteiros e estruturas lineares.
10. Avaliação I (escrita).

**Unidade II — Busca e a Estrutura Hierárquica.** Foco na evolução da busca binária para a árvore, e no desafio do balanceamento.

1. Recursividade I: fundamentos, pilha de execução e exemplos clássicos.
2. Recursividade II: exemplos clássicos e operações em listas usando recursão.
3. Busca Sequencial e Binária: implementação iterativa e recursiva, e suas limitações.
4. Busca Sequencial e Binária (continuação): exercícios práticos e discussão de complexidade.
5. Árvores: fundamentos, teoria visual, nós e representação em C.
6. Árvores Binárias de Busca (BST) I: inserção, busca e percursos recursivos.
7. Árvores Binárias de Busca (BST) II: o desafio do algoritmo de remoção.
8. Árvores Balanceadas I (conceitual): o problema da degeneração e rotações.
9. Revisão da Unidade II: da recursividade até a lógica de árvores.
10. Avaliação II (escrita).

**Unidade III — Balanceamento, Heaps e Ordenação.** Foco na estabilidade das árvores e nos grandes algoritmos de ordenação.

1. Árvores Balanceadas II (implementação): codificando rotações e fator de balanceamento (AVL).
2. Árvores Balanceadas III: finalização da AVL e testes de performance.
3. Heaps e Fila de Prioridade I: representação em vetor e algoritmos de subida/descida.
4. Heaps e Fila de Prioridade II: implementação da fila de prioridade.
5. Ordenação I: algoritmos de troca — Bubble Sort e Selection Sort ($O(n^2)$).
6. Ordenação II: Insertion Sort e a lógica de inserção ordenada.
7. Ordenação III: Quick Sort (divisão e conquista, e a escolha do pivô).
8. Ordenação IV: Merge Sort (complexidade $O(n \log n)$ e estabilidade).
9. Revisão Final: comparativo de todas as estruturas (tabela de complexidade).
10. Avaliação III / Projeto Prático.

## 2. Por Que C, e Não Python?

É comum questionar o uso de C quando linguagens como Python ou Java são mais concisas. A resposta está no objetivo da disciplina: Python e Java escondem o gerenciamento de memória atrás de um coletor de lixo automático, e uma lista é apenas `list.append()` — uma caixa preta cujo custo real é difícil de enxergar. Em C, o gerenciamento de memória é manual (`malloc`/`free`), a estrutura de uma lista é explícita (vetor ou ponteiros) e o custo de cada operação é visível, porque o acesso à RAM é direto. O foco deixa de ser produtividade de desenvolvimento e passa a ser entendimento de computação.

| Característica | Python / Java | Linguagem C |
| --- | --- | --- |
| **Gerenciamento de Memória** | Automático (Garbage Collector) | Manual (`malloc` / `free`) |
| **Estrutura de Lista** | Oculta (`list.append()`) | Explícita (Vetor vs. Ponteiros) |
| **Custo de Operação** | Difícil de medir (abstrato) | Visível (acesso direto à RAM) |
| **Foco** | Produtividade de Desenvolvimento | Entendimento de Computação |

Em Python, uma lista parece fazer tudo magicamente; em C, o custo real de cada operação fica exposto. Uma lista estática (vetor) ocupa memória contígua, tem acesso rápido — $O(1)$ pelo índice —, mas inserção lenta no meio — $O(n)$, pois é preciso deslocar elementos —, e seu tamanho é fixo, definido na compilação. Já uma lista dinâmica (encadeada) tem memória esparsa, com nós espalhados na heap; o acesso é lento — $O(n)$, pois é preciso percorrer ponteiros —, mas a inserção é rápida — $O(1)$, se já houver o ponteiro do nó anterior —, e o tamanho é flexível, crescendo conforme `malloc` é chamado.

!!! note "Nota Importante"
    Em Estrutura de Dados, não queremos apenas *usar* a estrutura, queremos entender **como ela é construída na memória**. C obriga a lidar com **ponteiros** e **endereços**, revelando o custo real de cada operação.

Essa exposição de custos depende de entender onde os dados vivem. A **stack** (pilha de execução) guarda variáveis locais e o escopo de funções, com gerenciamento automático em regime LIFO. A **heap** (monte) guarda dados alocados dinamicamente com `malloc`, com gerenciamento manual — e, portanto, risco de *memory leak* se o programador esquecer de liberar memória.

## 3. A Linguagem C: um Panorama Rápido

C foi criada entre 1969 e 1973 nos Bell Labs, por Dennis Ritchie e Ken Thompson, com o objetivo original de reescrever o sistema operacional UNIX — até então implementado em Assembly. Seu legado é comparável ao do latim para as línguas modernas: é a base sintática de C++, Java, C#, JavaScript, PHP e mesmo do interpretador de Python (CPython é escrito em C).

C continua no centro da infraestrutura de software atual: está nos kernels de sistemas operacionais (Linux, Windows, macOS, Android, iOS), nas engines de armazenamento de bancos de dados (PostgreSQL, MySQL, SQLite), em compiladores e interpretadores (GCC, LLVM, o próprio interpretador Python) e em sistemas embarcados — microcontroladores, IoT, dispositivos médicos — onde não há espaço para o *overhead* de linguagens mais abstratas.

Diferente de linguagens interpretadas, um programa em C passa por etapas explícitas antes de rodar: o pré-processamento processa diretivas como `#include` e `#define`; a compilação traduz o código para código de máquina; a montagem (*assembler*) gera arquivos objeto; e a linkagem junta bibliotecas e produz o executável final.

O primeiro programa de qualquer curso de C é o clássico "Hello World":

```c
#include <stdio.h>  // 1. Biblioteca Padrão de I/O

int main() {        // 2. Função principal (ponto de entrada)

    // 3. Saída de dados para o console
    printf("Ola, Estrutura de Dados!\n");

    return 0;       // 4. Retorna 0 indicando sucesso ao SO
}
```

Cada linha carrega uma decisão de design da linguagem: `#include <stdio.h>` importa as funções de entrada/saída (`printf`, `scanf`) — sem isso o compilador não reconhece `printf`; todo programa C precisa de uma função `main()`; `printf()` é a função de impressão formatada; `\n` é o caractere de escape para nova linha; o ponto e vírgula é obrigatório ao final de cada instrução; e `return 0` é a convenção que indica que o programa terminou sem erros.

Para compilar e executar:

```bash
# Compilar
gcc hello.c -o hello

# Executar (Linux/Mac)
./hello

# Executar (Windows)
hello.exe
```

## Síntese

C foi escolhida como ferramenta de ensino justamente por expor o gerenciamento de memória — ponteiros, stack, heap — que linguagens modernas escondem. Estrutura de Dados é, no fundo, uma disciplina sobre memória: entender como os dados são organizados na RAM importa mais do que decorar sintaxe. E C é a base de boa parte da infraestrutura de software do mundo: sistemas operacionais, bancos de dados, compiladores.

Para praticar antes do próximo capítulo: garanta que o compilador (GCC) e um editor (VS Code, Code::Blocks, etc.) estejam instalados e funcionando; modifique o `hello.c` para imprimir seu nome completo e seu número de matrícula, em duas linhas diferentes; e revise conceitos básicos de variáveis, tipos, expressões, condicionais, laços, funções, vetores, strings e ponteiros em C. Se precisar rever esses fundamentos com calma, o livro **[C para Programadores Python e VisuAlg](https://lambdageo.github.io/introducao-c/)** cobre exatamente isso, com exercícios por capítulo. O próximo capítulo parte daí para a implementação básica de uma pilha com vetores globais, introduzindo na prática a diferença entre stack e heap.

!!! question "Dúvida Comum"
    *"Preciso ser expert em C para passar?"*

    **Resposta:** Não. É preciso entender a lógica de memória. A sintaxe de C é pequena; o desafio é a lógica de ponteiros — e isso se constrói com prática ao longo do livro.

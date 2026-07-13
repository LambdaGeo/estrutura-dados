# Apresentação da disciplina

**👨‍🏫 Professor:** Sérgio Souza Costa

**🏫 Unidade:**I — Memória e Estruturas Lineares

**📍 Tópico:** Apresentação, Programa da Disciplina e Introdução ao C.

## **📋 1. Visão Geral da Disciplina**

### **🎯 Ementa Resumida**

- Recursividade e Tipos Abstratos de Dados (TAD).
- Estruturas Lineares: Pilhas, Filas, Listas Encadeadas.
- Estruturas Hierárquicas: Árvores (Busca, Balanceadas, Heaps).
- Algoritmos de Ordenação e Complexidade.

### **🗓️ Cronograma**

### **Unidade I: Memória e Estruturas Lineares**

*Foco: Ponteiros, Alocação e a base das estruturas de dados.*

1. **Apresentação da disciplina**.
2. **Pilha Estática I:** Implementação básica com vetores globais
3. **Pilha Estática II:** Funções, Ponteiros e Structs 
4. **Pilha Estática III:** Alocação dinâmica
5. **Lista Estática:** Inserção/Remoção em vetor e **Complexidade** (Melhor vs Pior caso).
6. **Lista Encadeada Dinâmica:** Nós, ponteiros e encadeamento físico.
7. **Fila I:** O conceito FIFO em vetor.
8. **Fila II:** Fila Circular (resolvendo o problema do deslocamento no vetor).
9. **Revisão Unidade I:** Consolidação de ponteiros e estruturas lineares.
10. **Avaliação I (Escrita).**

---

### **Unidade II: Busca e a Estrutura Hierárquica**

*Foco: A evolução da busca binária para a árvore e o desafio do balanceamento.*

1. **Recursividade I:** Fundamentos, Pilha de Execução e exemplos clássicos.
2. **Recursividade II:** Exemplos clássicos e operações em listas usando recursão.
3. **Busca Sequencial e Binária:** Implementação iterativa e recursiva. Limitações
4. **Busca Sequencial e Binária:** Implementação iterativa e recursiva. Limitações
5. **Árvores: Fundamentos:** Teoria visual, nós e representação em C.
6. **Árvores Binárias de Busca (BST) I:** Inserção, busca e percursos recursivos.
7. **Árvores Binárias de Busca (BST) II:** O desafio do algoritmo de **Remoção**.
8. **Árvores Balanceadas I (Conceitual):** O problema da degeneração e a aula visual de rotações.
9. **Revisão Unidade II:** De Recursividade até a lógica de Árvores.
10. **Avaliação II (Escrita).**

---

### **Unidade III: Balanceamento, Heaps e Ordenação**

*Foco: Estabilidade das árvores e os grandes algoritmos de ordenação.*

1. **Árvores Balanceadas II (Implementação):** Codificando rotações e fator de balanceamento (AVL).
2. **Árvores Balanceadas III:** Finalização da AVL e testes de performance.
3. **Heaps e Fila de Prioridade I:** Representação em vetor e algoritmos de subida/descida.
4. **Heaps e Fila de Prioridade II:** Implementação da Fila de Prioridade.
5. **Ordenação I:** Algoritmos de troca: Bubble Sort e Selection Sort (*O*(*n*2)).
    
    O(n2)
    
6. **Ordenação II:** Insertion Sort e a lógica de inserção ordenada.
7. **Ordenação III:** Quick Sort (Divisão e Conquista e a escolha do pivô).
8. **Ordenação IV:** Merge Sort (Complexidade *O*(*n*log*n*) e estabilidade).
    
    O(nlog⁡n)
    
9. **Revisão Final:** Comparativo de todas as estruturas (Tabela de Complexidade).
10. **Avaliação III / Projeto Prático?.**

---

## 📚 Anotações do Encontro 01

### 🕒 Parte 1: Por que C e não Python? (50 min)

### 🤔 O Dilema da Abstração

Muitos alunos questionam o uso de **C** quando linguagens como **Python** ou **Java** são mais concisas. A resposta está no **objetivo da disciplina**:

| Característica | Python / Java | Linguagem C |
| --- | --- | --- |
| **Gerenciamento de Memória** | Automático (Garbage Collector) | **Manual** (`malloc` / `free`) |
| **Estrutura de Lista** | Oculta (`list.append()`) | **Explícita** (Vetor vs. Ponteiros) |
| **Custo de Operação** | Difícil de medir (abstrato) | **Visível** (acesso direto à RAM) |
| **Foco** | Produtividade de Desenvolvimento | **Entendimento de Computação** |

### 💡 O Exemplo Crítico: Listas Estáticas vs. Dinâmicas

Em Python, uma lista parece fazer tudo magicamente. Em C, entendemos o custo real:

1. **Lista Estática (Vetor/Array):**
    - **Memória:** Contígua (blocos lado a lado).
    - **Acesso:** Rápido $O(1)$ pelo índice.
    - **Inserção:** Lenta $O(n)$ no meio (precisa deslocar elementos).
    - **Tamanho:** Fixo (definido na compilação).
2. **Lista Dinâmica (Encadeada/Linked List):**
    - **Memória:** Esparsa (nós espalhados na Heap).
    - **Acesso:** Lento $O(n)$ (precisa percorrer ponteiros).
    - **Inserção:** Rápida $O(1)$ (se tiver o ponteiro do nó anterior).
    - **Tamanho:** Flexível (cresce conforme `malloc`).

> **💡 Nota Importante:** Em Estrutura de Dados, não queremos apenas *usar* a estrutura, queremos entender **como ela é construída na memória**. C nos obriga a lidar com **ponteiros** e **endereços**, revelando o custo real de cada operação.
> 

### 🧠 Conceito Chave: Stack vs. Heap

- **Stack (Pilha):** Onde vivem variáveis locais e escopo de funções. Gerenciamento automático (LIFO).
- **Heap (Monte):** Onde vivem dados dinâmicos (alocados com `malloc`). Gerenciamento manual (risco de *memory leak*).

---

### 🕒 Parte 2: A Linguagem C e Hello World (50 min)

### 📜 Histórico e Importância

- **Criação:** 1969-1973, Bell Labs.
- **Autores:** Dennis Ritchie e Ken Thompson.
- **Objetivo Original:** Reescrever o sistema operacional **UNIX** (antes feito em Assembly).
- **Legado:** Considerada o "Latin" da programação. Sintaxe base para C++, Java, C#, JavaScript, PHP, Python (o interpretador CPython é escrito em C).

### 🏗️ Onde o C é usado hoje?

1. **Sistemas Operacionais:** Kernels (Linux, Windows, macOS, Android, iOS).
2. **Banco de Dados:** Engines de armazenamento (PostgreSQL, MySQL, SQLite).
3. **Compiladores/Interpretadores:** GCC, LLVM, Python Interpreter.
4. **Sistemas Embarcados:** Microcontroladores, IoT, dispositivos médicos (onde não há espaço para *overhead*).

### ⚙️ O Ciclo de Compilação

Diferente de linguagens interpretadas, o C passa por etapas explícitas antes de rodar:

1. **Pré-processamento:** Processa diretivas `#include` e `#define`.
2. **Compilação:** Traduz para código de máquina.
3. **Montagem (Assembler):** Gera arquivos objeto.
4. **Linkagem:** Junta bibliotecas e cria o executável final.

### 💻 Prática: Hello World

```c
#include <stdio.h>  // 1. Biblioteca Padrão de I/O

int main() {        // 2. Função principal (ponto de entrada)

    // 3. Saída de dados para o console
    printf("Ola, Estrutura de Dados!\\n");

    return 0;       // 4. Retorna 0 indicando sucesso ao SO
}
```

### 🔍 Dissecando o Código

- `#include <stdio.h>`: Importa funções de entrada/saída (`printf`, `scanf`). Sem isso, o compilador não reconhece o `printf`.
- `int main()`: Todo programa C deve ter um `main`.
- `printf()`: Função de impressão formatada.
- `\\n`: Caractere de escape para **nova linha** (newline).
- `;`: Ponto e vírgula obrigatório ao fim de cada instrução.
- `return 0`: Boa prática. Indica que o programa terminou sem erros.

### 🚀 Compilando no Terminal

```bash
# Compilar
gcc hello.c -o hello

# Executar (Linux/Mac)
./hello

# Executar (Windows)
hello.exe
```

---

## 📝 Resumo e Próximos Passos

### ✅ Takeaways da Aula

1. **C é uma ferramenta de ensino:** Escolhida para expor o gerenciamento de memória (ponteiros, stack, heap) que linguagens modernas ocultam.
2. **Estrutura de Dados é sobre Memória:** Entender como os dados são organizados na RAM é mais importante que a sintaxe.
3. **Ecossistema C:** É a base da infraestrutura de software mundial (OS, DB, Compiladores).
4. **Ciclo de Build:** Entender a diferença entre escrever o código (`.c`) e gerar o executável (`.exe`).

### 🏠 Tarefa de Casa

1. **Instalação:** Garantir que o compilador (GCC) e editor (VS Code, CodeBlocks, etc.) estejam instalados e funcionais.
2. **Prática:** Modificar o `hello.c` para:
    - Imprimir seu nome completo.
    - Imprimir seu número de matrícula.
    - Usar duas linhas diferentes (dois `printf` ou um com `\\n`).
3. **Leitura:** Revisar conceitos básicos de variáveis e tipos em C (`int`, `float`, `char`).

### 🔜 Próxima Aula

- **Tópico:** Pilha Estática e Memória.
- **Foco:** Implementação básica de pilha com vetores globais e introdução prática a **Stack vs Heap**.

---

> **⚠️ Dúvida Comum:** *"Preciso ser expert em C para passar?"*
> 
> 
> **Resposta:** Não. Precisa entender a lógica de memória. A sintaxe de C é pequena; o desafio é a lógica de ponteiros. Vamos praticar juntos.
>
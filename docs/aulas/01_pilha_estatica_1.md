# Pilha Estática I: Implementação básica com vetores globais

---

**Disciplina:** Estrutura de Dados / Algoritmos

**Público:** Iniciantes em C / Estrutura de Dados

**Objetivo Geral:** Compreender o conceito de Tipo Abstrato de Dados (TAD), entender a lógica LIFO da Pilha e vivenciar as limitações de uma implementação sem encapsulamento.

---

## 🕒 Aula 1 (50 min) – TAD, Pilha, Política de Acesso e Aplicações

### 1.1 Conceito de Tipo Abstrato de Dados (TAD)

**Tempo estimado:** 15 min

- **Definição Formal:**
    
    > "Um Tipo Abstrato de Dados (TAD) é uma forma de organizar uma coleção de dados junto com um conjunto de operações bem definidas, escondendo como essa coleção é realmente armazenada na memória."
    > 
- **Definição Simplificada (Para a turma):**
    
    > "Um TAD é como um 'container' de dados: ele define que tipo de dados você pode colocar dentro e quais operações faz sentido fazer com esse container, sem que o usuário precise saber os detalhes de implementação."
    > 
- **Ideias‑Chave:**
    1. **Abstração:** O usuário conhece a interface ("o que ela faz"), não o "como".
    2. **Encapsulamento:** O estado interno (ex.: o vetor, topo) fica "protegido"; o usuário só acessa por operações adequadas.
    3. **Reusabilidade:** O mesmo TAD pode ser usado em vários contextos.
- **Exemplos Informais:**
    - Pilha, Fila, Lista, Árvore. Todos são TADs, cada um com uma lógica específica de organização e acesso.

### 1.2 Pilha como TAD Simples

**Tempo estimado:** 20 min

### 1.2.1 Ideia Intuitiva

- **Desenho no Quadro:** Representar visualmente uma pilha de objetos.
    - Pilha de pratos.
    - Pilha de livros.
    - Pilha de caixas.
- **Conceito:** Elementos são colocados uns sobre os outros. Só o de cima está realmente "acessível" de forma direta.
- **Frase de Efeito:**
    
    > "Na pilha, o primeiro que entra pode ficar sepultado; o último que entra é o primeiro a sair."
    > 

### 1.2.2 Política de Acesso: LIFO

- **Sigla:** **LIFO** = *Last In, First Out* (Último a Entrar, Primeiro a Sair).
- **Regras:**
    1. **Inserção:** Sempre no topo da pilha.
    2. **Remoção:** Só o topo da pilha pode ser removido.
    3. **Acesso:** O usuário só vê o topo.
- **Operações Conceituais:**
    - `Push` (Empilhar): Coloca um elemento no topo.
    - `Pop` (Desempilhar): Remove o elemento do topo.
    - `Peek/Top` (Ver topo): Examina o topo sem remover.

### 1.2.3 Analogias com o Mundo Real

- **Pilha de Pratos:** Tudo novo é colocado em cima. Ao tirar, sempre se tira o de cima.
- **Navegador Web:** Cada página visitada é "empilhada". Ao clicar em "Voltar", desempilha a última página.
- **Editor de Texto:** Cada ação é empilhada. `Ctrl+Z` desempilha a ação mais recente.

### 1.3 Aplicações de Pilha em Programação

**Tempo estimado:** 15 min

- **Call Stack (Pilha de Chamadas):** Gerenciamento de funções e variáveis locais.
- **Avaliação de Expressões:** Notação pós-fixa (polonesa reversa) e infixa.
- **Algoritmos de Exploração:** DFS (Depth-First Search) e Backtracking.
- **Históricos:** Funcionalidades de "Voltar" em sistemas.
- **Mensagem Final aos Alunos:**
    
    > "Isso não é só teoria de aula; é algo que existe nos sistemas e nos programas que você já usa."
    > 

---

## 🕒 Aula 2 (50 min) – Implementação Estática Simples em C

### 2.1 Objetivo Desta Parte

**Tempo estimado:** 5 min

- Mostrar uma pilha muito "nua" em C usando apenas variáveis globais.
- **Restrições Intencionais:** Sem funções, sem ponteiros, sem `struct`.
- **Código Base:**
    
    ```c
    int pilha[MAX];
    int topo = -1;
    ```
    
- **Foco da Discussão:** Falta de reuso e falta de controle sobre o valor de `topo`.

### 2.2 Código no Quadro (Exemplo Completo)

**Tempo estimado:** 20 min (Digitação e Explicação)

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

### 2.3 Explicação Passo a Passo

**Tempo estimado:** 15 min

### 2.3.1 Estrutura Básica

- `#define MAX 10`: Vetor estático (fixo no tempo de compilação).
- `int pilha[MAX]`: Armazena os 10 inteiros.
- `int topo = -1`: Guarda o índice do último elemento inserido.
    - `topo == -1` ⇒ Pilha vazia.
    - `topo == 0` ⇒ Existe um elemento em `pilha[0]`.
    - `topo == MAX - 1` ⇒ Pilha cheia.

### 2.3.2 Lógica de Empilhar (Push)

```c
if (topo < MAX - 1) {
    topo++;           // 1. Avança o indicador
    pilha[topo] = x;  // 2. Guarda o valor na nova posição
} else {
    printf("Pilha cheia!\n");
}
```

- **Atenção:** Primeiro incrementa, depois atribui (porque `topo` começa em -1).

### 2.3.3 Lógica de Desempilhar (Pop)

```c
if (topo == -1) {
    printf("Pilha vazia!\n");
} else {
    int valor = pilha[topo]; // 1. Salva o valor atual
    topo--;                  // 2. Decrementa o indicador (esquece o elemento)
    printf("Desempilhado: %d\n", valor);
}
```

### 2.4 Exibição do Estado da Pilha (Tabela de Memória)

**Tempo estimado:** 5 min

- Desenhar no quadro para simular a execução:

| Comando | `topo` | `pilha` (índices 0, 1, 2, 3…) |
| --- | --- | --- |
| `topo = -1` | -1 | `[?, ?, ?, …]` |
| `empilha 10` | 0 | `[10, ?, ?, …]` |
| `empilha 20` | 1 | `[10, 20, ?, …]` |
| `empilha 30` | 2 | `[10, 20, 30, …]` |
| `desempilha` | 1 | `[10, 20, 30, …]` (30 acessado antes) |
| `empilha 40` | 2 | `[10, 20, 40, …]` (sobrescreve posição 2) |
- **Dica Visual:** Usar cores ou setas para mostrar que o índice `topo` "anda" para frente e para trás.

### 2.5 Problemas Dessa Versão (Discussão Crítica)

**Tempo estimado:** 5 min

- **Mensagem:** "O código funciona, mas viola os princípios de um TAD robusto."
1. **Falta de Reuso:**
    - O código está todo dentro do `main`.
    - Para usar em outro lugar, precisa copiar e colar a lógica.
    - Não existe um "módulo de pilha" importável.
2. **Falta de Controle sobre `topo`:**
    - Nada impede que alguém escreva no `main`:
        
        ```c
        topo = 1000;        // Quebra a lógica
        pilha[9999] = 42;   // Acesso indevido à memória
        ```
        
    - O `main` tem acesso direto ao vetor e à variável de controle. Isso quebra o **encapsulamento**.
3. **Poluição de Escopo:**
    - Variáveis globais (`pilha`, `topo`) podem ser alteradas acidentalmente por qualquer parte do código.

### 2.6 Resumo e Próximos Passos

**Tempo estimado:** 5 min

| Parte | Conceito Principal | Exemplo de Código Mostrado |
| --- | --- | --- |
| **Aula 1** | TAD como container; Pilha (LIFO) | Nada de código — só ideias/Analogias |
| **Aula 2** | Pilha estática em C: `int pilha[MAX]; int topo;` | `pilha[topo] = x; topo++;` e variantes |
| **Discussão** | Falta de reuso e controle; não é um TAD bem feito | Código comentado no quadro |
- **Gancho para a Próxima Aula:**
    - Como resolver esses problemas?
    - Introduzir `struct` para agrupar `pilha` e `topo`.
    - Definir funções `empilha()`, `desempilha()`, `pilhaVazia()`.
    - Transformar esse código "não‑TAD" em um TAD verdadeiro, reutilizável e com controle.

---
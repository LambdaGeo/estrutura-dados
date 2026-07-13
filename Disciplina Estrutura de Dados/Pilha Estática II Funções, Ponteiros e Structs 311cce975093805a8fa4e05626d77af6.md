# Pilha Estática II: Funções, Ponteiros e Structs

**Disciplina:** Estrutura de Dados / Algoritmos

**Unidade:** I — Memória e Estruturas Lineares

**Tema Central:** Evolução da implementação de Pilha em C (Funções, Structs e Ponteiros).

**Duração Sugerida:** 2 aulas × 50 minutos (Continuação da Aula de Teoria e Pilha "Nua").

**Pré-requisitos:**

- Conceito de Pilha (LIFO).
- Implementação "nua" com variáveis globais (visto na aula anterior).
- Sintaxe básica de C (variáveis, loops, condicionais).

---

## 🎯 Objetivos de Aprendizagem

1. Compreender o comportamento de **funções em C** (passagem por valor vs. referência).
2. Utilizar **`struct`** para agrupar dados e criar um tipo composto (`Pilha`).
3. Entender a necessidade de **ponteiros** para modificar estruturas dentro de funções.
4. Refatorar o código para respeitar o conceito de **TAD** (encapsulamento lógico).
5. Refletir sobre as limitações da alocação estática e preparar o terreno para alocação dinâmica.

---

## 🕒 Parte 1 – Introdução às Funções em C (50 min)

### 1.1 O Que é uma Função em C?

**Definição Didática:**

> Uma função em C é um **bloco de código** que recebe zero ou mais parâmetros, executa uma tarefa bem definida e pode retornar um único valor.
> 

**Frases para o Quadro:**

- "Função = subrotina ou procedimento especializado."
- "Divide um programa grande em pedaços menores e reutilizáveis."

### 1.2 Sintaxe Básica

```c
tipo_retorno nome_da_funcao(tipo1 param1, tipo2 param2, ...) {
    // comandos
    return valor; // Opcional se void
}
```

**Destaque:**

- `tipo_retorno`: `int`, `float`, `char`, `void`, etc.
- `nome_da_funcao`: Deve ser descritivo (ex: `empilha`, `calculaMedia`).
- `return`: Só aparece se o tipo de retorno não for `void`.

### 1.3 Exemplo Simples: Função que Calcula o Dobro

```c
#include <stdio.h>

int dobro(int x) {
    return 2 * x;
}

int main() {
    int n = 5;
    int resultado = dobro(n);
    printf("O dobro de %d é %d\\n", n, resultado);
    return 0;
}
```

**Pontos Didáticos:**

- Tipo `int` e retorno `int`.
- `n` é **copiado** para o parâmetro `x`.
- `x` é uma **variável local** da função; alterar `x` não altera `n`.

### 1.4 O Que é `void`?

- `void` indica que **não há valor de retorno**.
- Funções que só fazem algo (imprimir, inicializar, modificar estado) podem ser `void`.

```c
void imprimirMensagem() {
    printf("Olá de uma função void!\\n");
}
```

### 1.5 Passagem por Valor (Passagem por Cópia)

**Ideia-Chave:**

> Em C, os parâmetros de função são **passados por valor (por cópia)**.
> 

**Exemplo do Erro Comum:**

```c
void trocaErrada(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
    // a e b são cópias; os originais não mudam
}

int main() {
    int x = 10, y = 20;
    trocaErrada(x, y);
    printf("x=%d y=%d\\n", x, y); // Saída: x=10 y=20
    return 0;
}
```

**Conclusão para a Turma:**

> Se a função precisa **modificar** o valor de uma variável original, **copiar o valor não basta**. Precisamos passar a **referência** (endereço) da variável.
> 

---

## 🕒 Parte 2 – Revisita à Pilha e ao TAD (50 min)

### 2.1 Relembrando o TAD "Pilha"

Voltar ao conceito apresentado na Aula 1:

> *Um TAD é uma coleção de dados + um conjunto de operações bem definidas, escondendo a implementação.*
> 

**Pergunta para a Turma:**

> "Quais são as operações típicas que fazemos com uma pilha?"
> 

**Respostas Esperadas:**

- **Empilhar (`push`)**
- **Desempilhar (`pop`)**
- **Ver o topo (`top`/`peek`)**
- **Testar se está vazia (`isEmpty`)**
- **Testar se está cheia (`isFull`)**

### 2.2 Representando Essas Operações em C

**Pergunta:**

> "Como podemos representar essas operações em C? O que nos dá a linguagem?"
> 

**Resposta Guiada:**

- C não tem um tipo `Pilha` nativo.
- Temos tipos primitivos (`int`, `float`) e podemos construir tipos compostos com `struct`.
- Operações podem ser representadas por **funções**.
- **Nosso TAD de Pilha será:**
    - `struct pilha` → o tipo concreto (dados).
    - Funções → `empilha()`, `desempilha()`, `pilhaVazia()`, etc. (comportamento).

---

## 🕒 Parte 3 – Criando o Tipo "Pilha" com `struct`

### 3.1 Definição de Struct para Pilha

**Código no Quadro:**

```c
#define MAX 100

// Definição do tipo Pilha
typedef struct pilha {
    int valores[MAX];
    int topo;
} Pilha;
```

**Explicação:**

- `int valores[MAX]`: Armazena os elementos da pilha (vetor estático).
- `int topo`: Índice do topo da pilha.
- `typedef struct pilha { ... } Pilha;`: Cria um novo **tipo** `Pilha` que pode ser usado como `Pilha p1;`.

> **Observação:** Agora, `Pilha` é um tipo próprio, como `int` ou `float`, só que composto por um vetor e um `int`.
> 

### 3.2 Exemplo de Uso de `struct` Sem Funções

Mostrar o uso direto de membros da `struct` no `main` (transição da aula anterior):

```c
#include <stdio.h>

#define MAX 100

typedef struct pilha {
    int valores[MAX];
    int topo;
} Pilha;

int main() {
    Pilha p;
    p.topo = -1; // Inicializa a pilha vazia

    // Empilha 10 (Acesso direto)
    if (p.topo < MAX - 1) {
        p.topo++;
        p.valores[p.topo] = 10;
    }

    // Desempilha (Acesso direto)
    if (p.topo != -1) {
        int valor = p.valores[p.topo];
        printf("Desempilhado: %d\\n", valor);
        p.topo--;
    }

    return 0;
}
```

**Pontos Didáticos:**

- Uso de `p.valores` e `p.topo` para acessar campos (operador `.`).
- Mesmo código da pilha "nua", mas organizado em um tipo `Pilha`.
- **Problema:** O `main` ainda mexe diretamente no estado interno (`p.valores`, `p.topo`), violando o encapsulamento do TAD.

---

## 🕒 Parte 4 – Introduzindo Funções para a Pilha

### 4.1 Tentativa Sem Ponteiros (Passagem por Valor)

**Objetivo:** Mostrar o erro conceitual antes de corrigir.

```c
void empilha(int x, Pilha p) { // Recebe uma CÓPIA da struct
    if (p.topo < MAX - 1) {
        p.topo++;
        p.valores[p.topo] = x;
    } else {
        printf("Pilha cheia!\\n");
    }
}

int main() {
    Pilha p;
    p.topo = -1;

    empilha(10, p); // Passando a struct por valor

    // Mesmo após empilha, p não foi alterado
    if (p.topo != -1) {
        printf("Valor no topo: %d\\n", p.valores[p.topo]);
        // ⚠️ IMPRIME ERRO ou PILHA VAZIA, pois topo continua -1
    } else {
        printf("Pilha vazia!\\n");
    }

    return 0;
}
```

**O Que Acontece e Por Que Discutir:**

- `Pilha p` é passado **por valor** → `empilha` recebe uma cópia de `p`.
- A modificação de `p.topo` e `p.valores` ocorre na **cópia**, não no `p` original.
- Ao voltar para `main`, `p.topo` ainda é `1` e o elemento não aparece.

### 4.2 Introdução ao Conceito de Ponteiros

**Pergunta para a Turma:**

> "O que seria necessário para que a função `empilha` consiga realmente alterar a pilha passada? O que é o `p` que o `main` quer ver?"
> 

**Resposta Guiada:**

- Precisamos que a função receba não uma **cópia** da pilha, mas uma **referência** para a pilha.
- Em C, referência é feita com **ponteiros**.

### 4.3 Operadores Básicos de Ponteiros em C

**Mostrar no Quadro:**

```c
int x = 10;
int *ptr = &x;   // ptr guarda o endereço de x

// & → operador de endereço ("endereçar")
// * → operador de acesso ao valor apontado ("desreferenciar")
```

**Frase de Memória:**

> `&` → "Me dê o endereço"
> 
> - → "Me dê o valor que está nesse endereço"

### 4.4 Modificação da Função `empilha` para Usar Ponteiro

**Código Corrigido:**

```c
void empilha(int x, Pilha *p) { // Recebe o ENDEREÇO da pilha
    if (p->topo < MAX - 1) {    // Usa operador seta (->)
        p->topo++;
        p->valores[p->topo] = x;
    } else {
        printf("Pilha cheia!\\n");
    }
}
```

**Explicação de `p->topo`:**

- `p` é um ponteiro para `Pilha`.
- `p->topo` é equivalente a `(*p).topo` → primeiro desreferencia `p` e depois acessa o membro.
- Agora a função modifica o `Pilha` original, não uma cópia.

### 4.5 Código Completo com TAD de Pilha Simples

**Estado Desejado da Aula:**

```c
#include <stdio.h>

#define MAX 100

typedef struct pilha {
    int valores[MAX];
    int topo;
} Pilha;

// Interface do TAD
void inicializaPilha(Pilha *p);
int pilhaVazia(Pilha *p);
int pilhaCheia(Pilha *p);
void empilha(int x, Pilha *p);
int desempilha(Pilha *p);
int topoPilha(Pilha *p);

// Implementação
void inicializaPilha(Pilha *p) {
    p->topo = -1;
}

int pilhaVazia(Pilha *p) {
    return p->topo == -1;
}

int pilhaCheia(Pilha *p) {
    return p->topo == MAX - 1;
}

void empilha(int x, Pilha *p) {
    if (pilhaCheia(p)) {
        printf("Pilha cheia!\\n");
        return;
    }
    p->topo++;
    p->valores[p->topo] = x;
}

int desempilha(Pilha *p) {
    if (pilhaVazia(p)) {
        printf("Pilha vazia!\\n");
        return -1; // Valor de erro
    }
    int valor = p->valores[p->topo];
    p->topo--;
    return valor;
}

int topoPilha(Pilha *p) {
    if (pilhaVazia(p)) {
        printf("Pilha vazia!\\n");
        return -1;
    }
    return p->valores[p->topo];
}

// Uso do TAD
int main() {
    Pilha p;
    inicializaPilha(&p); // Passa o endereço

    empilha(10, &p);
    empilha(20, &p);
    empilha(30, &p);

    printf("Topo: %d\\n", topoPilha(&p));
    printf("Desempilhado: %d\\n", desempilha(&p));

    empilha(40, &p);

    while (!pilhaVazia(&p)) {
        printf("Desempilhando: %d\\n", desempilha(&p));
    }

    return 0;
}
```

**Pontos Didáticos:**

- O `main` usa apenas as funções de interface.
- O estado interno (`valores`, `topo`) é acessado só por meio de ponteiro dentro das funções.
- Aproxima-se de um TAD "limpo": quem usa só vê o tipo `Pilha` e as funções.

---

## 🕒 Parte 5 – Reflexão Final e Próximos Passos

### 5.1 Pergunta para a Turma

> "Se já temos ponteiros, e o `main` pode criar ponteiros para `Pilha`, por que continuamos usando um vetor estático `int valores[MAX]` dentro da estrutura? O que acontece se quisermos várias pilhas de tamanhos diferentes?"
> 

**Resposta Esperada (Guiada):**

- O vetor `valores[MAX]` é de tamanho **fixo em tempo de compilação**.
- Não conseguimos criar uma pilha de tamanho arbitrário (20, 30, 1000) com esse modelo atual.
- Se quisermos flexibilidade, o `valores` precisa ser **alocado dinamicamente**.

### 5.2 Caminho para a Próxima Aula

- Mostrar que, na próxima etapa, podemos:
    1. Substituir `int valores[MAX];` por `int *valores;` em `struct pilha`.
    2. Alocar `p->valores` com `malloc` de acordo com o tamanho desejado.
    3. Criar funções `criaPilha(int capacidade)` e `liberaPilha(Pilha *p)`.

> **Transição Didática:** "Hoje trabalhamos com funções, `struct`, ponteiros e passagem por referência. Na próxima aula, vamos usar **alocação dinâmica** para tornar a pilha verdadeiramente flexível e reutilizável para vários tamanhos."
> 

---

## 📝 Resumo da Aula (Para o Notion)

| Etapa | Conceito Central | Código-Exemplo Central |
| --- | --- | --- |
| **Introdução às Funções** | Funções, `void`, passagem por valor | `int dobro(int x)` e `trocaErrada()` |
| **TAD e Pilha** | Revisão de TAD e operações de pilha | Lista de operações (`empilha`, `desempilha`...) |
| **`struct` Pilha** | Criando um tipo composto para pilha | `typedef struct pilha { int valores[MAX]; int topo; }` |
| **Uso sem Funções** | Acessando membros diretamente com `.` | `p.valores[p.topo] = 10` |
| **Funções sem Ponteiros** | Passagem por valor → Modificação não persiste | `empilha(x, p)` com `Pilha` por valor |
| **Ponteiros e `->`** | `&` e `*`, passagem por referência | `empilha(x, &p)` e `p->topo` |
| **TAD de Pilha** | Interface clara, estado interno protegido | `empilha`, `desempilha`, `pilhaCheia`... |
| **Reflexão Final** | Limite do vetor estático; necessidade de `malloc` | `int *valores` e `criaPilha(int capacidade)` (Next Step) |
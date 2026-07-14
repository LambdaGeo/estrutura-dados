# Pilha Estática III: Alocação dinâmica

**Disciplina:** Estrutura de Dados

**Unidade:** I — Memória e Estruturas Lineares

**Tema Central:**

- Usar a pilha **sempre como ponteiro** (`Pilha *p`).
- Analogia com Java/Python: variáveis como ponteiros para objetos alocados no `heap`.
- Conceito de **alocação dinâmica**: `stack` vs `heap`.
- `malloc`, `calloc` e `free` com exemplos práticos.
- Relação entre **vetores e ponteiros**: `v[i]` é igual a `(v + i)`.
- Implementação de `Pilha` com:
    - `struct` alocada dinamicamente;
    - primeiro vetor estático, depois vetor **dinâmico**, definido por parâmetro `size`.

**Duração:** 2 aulas × 50 minutos

**Objetivo Didático:**

- Mostrar que, em C, podemos modelar o TAD de pilha **como se fosse um objeto referenciado por um ponteiro**, como em Java/Python.
- Introduzir alocação dinâmica, relação vetor/ponteiro e evoluir para uma pilha completamente dinâmica, com tamanho configurável.

---

## Parte 1 – Pilha como Ponteiro: Analogia com Java e Python

### 1.1 Pergunta Inicial para a Turma

> "Se já estamos acostumados a usar `Pilha *p`, será que podemos lidar com **pilhas sempre como ponteiros**? Ou seja, sempre trabalhar com endereços de pilhas e nunca com cópias de `Pilha` no `main`?"

**Resposta Guiada:**

- Em C, `Pilha *p` é um **ponteiro para a estrutura**, não a estrutura em si.
- Isso é semelhante ao que acontece em linguagens como **Java** e **Python**:
    - Quando fazemos `new Stack()` ou `pilha = Pilha()`, na verdade estamos:
        - Criando o objeto no **heap**;
        - E a variável é apenas um **ponteiro/referência** para esse objeto.
- Então, trabalhar com `Pilha *p` é como "tratar a pilha como referência", mesmo que a linguagem seja C.

**Frase Didática para o Quadro:**

> Em C, `Pilha *p` é o equivalente conceitual ao "objeto no heap, acessado por referência" em Java/Python.

---

## Parte 2 – Pergunta Sobre o Tamanho do Vetor

### 2.1 Outra Pergunta para a Turma

> "E o tamanho do vetor interno da pilha? Até agora, `MAX` é fixo em tempo de compilação. Será que podemos definir o tamanho do vetor **dinamicamente**?"

**Objetivo da Pergunta:**

- Levar o aluno a perceber que:
    - Uma pilha é um **container**;
    - Faz sentido que ela possa ter **diferentes tamanhos** em diferentes situações.

---

## Parte 3 – Alocação Dinâmica: `Stack` vs `Heap`

### 3.1 Visão Geral da Memória

Escrever no quadro uma visão simplificada:

| Área | Descrição | Gerenciamento |
| --- | --- | --- |
| **`stack`** (pilha de execução) | Espaço automático para variáveis locais | Cria e destrói automaticamente |
| **`heap`** (área dinâmica) | Espaço para alocação explícita | Programador aloca e libera manualmente |

**Características:**

- **`stack`:**
    - Usado para variáveis locais de funções.
    - Cria e destrói espaço automaticamente com chamadas/retornos.
    - Tamanho limitado.
- **`heap`:**
    - Usado para alocação **explícita** via `malloc`, `calloc`, `realloc`.
    - O programador aloca e **libera** com `free`.
    - Tamanho limitado apenas pela memória do sistema.

**Frase de Memória:**

> `stack` → memória "automática"; `heap` → memória "manual".

---

### 3.2 Funções de Alocação e Liberação

```c
#include <stdlib.h>

void *malloc(size_t tamanho_em_bytes);   // Aloca N bytes brutos (não inicializa)
void *calloc(size_t n, size_t size);     // Aloca n elementos de size bytes (inicializa em 0)
void free(void *ptr);                    // Liberta memória alocada
```

**Regra de Ouro:**

> Toda vez que se usa `malloc` ou `calloc`, mais cedo ou mais tarde se deve usar `free` (se `malloc` não falhar).

---

### 3.3 Exemplo 1: Alocar um Único Inteiro

**Código no Quadro:**

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *p = malloc(sizeof(int));

    if (p != NULL) {
        *p = 42;
        printf("Valor alocado: %d\n", *p);
        free(p);  // Libera a memória
    } else {
        printf("Falha na alocação!\n");
    }

    return 0;
}
```

**Pontos Didáticos:**

- `sizeof(int)` → Tamanho em bytes de um `int` na arquitetura (geralmente 4 bytes).
- `p` é um ponteiro na `stack`; o `int` de fato mora no `heap`.
- `p` acessa o inteiro alocado (desreferência).
- **Importante:** Sempre verificar se `malloc` retornou `NULL` (falha na alocação).

**Visualização de Memória:**

```
Stack:  [ p ] → contém endereço 0x1000
Heap:   [ 0x1000 ] → contém valor 42
```

---

### 3.4 Exemplo 2: Alocar um Vetor de Inteiros

**Código no Quadro:**

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n = 100;
    int *v = malloc(n * sizeof(int));

    if (v != NULL) {
        // Preenche o vetor
        for (int i = 0; i < n; i++) {
            v[i] = i * 2;
        }

        // Acessa alguns valores
        printf("v[0] = %d\n", v[0]);
        printf("v[50] = %d\n", v[50]);

        free(v);  // Libera o vetor
    } else {
        printf("Falha na alocação!\n");
    }

    return 0;
}
```

**Relação Entre Vetor e Ponteiro:**

- `v` é um ponteiro para o primeiro elemento.
- `v + i` é o endereço do elemento de índice `i`.
- `(v + i)` é o valor nesse endereço.

**Frase de Memória:**

> Para qualquer vetor `v`, vale:
> 
> ```
> v[i] ≡ *(v + i)
> ```

Isso mostra que **vetor e ponteiro são muito próximos em C**.

**Demonstração Prática:**

```c
printf("v[0] = %d\n", v[0]);      // Sintaxe de vetor
printf("*(v+0) = %d\n", *(v+0));  // Sintaxe de ponteiro (mesmo resultado)

printf("v[1] = %d\n", v[1]);
printf("*(v+1) = %d\n", *(v+1));  // Mesmo resultado
```

---

## Parte 4 – Voltando à Função de Inicialização da Pilha

### 4.1 Agora com `struct` Alocada em Tempo de Execução

Recomeçar a partir da definição de `Pilha` com **vetor estático**, mas alocando a `struct` dinamicamente:

```c
#define MAX 100

typedef struct pilha {
    int valores[MAX];  // Ainda estático
    int topo;
} Pilha;
```

**Pergunta para a Turma:**

> "Se a pilha agora é alocada com `malloc`, como acessamos os seus membros via ponteiro? Lembre: `Pilha *self = malloc(sizeof(Pilha))`."

---

### 4.2 Uso de `->` e Parênteses para Acesso a Membros

Mostrar explicitamente:

```c
Pilha *self = malloc(sizeof(Pilha));
if (self == NULL) {
    return NULL;
}

(*self).topo = -1;   // Funciona, mas é verboso
self->topo = -1;     // Equivalente, mais simples
```

**Explorar a Ordem de Avaliação:**

- `(*self).topo` → Primeiro `self` (desreferencia o ponteiro), depois acessa o membro `topo`.
- A expressão `self.topo` **não é o que queremos**:
    - O `.` tem precedência maior que o `*`, então seria `*(self.topo)` → erro, pois `self.topo` não existe antes de ser desreferenciado.

**Regra Gramatical:**

> Para acessar um membro de uma `struct` por meio de ponteiro, use `(*p).membro` ou `p->membro`.

---

### 4.3 Introdução ao Operador `->`

**Definir Formalmente:**

> `p->membro` é **sintaxe abreviada** para `(*p).membro`.

Mostrar:

```c
(*self).topo = -1;   // Forma longa
self->topo = -1;     // Forma curta
```

**Conclusão Didática:**

> `->` é só um atalho de sintaxe, mas é tão natural em C que quase nunca se vê `(*p).membro` em código real.

---

### 4.4 Código Completo com `struct` no `heap` (Vetor Ainda Estático)

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 100

typedef struct pilha {
    int valores[MAX];
    int topo;
} Pilha;

Pilha *criaPilha() {
    Pilha *self = malloc(sizeof(Pilha));
    if (self == NULL) {
        return NULL;
    }
    self->topo = -1;
    return self;
}

void empilha(int x, Pilha *self) {
    if (self->topo == MAX - 1) {
        printf("Pilha cheia!\n");
        return;
    }
    self->topo++;
    self->valores[self->topo] = x;
}

int desempilha(Pilha *self) {
    if (self->topo == -1) {
        printf("Pilha vazia!\n");
        return -1;
    }
    int valor = self->valores[self->topo];
    self->topo--;
    return valor;
}

int pilhaVazia(Pilha *self) {
    return self->topo == -1;
}

int main() {
    Pilha *p = criaPilha();
    if (p == NULL) {
        printf("Falha ao criar pilha!\n");
        return 1;
    }

    empilha(10, p);
    empilha(20, p);
    empilha(30, p);

    while (!pilhaVazia(p)) {
        printf("Desempilhando: %d\n", desempilha(p));
    }

    free(p);  // Libera a struct (vetor ainda estático)

    return 0;
}
```

**Observações:**

- O `main` trabalha apenas com ponteiros: `pilhaVazia(p)`, `empilha(..., p)`, `desempilha(p)`.
- O **estado interno da pilha** (`valores`, `topo`) é manipulado só por funções, usando `p->...`.
- O vetor `valores` ainda é de tamanho fixo (`MAX`).

---

## Parte 5 – Definir Dinamicamente o Tamanho do Vetor

### 5.1 Pergunta Voltada para o Vetor Interno

> "Se já conseguimos ter a `struct` no `heap`, e já vimos que `malloc` aceita parâmetros de tamanho, por que o próprio `valores` precisa ser fixo? Será que dá para passar o tamanho da pilha como parâmetro e alocar o vetor dinamicamente?"

---

### 5.2 Definição de `Pilha` com Vetor Dinâmico

```c
typedef struct pilha {
    int *valores;   // Agora é um ponteiro
    int topo;
    int tamanho;    // Tamanho máximo da pilha
} Pilha;
```

**Explicação:**

- `int *valores;` → Vetor alocado dinamicamente.
- `tamanho;` → Guarda o tamanho máximo que a pilha pode ter.

---

### 5.3 Função `criaPilha` com Parâmetro `size`

> "Criamos uma função `criaPilha` que recebe o tamanho desejado (`size`) e faz isso:
> 
> 1. Aloca a própria `struct Pilha` com `malloc(sizeof(Pilha))`.
> 2. Inicializa `topo = -1` e `tamanho = size`.
> 3. Aloca o vetor de `int` com `size * sizeof(int)`.
> 4. Retorna o ponteiro `self` para essa pilha (ou `NULL` se algo falhar)."

**Em Código:**

```c
Pilha *criaPilha(int size) {
    // 1. Aloca a struct Pilha
    Pilha *self = malloc(sizeof(Pilha));
    if (self == NULL) {
        return NULL;
    }

    // 2. Inicializa topo e tamanho
    self->topo = -1;
    self->tamanho = size;

    // 3. Aloca o vetor de inteiros
    self->valores = malloc(size * sizeof(int));
    if (self->valores == NULL) {
        free(self);   // Se malloc do vetor falha, libera a struct
        return NULL;
    }

    return self;
}
```

**Frase de Transição para Usar em Sala:**

> "Veja bem:
> `Pilha *self = malloc(sizeof(Pilha));self->topo = -1;self->valores = malloc(sizeof(int) * size);return self;`
> 
> Agora tanto a estrutura quanto o vetor interno são alocados no `heap`, e o tamanho da pilha é definido em tempo de execução."

---

### 5.4 Funções de Pilha Ajustadas para Vetor Dinâmico

**Funções de Verificação e Operação:**

```c
int pilhaCheia(Pilha *self) {
    return self->topo == self->tamanho - 1;
}

int pilhaVazia(Pilha *self) {
    return self->topo == -1;
}

void empilha(int x, Pilha *self) {
    if (pilhaCheia(self)) {
        printf("Pilha cheia!\n");
        return;
    }
    self->topo++;
    self->valores[self->topo] = x;
}

int desempilha(Pilha *self) {
    if (pilhaVazia(self)) {
        printf("Pilha vazia!\n");
        return -1;
    }
    int valor = self->valores[self->topo];
    self->topo--;
    return valor;
}

int topoPilha(Pilha *self) {
    if (pilhaVazia(self)) {
        printf("Pilha vazia!\n");
        return -1;
    }
    return self->valores[self->topo];
}
```

---

### 5.5 Função de Liberação Completa da Pilha

```c
void liberaPilha(Pilha *self) {
    if (self != NULL) {
        free(self->valores);   // Primeiro libera o vetor interno
        free(self);            // Depois libera a struct
    }
}
```

**Regra de Ouro de Liberação:**

> Libere primeiro o recurso mais "interno" (`valores`), depois o que o contém (`self`).

**O Que Acontece se Fizer Errado:**

```c
// ❌ ERRADO
free(self);            // Perde o endereço de self->valores
free(self->valores);   // Comportamento indefinido!

// ✅ CORRETO
free(self->valores);   // Libera o vetor primeiro
free(self);            // Depois libera a struct
```

---

### 5.6 Exemplo de Uso no `main`

```c
int main() {
    Pilha *p1 = criaPilha(10);   // Pilha com 10 elementos
    if (p1 == NULL) {
        printf("Falha ao criar pilha pequena!\n");
        return 1;
    }

    Pilha *p2 = criaPilha(1000); // Pilha grande
    if (p2 == NULL) {
        printf("Falha ao criar pilha grande!\n");
        liberaPilha(p1);
        return 1;
    }

    // Empilha alguns valores na primeira
    for (int i = 0; i < 10; i++) {
        empilha(i * 10, p1);
    }

    printf("Topo de p1: %d\n", topoPilha(p1));

    while (!pilhaVazia(p1)) {
        printf("Desempilhando: %d\n", desempilha(p1));
    }

    // Libera ambas as pilhas
    liberaPilha(p1);
    liberaPilha(p2);

    return 0;
}
```

---

## 📝 Resumo da Aula (Para o Notion)

| Tópico | Conceito Central | Exemplo‑Chave |
| --- | --- | --- |
| **Pilha como ponteiro** | `Pilha *p` é como referência a objeto no heap | `Pilha *p = criaPilha(100);` |
| **`stack` vs `heap`** | `stack` → automática; `heap` → manual | Desenho no quadro |
| **`malloc`/`calloc`/`free`** | Alocação e liberação explícita | `malloc(100 * sizeof(int)); free(v);` |
| **Exemplo inteiro** | Alocar um único valor | `int *p = malloc(sizeof(int)); *p = 42;` |
| **Exemplo vetor** | Alocar array dinâmico | `int *v = malloc(n * sizeof(int));` |
| **Relação vetor‑ponteiro** | `v[i] ≡ *(v + i)` | `v[0]` e `*(v+0)` são iguais |
| **`struct` estática no heap** | `int valores[MAX];` + `malloc(sizeof(Pilha))` | `self->topo = -1;` |
| **Uso de `*` e `->`** | `(*p).membro` vs `p->membro` | `self->topo` é mais simples |
| **Pilha com vetor dinâmico** | `int *valores;` + `malloc(size * sizeof(int))` | `self->valores = malloc(...);` |
| **`criaPilha` com `size`** | Tamanho definido em tempo de execução | `Pilha *p = criaPilha(50);` |
| **`liberaPilha`** | Liberar vetor primeiro, depois `struct` | `free(self->valores); free(self);` |
| **Verificação de `NULL`** | `malloc` pode falhar | `if (p == NULL) { ... }` |

---

## 💡 Dicas para o Professor

### 1. Erro Comum de `free`

Mostre no quadro o que acontece se esquecer de `free(self->valores);` e só chamar `free(self);`. Desenhar na memória: a `struct` some, mas o bloco do vetor fica "órfão", exemplificando bem o *memory leak*.

### 2. Parênteses em `(*p).`

Escreva `*p.topo` no quadro e pergunte o que acontece. Explique a precedência de operadores (`.` ganha de `*`). Isso justifica a existência do operador `->`.

### 3. Visualização de Memória

Ao mostrar `criaPilha`, desenhe dois blocos no Heap:

```
Heap:
┌─────────────────┐
│  Pilha *self    │ → 0x1000 (struct)
│  topo = -1      │
│  tamanho = 50   │
│  valores ───────┼──→ 0x2000 (vetor de 50 ints)
└─────────────────┘
```

Isso ajuda a entender por que precisamos de dois `free`.

### 4. Verificação de NULL

Sempre enfatize: `malloc` pode falhar. Em sistemas embarcados ou com memória limitada, isso é crítico.

### 5. Consistência de Nomes

Mantenha os nomes em português (`criaPilha`, `empilha`, `topo`) para não confundir com a sintaxe em inglês, já que o foco é a lógica de memória, não o vocabulário da linguagem.

### 6. Demonstração de Vazamento

Se possível, use uma ferramenta como `valgrind` para mostrar na prática o que acontece quando não se libera memória corretamente.

---

## 🔜 Próximo Passo Sugerido

> "E se a pilha preencher todo o vetor e ainda precisar crescer?
Podemos usar `realloc` para aumentar o `self->valores` em tempo de execução, fazendo uma pilha que 'cresce sozinha' quando enche.
Esse tópico pode virar uma aula avançada ou um estudo de caso."

**Ou:**

> "Na próxima aula, vamos aplicar esses mesmos conceitos (struct, ponteiros, malloc/free) para criar uma **Lista Encadeada**, onde cada elemento é alocado individualmente no heap."

# Lista de exercícios - Ponteiros

### 🧩 **Lista de Exercícios - Ponteiros em C**

Estes exercícios ajudarão você a praticar conceitos fundamentais sobre ponteiros, manipulação de endereços e passagem de parâmetros por referência. Vamos lá?

---

### 🔹 **1. Análise de Código com Ponteiro**

**Pergunta:** Qual será a saída deste programa, supondo que `i` ocupa o endereço `4094` na memória?

```c
#include <stdio.h>
int main() {
    int i = 5, *p;
    p = &i;
    printf("%p - %d - %d\n", p, *p + 2, 3 * (*p));
}

```

---

### 🔹 **2. Modificando Valor via Ponteiro**

**Tarefa:** Crie um programa que:

- Declare um inteiro `numero` com valor 35;
- Use um ponteiro `ptr` para modificar o valor de `numero`;
- Exiba mensagens antes e depois da modificação, utilizando apenas o ponteiro.

📌 **Saída esperada (exemplo):**

> O ponteiro ptr armazena o endereço ___ que,
> 
> 
> por sua vez, armazena o valor ___.
> 
> Agora, o ponteiro ptr armazena o endereço ___ que,
> 
> por sua vez, armazena o valor ___.
> 

---

### 🔹 **3. Função `troca()`**

**Objetivo:** Implemente uma função `troca()` que receba dois ponteiros e troque os valores armazenados nas variáveis apontadas por eles.

---

### 🔹 **4. Endereço de uma Variável**

Escreva uma função que receba uma variável como parâmetro e imprima o seu endereço de memória.

---

### 🔹 **5. Definição de Ponteiro**

O que é um ponteiro?

a) O endereço de uma variável

b) Uma variável que armazena endereços

c) O valor de uma variável

d) Um indicador da próxima variável acessada

✅ **Resposta esperada:** ___

---

### 🔹 **6. Avaliação de Expressões com Ponteiros**

Considere o código:

```c
int i = 3, j = 5;
int *p, *q;
p = &i;
q = &j;

```

Determine os valores das expressões:

a) `p == &i`

b) `*p - *q`

c) `**&p`

d) `3 * - *p / (*q) + 7`

---

### 🔹 **7. Análise de Código II**

**Pergunta:** Qual será a saída deste programa, supondo que `i` ocupa o endereço `4094`?

```c
int main() {
    int i = 5, *p;
    p = &i;
    printf("%x %d %d %d %d\n", p, *p + 2, **&p, 3 * *p, **&p + 4);
}

```

---

### 🔹 **8. Expressões Legais e Ilegais**

Se `i` e `j` são inteiros, e `p` e `q` são ponteiros para int, analise:

a) `p = &i;`

b) `*q = &j;`

c) `p = &*&i;`

d) `i = (*&)j;`

e) `i = *&j;`

f) `i = *&*&j;`

g) `q = *p;`

h) `i = (*p)++ + *q`

⚠️ Identifique quais dessas expressões **são ilegais**.
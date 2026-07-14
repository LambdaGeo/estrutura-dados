# Lista de Exercícios - Vetores em C

## 📊 Lista de Exercícios – Vetores em C

Os vetores permitem armazenar e manipular coleções de dados em C. Nesta lista, você vai trabalhar com leitura, processamento, substituições, contagens e manipulações de índices.

---

### 1. Menor Elemento e sua Posição

**Tarefa:**

Leia um vetor `N[20]`, encontre o **menor valor** armazenado e a **posição** desse valor no vetor.

**Saída esperada (exemplo):**

```
O menor elemento de N é 3 e sua posição dentro do vetor é: 6

```

---

### 2. Troca de Elementos Pares e Ímpares

**Tarefa:**

Leia um vetor `K[30]` e troque todos os elementos de **índice ímpar** com o **elemento par imediatamente posterior**.

Exemplo:

- Posição 1 ↔ 2
- Posição 3 ↔ 4
- Posição 5 ↔ 6
    
    *(e assim por diante, com cuidado para não sair dos limites do vetor)*
    

---

### 3. Multiplicação de Vetor por uma Variável

**Tarefa:**

Leia um vetor `S[20]` e uma variável `A`. Em seguida, imprima o **produto de A por cada elemento** do vetor.

**Exemplo:**

Se `A = 2` e `S = {1, 2, 3}`, a saída deve ser `2, 4, 6`.

---

### 4. Contar Números Pares em um Vetor

**Tarefa:**

Leia um vetor com 20 números inteiros e mostre:

- Todos os elementos
- Quantos **valores pares** existem no vetor

---

### 5. Análise de Código – Inversão de Vetor

**Contexto:**

Dado o vetor:

```
int vet[] = {7, 3, 1, 5, 13, 11, 9, 15};
```

**Código:**

```c
int x, i;
for (i = 0; i < 8; i++) {
    x = vet[i];
    vet[i] = vet[7 - i];
    vet[7 - i] = x;
}

```

**Pergunta:**

Qual será a **configuração final** do vetor após a execução do código?
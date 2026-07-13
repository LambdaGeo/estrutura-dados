# Lista de exercícios - Funções

### 🧠 **Lista de Exercícios: Funções em C**

Codifiquem as seguintes funções utilizando os conceitos aprendidos sobre **funções em C**. Para cada exercício, implemente a função conforme o protótipo e verifique seu funcionamento com testes no `main()`.

---

### 1️⃣ **Somatório de 1 até N**

Implemente uma função que retorne a soma de todos os inteiros de 1 até um número dado `n`.

🧮 Exemplo:

`somatorio(4)` → 1 + 2 + 3 + 4 = **10**

```c
int somatorio(int n);
```

---

### 2️⃣ **Fatorial de um Número**

Implemente uma função que retorne o fatorial de um número inteiro positivo.

🧮 Exemplo:

`fat(4)` → 4 × 3 × 2 × 1 = **24**

```c
int fat(int n);
```

---

### 3️⃣ **Número Perfeito**

Um número é dito **perfeito** quando ele é igual à soma de seus divisores (excluindo ele mesmo). Faça uma função que verifique essa propriedade.

🧮 Exemplo:

`ehPerfeito(6)` → divisores: 1, 2, 3 → 1 + 2 + 3 = 6 → **true**

```c
int ehPerfeito(int n);

```

---

### 4️⃣ **Raiz Quadrada com Subtrações Sucessivas**

Uma forma de calcular a raiz quadrada de um número é subtrair dele números ímpares consecutivos a partir de 1 até que o resultado seja menor ou igual a zero.

🧮 Exemplo:

`raiz_quadrada(16)`

16 - 1 = 15

15 - 3 = 12

12 - 5 = 7

7 - 7 = 0 → **Raiz quadrada é 4**

```c
int raiz_quadrada(int x);
```

---

### 5️⃣ **Divisão com Subtrações Sucessivas**

Implemente uma função que faça a divisão de dois números inteiros usando apenas **subtrações sucessivas**.

🧮 Exemplo:

`div(10, 3)` → 10 - 3 = 7 → 7 - 3 = 4 → 4 - 3 = 1 → **Resultado: 3**

```c
int div(int a, int b);
```

---
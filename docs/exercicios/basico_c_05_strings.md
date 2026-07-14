# Lista de exercícios - Strings

## 🔤 Lista de Exercícios – Strings em C

Nesta lista, você irá praticar operações com **strings** (cadeias de caracteres), como leitura, manipulação, contagem, verificação de palíndromos, criptografia simples, substituição e conversão de letras. Vamos colocar os ponteiros para trabalhar!

---

### 1. Imprimir String Invertida

**Tarefa:**

Receba uma string e imprima-a de trás para frente.

**Exemplo de entrada:**

`joao` → **Saída esperada:** `oaoj`

---

### 2. Verificar Palíndromo (Palavra)

**Tarefa:**

Crie um programa que verifique se uma **palavra** digitada é um **palíndromo**.

**Exemplos de palíndromos:**

`aba`, `radar`, `reter`, `rever`, `rir`, `rotor`

---

### 3. Verificar Palíndromo (Frase)

**Tarefa:**

Faça um programa que detecte se uma **frase** é um palíndromo, **ignorando espaços e o caractere hífen '-'**.

**Exemplos:**

- "Socorram-me subi no onibus em Marrocos"
- "Omitiram radar maritimo"

Para mais exemplos, veja: [Wikipedia – Palíndromo](http://pt.wikipedia.org/wiki/Pal%C3%ADndromo)

---

### 4. Contar Número de Vogais

**Tarefa:**

Receba uma string e conte quantas **vogais** existem nela (independente de maiúsculas ou minúsculas).

---

### 5. Contar Quantidade de Cada Vogal

**Tarefa:**

Baseado no exercício anterior, mostre quantas vezes aparece **cada vogal**, separando minúsculas e maiúsculas.

**Exemplo de saída para “Eu gosto de programar”:**

```
a = 2; e = 1; i = 0; o = 3; u = 1
A = 0; E = 1; I = 0; O = 0; U = 0
```

---

### 6. Criptografia por Substituição (Cifra de César)

**Contexto:**

Desloque cada letra da string em `n` posições no alfabeto.

**Exemplo (n = 2):**

Frase: `Eu gosto de programar`

Saída: `Gx iquvg fg rtqitcoct`

**Crie dois programas:**

- a) Um programa que **criptografa** uma frase com base em uma chave (`n`);
- b) Outro que **descriptografa** uma frase utilizando a mesma chave.

---

### 7. Contar Ocorrência de um Caractere

**Tarefa:**

Receba uma **letra** e uma **frase** digitadas pelo usuário, e conte quantas vezes essa letra aparece na frase.

---

### 8. Substituir Caractere

**Tarefa:**

Receba uma string `s`, um caractere `ch1` e um caractere `ch2`, e **substitua todas as ocorrências de `ch1` por `ch2`** na string.

---

### 9. Converter String para Maiúsculas

**Tarefa:**

Receba uma string e converta **todos os caracteres para maiúsculo**.
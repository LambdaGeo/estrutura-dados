# Laboratório - Um REPL para uma máquina baseada em pilha

**Objetivo**: implementar um interpretador para uma máquina baseada em pilha.

**Contexto**: Diversas linguagens de programação são compiladas para uma máquina abstrata baseada em Pilha. Nessa máquina, os operandos e os resultados das operações são armazenados em um pilha.

Nessa atividade iremos implementar um REPL (Read Eval Print Loop) similar ao que vocês utilizam quando interagem com o Python, porém interpretando comandos para uma máquina baseada em Pilha, como explicado no vídeo abaixo:

[https://www.youtube.com/watch?v=_j3jzoZaSbc](https://www.youtube.com/watch?v=_j3jzoZaSbc)

Deixarei disponível em https://github.com/profsergiocosta/lab-stackinterpreter o código fonte base para o desenvolvimento. Abaixo está o código que implementa o REPL. Esse código já está interagindo e lendo as entradas do usuário e passando para o interpretador.

```c
#include <stdio.h>

#include "interpret.h"

static void repl()
{
  char line[1024];
  for (;;)
  {
    printf("> ");

    if (!fgets(line, sizeof(line), stdin))
    {
      printf("\n");
      break;
    }

    interpret(line);
  }
}

int main () {

    repl();
    return 0;
}
```

Nó código base já tem o arquivo de cabeçalho do interpretador:

```c
#ifndef interprete_h
#define interprete_h

void interpret (const char *source) ;

#endif
```

E também  já está disponível a implementação da extração do comando e o argumento passado pelo usuário.

```c

#include <string.h>
#include <stdlib.h>
#include <stdio.h>

#include "interpret.h"
#include "stack"

void interpret (const char *source) {

		char op[10];
    char arg[10];

    sscanf (source, "%s%s", op, arg);
    printf("operação: %s\n", op);
    printf("argumento: %s\n",  arg);

}
```

Então, quando o usuário digitar:

```c
> push 10
```

O comando será push, e o argumento a constante 10. Você ja pode compilar e experimentar.

Ao desenvolver esse laboratório, é importante que façam em duas etapas. Na primeira dê suporte apenas a constantes e na segunda etapa inclue suporte a variáveis.

### **Descrição da Etapa 1**

Vocês devem implementar um interpretador que funcione no formato REPL, aceitando comandos digitados pelo usuário, interpretando e executando as operações usando uma **pilha**.

### 📋 **Comandos a serem implementados nesta etapa:**

1. `push <valor>`
    - Empilha um número inteiro na pilha.
    - Exemplo: `push 20`
2. `add`
    - Desempilha dois valores da pilha, soma, e empilha o resultado.
    - Exemplo:
        
        Entrada:
        
        ```
        push 5
        push 3
        add
        
        ```
        
        Resultado na pilha: `8`
        
3. `sub`
    - Desempilha dois valores, subtrai o segundo do primeiro, e empilha o resultado.
4. `mul`
    - Desempilha dois valores, multiplica, e empilha o resultado.
5. `div`
    - Desempilha dois valores, divide o primeiro pelo segundo (divisão inteira), e empilha o resultado.
6. `print`
    - Desempilha um valor e imprime imediatamente no console.

### ✅ **Regras e Observações**

- A pilha deve ser mantida em memória enquanto o programa estiver rodando.
- O REPL deve continuar executando até que o usuário digite um comando de parada (como `exit`).
- Não é necessário, nesta etapa, trabalhar com variáveis, apenas valores inteiros.

---

### 🧪 **Exemplo d Interação**

```
> push 10
> push 5
> add
> print
15
> push 8
> push 2
> div
> print
4
> exit

```

---

### 📂 **Organização Esperada do Projeto**

```

/maquina-pilha
│
├── main.c            // Loop principal REPL
├── interpret.c       // Processamento dos comandos
├── interpret.h
├── stack.c           // Implementação da pilha
├── stack.h
├── README.md
```

---

### 💡 **Sugestões**

- Usem listas para implementar a pilha.
- Dividam as responsabilidades do código: uma parte para o REPL, outra para a lógica da pilha.
- Tratem erros simples, como tentar desempilhar de uma pilha vazia.

---

Demonstração etapa 1

[https://www.youtube.com/watch?v=92Aqp95Dw64](https://www.youtube.com/watch?v=92Aqp95Dw64)

## **Etapa 2**

Ampliar a funcionalidade do interpretador da máquina virtual baseado em pilha, implementando uma **memória de variáveis** usando uma **lista encadeada**. Esta etapa introduz o uso de variáveis nomeadas e operações entre elas.

**Conceitos Praticados**

- Implementação e uso de **lista encadeada**
- Armazenamento e atualização de variáveis
- Integração entre estruturas de dados: **pilha** e **lista**

**Novos Comandos**

`push <valor | nome_variável>`

- Se for um número inteiro: empilha normalmente.
- Se for o nome de uma variável:
    - Busca na **lista encadeada** pelo nome.
    - Se encontrada, empilha o valor.
    - Se não encontrada, exibe erro: `Variável não encontrada`.

```c

push a
```

`pop <nome_variável>`

- Desempilha um valor da pilha.
- Se a variável existir na lista, **atualiza o valor**.
- Se não existir, **cria um novo nó** com o nome e o valor.

```c
pop resultado
```

---

### 🧵 **Estrutura da Lista (em `lista.h`)**

```c
struct node {
    char key[15];
    int value;
    struct node* next;
};

struct list {
    struct node* first;
};

```

### Funções sugeridas (em `lista.c`):

```c
void set_variable(struct list* l, const char* key, int value);
int get_variable(struct list* l, const char* key, int* found);

```

---

### 🧪 **Exemplo de Código Interpretado**

O interpretador deve ser capaz de ler e executar comandos como:

```
push 42
push 5
add
push 8
sub
pop a
push 56
push 8
add
pop b
push a
push b
add
push 6
add
print

```

**Explicação resumida do que esse código faz:**

- Empilha 42 e 5 → soma = 47
- Empilha 8 → subtrai: 47 - 8 = 39 → guarda em `a`
- Empilha 56 e 8 → soma = 64 → guarda em `b`
- Empilha `a` e `b` (valores 39 e 64) → soma = 103
- Empilha 6 → soma final = 109
- Imprime: `109`

---

### 🗂️ **Estrutura Esperada do Projeto**

```
/maquina-pilha
│
├── main.c             // REPL principal
├── interpret.c        // Interpretador de comandos
├── interpret.h
├── stack.c            // Pilha
├── stack.h
├── lista.c            // Lista encadeada (variáveis)
├── lista.h
├── README.md

```

---

### ✅ **Critérios de Avaliação**

- Implementação correta da lista encadeada
- Manipulação correta das variáveis com `push` e `pop`
- Integração com a pilha
- Código limpo e modular
- README claro e completo

---

[https://www.youtube.com/watch?v=WpFQuXFjyNQ](https://www.youtube.com/watch?v=WpFQuXFjyNQ)
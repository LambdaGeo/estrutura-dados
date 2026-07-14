# Lista de Exercícios — Árvores Binárias de Busca (ABB)

## *Foco: Inserção, Busca, Remoção e Propriedades de Ordenação*

!!! warning "Atenção"
    Esta lista assume a **propriedade de Árvore Binária de Busca**:

    Para todo nó `N`, todos os valores na subárvore **esquerda** são **menores** que `N->valor`, e todos os valores na subárvore **direita** são **maiores** que `N->valor`.

    Valores duplicados **não são permitidos** nesta lista.

---

## 📋 Convenções e Pré-requisitos

### Estrutura de Dados

```c
typedef struct Arvore {
    int valor;
    struct Arvore* esquerda;
    struct Arvore* direita;
} Arvore;
```

### Funções Auxiliares Disponibilizadas

```c
// Cria um novo nó com o valor informado e filhos especificados
Arvore* criar_arvore(int valor, Arvore* esq, Arvore* dir);

// Libera toda a memória da árvore (pós-ordem)
void liberar_arvore(Arvore* raiz);

// Percursos básicos (já implementados)
void pre_ordem(Arvore* raiz);
void em_ordem(Arvore* raiz);   // Em ABB: retorna valores em ordem crescente!
void pos_ordem(Arvore* raiz);
```

### Regras Gerais

- Todas as funções devem ser **recursivas**, salvo indicação contrária.
- Árvores vazias são representadas por `NULL`.
- Use `int` para valores e retornos lógicos (`1` = verdadeiro, `0` = falso).
- **Não modifique a estrutura** em funções de consulta (busca, validação, etc.).
- Em funções de modificação (inserção, remoção), retorne a nova raiz se necessário.

---

## 🔹 Nível 1: Compreensão da Propriedade ABB

### Exercício 1 — Identificação Visual

Para cada árvore abaixo, indique se **é ou não** uma ABB válida. Justifique brevemente.

```
a)          b)          c)
    5           5           10
   / \         / \         /  \
  3   8       3   8       5    15
 / \   \     /   / \     / \   / \
1   4   9   2   7   9   3  7  12 20
```

### Exercício 2 — Previsão de `em_ordem`

Considere a ABB abaixo:

```
        50
       /  \
     30    70
    /  \   / \
  20  40 60  80
```

a) Qual sequência será impressa por `em_ordem(raiz)`?

b) Por que essa propriedade é útil em ABBs?

### Exercício 3 — Montagem por Inserção Sequencial

Dada a sequência de inserções: `50, 30, 70, 20, 40, 60, 80`

a) Desenhe a ABB resultante, inserindo um valor por vez na ordem dada.

b) Escreva o código C que monta essa árvore **usando apenas `inserir_abr()`** (função do Exercício 4).

---

## 🔹 Nível 2: Operações Fundamentais de ABB

### Exercício 4 — Inserção em ABB

Implemente:

```c
Arvore* inserir_abr(Arvore* raiz, int valor);
```

Insere `valor` na ABB mantendo a propriedade de busca.

Retorna a raiz da árvore (pode mudar apenas na primeira inserção).

!!! tip "Dica recursiva"
    - Se `raiz == NULL`: crie e retorne novo nó
    - Se `valor < raiz->valor`: insira à esquerda
    - Se `valor > raiz->valor`: insira à direita
    - Se igual: ignore (sem duplicatas)

### Exercício 5 — Busca em ABB

Implemente:

```c
Arvore* buscar_abr(Arvore* raiz, int alvo);
```

Retorna ponteiro para o nó com `alvo`, ou `NULL` se não existir.

> Aproveite a propriedade ABB para **não percorrer toda a árvore**.

### Exercício 6 — Menor e Maior Valor

Implemente:

```c
int minimo_abr(Arvore* raiz);   // Assume árvore não-vazia
int maximo_abr(Arvore* raiz);   // Assume árvore não-vazia
```

> Dica: o mínimo está sempre no nó mais à esquerda; o máximo, no mais à direita.

### Exercício 7 — Validação de ABB

Implemente:

```c
int eh_abr(Arvore* raiz);
```

Retorna `1` se a árvore satisfaz a propriedade de busca, `0` caso contrário.

!!! warning "Cuidado"
    Não basta verificar `esq->valor < raiz->valor < dir->valor`.

    Todos os valores da subárvore esquerda devem ser menores que a raiz, e todos da direita, maiores.

    **Dica:** Use uma função auxiliar com limites:

    `int eh_abr_aux(Arvore* raiz, int min, int max);`

---

## 🔹 Nível 3: Remoção e Operações Avançadas

### Exercício 8 — Remoção em ABB

Implemente:

```c
Arvore* remover_abr(Arvore* raiz, int valor);
```

Remove o nó com `valor` da ABB, mantendo a propriedade de busca.

Retorna a nova raiz da árvore.

!!! note "Casos a considerar"
    1. Nó não encontrado → retorna `raiz`
    2. Nó é folha → libera e retorna `NULL`
    3. Nó tem um filho → retorna o filho no lugar
    4. Nó tem dois filhos → substitua pelo **sucessor** (menor da subárvore direita) ou pelo **antecessor** (maior da subárvore esquerda), e remova recursivamente esse substituto.

### Exercício 9 — Sucessor e Antecessor

Implemente:

```c
Arvore* sucessor_abr(Arvore* raiz, int valor);  // Retorna nó com o sucessor de 'valor'
Arvore* antecessor_abr(Arvore* raiz, int valor); // Retorna nó com o antecessor de 'valor'
```

- **Sucessor**: menor valor **maior** que `valor` na árvore
- **Antecessor**: maior valor **menor** que `valor` na árvore
- Retorna `NULL` se não existir.

> Dica: use busca em ABB + lógica de "último candidato válido".

### Exercício 10 — Contagem de Nós em Intervalo

Implemente:

```c
int contar_no_intervalo(Arvore* raiz, int min, int max);
```

Retorna quantos nós possuem valores `min <= valor <= max`.

!!! tip "Otimização ABB"
    Se `raiz->valor < min`, não percorra a esquerda.

    Se `raiz->valor > max`, não percorra a direita.

---

## 🔹 Nível 4: Desafios e Aplicações

### Exercício 11 — Altura Mínima e Máxima de ABB

Dado `n` valores distintos inseridos em uma ABB:
a) Qual é a **altura mínima possível**? (desenhe um exemplo para n=7)

b) Qual é a **altura máxima possível**? (desenhe um exemplo para n=7)

c) Implemente:

```c
int altura_abr(Arvore* raiz);  // Já feita na lista anterior, mas revise com foco em ABB
```

### Exercício 12 — Construção de ABB Balanceada a Partir de Vetor Ordenado

Implemente:

```c
Arvore* construir_abr_balanceada(int vet[], int inicio, int fim);
```

Dado um vetor **já ordenado**, construa uma ABB com **altura mínima** (balanceada).

> Estratégia: escolha o elemento do meio como raiz, recursivamente construa esquerda e direita.

### Exercício 13 — Verificação de Subárvore ABB

Implemente:

```c
int eh_subabr(Arvore* raiz, Arvore* sub);
```

Retorna `1` se `sub` é uma subárvore válida de `raiz` (mesma estrutura e valores), considerando propriedades de ABB.

### Exercício 14 — Impressão por Níveis (BFS) em ABB

Implemente:

```c
void imprimir_por_niveis(Arvore* raiz);
```

Imprime os valores da ABB nível a nível, da esquerda para a direita.

Exemplo para a árvore do Exercício 2:

```
Nível 0: 50
Nível 1: 30 70
Nível 2: 20 40 60 80
```

> Use uma fila (pode implementar com vetor circular ou lista encadeada).

### Exercício 15 — Contagem de Nós por Faixa de Altura

Implemente:

```c
int contar_nos_por_altura(Arvore* raiz, int h_min, int h_max);
```

Retorna quantos nós estão em níveis (profundidade) entre `h_min` e `h_max` (raiz = nível 0).

---

## 🔹 Bônus: Aplicações Práticas

### Exercício B1 — Conjuntos com ABB

Implemente um TAD simples de conjunto usando ABB:

```c
Arvore* conjunto_criar(void);
Arvore* conjunto_inserir(Arvore* c, int valor);
int conjunto_pertence(Arvore* c, int valor);
Arvore* conjunto_uniao(Arvore* a, Arvore* b);   // Retorna nova ABB com união
Arvore* conjunto_interseccao(Arvore* a, Arvore* b); // Retorna nova ABB com interseção
```

### Exercício B2 — Contagem de Ocorrências (Com Duplicatas Permitidas)

Modifique a estrutura para permitir contagem:

```c
typedef struct Arvore {
    int valor;
    int ocorrencias;  // novo campo
    struct Arvore* esquerda;
    struct Arvore* direita;
} Arvore;
```

Implemente:

```c
Arvore* inserir_com_contagem(Arvore* raiz, int valor);
int contar_ocorrencias(Arvore* raiz, int valor);
```

### Exercício B3 — Transformação: ABB → Lista Encadeada Ordenada

Implemente:

```c
typedef struct NoLista {
    int valor;
    struct NoLista* prox;
} NoLista;

NoLista* abr_para_lista(Arvore* raiz);
```

Retorna uma lista encadeada com os valores da ABB em ordem crescente.

> Dica: use `em_ordem` para percorrer e construir a lista.

---

## 📦 Arquivo Cabeçalho Sugerido (`abb.h`)

```c
#ifndef ABB_H
#define ABB_H

typedef struct Arvore {
    int valor;
    struct Arvore* esquerda;
    struct Arvore* direita;
} Arvore;

// Funções fornecidas
Arvore* criar_arvore(int valor, Arvore* esq, Arvore* dir);
void liberar_arvore(Arvore* raiz);
void em_ordem(Arvore* raiz);

// Operações fundamentais
Arvore* inserir_abr(Arvore* raiz, int valor);
Arvore* buscar_abr(Arvore* raiz, int alvo);
int minimo_abr(Arvore* raiz);
int maximo_abr(Arvore* raiz);
int eh_abr(Arvore* raiz);

// Remoção e navegação
Arvore* remover_abr(Arvore* raiz, int valor);
Arvore* sucessor_abr(Arvore* raiz, int valor);
Arvore* antecessor_abr(Arvore* raiz, int valor);

// Consultas avançadas
int contar_no_intervalo(Arvore* raiz, int min, int max);
int altura_abr(Arvore* raiz);
Arvore* construir_abr_balanceada(int vet[], int inicio, int fim);
void imprimir_por_niveis(Arvore* raiz);

#endif
```

---

## ✅ Critérios de Avaliação Sugeridos

| Critério | Pontuação |
| --- | --- |
| Correção da propriedade ABB nas operações | 30% |
| Eficiência: aproveitamento da ordenação (evitar percursos desnecessários) | 25% |
| Tratamento de casos-base e borda (árvore vazia, nó único, remoção de raiz) | 20% |
| Clareza, recursão bem estruturada e comentários | 15% |
| Liberação correta de memória e ausência de vazamentos | 10% |

---

## 💡 Dicas Estratégicas para Resolução

1. **Desenhe antes de codificar**: esboce a árvore e simule a operação manualmente.
2. **Pense nos casos-base primeiro**: `raiz == NULL` é seu amigo na recursão.
3. **Validação de ABB exige limites**: não compare apenas com o pai — use `min`/`max` propagados.
4. **Remoção com dois filhos**: escolha sucessor ou antecessor, mas seja consistente.
5. **Teste incrementalmente**:
    - Árvore vazia → inserir 1 elemento → inserir em ordem crescente/decrescente → árvore balanceada.

---

!!! tip "Próximo passo sugerido"
    Após dominar esta lista, explore **árvores AVL** ou **Rubro-Negras** para entender balanceamento automático e garantia de altura logarítmica.

*Material elaborado para a disciplina de Estrutura de Dados — Curso de Engenharia de Computação*

*Prof. Sérgio Souza Costa | Atualizado: 2026*
# Trabalho Prático: Implementação e Análise de Algoritmos de Ordenação em C

**Disciplina:** Estrutura de Dados / Programação

**Formato:** No máximo 3 alunos

**Linguagem:** C (padrão C99 ou C11)

**Duração sugerida:** 4 semanas

**Repositório:** GitHub (público ou privado com acesso ao professor)

---

## 🎯 Objetivos de Aprendizagem

1. Implementar **3 algoritmos básicos** e **3 algoritmos avançados** de ordenação em C.
2. Vivenciar o **controle de versão** com Git em equipe, com fluxo flexível e focado no histórico.
3. Aplicar noções básicas de **qualidade e medição**: testes, cobertura (`gcov`) e profiling de desempenho (`gprof`).
4. Produzir **documentação técnica** e **análise empírica** dos resultados.
5. Desenvolver **transparência acadêmica** no uso de IA, validando e explicando todo o código entregue.

---

## 👥 Organização do grupo

Cada trio define sua própria divisão de tarefas. Sugestão inicial (opcional):

- **Membro 1:** Algoritmos básicos + testes iniciais
- **Membro 2:** Algoritmos avançados + benchmarks
- **Membro 3:** Qualidade (`gcov`, `gprof`, `cppcheck`), `Makefile` e documentação

✅ **Regra única:** Todos devem conseguir compilar, executar e explicar qualquer parte do código. O histórico Git deve refletir contribuição ativa de pelo menos 2 integrantes.

---

## 🔢 Algoritmos Obrigatórios

| Categoria | Algoritmos | Assinatura Padrão |
| --- | --- | --- |
| **Básicos** | Bubble Sort, Selection Sort, Insertion Sort | `void algoritmoSort(int v[], int n);` |
| **Avançados** | Merge Sort, Quick Sort, Heap Sort | `void algoritmoSort(int v[], int n);` |

Cada algoritmo deve estar em **arquivo `.c` separado**. O `main.c` pode conter chamadas, menu ou execução direta dos testes.

---

## 🌿 Fluxo Git/GitHub (Flexível)

Não há exigência de *branch protection*, revisão obrigatória ou bloqueio de `push` direto na `main`. O foco é **criar o hábito de versionar incrementalmente**.

### ✅ Esperado no Histórico

- **Commits frequentes:** mínimo 1 a cada 2-3 dias de trabalho
- **Mensagens descritivas:**
    - ✅ `feat: adiciona heap sort`
    - ✅ `fix: corrige índice no partition do quicksort`
    - ✅ `docs: atualiza benchmark e uso de IA`
    - ❌ `update`, `fix`, `aaa`, `salva tudo`
- **Participação visível:** `git log` deve mostrar commits de pelo menos 2 emails/nomes diferentes
- **Branches & PRs:** opcionais. Podem trabalhar direto na `main` ou criar branches por funcionalidade. Se usarem PRs, basta uma descrição breve.

> 💡 **Dica:** Sempre rode `git pull` antes de começar e `git push` após testar uma nova funcionalidade. Isso evita conflitos e gera histórico natural.
> 

---

## 🛠️ Requisitos Técnicos & Ferramentas

### 1. Compilação & Build

- Compilação via `make` (modelo fornecido abaixo).
- Zero erros de compilação. Warnings críticos corrigidos.

### 2. Testes Básicos

- Arquivo `tests/test_basic.c` com **≥2 casos por algoritmo** (ex: vetor aleatório, já ordenado, invertido).
- Cada teste deve imprimir `✓ PASSOU` ou `✗ FALHOU`.
- Comando: `make test`

### 3. Cobertura de Código (`gcov`)

O **gcov** é uma ferramenta do GCC para medir **cobertura de código** (code coverage), ou seja, descobrir quais linhas do programa foram executadas durante os testes. ([GCC](https://gcc.gnu.org/onlinedocs/gcc/Gcov.html?utm_source=chatgpt.com))

## Compilar com suporte a cobertura

A forma mais simples é usar a flag `--coverage`:

```bash
gcc --coverage -g -O0 main.c -o main
```

ou explicitamente:

```bash
gcc -fprofile-arcs -ftest-coverage -g -O0 main.c -o main
```

As opções `-fprofile-arcs` e `-ftest-coverage` fazem o GCC gerar os arquivos necessários para o gcov. ([GCC](https://gcc.gnu.org/onlinedocs/gcc/Invoking-Gcov.html?utm_source=chatgpt.com))

Após a compilação, você verá arquivos:

```
main.gcno
```

---

## 2. Executar o programa ou os testes

```bash
./main
```

ou

```bash
make test
```

Após a execução, será criado:

```
main.gcda
```

Esse arquivo contém as estatísticas de execução. ([GCC](https://gcc.gnu.org/onlinedocs/gcc/Invoking-Gcov.html?utm_source=chatgpt.com))

---

## 3. Gerar o relatório

Execute:

```bash
gcov main.c
```

ou

```bash
gcov main.gcda
```

Será criado:

```
main.c.gcov
```

e um resumo semelhante a:

```
File 'main.c'
Lines executed:85.71% of 14
Creating 'main.c.gcov'
```

([Hexmos](https://hexmos.com/freedevtools/tldr/linux/gcov/?utm_source=chatgpt.com))

---

## 4. Interpretar o resultado

Exemplo de `main.c.gcov`:

```c
        1:int main() {
        1:    int x = 10;
        1:    if (x > 5)
        1:        printf("Maior\n");
    #####:    else
    #####:        printf("Menor\n");
        1:}
```

Significado:

- `1:` → executada 1 vez
- `5:` → executada 5 vezes
- `#####:` → nunca executada

([GCC](https://gcc.gnu.org/onlinedocs/gcc-8.1.0/gcc/Invoking-Gcov.html?utm_source=chatgpt.com))

---

## 5. Cobertura de branches

Para verificar cobertura de decisões (`if`, `while`, etc.):

```bash
gcov -b main.c
```

ou

```bash
gcov --branch-probabilities main.c
```

Isso mostra quais ramos foram tomados e com que frequência. ([Hexmos](https://hexmos.com/freedevtools/tldr/linux/gcov/?utm_source=chatgpt.com))

---

## Exemplo completo

Arquivo `main.c`:

```c
#include <stdio.h>

int soma(int a, int b) {
    return a + b;
}

int main() {
    if (soma(2, 3) == 5)
        printf("OK\n");

    return 0;
}
```

Compilar:

```bash
gcc --coverage -O0 -g main.c -o main
```

Executar:

```bash
./main
```

Gerar cobertura:

```bash
gcov main.c
```

Resultado:

```
Lines executed:100.00% of 6
```

---

## Gerando relatório HTML

Normalmente usa-se o **gcovr** ou **lcov**, que são interfaces mais amigáveis para o gcov. O gcovr pode gerar relatórios HTML diretamente. ([GitHub](https://github.com/gcovr/gcovr?utm_source=chatgpt.com))

```bash
gcovr --html-details coverage.html
```

ou

```bash
gcovr -r . --html --html-details -o coverage.html
```

Se você estiver usando **CMake**, **Makefile**, **GitLab CI**, **GitHub Actions** ou **pytest para projetos C/C++**, posso mostrar uma configuração completa de cobertura para o seu ambiente.

### 4. Profiling de Desempenho (`gprof`)

O **gprof** é uma ferramenta de **profiling** do GCC. Enquanto o **gcov** responde *"quais linhas foram executadas?"*, o **gprof** responde *"onde o programa gastou mais tempo?"*.

---

## 1. Compilar com suporte ao gprof

Use a opção `-pg` tanto na compilação quanto na linkedição:

```bash
gcc -pg bubble.c -o bubble
```

ou

```bash
gcc -pg -O0 -g bubble.c -o bubble
```

---

## 2. Executar o programa

```bash
./bubble
```

Após a execução será criado o arquivo:

```
gmon.out
```

Esse arquivo contém os dados coletados durante a execução.

---

## 3. Gerar o relatório

```bash
gprof bubble gmon.out
```

ou simplesmente

```bash
gprof bubble
```

Saída típica:

```
Flat profile:

Each sample counts as 0.01 seconds.

 %   cumulative   self
time   seconds   seconds   calls  ms/call  ms/call  name
85.0      0.17     0.17        1   170.00   170.00  bubbleSort
10.0      0.19     0.02        1    20.00    20.00  imprimirVetor
 5.0      0.20     0.01        1    10.00    10.00  main
```

---

## 4. Salvar em arquivo

```bash
gprof bubble gmon.out > perfil.txt
```

Depois:

```bash
cat perfil.txt
```

---

## 5. Exemplo com Bubble Sort

Considere:

```c
void bubbleSort(int v[], int n) {
    int i, j, tmp;

    for (i = 0; i < n - 1; i++) {
        for (j = 0; j < n - i - 1; j++) {
            if (v[j] > v[j + 1]) {
                tmp = v[j];
                v[j] = v[j + 1];
                v[j + 1] = tmp;
            }
        }
    }
}
```

Se você ordenar um vetor grande:

```c
int v[10000];
```

e executar o programa, o relatório provavelmente mostrará que quase todo o tempo foi gasto em `bubbleSort`.

---

## 6. Grafo de chamadas

Uma das partes mais úteis do relatório é o **Call Graph**:

```
index % time    self  children    called     name

[1]    95.0    0.17    0.01       1         main
                0.17    0.00       1/1       bubbleSort [2]

[2]    85.0    0.17    0.00       1         bubbleSort
```

Ele mostra:

- Quem chamou a função.
- Quantas vezes ela foi chamada.
- Quanto tempo ela gastou.
- Quanto tempo gastaram as funções chamadas por ela.

---

## Comparação rápida

| Ferramenta | Objetivo |
| --- | --- |
| **gcov** | Cobertura de código |
| **gprof** | Desempenho e tempo de execução |
| **valgrind/massif** | Uso de memória |
| **valgrind/callgrind** | Perfil detalhado de chamadas |
| **perf** (Linux) | Profiling moderno do sistema |

---

### Fluxo completo

```bash
# Compilar
gcc -pg -O0 bubble.c -o bubble

# Executar
./bubble

# Gerar relatório
gprof bubble gmon.out > relatorio.txt

# Visualizar
less relatorio.txt
```

---

## 🤖 Política de Uso de IA & Transparência

✅ **Permitido & Incentivado:**

- Gerar trechos para estudo, pedir explicação de erros, revisar formatação, sugerir nomes de variáveis, usar como "tutor".
❌ **Não permitido:**
- Entregar código completo sem entender, testar ou adaptar. Ocultar prompts ou ferramentas utilizadas.

📝 **Obrigatório:** Criar `docs/uso-ia.md` seguindo este modelo:

```markdown
# 🤖 Uso de Ferramentas de IA no Projeto

## Ferramentas Utilizadas
- [ ] ChatGPT / GPT-4o
- [ ] GitHub Copilot
- [ ] Claude / Gemini
- [ ] Outra: _______________

## Como Usamos (exemplos reais)
| Prompt / Solicitação | O que a IA gerou | O que adaptamos/validamos |
|----------------------|------------------|---------------------------|
| "Explique como o heapify restaura o max-heap" | Texto + pseudocódigo | Reescrevemos em C, ajustamos índices 2i+1 e adicionamos testes |
| "Corrija warning unused variable em merge.c" | Sugeriu remover var | Mantivemos, renomeamos e usamos no laço |

## Validação & Domínio
- [ ] Compilamos e rodamos todo código gerado ou sugerido
- [ ] Todos conseguem explicar o funcionamento de cada algoritmo em 2 minutos
- [ ] Não submetemos blocos inteiros sem revisão linha a linha

## Reflexão Final (3-5 linhas)
A IA acelerou a compreensão de conceitos como particionamento recursivo, mas exigiu atenção redobrada em casos de borda. O maior aprendizado foi questionar a saída da IA em vez de aceitá-la como verdade absoluta.
```

> ⚖️ **Avaliação:** Uso de IA **não penaliza**. Falta de transparência, código não testado ou trio incapaz de explicar a entrega **penaliza**.
> 

---

## 📁 Estrutura Obrigatória do Repositório

```
ordenacao-trio/
├── README.md                  # Instruções de build, membros, links
├── Makefile                   # Modelo fornecido
├── src/
│   ├── basicos/               # bubble.c, selection.c, insertion.c
│   ├── avancados/             # merge.c, quick.c, heap.c
│   └── main.c                 # Ponto de entrada
├── tests/
│   └── test_basic.c           # Testes manuais
├── docs/
│   ├── cobertura.md           # Relatório gcov + análise
│   ├── perfil_bruto.txt       # Saída do gprof (gerada automaticamente)
│   ├── perfil.md              # Interpretação do profiling
│   └── uso-ia.md              # Transparência de prompts e validação
└── .gitignore
```

---

## 📅 Cronograma Sugerido

| Semana | Foco | Meta Git |
| --- | --- | --- |
| **1** | Setup, `Makefile`, 2 básicos, 1 teste cada | Commits iniciais + estrutura |
| **2** | Completar básicos, 2 avançados, testes rodando | Histórico crescente (≥5 commits) |
| **3** | Completar avançados, `gcov`, `gprof`, `cppcheck` | Commits de refino + `docs/` |
| **4** | Ajustes finais, tag `v1.0`, revisão geral | Entrega + link no sistema |

---

## 📊 Rubrica de Avaliação (100 pts)

| Critério | O que será observado | Peso |
| --- | --- | --- |
| **Funcionalidade** | 6 algoritmos compilam, executam e ordenam corretamente | 25 |
| **Histórico Git** | Commits regulares, mensagens claras, participação do trio, evolução visível | 20 |
| **Qualidade & Testes** | Testes passam, `gcov` ≥70% nas funções, `cppcheck` limpo de erros críticos | 20 |
| **Documentação & Análise** | `docs/cobertura.md`, `docs/perfil.md`, `README` funcional | 20 |
| **Colaboração & IA** | Divisão equilibrada, `docs/uso-ia.md` preenchido, código explicável | 15 |

> ⚠️ Repositórios com 1-2 commits no dia da entrega, mensagens vazias ou código que o trio não consegue modificar serão penalizados na categoria Git/Colaboração.
> 

---

## 🎥 Defesa do Trabalho: Apresentação em Vídeo

Esta atividade serve como a **defesa oral do trabalho prático** e sua nota (**4,0 pontos**) substituirá a avaliação escrita da Terceira Unidade. O objetivo é demonstrar o domínio sobre o código desenvolvido e as ferramentas utilizadas.

### Entrega do Vídeo
- **Formato:** Gravação com duração entre **8 e 15 minutos** postada no YouTube (como público ou não listado).
- **Envio:** O link do vídeo deve ser enviado no SIGAA junto com a entrega do repositório.

### Estrutura Obrigatória do Vídeo
1. **Apresentação da Equipe:** Apresentar os integrantes, turma e objetivos gerais.
2. **Implementação dos Algoritmos:** Mostrar a organização do código-fonte (arquivos e estrutura) e explicar partes relevantes dos algoritmos desenvolvidos.
3. **Demonstração da Execução:** Compilar e executar o programa ao vivo no vídeo, mostrando a entrada de dados, saída de testes e a coleta das métricas.
4. **Análise Experimental:** Discutir a tabela de tempos de execução, contagens de comparações e trocas, comparando a performance dos algoritmos na prática com a teoria de complexidade.
5. **Uso de Ferramentas:** Demonstrar o funcionamento do `gcov` (cobertura obtida), `gprof` (funções mais pesadas/gargalos) e `cppcheck` (correções feitas).
6. **Conclusões:** Responder qual algoritmo performou melhor, se as medições batem com a teoria estudada e quais dificuldades a equipe encontrou.

### Critérios de Avaliação do Vídeo (Total: 4.0 pts)
| Critério | O que será observado | Pontos |
| --- | --- | --- |
| **Organização e Clareza** | Apresentação didática, áudio nítido, divisão do tempo e boa estrutura | 1.0 |
| **Demonstração do Código** | Explicação concisa da implementação e compilação/execução correta | 1.0 |
| **Análise de Resultados** | Discussão fundamentada nas medições empíricas comparando os algoritmos | 1.0 |
| **Domínio e Participação** | Todos os integrantes do grupo devem falar e demonstrar autoria do código | 1.0 |

### Regras Gerais
- Os grupos devem ser exatamente os mesmos do trabalho prático.
- Não serão aceitas apresentações compostas apenas de slides; é obrigatório alternar para a tela do terminal e editor para mostrar o código e a execução real.
- A voz e explicações devem ser claras e audíveis por todos os integrantes.

---

## 📦 Entrega do Projeto

Para concluir a entrega do laboratório, certifique-se de realizar os seguintes passos:

1. **Repositório GitHub** atualizado (público ou com acesso liberado ao professor).
2. **Tag de Versão**: Criar uma tag git da entrega final:
   ```bash
   git tag -a v1.0 -m "Entrega final do trabalho de ordenação"
   git push origin main --tags
   ```
3. **Envio via SIGAA**: Enviar em um único comentário por equipe:
   - Nomes completos dos integrantes da equipe.
   - Link do repositório GitHub.
   - Link do vídeo de apresentação no YouTube.

---

## 📎 Apêndice: `Makefile` Base (Pronto para uso)

Copie este arquivo para a raiz do repositório. Ele já inclui alvos para compilação, testes, `gcov` e `gprof`.

```makefile
CC = gcc
CFLAGS = -Wall -Wextra -std=c11 -O2
GCOV_FLAGS = -fprofile-arcs -ftest-coverage -g
PROFILE_FLAGS = -pg -g -O0

SRCS = src/main.c src/basicos/bubble.c src/basicos/selection.c src/basicos/insertion.c \\
       src/avancados/merge.c src/avancados/quick.c src/avancados/heap.c
TEST_SRCS = tests/test_basic.c $(filter-out src/main.c,$(SRCS))
OBJS = $(SRCS:.c=.o)
TEST_OBJS = $(TEST_SRCS:.c=.o)

TARGET = sort_main
TEST_TARGET = test_basic

all: $(TARGET)

$(TARGET): $(OBJS)
	$(CC) $(CFLAGS) -o $@ $^

$(TEST_TARGET): $(TEST_OBJS)
	$(CC) $(CFLAGS) -o $@ $^

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

test: $(TEST_TARGET)
	./$(TEST_TARGET)

coverage: CFLAGS += $(GCOV_FLAGS)
coverage: clean test
	@echo "✅ Dados de cobertura gerados. Rode: gcov src/basicos/*.c src/avancados/*.c"

profile: clean
	$(CC) $(PROFILE_FLAGS) $(CFLAGS) -o sort_profile $(SRCS) tests/test_basic.c
	./sort_profile
	gprof sort_profile gmon.out > docs/perfil_bruto.txt
	@echo "✅ Profiling gerado em docs/perfil_bruto.txt"
	@echo "💡 Abra o arquivo e analise a seção 'Flat Profile'"

clean:
	rm -f $(TARGET) $(TEST_TARGET) sort_profile $(OBJS) $(TEST_OBJS) *.gcda *.gcno *.gcov gmon.out

.PHONY: all test coverage profile clean
```

---

## 💡 Dicas Rápidas para Iniciantes

| Ferramenta | Dica Crucial |
| --- | --- |
| `gcov` | Se cobertura < 70%, adicione testes com `n=0`, `n=1`, vetores com duplicatas e invertidos. |
| `gprof` | Não rode com `-O2`. O otimizador distorce medições. Use `make profile` (já aplica `-O0`). |
| `git` | Mensagens como `fix: ajusta condição de parada no quicksort` valem mais que 10 commits `update`. |
| IA | Peça explicação, não código pronto. Valide linha a linha. A IA é copilot, não piloto. |
| Entrega | Teste `make clean && make all && make test && make coverage && make profile` antes de dar `push`. |

---

✅ **Este documento está pronto para ser distribuído como PDF, postado na LMS ou fixado como `README` do repositório-template.**

Se quiser, posso gerar:

- Um `README.md` template já preenchido com as seções obrigatórias
- Um arquivo `diario.md` com perguntas-guia semanais
- Um script bash de correção rápida para o professor

Basta avisar! 🚀
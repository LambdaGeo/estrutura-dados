# Lista de Exercícios - Estruturas Heterogêneas

## Caros alunos,

Esta lista de exercícios foi elaborada para aprofundar e consolidar os conceitos fundamentais de estruturas de dados na linguagem C. Abordaremos os seguintes tópicos: registros (`structs`), vetores de registros, o uso de ponteiros para manipulação de dados e a alocação dinâmica de memória. O objetivo é conectar a teoria à prática, permitindo que vocês apliquem o conhecimento adquirido para resolver problemas concretos. Conforme discutido em nosso material de referência, buscaremos não apenas soluções que funcionem, mas sim algoritmos que demonstrem as três qualidades fundamentais de um bom código: **correção**, **eficiência** e **elegância**. Encarem cada questão como uma oportunidade de fortalecer sua lógica e habilidade de programação sob estes princípios.

--------------------------------------------------------------------------------

## 1. Questões Teóricas (Conceitos Fundamentais)

Para as questões a seguir, elabore respostas discursivas curtas, justificando-as com base nos princípios da linguagem C e nos conceitos estudados.

### 1.1. Propósito dos Registros ()

Registros, ou `structs`, são descritos como "coleções de dados heterogêneos". Com base nesse conceito, explique com suas próprias palavras por que as `structs` são uma ferramenta poderosa na programação em C. Forneça um exemplo prático (diferente de `ponto` ou `aluno`) onde o uso de uma `struct` seria claramente mais vantajoso do que utilizar variáveis individuais para representar uma entidade.

### 1.2. Acesso a Membros: Operador Ponto () vs. Operador Seta ()

Diferencie o uso do operador de acesso a membro (`.`) e o operador de acesso a membro via ponteiro (`->`). Explique em qual cenário cada um deve ser utilizado e por que a tentativa de usar um no lugar do outro resultaria em um erro de compilação. Justifique sua resposta com base na diferença entre uma variável do tipo `struct` e um ponteiro para uma `struct`.

### 1.3. Alocação Dinâmica de Memória

Descreva o ciclo de vida da memória alocada dinamicamente com `malloc`. Em sua resposta, aborde os seguintes pontos:

1. Por que é crucial verificar se o ponteiro retornado por `malloc` é `NULL`?
2. Qual é a principal consequência de não liberar a memória com a função `free()` após seu uso? (Explique o conceito de "vazamento de memória" ou *memory leak*).

### 1.5. O Operador com Estruturas

O operador `sizeof` é utilizado para determinar o tamanho, em bytes, de um tipo de dado ou variável. Explique a diferença entre o valor retornado por `sizeof(struct aluno)` e `sizeof(struct aluno *)`. Justifique essa diferença com base no que cada uma dessas expressões representa em termos de alocação de memória.

--------------------------------------------------------------------------------

## 2. Questões Práticas (Implementação em C)

Para os exercícios a seguir, escreva o código em C correspondente, seguindo as melhores práticas de documentação e leiaute.

### 2.1. Definição e Instanciação de um

Defina uma `struct` chamada `Produto` para armazenar as seguintes informações:

- `codigo` (`int`)
- `descricao` (`char[]` com espaço para 50 caracteres, mais o terminador nulo)
- `preco` (`float`)

Em seguida, escreva uma função `main` que declare uma variável do tipo `Produto`, inicialize seus campos com valores de sua escolha e, por fim, imprima os dados do produto na tela de forma organizada.

### 2.2. Função com como Parâmetro (por Valor)

Escreva uma função chamada `aplica_desconto`. Esta função deve receber como parâmetros uma variável do tipo `Produto` (definida no exercício anterior) e um valor `float` representando o percentual de desconto. A função deve calcular o novo preço e retornar uma **nova** estrutura `Produto` com o preço atualizado. A estrutura original passada como parâmetro **não** deve ser modificada.

### 2.3. Função com Ponteiro para como Parâmetro

Escreva uma função chamada `atualiza_preco`. Diferentemente do exercício anterior, esta função deve receber um **ponteiro** para uma `struct` `Produto` e um valor `float` representando o percentual de aumento. A função deve modificar o preço do produto diretamente na memória, alterando o valor na estrutura original. A função deve ter retorno `void`.

### 2.4. Manipulação de Vetor de Registros

Escreva um programa completo que realize as seguintes tarefas:

1. Declare um vetor estático com capacidade para 5 `Produto`s.
2. Crie um laço que solicite ao usuário que preencha os dados (código, descrição e preço) para cada um dos 5 produtos.
3. Implemente e chame uma função que receba o vetor de produtos e seu tamanho como parâmetros. Essa função deve encontrar e imprimir na tela os dados do produto mais caro.

### 2.5. Alocação Dinâmica de um Único Registro

Implemente uma função `cria_produto` que não recebe parâmetros. Dentro da função, você deve:

1. Alocar dinamicamente memória para uma `struct` `Produto`.
2. Verificar se a alocação foi bem-sucedida.
3. Solicitar ao usuário que digite os dados do produto.
4. Retornar o ponteiro para a área de memória alocada e preenchida.

### 2.6. Alocação Dinâmica de um Vetor de Registros

Escreva um programa que primeiro pergunte ao usuário quantos produtos ele deseja cadastrar (`n`). Em seguida, o programa deve:

1. Alocar dinamicamente um vetor de `n` posições para `Produto`s.
2. Verificar se a alocação de memória ocorreu com sucesso.
3. Preencher o vetor com os dados de `n` produtos inseridos pelo usuário.
4. Imprimir os dados de todos os produtos cadastrados.
5. Liberar a memória alocada para o vetor ao final da execução.

### 2.7. Busca em um Vetor de Registros

Crie uma função `busca_produto_por_codigo` que recebe um vetor de `Produto`s, seu tamanho e um código (inteiro) a ser buscado. A função deve percorrer o vetor e:

- Se encontrar um produto com o código correspondente, deve retornar o **índice** desse produto no vetor.
- Se não encontrar nenhum produto com o código informado, deve retornar **1**.

Para a lógica de percurso, inspire-se na função `Busca` apresentada no Capítulo 3 do livro de referência, que varre o vetor do fim para o começo.
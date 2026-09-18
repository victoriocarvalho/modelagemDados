# Aula 6 - Formas Normais

## Teoria: Formas Normais

As **formas normais** são regras para organizar tabelas relacionais de modo a reduzir a repetição desnecessária de dados e evitar problemas de inserção, alteração e exclusão. Normalizar uma tabela significa verificar como seus atributos dependem das chaves e, quando necessário, decompor a tabela em estruturas menores, sem perder as informações nem os relacionamentos entre os dados.

Uma dependência funcional `X -> Y` significa que o valor de `X` determina um único valor de `Y`. Por exemplo, em `Produto`, o código do produto determina seu nome: `id_produto -> nome_produto`. As formas normais usam esse tipo de dependência para identificar organizações inadequadas dos dados.

### Primeira Forma Normal (1FN)

Uma tabela está na **Primeira Forma Normal** quando cada célula armazena um único valor, os atributos são atômicos e não existem grupos repetidos ou listas dentro de uma coluna.

Considere a tabela abaixo:

| id_venda | data | produtos |
|---|---|---|
| 101 | 2026-09-18 | Caneta, Caderno |

A coluna `produtos` contém mais de um valor na mesma célula. Essa tabela não está na 1FN, pois fica difícil consultar, alterar ou relacionar cada produto individualmente.

Uma possível solução é separar a venda de seus itens:

**Venda**

| id_venda | data |
|---|---|
| 101 | 2026-09-18 |

**Produto**

| id_produto | nome_produto |
|---|---|
| 10 | Caneta |
| 20 | Caderno |

**ItemVenda**

| id_venda | id_produto |
|---|---|
| 101 | 10 |
| 101 | 20 |

Agora cada célula possui um único valor e cada linha de `ItemVenda` representa a participação de um produto na venda. O nome de cada produto é armazenado na tabela `Produto`.

#### Para refletir

A violação da 1FN nesse caso resulta de uma sequência de erros conceituais. Primeiro, não se identificou que `Produto` é uma entidade independente da venda, que deveria ser modelada como uma entidade relacionada a `Venda`, e não como um atributo da venda. Segundo, mesmo que `Produto` não tivesse sido identificado como entidade, reconhecer que `produtos` era um atributo multivalorado levaria, na transformação para o modelo lógico, à criação de uma tabela própria para os itens.

Assim, embora as formas normais sejam estratégias específicas do modelo relacional, no nível lógico, elaborar um bom modelo conceitual já é um grande passo para evitar violações à 1FN.

### Segunda Forma Normal (2FN)

Uma tabela está na **Segunda Forma Normal** quando está na 1FN e todo atributo que não faz parte da chave primária depende da chave inteira, e não apenas de uma parte dela. Essa forma normal é relevante principalmente quando a chave primária é composta.

Considere:

**ItemVenda** (`id_venda`, `id_produto`)

| id_venda | id_produto | quantidade | nome_produto |
|---|---|---:|---|
| 101 | 10 | 1 | Caneta |
| 101 | 20 | 2 | Caderno |

A chave é composta por `(id_venda, id_produto)`. A `quantidade` depende da venda e do produto juntos, mas `nome_produto` depende apenas de `id_produto`. Portanto, `nome_produto` depende de apenas uma parte da chave, violando a 2FN.

Para corrigir, separamos os dados do produto dos dados específicos do item vendido:

**Produto**

| id_produto | nome_produto |
|---|---|
| 10 | Caneta |
| 20 | Caderno |

**ItemVenda**

| id_venda | id_produto | quantidade |
|---|---|---:|
| 101 | 10 | 1 |
| 101 | 20 | 2 |

Assim, `quantidade` permanece dependente da chave composta inteira, enquanto o nome fica armazenado uma única vez em `Produto`.

#### Para refletir

A violação da 2FN nesse caso também pode ser evitada com uma boa identificação dos conceitos no modelo conceitual. O `nome_produto` é uma característica de `Produto`, e não da participação do produto em uma venda. Ao modelar `Produto` como uma entidade e `quantidade` como um atributo do relacionamento entre `Venda` e `Produto`, a transformação para o modelo lógico separa naturalmente os dados do produto dos dados do item vendido.

Assim, embora a 2FN seja verificada no modelo relacional, decisões corretas no modelo conceitual ajudam a impedir que atributos dependentes apenas de parte de uma chave composta sejam colocados na tabela errada.

### Terceira Forma Normal (3FN)

Uma tabela está na **Terceira Forma Normal** quando está na 2FN e nenhum atributo que não faz parte da chave depende de outro atributo que também não faz parte da chave. Em outras palavras, não deve haver dependência transitiva entre atributos não chave.

Considere:

**Produto** (`id_produto`)

| id_produto | nome_produto | id_categoria | nome_categoria |
|---|---|---|---|
| 10 | Caneta | 1 | Papelaria |
| 20 | Caderno | 1 | Papelaria |

O `id_produto` determina `id_categoria`, e `id_categoria` determina `nome_categoria`. Logo, `nome_categoria` depende indiretamente de `id_produto`, por meio de `id_categoria`. Essa dependência transitiva viola a 3FN e faz o nome da categoria se repetir.

A solução é criar uma tabela própria para a categoria:

**Produto**

| id_produto | nome_produto | id_categoria |
|---|---|---|
| 10 | Caneta | 1 |
| 20 | Caderno | 1 |

**Categoria**

| id_categoria | nome_categoria |
|---|---|
| 1 | Papelaria |

Agora cada atributo não chave depende diretamente da chave da sua própria tabela, e o `id_categoria` pode ser usado como chave estrangeira em `Produto`.

#### Para refletir

A violação da 3FN nesse caso ocorre porque `nome_categoria`, embora apareça na tabela `Produto`, é uma característica de `Categoria`. Ao identificar `Categoria` como uma entidade e relacioná-la a `Produto`, o modelo conceitual orienta a criação de uma tabela própria para a categoria e evita a repetição de seu nome.

Assim, mesmo que a dependência transitiva seja uma questão do modelo relacional, reconhecer no modelo conceitual a independência e a responsabilidade de cada conceito ajuda a evitar que um atributo não chave dependa de outro atributo não chave.

## Atividade prática: revisão do modelo da Aula 1

Retome o modelo desenvolvido na Aula 1 e verifique se as tabelas geradas estão nas três primeiras formas normais. Analise as dependências entre os atributos e procure violações da 1FN, da 2FN ou da 3FN.

Como dica, reflita especialmente sobre a dependência entre a `raça` e o `tipo_animal`, cujos valores podem ser, por exemplo, `cachorro` e `gato`. Pergunte-se se essa informação está sendo repetida para vários animais, se um atributo não chave determina outro e se `raça` e `tipo_animal` deveriam pertencer a uma entidade ou relacionamento próprio.

Depois:

1. crie uma nova versão do modelo conceitual, com os conceitos e relacionamentos necessários para representar corretamente essas dependências;
2. gere um novo modelo lógico e verifique se ele está na 1FN, na 2FN e na 3FN;
3. gere o modelo físico e o script SQL correspondente;
4. compare os novos modelos com os produzidos na Aula 1 e registre quais repetições ou dependências inadequadas foram eliminadas.

Observe que o problema pode ser resolvido diretamente no modelo conceitual, identificando uma entidade ou relacionamento que não havia sido percebido. Também é possível manter o modelo conceitual original e corrigir a estrutura apenas no modelo lógico, decompondo as tabelas. Compare as duas alternativas e observe como uma boa decisão conceitual costuma tornar a transformação para o modelo lógico mais natural.

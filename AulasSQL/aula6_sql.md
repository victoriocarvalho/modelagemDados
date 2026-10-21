# Aula 6 — Subconsultas

Nas aulas anteriores, aprendemos a consultar e filtrar registros, agrupar resultados e combinar tabelas com junções. Em algumas situações, o resultado de uma consulta pode ser usado por outra consulta. Chamamos essa consulta interna de **subconsulta**.

O objetivo desta aula é compreender como uma subconsulta funciona e utilizá-la em situações em que seu resultado ajuda a responder uma pergunta. Também vamos comparar uma subconsulta com `JOIN` e discutir por que não devemos substituir uma junção por uma subconsulta sem necessidade.

Nesta aula estudaremos:

- o conceito de subconsulta;
- subconsultas que retornam um único valor;
- subconsultas correlacionadas, que dependem de cada linha da consulta externa;
- quando uma junção é mais apropriada;
- como avaliar possíveis impactos de desempenho.

## O que é uma subconsulta?

Uma subconsulta é um comando `SELECT` escrito dentro de outro comando SQL. Normalmente, ela fica entre parênteses. A consulta interna obtém um valor ou um conjunto de valores, que é utilizado pela consulta externa.

Por exemplo, podemos querer descobrir quem recebe o maior salário. Primeiro, uma consulta calcula o maior salário; depois, a consulta externa procura os funcionários que recebem esse valor:

```sql
SELECT nome, salario
FROM funcionario
WHERE salario = (
    SELECT MAX(salario)
    FROM funcionario
);
```

A subconsulta `SELECT MAX(salario) FROM funcionario` retorna um único valor. A consulta externa compara o salário de cada funcionário com esse valor.

Se mais de um funcionário tiver o maior salário, todos serão retornados. Isso é adequado quando queremos identificar todas as pessoas empatadas na maior remuneração.

## Maior salário de cada departamento

Agora queremos encontrar o nome e o salário do funcionário mais bem remunerado de cada departamento. A subconsulta abaixo calcula o maior salário do departamento do funcionário analisado pela consulta externa:

```sql
SELECT d.nome AS nome_departamento,
       f.nome AS nome_funcionario,
       f.salario
FROM funcionario AS f
INNER JOIN departamento AS d
    ON d.id_departamento = f.id_departamento
WHERE f.salario = (
    SELECT MAX(f2.salario)
    FROM funcionario AS f2
    WHERE f2.id_departamento = f.id_departamento
)
ORDER BY d.nome, f.nome;
```

Observe que a subconsulta usa `f2` para consultar a tabela `funcionario` novamente. A condição `f2.id_departamento = f.id_departamento` compara o departamento da subconsulta com o departamento do funcionário da consulta externa.

Essa dependência da linha externa caracteriza uma **subconsulta correlacionada**. Conceitualmente, para cada funcionário da consulta externa, verificamos o maior salário do departamento ao qual ele pertence. Se houver empate no maior salário de um departamento, todos os funcionários empatados serão exibidos.

Uma consulta com `GROUP BY` poderia informar o maior salário de cada departamento, mas não seria suficiente, por si só, para identificar o nome do funcionário que recebe esse salário. A subconsulta correlacionada permite comparar cada funcionário com o máximo calculado para seu departamento.

## Subconsulta ou JOIN?

Suponha que queremos obter os funcionários que trabalham no departamento chamado `Tecnologia`. Como a consulta precisa relacionar cada funcionário ao departamento, `JOIN` é a forma mais direta:

```sql
SELECT f.nome AS nome_funcionario,
       f.cargo,
       f.salario,
       d.nome AS nome_departamento
FROM funcionario AS f
INNER JOIN departamento AS d
    ON d.id_departamento = f.id_departamento
WHERE d.nome = 'Tecnologia';
```

Podemos expressar um filtro semelhante com uma subconsulta:

```sql
SELECT f.nome AS nome_funcionario,
       f.cargo,
       f.salario
FROM funcionario AS f
WHERE f.id_departamento IN (
    SELECT d.id_departamento
    FROM departamento AS d
    WHERE d.nome = 'Tecnologia'
);
```

A subconsulta encontra os identificadores dos departamentos chamados `Tecnologia`; a consulta externa seleciona os funcionários vinculados a esses identificadores. Usamos `IN` porque o nome do departamento não é necessariamente único: a consulta interna pode retornar mais de um identificador. Um `=` exigiria que a subconsulta retornasse no máximo uma linha.

As duas formas podem ser úteis, mas neste caso `JOIN` é mais claro: estamos relacionando funcionários e departamentos, e ainda podemos exibir campos das duas tabelas. Use subconsultas para situações em que o resultado de uma consulta interna realmente seja necessário, como comparar um valor com o salário máximo. Não use uma subconsulta apenas para reescrever uma junção que expressa diretamente o relacionamento entre as tabelas.

Uma situação comum para usar `IN` é verificar se um registro está relacionado a pelo menos uma linha de outra tabela. Por exemplo, para listar os produtos que já foram vendidos:

```sql
SELECT p.nome
FROM produto AS p
WHERE p.id_produto IN (
    SELECT iv.id_produto
    FROM item_venda AS iv
);
```

A subconsulta retorna os identificadores dos produtos que aparecem em `item_venda`, e a consulta externa seleciona os produtos com esses identificadores. Cada produto aparece uma única vez, mesmo que tenha sido vendido em várias vendas.

Também podemos obter esse resultado com um `JOIN`, mas um produto vendido mais de uma vez pode aparecer repetido. Para exibir cada produto apenas uma vez, acrescentamos `DISTINCT`:

```sql
SELECT DISTINCT p.nome
FROM produto AS p
INNER JOIN item_venda AS iv
    ON iv.id_produto = p.id_produto;
```

Portanto, `IN` é uma forma direta de expressar um teste de pertencimento; ele não resolve algo impossível com `JOIN`. A diferença prática é que `IN` expressa a intenção de verificar a existência de uma correspondência sem combinar as linhas no resultado.

De forma geral considere:

- usar `JOIN` quando precisar combinar registros relacionados ou retornar colunas de várias tabelas;
- usar uma subconsulta quando o resultado interno tiver um papel claro, como fornecer um valor para comparação ou um conjunto de identificadores para `IN`;

## Resumo da aula

- Uma subconsulta é um `SELECT` dentro de outro comando SQL.
- Uma subconsulta escalar, como `MAX(salario)`, retorna um valor que pode ser usado pela consulta externa.
- Uma subconsulta correlacionada consulta valores da linha atual da consulta externa.
- Para obter colunas relacionadas de várias tabelas, `JOIN` costuma expressar a intenção com mais clareza.

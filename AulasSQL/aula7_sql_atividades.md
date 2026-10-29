# Atividade da aula 7 — OUTER JOIN

**Atividade individual**

## Objetivo

Nesta atividade, você praticará `LEFT JOIN` e `RIGHT JOIN` para consultar registros relacionados, inclusive quando não existe uma correspondência na outra tabela. Os exercícios também retomam agregações, `GROUP BY`, `HAVING`, `WHERE`, ordenação e paginação.

Consideramos que esta atividade será realizada após a execução das atividades anteriores, usando o banco `Loja` já preparado. Os exercícios desta lista devem ser respondidos com consultas `SELECT` e, quando indicado, com junções externas.

## Como executar a atividade

1. Abra o banco `Loja` utilizado nas atividades anteriores.
2. Mantenha os dados criados e inseridos nas atividades anteriores.
3. Execute uma única vez o script da seção 1 antes de iniciar os exercícios. Ele acrescenta dados que permitem testar situações sem correspondência entre as tabelas.
4. Escreva uma consulta `SELECT` para cada exercício. Não altere nem remova dados do banco durante a resolução.
5. Nos exercícios que solicitam todos os registros de uma tabela, escolha a junção externa de modo que essa tabela seja preservada no resultado.

## 1. Preparação dos dados

Execute o script abaixo uma única vez. As verificações com `NOT EXISTS` evitam duplicação caso seja necessário executá-lo novamente.

```sql
INSERT INTO categoria (nome_categoria, percentual_icms)
SELECT 'Categoria sem Produtos - Outer Join', 10.00
WHERE NOT EXISTS (
    SELECT 1
    FROM categoria
    WHERE nome_categoria = 'Categoria sem Produtos - Outer Join'
);

INSERT INTO categoria (nome_categoria, percentual_icms)
SELECT 'Demonstração Outer Join', 10.00
WHERE NOT EXISTS (
    SELECT 1
    FROM categoria
    WHERE nome_categoria = 'Demonstração Outer Join'
);

INSERT INTO produto (
    codigo, nome, descricao, preco_venda, quantidade_estoque, id_categoria
)
SELECT 2999,
       'Produto sem Vendas - Outer Join',
       'Produto inserido para praticar junções externas.',
       49.90,
       12,
       c.id_categoria
FROM categoria AS c
WHERE c.nome_categoria = 'Demonstração Outer Join'
  AND NOT EXISTS (
      SELECT 1
      FROM produto
      WHERE codigo = 2999
  );

INSERT INTO cliente (
    cpf, nome_completo, data_nascimento, tipo_logradouro,
    nome_logradouro, numero, complemento, bairro, cidade,
    estado, data_cadastro
)
SELECT '999.999.999-99',
       'Cliente sem Compras - Outer Join',
       DATE '1990-01-15',
       'Rua',
       'das Consultas',
       '100',
       NULL,
       'Centro',
       'Vitória',
       'ES',
       CURRENT_DATE
WHERE NOT EXISTS (
    SELECT 1
    FROM cliente
    WHERE cpf = '999.999.999-99'
);

INSERT INTO vendedor (
    matricula, cpf, nome_completo, data_nascimento,
    tipo_logradouro, nome_logradouro, numero, complemento,
    bairro, cidade, estado, salario, percentual_comissao
)
SELECT 9999,
       '888.888.888-88',
       'Vendedor sem Vendas - Outer Join',
       DATE '1988-08-20',
       'Avenida',
       'das Consultas',
       '200',
       NULL,
       'Centro',
       'Vitória',
       'ES',
       2500.00,
       5.00
WHERE NOT EXISTS (
    SELECT 1
    FROM vendedor
    WHERE matricula = 9999
);

INSERT INTO venda (numero, data_venda, id_cliente, id_vendedor)
SELECT 7999,
       DATE '2026-12-20',
       (SELECT MIN(id_cliente) FROM cliente),
       (SELECT MIN(id_vendedor) FROM vendedor)
WHERE NOT EXISTS (
    SELECT 1
    FROM venda
    WHERE numero = 7999
);
```

O script cria uma categoria sem produtos, um produto sem vendas, um cliente sem compras, um vendedor sem vendas e uma venda sem itens. Confira se esses registros foram inseridos antes de iniciar os exercícios.

## 2. Exercícios

### 2.1 Junções externas básicas

1. Exiba o nome de todas as categorias e, quando houver, o nome dos produtos pertencentes a cada categoria. Organize o resultado pelo nome da categoria e, dentro de cada categoria, pelo nome do produto.

2. Exiba o nome de todos os produtos e o nome de sua categoria. Inclua também as categorias que não possuem produtos. Use `RIGHT JOIN` nesta consulta e ordene pelo nome da categoria e pelo nome do produto.

3. Exiba o nome completo de todos os clientes, o número e a data de suas vendas. Inclua os clientes que não possuem vendas e ordene pelo nome do cliente e pela data da venda.

4. Exiba o nome completo de todos os vendedores, o número e a data de suas vendas. Inclua os vendedores que não realizaram vendas. Use `RIGHT JOIN` e ordene pelo nome do vendedor e pela data da venda.

5. Exiba o número e a data de todas as vendas, juntamente com o nome dos produtos presentes em seus itens. Inclua as vendas que não possuem itens e ordene pelo número da venda e pelo nome do produto.

6. Exiba o nome de todos os produtos e o número das vendas nas quais cada um apareceu. Inclua os produtos que ainda não foram vendidos e ordene pelo nome do produto e pelo número da venda.

### 2.2 Identificando registros sem correspondência

7. Exiba o nome das categorias que não possuem produtos cadastrados. Ordene pelo nome da categoria.

8. Exiba o código e o nome dos produtos que ainda não apareceram em nenhum item de venda. Ordene pelo nome do produto.

9. Exiba o nome completo dos clientes que não possuem vendas registradas. Ordene alfabeticamente.

10. Exiba a matrícula e o nome completo dos vendedores que não realizaram vendas. Ordene pelo nome completo.

11. Exiba o número e a data das vendas que não possuem itens registrados. Ordene da venda mais recente para a mais antiga.

12. Exiba o nome completo dos clientes que não possuem telefone cadastrado. Ordene pelo nome completo.

13. Exiba a matrícula e o nome completo dos vendedores que não possuem telefone cadastrado. Ordene pelo nome completo.

14. Exiba o nome de cada categoria e o nome de cada produto associado, mas retorne somente as linhas que representam categorias sem produtos. Ordene pelo nome da categoria.

### 2.3 Contagens e agregações com junções externas

15. Para cada categoria, informe o nome e a quantidade de produtos associados, incluindo as categorias sem produtos. Ordene da maior para a menor quantidade e, em caso de empate, pelo nome da categoria.

16. Para cada cliente, informe o nome completo e a quantidade de vendas registradas, incluindo os clientes sem vendas. Ordene do maior para o menor número de vendas e, em caso de empate, pelo nome do cliente.

17. Para cada vendedor, informe a matrícula, o nome completo e a quantidade de vendas realizadas, incluindo os vendedores sem vendas. Ordene do maior para o menor número de vendas e, em caso de empate, pelo nome do vendedor.

18. Para cada venda, informe seu número, sua data e a quantidade de produtos diferentes registrados nos itens. Inclua as vendas sem itens e ordene pela data mais recente.

19. Para cada categoria, informe o nome, a quantidade de produtos, o menor preço, o maior preço e o preço médio dos produtos. Inclua as categorias sem produtos e ordene pelo nome da categoria.

20. Para cada cliente, informe o nome completo, a quantidade total de unidades compradas e o valor total gasto. Inclua os clientes sem compras e ordene do maior para o menor valor total gasto.

21. Para cada vendedor, informe o nome completo, a quantidade total de unidades vendidas e o valor total vendido. Inclua os vendedores que não realizaram vendas e ordene do maior para o menor valor total vendido.

22. Para cada categoria, informe o nome, a quantidade total de unidades vendidas e o valor total vendido. Inclua as categorias cujos produtos não foram vendidos e ordene do maior para o menor valor total vendido.

### 2.4 Filtros e junções externas mais elaboradas

23. Exiba o nome das categorias que possuem menos de dois produtos, incluindo as categorias sem produtos. Mostre também a quantidade de produtos de cada categoria e ordene pelo nome.

24. Exiba o nome completo dos clientes que realizaram menos de duas compras, incluindo aqueles que não realizaram nenhuma. Mostre também a quantidade de vendas de cada cliente e ordene pelo nome.

25. Exiba o nome completo dos vendedores que realizaram menos de duas vendas, incluindo aqueles que não realizaram nenhuma. Mostre também a quantidade de vendas de cada vendedor e ordene pelo nome.

26. Considerando apenas as vendas realizadas em 2026, exiba o nome completo de todos os clientes e a quantidade de vendas realizadas por cada um naquele ano. Inclua os clientes que não fizeram vendas em 2026 e ordene do maior para o menor número de vendas.

27. Considerando apenas as vendas realizadas em 2026, exiba o nome completo de todos os vendedores e o valor total vendido por cada um naquele ano. Inclua os vendedores que não realizaram vendas em 2026 e ordene do maior para o menor valor vendido.

28. Considerando somente os produtos da categoria `Eletrônicos`, exiba o nome completo de todos os clientes e o número das vendas em que compraram produtos dessa categoria. Inclua os clientes que não compraram produtos da categoria `Eletrônicos` e ordene pelo nome do cliente e pelo número da venda.

29. Exiba o nome de cada categoria, a quantidade de produtos cadastrados e a quantidade total de unidades vendidas de seus produtos. Inclua as categorias sem produtos e as categorias cujos produtos ainda não foram vendidos. Retorne apenas as categorias com até dois produtos e ordene pelo nome.

30. Exiba o nome completo de cada vendedor, a quantidade de vendas realizadas em 2026 e o valor total vendido nesse ano. Inclua os vendedores sem vendas em 2026. Retorne somente os vendedores cujo valor total vendido seja inferior a 1.000 ou que não tenham vendido nesse ano. Ordene primeiro pelo valor total vendido, do menor para o maior, e depois pelo nome do vendedor.

## Entrega

Entregue um único arquivo com extensão `.sql`, contendo as respostas dos 30 exercícios. Para cada questão, inclua o número e o enunciado em um comentário SQL, seguidos da consulta elaborada para respondê-la. Organize o arquivo na mesma ordem dos exercícios. Por exemplo:

```sql
-- 1. Exiba o nome de todas as categorias e, quando houver, o nome dos produtos pertencentes a cada categoria.
SELECT c.nome_categoria,
       p.nome AS nome_produto
FROM categoria AS c
LEFT JOIN produto AS p
    ON p.id_categoria = c.id_categoria;
```

Não é necessário incluir os resultados das consultas, explicações ou textos fora dos comentários que identificam cada questão. Todas as respostas devem ser consultas `SELECT`; não altere nem remova dados do banco.

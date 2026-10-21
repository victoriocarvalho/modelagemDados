# Atividade da aula 5 — Funções de agregação

**Atividade individual**

## Objetivo

Nesta atividade, você praticará as funções `COUNT`, `MIN`, `MAX`, `AVG` e `SUM`, o agrupamento com `GROUP BY` e a filtragem de grupos com `HAVING`. Também usará `WHERE`, junções, ordenação e paginação em consultas de resumo.

Consideramos que esta atividade será realizada depois da execução das atividades anteriores, usando o banco `Loja` já preparado. Os exercícios devem ser resolvidos com os recursos estudados até a aula 5. 

## 1. Agregações em uma tabela

1. Informe a quantidade total de produtos cadastrados.

2. Na tabela de telefones, informe a quantidade de registros associados a clientes e quantos estão associados a vendedores.

3. Informe o preço médio de venda de todos os produtos.

4. Informe o menor e o maior preço de venda entre os produtos.

5. Calcule a quantidade total de unidades em estoque, somando o estoque de todos os produtos.

6. Informe quantos produtos existem em cada categoria, exibindo o identificador da categoria.

7. Para cada categoria, exiba o preço médio, o menor preço e o maior preço de seus produtos.

8. Para cada categoria, calcule o total de unidades em estoque. Ordene as categorias da maior para a menor quantidade total e exiba somente as três primeiras.

## 2. Agregações usando mais de uma tabela

9. Exiba o nome de cada categoria e a quantidade de produtos associados a ela.

10. Para cada categoria, exiba o nome, o preço médio e o maior preço de venda de seus produtos.

11. Para cada categoria, exiba o nome, a quantidade de produtos e o total de unidades em estoque.

12. Exiba o nome completo de cada vendedor e a quantidade de vendas realizadas por ele.

13. Exiba o nome completo de cada cliente e a quantidade de vendas registradas para ele.

14. Para cada venda, exiba seu número e a quantidade de itens diferentes registrados nela.

15. Para cada vendedor, calcule a quantidade total de unidades vendidas e o valor total vendido, considerando todos os itens de suas vendas.

16. Para cada categoria, calcule a quantidade total de unidades vendidas.

17. Para cada categoria, calcule o valor total vendido. Considere o preço praticado em cada item da venda, multiplicado pela quantidade vendida, e organize as categorias do maior para o menor valor total.

18. Para cada cliente, calcule a quantidade total de unidades compradas e o valor total gasto em suas compras.

## 3. Filtrando grupos com HAVING

19. Considerando somente os clientes do Espírito Santo, informe quantos clientes há em cada cidade. Exiba apenas as cidades que possuem mais de um cliente.

20. Considerando somente produtos com estoque maior que zero, informe quantos produtos há em cada categoria. Exiba apenas as categorias com mais de um produto em estoque.

21. Para cada categoria, considere somente os produtos com preço de venda igual ou superior a 100. Calcule o preço médio e exiba apenas as categorias cuja média seja maior que 200.

22. Exiba o nome dos vendedores que realizaram mais de uma venda e a quantidade de vendas de cada um.

23. Exiba o nome dos clientes que possuem pelo menos duas vendas registradas e a quantidade de vendas de cada um.

24. Para cada produto vendido, calcule a quantidade total de unidades vendidas. Exiba somente os produtos cuja quantidade total vendida seja maior que uma unidade.

25. Para cada venda, calcule a quantidade total de unidades incluídas em seus itens. Exiba somente as vendas com mais de uma unidade.

26. Considerando apenas as vendas realizadas em 2026, calcule o valor total vendido em cada categoria. Exiba somente as categorias cujo total seja superior a 500.

27. Considerando apenas as vendas realizadas em 2026, calcule para cada vendedor a quantidade de vendas e o valor total vendido. Exiba somente os vendedores cujo valor total vendido seja superior a 500.

28. Considerando somente os itens de produtos da categoria `Eletrônicos`, calcule por produto a quantidade total vendida. Exiba apenas os produtos com mais de uma unidade vendida.

29. Para cada categoria, calcule a quantidade de unidades vendidas. Exiba somente as categorias com pelo menos uma unidade vendida, ordenando da maior para a menor quantidade, e limite o resultado às três primeiras categorias.

30. Para cada categoria que tenha preço médio de produtos superior a 100, exiba o nome da categoria, a quantidade de produtos e o preço médio. Ordene pela média, da maior para a menor, e apresente a segunda página, considerando três categorias por página.

## Entrega

Entregue um único arquivo com extensão `.sql`, contendo as respostas dos 30 exercícios. Para cada questão, inclua o número e o enunciado em um comentário SQL, seguidos do script elaborado para respondê-la. Organize o arquivo na mesma ordem dos exercícios. Por exemplo:

```sql
-- 1. Informe a quantidade total de produtos cadastrados.
SELECT COUNT(*) AS quantidade_produtos
FROM produto;
```

Não é necessário incluir os resultados das consultas, explicações ou textos fora dos comentários que identificam cada questão. Todas as respostas devem ser consultas `SELECT`; não altere nem remova dados do banco.

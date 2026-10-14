# Atividade — Consultando dados com INNER JOIN

**Atividade individual**

## Objetivo

Nesta atividade você praticará o uso de `INNER JOIN` para consultar, alterar e remover dados relacionados que estão armazenados em tabelas diferentes.

Os exercícios também praticarão:

- relacionamento entre chaves primárias e chaves estrangeiras;
- junções envolvendo duas tabelas;
- junções envolvendo três ou mais tabelas;
- filtros com `WHERE` em consultas com junções;
- uso de junções em `UPDATE` e `DELETE`.

Será utilizado o mesmo banco `Loja` das atividades anteriores. Em cada exercício, todas as tabelas necessárias deverão ser relacionadas por meio de `INNER JOIN`.

## Como executar a atividade

1. Abra o banco `Loja` utilizado nas atividades das aulas 1 e 2.
2. Mantenha os dados inseridos no script inicial da atividade da aula 2.
3. Se você já executou os `UPDATEs` e `DELETEs` da atividade da aula 2, prefira usar uma cópia do banco antes dessas alterações ou restaure os dados necessários.
4. Execute uma única vez o script da seção 1 para acrescentar uma venda de um produto da categoria `Eletrônicos` realizada em 2026.
5. Execute primeiro todos os exercícios de `SELECT`. Deixe os exercícios de `UPDATE` e `DELETE` para o final, pois eles modificam os dados.
6. Antes de cada `UPDATE` ou `DELETE`, faça uma consulta de conferência com as mesmas junções e condições para identificar os registros que serão afetados.
7. Não utilize produto cartesiano. Relacione as tabelas pelas chaves correspondentes.

Os exercícios não fornecem os comandos SQL. Escreva os scripts a partir da descrição do domínio.

## 1. Preparação dos dados

Execute uma única vez o script abaixo. Ele acrescenta uma venda realizada em 2026 para um produto da categoria `Eletrônicos`, garantindo resultados para os exercícios que consultam essa situação.

```sql
INSERT INTO venda (numero, data_venda, id_cliente, id_vendedor)
VALUES (
    7001,
    DATE '2026-05-10',
    (SELECT id_cliente
     FROM cliente
     WHERE nome_completo = 'Eduardo Martins'),
    (SELECT id_vendedor
     FROM vendedor
     WHERE nome_completo = 'Marina Alves')
);

INSERT INTO item_venda (
    id_venda, id_produto, quantidade, preco_vendido
)
VALUES (
    (SELECT id_venda
     FROM venda
     WHERE numero = 7001),
    (SELECT id_produto
     FROM produto
     WHERE codigo = 2006),
    1,
    (SELECT preco_venda
     FROM produto
     WHERE codigo = 2006)
);
```

O produto de código `2006` foi inserido na atividade da aula 2 na categoria `Eletrônicos`. Confira se a venda e o item foram inseridos antes de iniciar os exercícios.

## 2. Exercícios de SELECT

Escreva uma consulta para cada exercício. Todas as consultas devem utilizar `INNER JOIN` para relacionar as tabelas envolvidas.

### 2.1 Junções envolvendo duas tabelas

1. Selecione o nome de cada produto e o nome da respectiva categoria.

2. Selecione o nome e o preço de venda dos produtos pertencentes à categoria `Eletrônicos`.

3. Selecione o nome da categoria, o nome do produto e o preço de venda dos produtos cujo preço seja maior que 100.

4. Selecione o nome completo de cada cliente, o número da venda e a data da venda correspondente.

5. Selecione o nome completo dos vendedores, o número e a data das vendas realizadas em abril de 2026.

### 2.2 Junções envolvendo três ou mais tabelas

6. Selecione o nome completo do cliente, o nome completo do vendedor, o número e a data de cada venda.

7. Selecione o número da venda, o nome do produto, a quantidade e o preço praticado em cada item de venda.

8. Selecione o nome completo dos clientes e o nome dos produtos comprados por eles.

9. Selecione o nome completo do cliente e o nome do produto de todos os clientes que compraram algum produto da categoria `Eletrônicos` em 2026.

10. Selecione o nome completo do vendedor, o nome completo do cliente, o nome do produto e a data das vendas realizadas em 2026.

11. Selecione o nome da categoria, o nome do produto, o número da venda, a quantidade e o preço praticado nos itens vendidos.

12. Selecione o nome completo dos clientes, o nome da categoria e o nome dos produtos da categoria `Acessórios` comprados por esses clientes.

13. Selecione o nome completo dos vendedores, o nome da categoria e o nome dos produtos vendidos por cada vendedor.

14. Selecione o nome completo dos clientes e seus telefones para os clientes que possuem pelo menos uma venda registrada.

15. Selecione o nome completo dos vendedores e seus telefones para os vendedores que realizaram pelo menos uma venda.

16. Selecione o nome da categoria, o nome do produto e o número das vendas nas quais cada produto foi vendido.

17. Selecione o nome completo dos clientes e o nome dos produtos com preço de venda superior a 500 que foram comprados por eles.

18. Selecione o nome completo dos vendedores e o nome completo dos clientes das vendas realizadas para clientes do estado do Espírito Santo.

19. Selecione o nome do produto, o nome da categoria e o número da venda dos itens cuja quantidade seja maior que 1.

20. Selecione o nome completo do cliente, o nome completo do vendedor, o nome da categoria e o nome do produto para cada item vendido em 2026.

## 3. Exercícios de UPDATE

Antes de cada alteração, faça uma consulta com as mesmas junções e condições para conferir os registros que serão afetados. Depois execute o `UPDATE` e consulte novamente os registros modificados.

21. Conceda um reajuste de 10% no salário dos vendedores que realizaram vendas em abril de 2026.

22. Aumente em 5% o preço de venda dos produtos pertencentes à categoria `Acessórios`.

23. Altere o percentual de comissão para 8 dos vendedores que realizaram vendas para clientes do estado do Espírito Santo.

## 4. Exercício de DELETE

Realize este exercício por último. Antes da exclusão, faça uma consulta com as mesmas junções e condições para conferir os registros. Não remova registros diferentes dos solicitados.

24. Remova os produtos da categoria `Descontinuados` que possuem estoque igual a zero.

## 5. Entrega

Entregue um único arquivo com extensão `.sql` contendo as respostas dos 24 exercícios.

O arquivo deve conter apenas, para cada questão, o número e o enunciado escritos em um comentário SQL, seguidos do script elaborado para responder à questão. Organize o arquivo na mesma ordem dos exercícios. Por exemplo:

```sql
-- 1. Selecione o nome de cada produto e o nome da respectiva categoria.
SELECT p.nome, c.nome_categoria
FROM produto AS p
INNER JOIN categoria AS c
    ON c.id_categoria = p.id_categoria;
```

Não é necessário incluir resultados das consultas, explicações ou textos fora dos comentários que identificam cada questão.

# Atividade da aula 6 — Subconsultas

**Atividade individual**

## Objetivo

Nesta atividade, você praticará subconsultas escalares, subconsultas que retornam conjuntos de valores e subconsultas com funções de agregação. A lista aumenta gradualmente de dificuldade e combina subconsultas com recursos estudados anteriormente.

Consideramos que esta atividade será realizada depois da execução das atividades anteriores, usando o banco `Loja` já preparado. Use subconsultas para atender aos enunciados e combine-as com `JOIN` quando precisar obter dados relacionados de outra tabela. Não use subconsultas apenas para substituir uma junção que expresse diretamente o relacionamento entre tabelas.

## Exercícios

1. Selecione o nome e o preço de venda dos produtos cujo preço seja maior que o preço médio de todos os produtos. Ordene do mais caro para o mais barato.

2. Selecione a matrícula, o nome completo e o salário dos vendedores que recebem o maior salário da empresa. Se houver empate, apresente todos os vendedores empatados.

3. Selecione o nome e o preço de venda dos produtos que já apareceram em pelo menos um item de venda.

4. Selecione o nome completo dos clientes que possuem pelo menos uma venda registrada. Ordene os nomes alfabeticamente.

5. Selecione o nome das categorias cujo preço médio dos produtos associados seja maior que 100. Ordene o resultado pelo nome da categoria.

6. Selecione a matrícula, o nome completo, o estado e o salário dos vendedores que recebem acima da média salarial dos vendedores do Espírito Santo. Ordene do maior para o menor salário.

7. Selecione o código e o nome dos produtos que nunca apareceram em um item de venda. Ordene os produtos pelo nome.

8. Selecione o nome completo dos clientes que possuem pelo menos duas vendas registradas. Ordene os nomes alfabeticamente.

9. Para cada categoria, selecione o nome da categoria, o nome do produto e o preço de venda dos produtos que possuem o maior preço naquela categoria. Se houver empate, apresente todos os produtos empatados. Ordene pelo nome da categoria e pelo nome do produto.

10. Para cada estado em que há vendedores cadastrados, identifique o nome completo e o salário do(s) vendedor(es) que recebe(m) o maior salário naquele estado. Ordene pelo estado e pelo nome do vendedor.

## Entrega

Entregue um único arquivo com extensão `.sql`, contendo as respostas dos dez exercícios. Para cada questão, inclua o número e o enunciado em um comentário SQL, seguidos da consulta elaborada para respondê-la. Organize o arquivo na mesma ordem dos exercícios. Por exemplo:

```sql
-- 1. Selecione o nome e o preço de venda dos produtos cujo preço seja maior que o preço médio de todos os produtos.
SELECT nome, preco_venda
FROM produto
WHERE preco_venda > (
    SELECT AVG(preco_venda)
    FROM produto
);
```

Não é necessário incluir os resultados das consultas, explicações ou textos fora dos comentários que identificam cada questão. Todas as respostas devem ser consultas `SELECT`; não altere nem remova dados do banco.

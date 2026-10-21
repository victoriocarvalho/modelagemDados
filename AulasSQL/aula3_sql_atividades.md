# Atividade da aula 3 — Ordenação e paginação

**Atividade individual**

## Objetivo

Nesta atividade, você praticará a ordenação e a paginação de resultados usando `ORDER BY`, `LIMIT` e `OFFSET`.

Será utilizado o mesmo banco `Loja` das atividades anteriores. Para manter o foco nos comandos desta aula, cada exercício deve consultar apenas uma tabela.

## Como executar a atividade

Consideramos que esta atividade será realizada depois da execução das atividades anteriores, usando o banco `Loja` já preparado.

Para garantir que haja mais de nove produtos, como necessário para alguns exercícios, execute o `INSERT` abaixo uma única vez:

```sql
INSERT INTO produto (
    codigo, nome, descricao, preco_venda, quantidade_estoque, id_categoria
)
VALUES (
    3001,
    'Bomba portátil',
    'Bomba de ar portátil para bicicletas',
    79.90,
    22,
    4
);
```

Os exercícios não fornecem os comandos SQL. Escreva as consultas a partir das descrições.

## Exercícios

1. Selecione o código e o nome de todos os produtos, organizando o resultado em ordem alfabética pelo nome.

2. Selecione a matrícula, o nome completo e o salário de todos os vendedores, do maior para o menor salário.

3. Selecione o nome, o identificador da categoria, o preço de venda e a quantidade em estoque dos produtos. Organize primeiro pelo identificador da categoria em ordem crescente; dentro de cada categoria, pelo estoque do maior para o menor; e, em caso de empate, pelo nome em ordem alfabética.

4. Selecione todos os dados de até cinco produtos, sem definir uma ordem específica para o resultado.

5. Selecione o nome e o preço de venda de todos os produtos, ordenando-os pelo preço do maior para o menor. Em caso de empate no preço, use o identificador do produto em ordem crescente.

6. Partindo da consulta anterior, apresente somente os três produtos com os maiores preços de venda.

7. Usando a mesma ordenação do exercício 5, apresente os produtos que ocupam da quarta à sexta posição na listagem.

8. Usando a mesma ordenação do exercício 5, apresente os produtos que ocupam da sétima à nona posição na listagem.

9. Organize os clientes em ordem alfabética pelo nome completo e obtenha os resultados em páginas de cinco clientes. Apresente as consultas para a primeira e a segunda página. Se houver nomes iguais, use o identificador do cliente como critério adicional de ordenação.

10. Organize os produtos do menor para o maior estoque; em caso de empate, ordene pelo preço de venda do maior para o menor e, persistindo o empate, pelo identificador do produto. Apresente a terceira página, considerando quatro produtos por página.

## Entrega

Entregue um único arquivo com extensão `.sql`, contendo as respostas dos dez exercícios. Para cada questão, inclua apenas o número e o enunciado em um comentário SQL, seguidos da consulta criada para respondê-la. Organize o arquivo na mesma ordem dos exercícios. Por exemplo:

```sql
-- 1. Selecione o código e o nome de todos os produtos, organizando o resultado em ordem alfabética pelo nome.
SELECT codigo, nome
FROM produto
ORDER BY nome;
```

Não é necessário incluir os resultados das consultas, explicações ou textos fora dos comentários que identificam cada questão.

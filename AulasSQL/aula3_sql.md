# Aula 3 — Ordenação e paginação de resultados

É muito comum que uma consulta retorne muitas linhas. Em vez de apresentar todos os resultados de uma só vez, podemos ordená-los e dividi-los em partes menores, chamadas páginas. Isso facilita a leitura e é especialmente útil em aplicações e sites.

Nesta aula, vamos estudar três recursos que permitem ordenar e paginar resultados: `ORDER BY`, `LIMIT` e `OFFSET`.

## Ordenando resultados com ORDER BY

Por padrão, o banco de dados não garante uma ordem específica para as linhas retornadas por uma consulta. Para definir a ordem dos resultados, usamos `ORDER BY`.

O exemplo abaixo lista os funcionários em ordem alfabética pelo nome:

```sql
SELECT nome, cargo, salario
FROM funcionario
ORDER BY nome ASC;
```

`ASC` indica ordem crescente. Para textos, isso corresponde à ordem alfabética; para números e datas, corresponde do menor para o maior e do mais antigo para o mais recente, respectivamente. Como `ASC` é o padrão, também poderíamos escrever apenas `ORDER BY nome`.

Para inverter a ordem, usamos `DESC`. Por exemplo, para listar os funcionários do maior para o menor salário:

```sql
SELECT nome, cargo, salario
FROM funcionario
ORDER BY salario DESC;
```

### Ordenando por mais de um critério

Podemos informar vários critérios separados por vírgulas. O banco aplica o primeiro critério e usa o seguinte para ordenar as linhas que empataram no anterior.

```sql
SELECT nome, id_departamento, salario
FROM funcionario
ORDER BY id_departamento ASC,
         salario DESC,
         nome ASC;
```

Primeiro, os funcionários são organizados pelo identificador do departamento em ordem crescente. Dentro de cada departamento, são ordenados pelo salário do maior para o menor. Se dois funcionários do mesmo departamento tiverem o mesmo salário, seus nomes são usados como critério de desempate, em ordem alfabética.

## Limitando a quantidade de resultados com LIMIT

`LIMIT` restringe o número máximo de linhas retornadas. Ele pode ser usado sem `ORDER BY`:

```sql
SELECT nome, cargo, salario
FROM funcionario
LIMIT 5;
```

Essa consulta retorna no máximo cinco linhas. Como não há `ORDER BY`, não há garantia de quais funcionários serão retornados nem da ordem em que aparecerão. Para escolher resultados de maneira previsível, normalmente combinamos `LIMIT` com uma ordenação.

### Combinando ORDER BY e LIMIT

Para listar os três funcionários com maiores salários:

```sql
SELECT nome, salario
FROM funcionario
ORDER BY salario DESC
LIMIT 3;
```

`ORDER BY` organiza os salários do maior para o menor e `LIMIT 3` restringe o resultado a três linhas. Se houver empate na posição de corte — por exemplo, vários funcionários empatados no terceiro maior salário — a consulta ainda retornará no máximo três linhas. Sem outro critério de ordenação, não há garantia de qual funcionário empatado será incluído. Para tornar a escolha previsível, podemos acrescentar um critério de desempate, como `nome ASC`.

## Paginação com OFFSET

`OFFSET` indica quantas linhas ordenadas devem ser ignoradas antes de começar a apresentar os resultados. Combinado com `LIMIT`, permite buscar uma página por vez.

Para listar os funcionários em ordem alfabética, cinco por página:

```sql
SELECT id_funcionario, nome, cargo, salario
FROM funcionario
ORDER BY nome ASC, id_funcionario ASC
LIMIT 5 OFFSET 0;
```

Essa consulta retorna a primeira página: até cinco funcionários, ordenados pelo nome. O identificador é um critério adicional para manter a ordem definida caso existam nomes iguais.

Para obter a segunda página, ignoramos os cinco registros da primeira:

```sql
SELECT id_funcionario, nome, cargo, salario
FROM funcionario
ORDER BY nome ASC, id_funcionario ASC
LIMIT 5 OFFSET 5;
```

Na terceira página, ignoramos os dez primeiros:

```sql
SELECT id_funcionario, nome, cargo, salario
FROM funcionario
ORDER BY nome ASC, id_funcionario ASC
LIMIT 5 OFFSET 10;
```

Assim, para páginas de cinco linhas, o `OFFSET` é `0` na primeira página, `5` na segunda, `10` na terceira e assim por diante. Em geral, para buscar uma página de número `n` com `t` linhas por página, usamos `LIMIT t OFFSET (n - 1) * t`.

### Paginação em sites

Esse recurso é muito útil na construção de sites e sistemas. Uma caixa de e-mail, por exemplo, pode mostrar dez mensagens por vez: a primeira página usa `LIMIT 10 OFFSET 0`, a segunda usa `LIMIT 10 OFFSET 10`, a terceira usa `LIMIT 10 OFFSET 20`, e assim sucessivamente.

Em aplicações reais, a consulta também deve usar uma ordenação consistente. Caso contrário, os registros podem aparecer em páginas diferentes ou mudar de posição entre consultas.

## Resumo da aula

- `ORDER BY` define a ordem dos resultados; use `ASC` para crescente e `DESC` para decrescente.
- É possível ordenar por vários critérios; cada critério seguinte ajuda a desempatar o anterior.
- `LIMIT` restringe o número máximo de linhas retornadas.
- Sem `ORDER BY`, não há garantia sobre quais linhas um `LIMIT` retornará.
- `OFFSET` ignora uma quantidade de linhas e, combinado com `LIMIT`, permite paginar resultados.
- Para resultados estáveis, use critérios de ordenação que desfaçam empates, como uma chave única ao final da ordenação.

# Atividade — SQL-DML: filtrando dados com WHERE

**Atividade individual**

## Objetivo

Nesta atividade você praticará o uso da cláusula `WHERE` nos comandos `SELECT`, `UPDATE` e `DELETE`.

Também serão praticados:

- condições com `AND` e `OR`;
- testes com `IS NULL`;
- pesquisas textuais com `LIKE`;
- funções de strings;
- consultas simples envolvendo datas;
- alterações e exclusões filtradas.

Será utilizado o mesmo banco `Loja` criado na atividade da aula 1. Os exercícios devem continuar usando scripts que consultam, alteram ou removem dados de apenas uma tabela por vez. Não utilize `JOIN`, subconsultas ou consultas envolvendo várias tabelas nos exercícios.

## Como executar a atividade

1. Abra o banco `Loja` utilizado na atividade da aula 1.
2. Confirme que as tabelas do modelo varejista já existem.
3. Execute uma única vez o script de inserção da seção 1 antes de iniciar os exercícios.
4. Se você estiver usando uma cópia do banco depois de concluir a atividade da aula 1, mantenha os registros já existentes. O script acrescentará novos dados com identificadores de domínio diferentes.
5. Se o script da seção 1 já tiver sido executado, não o execute novamente sem restaurar o banco, pois as colunas com restrição `UNIQUE` causarão erro.
6. Execute primeiro todos os exercícios de `SELECT`. Deixe os exercícios de `UPDATE` e `DELETE` para o final, pois eles modificam os dados.
7. Antes de cada `UPDATE` ou `DELETE`, faça uma consulta de conferência usando a mesma condição para identificar os registros que serão afetados.

Os exercícios não fornecem os comandos SQL. Escreva os scripts a partir da descrição do domínio.

## 1. Inserções iniciais

Execute o script abaixo uma única vez para acrescentar dados ao banco da atividade anterior. Os registros foram escolhidos para produzir resultados variados nas consultas e para permitir alterações e exclusões controladas.

### Clientes

```sql
INSERT INTO cliente (
    cpf, nome_completo, data_nascimento, tipo_logradouro,
    nome_logradouro, numero, complemento, bairro, cidade,
    estado, data_cadastro
)
VALUES
    ('444.555.111-22', 'ana silva', '1998-04-15', 'Rua',
     'das Acácias', '101', 'Apto 201', 'Centro', 'Vitória',
     'ES', '2026-04-01'),
    ('555.666.222-33', 'Bruna Ferreira', '1992-08-21', 'Avenida',
     'Beira-Mar', '220', NULL, 'Praia do Canto', 'Vitória',
     'ES', '2026-04-02'),
    ('666.777.333-44', 'Carlos Silva', '1987-01-30', 'Rua',
     'Sete de Setembro', '330', 'Casa', 'Centro', 'Vitória',
     'ES', '2026-04-03'),
    ('777.888.444-55', 'Daniela Costa', '1995-12-10', 'Rua',
     'dos Ipês', '440', NULL, 'Jardim da Penha', 'Vitória',
     'ES', '2026-04-04'),
    ('888.999.555-66', 'Eduardo Martins', '1979-06-05', 'Avenida',
     'Paulista', '550', 'Sala 4', 'Bela Vista', 'São Paulo',
     'SP', '2026-04-05'),
    ('999.111.666-77', 'Fernanda Lima', '2001-09-18', 'Rua',
     'do Comércio', '660', NULL, 'Centro', 'Belo Horizonte',
     'MG', '2026-04-06'),
    ('111.333.777-88', 'Gabriel Souza', '1990-03-22', 'Rua',
     'das Palmeiras', '770', 'Apto 302', 'Savassi', 'Belo Horizonte',
     'MG', '2026-04-07'),
    ('222.444.888-99', 'Excluir Cliente', '1988-11-11', 'Rua',
     'Temporária', '880', NULL, 'Centro', 'Vitória',
     'ES', '2026-04-08');
```

### Vendedores

```sql
INSERT INTO vendedor (
    matricula, cpf, nome_completo, data_nascimento,
    tipo_logradouro, nome_logradouro, numero, complemento,
    bairro, cidade, estado, salario, percentual_comissao
)
VALUES
    (2001, '666.111.222-33', 'joao silva', '1989-02-14', 'Rua',
     'Central', '201', NULL, 'Centro', 'Vitória', 'ES', 2600.00, 3.00),
    (2002, '777.222.333-44', 'Marina Alves', '1993-07-25', 'Avenida',
     'Expedicionários', '302', 'Sala 5', 'Praia do Canto', 'Vitória', 'ES',
     3800.00, 5.00),
    (2003, '888.333.444-55', 'Carlos Andrade', '1984-10-09', 'Rua',
     'da Praia', '403', NULL, 'Centro', 'Vitória', 'ES', 4700.00, 6.50),
    (2004, '999.444.555-66', 'Patricia Souza', '1990-05-19', 'Rua',
     'dos Lírios', '504', 'Apto 101', 'Jardim Camburi', 'Vitória', 'ES',
     5400.00, 7.50),
    (2005, '111.555.666-77', 'Rafael Mendes', '1982-12-01', 'Avenida',
     'Brasil', '605', NULL, 'Centro', 'São Paulo', 'SP', 6800.00, 9.00),
    (2006, '222.666.777-88', 'Excluir Vendedor', '1986-04-04', 'Rua',
     'Temporária', '706', NULL, 'Centro', 'Vitória', 'ES', 2100.00, 2.00);
```

### Categorias

```sql
INSERT INTO categoria (nome_categoria, percentual_icms)
VALUES
    ('Acessórios', 8.00),
    ('Eletrônicos', 15.00),
    ('Ferramentas', 11.00),
    ('Iluminação', 13.00),
    ('Descontinuados', 5.00);
```

Considerando o banco da atividade anterior, essas categorias receberão os próximos identificadores disponíveis. No banco inicial da atividade 1, elas receberão os identificadores de categoria 4 a 8.

### Produtos

```sql
INSERT INTO produto (
    codigo, nome, descricao, preco_venda, quantidade_estoque, id_categoria
)
VALUES
    (2001, 'Cabo de freio', 'Cabo de freio para bicicleta urbana',
     29.90, 40, 4),
    (2002, 'Capacete urbano', 'Capacete para uso em deslocamentos urbanos',
     199.90, 18, 4),
    (2003, 'Kit ferramentas', 'Kit básico para manutenção de bicicletas',
     349.90, 6, 6),
    (2004, 'Lanterna recarregável', 'Lanterna dianteira com bateria recarregável',
     89.90, 25, 7),
    (2005, 'Cadeado reforçado', 'Cadeado para proteção da bicicleta',
     119.90, 12, 4),
    (2006, 'Câmera de ação', 'Câmera compacta para registrar trilhas',
     899.90, 3, 5),
    (2007, 'Descontinuado - campainha', 'Campainha de modelo antigo',
     9.90, 0, 8),
    (2008, 'Descontinuado - suporte', 'Suporte de garrafa de modelo antigo',
     19.90, 0, 8);
```

### Telefones

```sql
INSERT INTO telefone (id_vendedor, id_cliente, telefone)
VALUES
    (NULL, 4, '(27) 99999-7001'),
    (NULL, 4, '(27) 98888-7002'),
    (NULL, 5, '(27) 97777-7003'),
    (NULL, 6, '(27) 96666-7004'),
    (NULL, 7, '(31) 95555-7005'),
    (3, NULL, '(27) 94444-7006'),
    (4, NULL, '(27) 93333-7007'),
    (5, NULL, '(11) 92222-7008');
```

### Vendas e itens de venda

```sql
INSERT INTO venda (numero, data_venda, id_cliente, id_vendedor)
VALUES
    (6001, '2026-04-10', 4, 3),
    (6002, '2026-04-11', 5, 4),
    (6003, '2026-04-12', 6, 5),
    (6004, '2026-04-13', 7, 3);

INSERT INTO item_venda (
    id_venda, id_produto, quantidade, preco_vendido
)
VALUES
    (4, 4, 2, 29.90),
    (4, 5, 1, 199.90),
    (5, 6, 1, 349.90),
    (5, 7, 2, 89.90),
    (6, 8, 1, 899.90),
    (6, 5, 1, 119.90),
    (7, 4, 3, 29.90),
    (7, 6, 1, 349.90);
```

Confira se os dados foram inseridos antes de continuar. Nas consultas desta atividade, continue consultando uma tabela por vez.

## 2. Exercícios de SELECT

Em cada exercício, escreva uma consulta que use apenas uma tabela. Escolha as colunas, os operadores, as funções e as condições necessários para atender ao pedido.

### 2.1 Consultas básicas e condições simples

1. Selecione todos os dados dos clientes.

2. Selecione o nome completo, a cidade e o estado de todos os clientes.

3. Selecione o nome completo e a data de nascimento dos clientes que nasceram antes de 1990.

4. Selecione todos os dados dos clientes que moram no estado do Espírito Santo.

5. Selecione o nome completo e a cidade dos clientes cujo nome contém `Silva`.

6. Selecione o nome completo dos clientes cujos nomes começam com a letra `A`, aceitando letras maiúsculas ou minúsculas.

7. Selecione os dados dos clientes que não possuem complemento no endereço.

8. Selecione a matrícula, o nome completo e o salário dos vendedores que recebem mais de 4000.

9. Selecione os vendedores que recebem menos de 3000 ou possuem percentual de comissão superior a 8.

10. Selecione a matrícula, o nome completo, o salário e o percentual de comissão dos vendedores que recebem pelo menos 3500 e possuem comissão de pelo menos 5.

### 2.2 LIKE e funções de strings

11. Selecione o nome completo dos vendedores cujo nome termina com a letra `a`.

12. Selecione o nome completo dos vendedores que possuem `Silva` ou `Souza` no nome.

13. Selecione o nome de cada categoria e a quantidade de caracteres de seu nome.

14. Exiba o nome de cada categoria em maiúsculas e em minúsculas.

15. Selecione o nome e os três primeiros caracteres dos produtos.

### 2.3 Condições combinadas e datas

16. Selecione os dados dos produtos com preço de venda entre 100 e 500 e estoque maior que 5.

17. Selecione o nome, o preço e o estoque dos produtos cujo estoque é zero ou cujo preço é maior que 500.

18. Selecione os itens de venda cuja quantidade é maior que 1 e cujo preço praticado é menor que 200.

19. Selecione o número e a data das vendas realizadas a partir de 11 de abril de 2026.

20. Selecione os números de telefone que contêm a sequência `9999` ou pertencem ao código de área `27`.

## 3. Exercícios de UPDATE

Antes de cada alteração, faça uma consulta para conferir os registros que atendem à condição. Depois execute o `UPDATE` e consulte novamente os registros modificados.

21. Conceda um reajuste de 10% aos vendedores que recebem salário inferior a 3000.

22. Conceda um reajuste de 5% aos produtos que possuem estoque inferior a 10 unidades.

23. Altere o percentual de ICMS das categorias que possuem percentual inferior a 12 para 12.

24. Preencha o complemento do endereço dos clientes que não possuem complemento com o texto `Não informado`.

25. Aumente em 5% o preço praticado nos itens de venda cujo preço seja inferior a 50.

26. Altere a primeira letra para maiúscula nos nomes de clientes que começam com a letra `a` minúscula, preservando o restante do nome.

## 4. Exercícios de DELETE

Os exercícios de exclusão devem ser realizados por último. Antes de cada exclusão, execute uma consulta com a mesma condição para conferir os registros. Não remova registros diferentes dos solicitados.

27. Remova os telefones que contêm a sequência `700`.

28. Remova os produtos cujo nome começa com `Descontinuado`.

29. Remova o cliente cujo nome é `Excluir Cliente`.

30. Remova o vendedor cujo nome é `Excluir Vendedor`.

## 5. Entrega

Entregue um único arquivo com extensão `.sql` contendo as respostas dos 30 exercícios.

O arquivo deve conter apenas, para cada questão, o número e o enunciado escritos em um comentário SQL, seguidos do script elaborado para responder à questão. Organize o arquivo na mesma ordem dos exercícios. Por exemplo:

```sql
-- 1. Liste os nomes e os preços de todos os produtos.
SELECT nome, preco
FROM produto;
```

Não é necessário incluir resultados das consultas, explicações ou textos fora dos comentários que identificam cada questão.

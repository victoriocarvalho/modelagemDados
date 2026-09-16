# Atividade de Modelo Físico 5

**Atividade individual**

---

## Objetivo

A partir do modelo lógico criado na [AtividadeModeloLogico5.md](../AtividadesModeloLogico/AtividadeModeloLogico5.md), gere e execute o **modelo físico** do cenário da loja varejista. O objetivo é criar o banco PostgreSQL e inserir registros de clientes e vendedores, observando como a estratégia de mapeamento da herança organiza os dados.

## Passo a passo

1. Abra no BRModelo o modelo lógico produzido na [AtividadeModeloLogico5.md](../AtividadesModeloLogico/AtividadeModeloLogico5.md), utilizando a estratégia de herança escolhida na atividade.
2. Gere automaticamente o script SQL-DDL do modelo físico.
3. Crie no Aiven um banco chamado `dinamica5` e verifique se o serviço PostgreSQL está em execução.
4. No DBeaver, crie uma conexão com o banco `dinamica5` e abra um script SQL.
5. Copie o script gerado pelo BRModelo para o DBeaver e execute-o.
6. Observe as tabelas criadas para `Pessoa`, `Cliente` e `Vendedor`, de acordo com a abordagem de herança escolhida.
7. Confira se as chaves primárias, as chaves estrangeiras e as restrições de integridade foram criadas corretamente.
8. Insira os dados do teste prático apresentado a seguir. Os dados não estão separados entre atributos de `Pessoa` e atributos dos papéis; observe onde cada valor deve ser colocado de acordo com a estratégia escolhida.
9. Consulte as tabelas para confirmar os registros inseridos.

## Teste prático: clientes, vendedores e tutoria

Insira os clientes e vendedores com os dados abaixo. Os demais dados nao informados abaixo podem ser preenchidos com os valores que você preferir.


### Clientes

| CPF | nome | dataTornouCliente |
|---|---|---:|
| 111.222.333-44 | Ana Souza | 29/01/2025 |
| 222.333.444-55 | Bruno Lima | 03/05/2025 |

### Vendedores

| CPF | nome | idade | matrícula |matriculaDoTutor |
|---|---|---:|---:|---|
| 333.444.555-66 | Carla Mendes | 42 | 2001 | 2002 |
| 444.555.666-77 | Diego Costa | 51 | 2002 | deixe vazio |
| 111.222.333-44 | Ana Souza | 29 | 2003 | 2002 |

Ana Souza aparece nos dois cadastros para representar uma pessoa que exerce simultaneamente os papéis de `Cliente` e `Vendedor`. Observe como essa situação deve ser armazenada de acordo com a estratégia de herança escolhida.

Ao inserir os vendedores, tente primeiro inserir Carla Mendes, que possui como tutor o vendedor de matrícula `2002`. Faça isso antes de inserir Diego Costa, que é o tutor indicado.

### Verificação da tutoria

O banco aceitou a inserção de Carla antes do cadastro de Diego? Em seguida, cadastre Diego, tente inserir Carla novamente e verifique se a operação foi aceita. A chave estrangeira da tutoria deve exigir que o tutor já exista na tabela correspondente.

Ao final, confirme que foram cadastrados **2 clientes**, **3 vendedores** e que Ana Souza pode aparecer nos dois papéis sem deixar de representar a mesma pessoa, conforme a estratégia de mapeamento utilizada.

---

**Bom trabalho!**

[Voltar para o Arquivo Principal da Dinâmica 5](../dinamica5.md)

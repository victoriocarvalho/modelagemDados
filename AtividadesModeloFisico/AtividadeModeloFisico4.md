# Atividade de Modelo Físico 4

**Atividade individual**

---

## Objetivo

A partir do modelo lógico criado na [AtividadeModeloLogico4.md](../AtividadesModeloLogico/AtividadeModeloLogico4.md), gere e execute o **modelo físico** do cenário da loja varejista. O objetivo é criar o banco PostgreSQL e inserir clientes com diferentes quantidades de telefones.

## Passo a passo

1. Abra no BRModelo o modelo lógico produzido na [AtividadeModeloLogico4.md](../AtividadesModeloLogico/AtividadeModeloLogico4.md).
2. Gere automaticamente o script SQL-DDL do modelo físico.
3. Crie no Aiven um banco chamado `dinamica4` e verifique se o serviço PostgreSQL está em execução.
4. No DBeaver, crie uma conexão com o banco `dinamica4` e abra um script SQL.
5. Copie o script gerado pelo BRModelo para o DBeaver e execute-o.
6. Verifique se foram criadas as tabelas de `Cliente`, `Vendedor`, `Produto`, `Categoria`, `Venda` e as tabelas necessárias para os atributos multivalorados, como os telefones.
7. Confira se as chaves primárias, as chaves estrangeiras e as restrições de integridade foram criadas corretamente.
8. Insira os dados do teste prático apresentado a seguir, utilizando os nomes das tabelas e das colunas gerados ou ajustados no seu modelo.
9. Consulte os dados inseridos para confirmar que os três clientes foram cadastrados e que os telefones foram armazenados corretamente.

## Teste prático: clientes, endereços e telefones

Insira os três clientes abaixo na tabela correspondente. Separe as partes do endereço nas colunas geradas para o atributo composto `endereco`.

### Clientes

| CPF | nome | idade | tipo_logradouro | nome_logradouro | numero | complemento | bairro | cidade | estado |
|---|---|---:|---|---|---:|---|---|---|---|
| 111.222.333-44 | Ana Souza | 29 | Rua | das Flores | 120 | Apto 301 | Centro | Vitória | ES |
| 222.333.444-55 | Bruno Lima | 35 | Avenida | Nossa Senhora da Penha | 850 | Sala 12 | Praia do Canto | Vitória | ES |
| 333.444.555-66 | Carla Mendes | 41 | Praça | do Sol | 45 | deixe vazio | Jardim da Penha | Vitória | ES |

### Telefones

Insira os telefones na tabela criada para o atributo multivalorado `telefones`, relacionando cada número ao CPF do respectivo cliente:

| CPF do cliente | telefone |
|---|---|
| 111.222.333-44 | (27) 99999-1111 |
| 111.222.333-44 | (27) 98888-2222 |
| 222.333.444-55 | (27) 97777-3333 |

Não insira telefone para o cliente de CPF `333.444.555-66`.

Ao final, consulte as tabelas e confirme:

- Foram cadastrados **3 clientes**.
- O cliente `111.222.333-44` possui **2 telefones**.
- O cliente `222.333.444-55` possui **1 telefone**.
- O cliente `333.444.555-66` possui **0 telefones**.

---

**Bom trabalho!**

[Voltar para o Arquivo Principal da Dinâmica 4](../dinamica4.md)

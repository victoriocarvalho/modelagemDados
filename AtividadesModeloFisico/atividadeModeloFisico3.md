# Atividade de Modelo Físico 3

**Atividade individual**

---

## Objetivo

A partir do modelo lógico criado na [AtividadeModeloLogico3.md](../AtividadesModeloLogico/AtividadeModeloLogico3.md), gere e execute o **modelo físico** do cenário da empresa de projetos. O foco será verificar como os relacionamentos de coordenação e colaboração, seus atributos e seus períodos históricos são representados no banco.

## Passo a passo

1. Abra no BRModelo o modelo lógico produzido na [AtividadeModeloLogico3.md](../AtividadesModeloLogico/AtividadeModeloLogico3.md).
2. Gere automaticamente o script SQL-DDL do modelo físico.
3. Crie no Aiven um banco chamado `dinamica3` e verifique se o serviço PostgreSQL está em execução.
4. No DBeaver, crie uma conexão com o banco `dinamica3` e abra um script SQL.
5. Copie o script gerado pelo BRModelo para o DBeaver e execute-o.
6. Verifique se foram criadas as tabelas de `Funcionario`, `Projeto` e as tabelas associativas dos relacionamentos `coordena` e `colabora`.
7. Confirme se as chaves estrangeiras e os atributos `data_inicio`, `data_fim` e `funcao_colaborador` foram criados nas tabelas correspondentes.

## Questões para análise

1. Quais tabelas foram criadas a partir das entidades `Funcionario` e `Projeto`? Quais tabelas representam os relacionamentos `coordena` e `colabora`?
2. As duas associações entre funcionário e projeto foram implementadas separadamente? Por que isso é necessário?
3. Quais chaves estrangeiras existem em cada tabela associativa? Elas referenciam as tabelas corretas?
4. Em quais tabelas foram criados `data_inicio`, `data_fim` e `funcao_colaborador`? Por que esses atributos não devem ficar diretamente em `Funcionario` ou `Projeto`?
5. Como o modelo físico permite consultar os coordenadores anteriores de um projeto?
6. Como o banco diferencia a relação de coordenação da relação de colaboração?
7. Tente inserir uma colaboração ou coordenação referenciando um funcionário ou projeto inexistente. O que aconteceu? Qual restrição foi responsável pelo resultado?

## Para Refletir

O script SQL representa corretamente o modelo lógico, mas a existência das tabelas e chaves estrangeiras não garante todas as regras de negócio. Analise o banco criado e responda:

### Teste prático: funcionários, projetos e relacionamentos

Insira os dados abaixo nas tabelas correspondentes. Utilize os nomes das tabelas associativas gerados ou ajustados no seu modelo lógico.

#### Funcionários

| matrícula | nome | especialidade | email |
|---|---|---|---|
| 1 | João Silva | Desenvolvimento Backend | joao@empresa.com |
| 2 | Maria Santos | Análise de Requisitos | maria@empresa.com |
| 3 | Pedro Oliveira | Testes de Software | pedro@empresa.com |

#### Projetos

| código do projeto | nome do projeto | descrição | data de início |
|---|---|---|---|
| 101 | Portal do Cliente | Desenvolvimento do portal de atendimento | 2024-01-10 |
| 102 | Aplicativo de Vendas | Criação de aplicativo para vendas | 2024-03-01 |

#### Coordenações

Na tabela associativa do relacionamento `coordena`, insira os registros abaixo. O projeto 101 teve dois coordenadores em períodos diferentes:

| funcionário | projeto | data de início | data de fim |
|---|---|---|---|
| 1 | 101 | 2024-01-10 | 2024-06-30 |
| 2 | 101 | 2024-07-01 | 2024-12-31 |
| 2 | 102 | 2024-03-01 | deixe vazio, pois é a coordenação atual |

#### Colaborações

Na tabela associativa do relacionamento `colabora`, insira os seguintes registros:

| funcionário | projeto | função | data de início | data de fim |
|---|---|---|---|---|
| 1 | 101 | Desenvolvedor Backend | 2024-01-10 | deixe vazio |
| 3 | 101 | Testador | 2024-02-01 | 2024-08-31 |
| 1 | 102 | Arquiteto de Software | 2024-03-01 | deixe vazio |
| 3 | 102 | Testador | 2024-04-01 | deixe vazio |

Depois de inserir os dados, consulte as tabelas e responda:

1. Quantos funcionários e projetos foram cadastrados?
2. Quantos registros existem em cada tabela associativa?
3. Como o histórico mostra que João e Maria coordenaram o projeto 101 em períodos diferentes?
4. Quais funcionários colaboram em cada projeto e quais funções exercem?
5. Quais registros ainda estão vigentes, isto é, possuem a data de fim vazia?

### Questões sobre integridade histórica

1. É possível inserir duas chefias históricas com períodos sobrepostos para o mesmo projeto? O modelo físico impede essa situação?
2. Que restrição, validação ou mecanismo poderia ser criado para garantir que não existam períodos de coordenação conflitantes?

---

**Bom trabalho!**

[Voltar para o Arquivo Principal da Dinâmica 3](../dinamica3.md)

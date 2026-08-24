# Atividade de Modelo Físico 2

**Atividade Individual**

---

## Tarefa

A partir do modelo lógico produzido na [AtividadeModeloLogico2.md](../AtividadesModeloLogico/AtividadeModeloLogico2.md), crie o **modelo físico** para o cenário da escola de línguas. Utilize a ferramenta **BRModelo** para gerar o script SQL de criação do esquema e execute este script em um banco PostgreSQL no Aiven, utilizando o **DBeaver**.

O modelo lógico contém os relacionamentos 1:N entre `Curso` e `Turma` e entre `Professor` e `Turma`, além do relacionamento N:N entre `Professor` e `Curso`, representado por uma tabela associativa. Essa tabela também deve armazenar o atributo `descrição da habilitação`.

### Requisitos do Modelo Físico:

1. **Crie o esquema do banco** em SQL usando DDL.
2. **Defina as tabelas** correspondentes às entidades e à tabela associativa do modelo lógico.
3. **Defina os tipos dos atributos** de cada tabela.
4. **Crie as chaves primárias**, incluindo a chave primária composta da tabela associativa, caso essa seja a solução gerada pelo BRModelo.
5. **Crie as chaves estrangeiras** e as restrições de integridade referencial.
6. **Verifique a consistência** do esquema em relação ao modelo lógico.
7. **Execute o script** no banco PostgreSQL do Aiven pelo DBeaver.

---

## Passo a passo sugerido

### 1. Criação do modelo físico no BRModelo

Use o BRModelo para gerar o script de criação do esquema a partir do modelo lógico produzido na [AtividadeModeloLogico2.md](../AtividadesModeloLogico/AtividadeModeloLogico2.md). O objetivo desta etapa é transformar as tabelas, as chaves e os relacionamentos em instruções SQL.

O script SQL deve conter comandos de criação das tabelas e das restrições. Verifique especialmente se a tabela associativa do relacionamento N:N foi criada e se contém as chaves estrangeiras de `Professor` e `Curso`, além do atributo `descrição da habilitação`.

### 2. Criação do banco no Aiven

Crie o banco de dados no Aiven:

1. Faça login no Aiven.
2. Verifique se o seu serviço está rodando.
3. Clique sobre o nome do seu serviço para abrir os detalhes.
4. Na barra lateral, selecione a opção **Databases** e clique em **Adicionar database**.
5. Defina o nome `dinamica2` para o seu banco de dados.

### 3. Criação do esquema do banco pelo DBeaver

1. Crie uma nova conexão no DBeaver para se conectar ao banco que acabou de criar no Aiven. Siga os mesmos passos das aulas anteriores, alterando o nome do banco para `dinamica2`.
2. Conecte-se ao banco pelo DBeaver e abra uma nova janela de script SQL.
3. Gere o modelo físico a partir do modelo lógico no BRModelo.
4. Copie o script gerado para a janela de script do DBeaver e execute-o.
5. Verifique se foram criadas as tabelas de `Professor`, `Curso`, `Turma` e a tabela associativa da habilitação.
6. Verifique se as chaves primárias e estrangeiras foram criadas corretamente.

---

## Para Refletir

O relacionamento N:N entre `Professor` e `Curso` é representado no modelo físico por uma tabela associativa. Ela permite registrar várias habilitações para cada professor e vários professores habilitados para cada curso. Já os relacionamentos 1:N com `Turma` são representados por chaves estrangeiras nas tabelas do lado N.

### Questões para Análise:

1. **Estrutura do banco**: leia os comandos SQL executados. Quais tabelas foram criadas? É possível identificar quais tabelas vieram das entidades e qual tabela foi criada para representar o relacionamento N:N?

2. **Relacionamento N:N**: qual tabela representa a habilitação entre professores e cursos? Quais chaves estrangeiras ela possui? Como essas chaves permitem registrar várias combinações entre professores e cursos?

3. **Atributo da habilitação**: em qual tabela foi criado o atributo `descrição da habilitação`? Por que ele deve ficar na tabela associativa, e não diretamente em `Professor` ou `Curso`?

4. **Chave primária da tabela associativa**: a tabela associativa possui uma chave primária composta pelas chaves de `Professor` e `Curso`? Qual é a importância dessa chave para evitar a duplicação da mesma habilitação?

5. **Comparação com o relacionamento 1:N**: como o relacionamento N:N foi implementado no modelo físico em comparação com os relacionamentos 1:N que envolvem `Turma`? Por que os relacionamentos 1:N não precisam de uma tabela associativa equivalente?

6. **Transposição de chaves**: por que não seria suficiente transpor apenas a chave de `Professor` para `Curso`, ou apenas a chave de `Curso` para `Professor`, para representar todas as habilitações? Como isso limitaria os registros possíveis?

7. **Integridade referencial**: tente inserir na tabela associativa uma habilitação para um professor ou curso inexistente. O banco aceitou? Qual restrição impediu ou permitiu a operação?

8. **Teste prático do relacionamento N:N**: depois de inserir os dados abaixo, consulte a tabela associativa. Quantas habilitações devem aparecer? O resultado corresponde ao relacionamento representado no modelo lógico?

#### Dados para inserir

Insira os seguintes professores:

| matrícula | nome | nacionalidade |
|---|---|---|
| 1 | João Silva | Brasileira |
| 2 | Maria Santos | Portuguesa |

Insira os seguintes cursos:

| código do curso | idioma | nível |
|---|---|---|
| 101 | Inglês | Básico |
| 102 | Espanhol | Intermediário |
| 103 | Francês | Avançado |

Na tabela associativa do relacionamento de habilitação, insira os seguintes registros:

- O professor de matrícula `1` deve ser habilitado nos cursos `101`, `102` e `103`.
- O professor de matrícula `2` deve ser habilitado nos cursos `101` e `102`.
- Informe uma descrição para cada habilitação, como `Experiência profissional na área`.

Em seguida, crie uma turma para cada curso:

| código da turma | horário | dia da semana | curso | professor |
|---|---|---|---|---|
| 201 | 08:00 | Segunda-feira | 101 | 1 |
| 202 | 14:00 | Quarta-feira | 102 | 2 |
| 203 | 19:00 | Sexta-feira | 103 | 1 |

Verifique se os relacionamentos 1:N foram representados corretamente: cada turma deve estar vinculada a um único curso e a um único professor, enquanto um professor ou curso pode estar associado a várias turmas.

---

## Para Refletir: habilitação do professor e turma

No modelo conceitual, a escola informa quais professores estão habilitados para lecionar quais cursos. Porém, os relacionamentos que ligam `Turma` a `Professor` e `Curso` são armazenados separadamente no modelo lógico.

1. Crie uma nova turma do curso `103` (Francês Avançado), mas atribua essa turma ao professor de matrícula `2` (Maria Santos). O banco permitiu criar essa turma? Observe os dados inseridos.
2. O professor de matrícula `2` está habilitado para o curso `103`? Consulte a tabela associativa para verificar.
3. Faz sentido, de acordo com as regras do domínio, que esse professor lecione essa turma? Explique.
4. Se o banco permitiu a inserção, por que as chaves estrangeiras existentes não foram suficientes para impedir essa situação?
5. Como poderíamos evitar esse problema e garantir que o professor de uma turma esteja habilitado para o curso daquela turma? Considere possibilidades como uma restrição adicional no banco de dados, uma alteração no modelo lógico ou uma validação implementada na aplicação.

---

**Bom trabalho!**

[Voltar para o Arquivo Principal da Dinâmica 2](../dinamica2.md)

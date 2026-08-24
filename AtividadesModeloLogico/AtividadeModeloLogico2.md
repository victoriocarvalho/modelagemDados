# Atividade de Modelo Lógico 2

**Atividade individual**

---

## Objetivo

Nesta atividade, você deve transformar em um **modelo lógico** a versão final do modelo conceitual desenvolvido na [atividadeMER2.md](../AtividadesModeloConceitual/atividadeMER2.md), referente ao cenário da escola de línguas.

O objetivo é compreender como entidades, atributos e relacionamentos do modelo conceitual são convertidos em tabelas, colunas, chaves primárias e chaves estrangeiras. Daremos atenção especial ao mapeamento de relacionamentos **N:N**, tanto na versão sem atributos quanto na versão final, que possui o atributo `descrição da habilitação` ou `motivo da habilitação`.

---

## Modelo conceitual de origem

Utilize como ponto de partida a **segunda versão** do modelo conceitual criada na [atividadeMER2.md](../AtividadesModeloConceitual/atividadeMER2.md). Nessa versão, o modelo representa:

- As entidades `Professor`, `Curso` e `Turma`.
- Os atributos identificadores e demais atributos de cada entidade.
- O relacionamento N:N entre `Professor` e `Curso`, que representa as habilitações.
- O atributo `descrição da habilitação` associado ao relacionamento entre `Professor` e `Curso`.
- Os relacionamentos 1:N entre `Curso` e `Turma` e entre `Professor` e `Turma`.

Confira se o modelo conceitual está completo e correto antes de iniciar a transformação para o modelo lógico.

---

## Tarefa: gerar o modelo lógico automaticamente

Crie o modelo lógico utilizando a **opção de geração automatizada do BRModelo**.

### Instruções

1. Abra no BRModelo a versão final do modelo conceitual desenvolvida na [atividadeMER2.md](../AtividadesModeloConceitual/atividadeMER2.md).
2. Revise as entidades, os atributos identificadores, os relacionamentos e as cardinalidades.
3. Utilize a funcionalidade do BRModelo para gerar automaticamente o modelo lógico a partir do modelo conceitual.
4. Observe as tabelas, colunas, chaves primárias e chaves estrangeiras criadas pelo programa.
5. Verifique especialmente o resultado gerado para o relacionamento N:N entre `Professor` e `Curso`.
6. Verifique onde foi colocado o atributo `descrição da habilitação` ou `motivo da habilitação`.
7. Salve o modelo lógico gerado no formato do BRModelo.

Nesta atividade, não é necessário criar uma versão manual. O foco é analisar o resultado produzido pela transformação automatizada e relacioná-lo às regras de mapeamento estudadas.

### Entregável

- Um arquivo do BRModelo contendo o modelo lógico gerado automaticamente a partir da versão final do modelo conceitual da atividadeMER2.md.
- As respostas às questões de análise apresentadas a seguir.

---

## Questões para análise

### 1. Entidades e atributos

Analise o modelo lógico gerado e responda:

1. Quais tabelas foram criadas a partir das entidades `Professor`, `Curso` e `Turma`?
2. Quais colunas foram criadas a partir dos atributos dessas entidades?
3. Quais atributos identificadores se transformaram em chaves primárias?
4. Os nomes e os tipos dos atributos foram mantidos, modificados ou definidos automaticamente pelo BRModelo? Explique.

### 2. Transformação dos relacionamentos 1:N

O cenário possui relacionamentos 1:N envolvendo `Turma`, `Curso` e `Professor`. Analise como eles foram transformados no modelo lógico e responda:

1. Quais chaves primárias foram transpostas para as tabelas do lado N?
2. Em quais tabelas foram criadas as chaves estrangeiras referentes aos relacionamentos 1:N?
3. Como é possível identificar, no modelo lógico, que cada turma está associada a um único curso e a um único professor?
4. Por que, no relacionamento 1:N, a transposição da chave primária do lado 1 para o lado N é suficiente para representar a associação?

### 3. Transformação do relacionamento N:N

No modelo conceitual, um professor pode estar habilitado para vários cursos e um curso pode ter vários professores habilitados. Observe como o BRModelo transformou esse relacionamento N:N e responda:

1. Foi criada uma nova tabela para representar o relacionamento entre `Professor` e `Curso`? Qual é o nome dessa tabela? Percebe o padrão de nomes automático dado pelo BRModelo?
    1.1. Altere o nome desta tabela para um nome que descreva melhor o objetivo dela. Qual nome você deu?
2. Quais chaves estrangeiras essa tabela recebeu?
3. Como essas chaves estrangeiras identificam o professor e o curso relacionados?
4. A combinação das chaves estrangeiras forma uma chave primária composta? Explique o papel dessa chave.
5. Como o modelo lógico permite representar que um curso possui vários professores habilitados?

### 4. Atributo do relacionamento N:N

Na versão final do modelo conceitual, o relacionamento de habilitação possui o atributo `descrição da habilitação` ou `motivo da habilitação`. Analise seu tratamento no modelo lógico e responda:

1. Em qual tabela o atributo do relacionamento foi colocado?
2. Por que esse atributo não deve ser colocado diretamente na tabela `Professor`?
3. Por que esse atributo não deve ser colocado diretamente na tabela `Curso`?
4. Imagine que o mesmo professor seja habilitado para dois cursos por motivos diferentes. O modelo lógico consegue registrar as duas descrições? Explique.
5. O que poderia acontecer com os dados se o atributo do relacionamento fosse colocado na tabela `Professor` ou na tabela `Curso`?

### 5. Comparação entre relacionamentos N:N e 1:N

Compare os dois processos de transformação e responda:

1. Qual é a principal diferença entre o mapeamento do relacionamento N:N entre `Professor` e `Curso` e o mapeamento dos relacionamentos 1:N que envolvem `Turma`?
2. Por que não seria possível transformar o relacionamento N:N apenas transpondo a chave primária de `Professor` para `Curso` ou transpondo a chave primária de `Curso` para `Professor`?
3. Por que a tabela associativa é necessária para representar corretamente um relacionamento N:N?

### 6. Conferência do modelo gerado

Faça uma revisão final do modelo lógico e responda:

1. Todas as entidades do modelo conceitual foram transformadas em tabelas?
2. Todos os atributos das entidades foram transformados em colunas?
3. Todas as chaves primárias foram definidas corretamente?
4. Os relacionamentos 1:N possuem chaves estrangeiras nas tabelas adequadas?
5. O relacionamento N:N possui uma tabela associativa?
6. O atributo da habilitação foi mantido na tabela associativa?
7. O modelo lógico gerado representa todas as regras apresentadas no cenário da escola de línguas?
8. Você identificou alguma decisão automática do BRModelo que precisaria ser revisada ou ajustada? Justifique.

---

## Conclusão

A transformação de um relacionamento 1:N normalmente pode ser feita pela transposição da chave primária do lado 1 para a tabela do lado N. Já um relacionamento N:N exige uma tabela associativa, pois cada lado pode estar relacionado a várias instâncias do outro lado. Essa tabela recebe as chaves das entidades participantes e também pode armazenar atributos que pertencem à associação, como o motivo da habilitação de um professor para um curso.

---

**Bom trabalho!**

[Voltar para o Arquivo Principal da Dinâmica 2](../dinamica2.md)

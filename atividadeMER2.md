# Atividade de Modelagem Conceitual de Dados

## MER - Tipos de Relacionamentos

**Atividade Individual**

---

## Cenário: Escola de Línguas

Uma escola de idiomas deseja implementar um sistema para gerenciar seus cursos, professores e turmas ofertadas. 

A escola mantém um cadastro de seus **professores**. De cada professor deseja-se registrar seu número de matrícula (que o identifica unicamente), nome completo e nacionalidade.

A escola oferece vários **cursos** de idiomas. De cada curso deseja-se armazenar um código do curso (que o identifica unicamente), nome do idioma e nível (básico, intermediário, avançado).

Um **professor pode estar habilitado a lecionar vários cursos** e um **curso pode ter vários professores habilitados**. 

Os cursos são oferecidos em **turmas**. De cada turma deseja-se armazenar um código de turma (que a identifica unicamente), horário e dia da semana. Cada turma é sempre de um curso específico e é lecionada por um único professor.

---

## Tarefa

Desenvolva um **Modelo Entidade Relacionamento (MER)** para o cenário descrito acima utilizando a ferramenta **BRModelo**.

### Requisitos do Modelo:

1. **Identifique as 3 entidades** mencionadas no cenário
2. **Defina os atributos** de cada entidade
3. **Indique o atributo identificador** (chave primária) de cada entidade
4. **Represente os relacionamentos indicando corretamente as cardinalidades**

### Dicas:

- Quantos relacionamentos 1 para N existem neste cenário?
- O relacionamento N para N entre Professor e Curso não possui atributos, apenas expressa quais professores estão habilitados para quais cursos
- Observe que uma turma depende de duas entidades: um curso e um professor

---

## Para Refletir

Analise o seu modelo e responda aos seguintes questionamentos:

1. **Faria sentido** um professor ser alocado para lecionar uma turma de um curso para o qual ele **não está habilitado**? Por quê?

2. **Seu modelo MER atual permite** que isso aconteça? Ou seja, é possível ter uma turma atribuída a um professor e a um curso, mesmo que o professor não esteja habilitado para aquele curso?

3. **Discussão**: O que você observou é um exemplo de **restrição de integridade**. Nem todas as restrições de integridade podem ser capturadas diretamente no diagrama MER. O modelo MER garante que existe uma habilitação entre Professor e Curso, mas não garante que o professor que leciona a turma está habilitado no curso daquela turma. Essa é uma restrição que precisaria ser implementada através de outras técnicas (como regras de negócio, validações no banco de dados, etc.).

---

## Tarefa 2 - Atributos em Relacionamentos N:N

A escola deseja registrar também o **motivo pela qual um professor é considerado habilitado** para lecionar um determinado curso. Por exemplo:

- **João** é habilitado para o curso **Intermediário de Inglês** porque é **nativo americano com 10 anos de experiência em ensino**
- **Manuela** é habilitada para o curso **Francês Avançado** porque possui **certificação DELF C2 e viveu 5 anos na França**
- **Pedro** é habilitado para **Português para Estrangeiros** porque é **falante nativo e possui formação pedagógica**

### Questão Reflexiva:

1. **Onde deve estar essa informação no modelo?** Esse "motivo da habilitação" é um atributo:
   - Do **Professor**? (Não, pois cada professor pode ter motivos diferentes para cada curso)
   - Do **Curso**? (Não, pois o motivo é específico de cada professor)
   - Do **Relacionamento** entre Professor e Curso? (Sim! É uma característica da habilitação específica)

2. **Consequência**: Se um relacionamento N:N possui atributos, como isso deve ser representado no diagrama MER?

### Tarefa:

Desenvolva uma **segunda versão do seu modelo MER** que inclua o atributo "descrição da habilitação" (ou "motivo da habilitação"). Utilize novamente a ferramenta **BRModelo** para criar este novo diagrama.

Comparar as duas versões do modelo é uma excelente forma de compreender como relacionamentos N:N podem ter atributos próprios!

---

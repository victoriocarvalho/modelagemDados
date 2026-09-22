# Introdução

## Visão geral do projeto e da implementação de bancos de dados

O processo de projeto e implementação de um banco de dados pode ser organizado em três etapas principais: o desenvolvimento do **modelo conceitual**, a construção do **modelo lógico** e a implementação do **modelo físico**.

### Modelo conceitual

Nosso processo começa com uma atividade de modelagem conceitual. Nessa etapa, o foco está em compreender os conceitos importantes de um domínio e as relações entre esses conceitos, sem nos preocuparmos ainda com detalhes de implementação, como tabelas, colunas, tipos de dados ou comandos SQL.

A comunidade de banco de dados tradicionalmente utiliza o **Modelo Entidade-Relacionamento (MER)** para representar modelos conceituais. Outras comunidades, como a de orientação a objetos, utilizam, por exemplo, diagramas de classes. Abstraindo a forma de representação, o objetivo é o mesmo: capturar os conceitos do domínio e as relações entre eles.

### Modelo lógico

Na segunda etapa, desenvolvemos o modelo lógico. Nesse momento, adequamos o modelo conceitual às restrições de implementação do modelo de dados que será utilizado. Nesta disciplina, trabalharemos com o **modelo relacional**.

No modelo relacional, os dados são organizados em relações, representadas por tabelas. Cada tabela possui linhas, que representam registros, e colunas, que representam atributos dos registros. As tabelas podem se relacionar por meio de chaves primárias e chaves estrangeiras. Também precisamos seguir regras de organização para reduzir repetições e evitar problemas de consistência, como as regras das **formas normais**.

### Modelo físico

Na terceira etapa, transformamos o modelo lógico em um código que implementará de fato o banco de dados. Esse código constitui o modelo físico. No caso de bancos relacionais, utilizamos a linguagem **SQL** para criar tabelas, colunas, chaves, restrições e outros objetos do banco.

## Método de ensino

Uma possibilidade de ensino seria abordar as etapas de forma sequencial: primeiro todo o modelo conceitual, depois o modelo lógico e, por fim, o modelo físico. Nesse formato, porém, os alunos só chegariam a ver bancos de dados implementados no final do semestre. Ademais, em experiências anteriores notei que os conceitos abstratos de modelagem conceitual são mais facilmente entendidos quando são concretizados no modelo lógico e no banco de dados implementado.

Assim, neste curso, abordaremos as três etapas em diferentes **dinâmicas**. Em cada dinâmica, passaremos pelo modelo conceitual, pela transformação para o modelo lógico e pela implementação do modelo físico, chegando à criação ou à atualização de um banco de dados. Cada dinâmica terá foco em pontos específicos da modelagem conceitual e em como esses pontos são tratados nos modelos seguintes.

Essa abordagem permite relacionar continuamente os conceitos estudados à sua implementação. Assim, cada novo conteúdo pode ser compreendido, transformado e testado em um banco de dados.

## Índice das dinâmicas

### [Dinâmica 1 - Primeiro banco de dados](dinamica1.md)

### Principais Conceitos Abordados
#### Modelo conceitual

- Entidades, atributos e atributos identificadores.
- Relacionamentos 1:N e cardinalidades.

#### Modelo lógico

- Tabelas, colunas, chaves primárias e chaves estrangeiras.
- Transposição de chave no relacionamento 1:N.
- Integridade referencial.

#### Modelo físico

- SGBD, PostgreSQL, Aiven e DBeaver.
- SQL-DDL, tabelas, tipos e restrições.

### [Dinâmica 2 - Relacionamentos N:N](dinamica2.md)

### Principais Conceitos Abordados
#### Modelo conceitual

- Relacionamentos N:N e seus atributos.

#### Modelo lógico

- Tabela associativa.
- Transformação de N:N em dois relacionamentos 1:N.
- Chaves estrangeiras e chave primária composta.

#### Modelo físico

- Script SQL-DDL do relacionamento N:N.
- Restrições de integridade referencial.

### [Dinâmica 3 - Múltiplos relacionamentos entre duas entidades e dados históricos](dinamica3.md)

### Principais Conceitos Abordados
#### Modelo conceitual

- Mais de um relacionamento entre as mesmas entidades.
- Papéis, relacionamentos 1:1 e dados históricos.
- Necessidade de dados históricos.

#### Modelo lógico

- Mapeamento individual de relacionamentos.
- Chaves estrangeiras orientadas a papéis.
- Escolha do lado que recebe a chave no relacionamento 1:1.

#### Modelo físico

- Script SQL para relacionamentos múltiplos.
- Tabelas associativas, chaves estrangeiras e histórico.

### [Dinâmica 4 - Atributos multivalorados e compostos](dinamica4.md)

#### Principais conceitos abordados

##### Modelo conceitual

- Atributos monovalorados, multivalorados, simples e compostos.
- Discussão sobre representar um conceito como entidade ou atributo composto.

##### Modelo lógico

- Transformação de atributos compostos em colunas.
- Transformação de atributos multivalorados em tabelas.

##### Modelo físico

- Geração do script SQL e criação do banco a partir do modelo lógico.

### [Dinâmica 5 - Heranças e autorrelacionamentos](dinamica5.md)

#### Principais conceitos abordados

##### Modelo conceitual

- Herança, generalização e especialização.
- Autorrelacionamentos e definição de papéis.

##### Modelo lógico

- Estratégias de mapeamento de heranças.
- Mapeamento de autorrelacionamentos 1:N e N:N.

##### Modelo físico

- Geração das tabelas que representam heranças.
- Restrições de integridade referencial em autorrelacionamentos.

### [Dinâmica 6 - Formas normais](dinamica6.md)

#### Principais conceitos abordados

- Dependências funcionais.
- Primeira, segunda e terceira formas normais.
- Identificação e correção de repetições e dependências inadequadas.
- Revisão dos modelos da Aula 1 para produzir novos modelos conceitual, lógico e físico em conformidade com as três formas normais.

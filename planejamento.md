# Planejamento da disciplina

A disciplina de banco de dados pode ser dividida em duas partes principais: modelagem de dados e implementação de bancos de dados.
Tradicionalmente ensino as etapas sequencialmente: primeiro modelamos em nível conceitual, depois transformamos o modelo conceitual em lógico, em seguida geramos o SQL de criação do esquema a partir do modelo lógico e, por fim, estudamos o DML para manipular os dados do banco.

Apesar de essa sequência deixar bem claro os objetivos de cada fase e nos permitir focar em técnicas bem definidas para cada ponto do processo, percebo dois problemas acontecerem reiteradamente: (i) os alunos tem muitas dificuldades de abstração e de entendimento dos objetivos do modelos conceitual e (ii) muitos ficam desmotivados por não enxergarem o link desses modelos conceituais com a prática de desenvolvimento. Nesse contexto, tentando mitigar esses problemas, decidi experimentar neste semestre uma estratégia na qual faremos várias iterações passando por todas as etapas do processo, de forma que, em cada iteração discutiremos conceitos e técnicas relativas às fases da modelagem de dados (modelo conceitual, modelo lógico e modelo físico). Depois, em um segundo momento, voltaremos aos bancos gerados nessas iterações para estudar os comandos de manipulação de dados do SQL (SQL-DML).

## Aula 0
### Conteúdos
- Dar uma visão geral do processo de projeto de banco de dados.
- Ensinar conceitos como modelagem conceitual, modelo lógico, modelo físico, SQL, SGBD, Servidor em nuvem. 
- Definir ferramentas e ambiente que será utilizando
- Ferramentas e ambientes:
    - Usaremos o BRModelo Offline para criar os modelos conceituais, lógicos e os SQLs de criação dos esquemas.
    - Usaremos o PostgreSQL como SGBD
    - Usaremos aiven.io para hospedar nosso serviço PostgreSQL
    - Usaremos o DBeaver como ferramenta de gestão de banco de dados.
### Prática
- Nesta aula faremos uma dinâmica de gerar um pequeno banco, com duas entidades apenas, passando por todas as fases da modelagem e implementação. Criaremos o modelo conceitual no BRModelo e usaremos o próprio BRModelo para gerar o modelo lógico e o físico (SQL de criação do Esquema), criaremos nosso serviço no aiven.io e usaremos o DBeaver para rodar o script de criação do banco no aiven. Por fim, usaremos o DBeaver para visualizar as tabelas criadas.
- Os slides utilizados para esta dinâmica podem ser acessados pelo link: https://docs.google.com/presentation/d/1Bp8PJmSa8cqK4wt9CfU-UcSK8BUpbiEv/
- A partir daqui, cada aula terá uma seção de "conteúdos" e uma seção de "prática" de Modelo Conceitual,  uma seção de "conteúdos" e uma seção de "prática" de Modelo Lógico e uma seção de "conteúdos" e uma seção de "prática" de Modelo Físico.

## Aula 1
### Conteúdos de Modelo Conceitual
- Vamos fazer modelos conceituais utilizando as notações de Modelo Entidade-Relacionamento (MER)
- Conceitos de **Entidades**, **Atributos** e **Relacionamentos**
- Notações básicas do MER para Entidade, atributos e relacionamentos.
- Por enquanto vamos trabalhar apenas com atributos simples e monovalorados. Vamos diferenciar apenas os atributos identificadores.
- Importante notar a ordem de leitura de um relacionamento em um modelo ER.
- Cardinalidades de um relacionamento: em cada extremidade do relacionamento temos uma cardinalidade mínima e uma máxima. A mínima é, tipicamente 0 ou 1 e a máxima é tipicamente 1 ou n.
- Falar que a cardinalidade máxima é que "define" o tipo do relacionamento, que pode ser 1:1, 1:N ou N:N

- Para ilustrar os conceitos na aula vaoms utilizar os conceitos de cliente e de animal de estimação e o relacionamento entre eles da atividadeMER1.md.

### Prática de Modelo Conceitual
link para atividadeMER1.md

### Conteúdos de Modelo Lógico
- Como vamos trabalhar com bancos de dados relacionais, usaremos modelos relacionais em nosso nível lógico.
- Em modelos relacionais tudo é modelado como tabelas e colunas nestas tabelas.
- Em uma transformação básica do modelo conceitual para o lógico, **entidades** dão origem a tabelas e atributos a colunas das tabelas. Veremos mais a frente que alguns atributos especiais podem dar origem a tabelas, mas ainda não é o caso.
- Os atributos identificadores darão origem às **chaves primárias** das tabelas. As chaves primárias identificam unicamente cada registro da tabela e tem papel importante no mapeamento de relacionamentos, como veremos a seguir. Caso a entidade não tenha um atributo identificador mapeado em nível conceitual, precisaremos criar um atributo identificador neste nível. Em geral, mesmo quando há atributos identificadores no domínio conceitual da entidade, é uma boa prática definir um atributo de fora do domínio para usar como chave primária a fim de evitar que alterações do domínio tragam impactos muito grandes na manutenção do seu banco de dados.
- Os relacionamentos devem ser mapeados também como tabelas e/ou colunas.
- Nesta aula só trabalharemos com o mapeamento de relacionamentos 1:N. 
    - Para mapear estes relacionamentos, a chave primária da tabela que está no lado 1 do relacionamento é exportada para a tabela que está do lado n, dano origem ao conceito de **chave estrangeira**. Uma **chave estrangeira** identifica, em uma tabela, uma linha de outra tabela relacionada. Em relacionamentos 1:N, é sempre a chave do lado 1 que é exportada para o lado N para atender a uma regra básica de bancos relacionais: os atributos devem ser atômicos, ou seja, para cada linha (instância da entidade) deve-se ter apenas um valor para cada coluna (atributo). Se tentarmos exportar a chave primária do lado N para o lado 1, para cada linha da tabela teremos N valores para a chave estrangeira gerada, o que não é permitido. Por isso exportamos sempre a chave primária do lado 1 para o lado N.

    - Além da chave estrangeira, criamos também uma **restrição de integridade referencial**. A **restrição de integridade referencial** serve para evitar inconsistência de dados entre as chaves estrangeiras e primárias do seu banco
- Ilustrar os conceitos desta teoria com o exemplo da atividadeMER1.md
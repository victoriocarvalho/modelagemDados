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

### Conteudos de Modelo Físico

- O modelo físico será feito em forma de um script SQL
- Falar aqui do conceito de SQL
- Falar que nesse momento vamos ver apenas a parte DDL (Data Description Language) do SQL
- SQL DDL é utilizado para definir o esquema do banco. introduzir o conceito de Esquema
- Vamos criar tabelas e restrições de integridade.
- Vamos gerar o script utilizando a geração automatica do BrModelo e executar no nosso banco do Aiven, conectando pelo DBeaver.

### Prática de Modelo Físico

Passos
- Crie um novo banco de dados no seu serviço do aiven.io:
    1 - Faça login no aiven
    2 - Verifique que seu serviço esteja rodando
    3 - Clique sobre o nome do seu serviço para abrir os detalhes
    4 - Na barra do lado direito selecione a opção databases e depois clique em adicionar database.
    5 - Defina o nome "dinamica1" para seu banco de dados.
- Agora crie uma nova conexão no Dbeaver para se conectar com o banco que acabou de criar no aiven. Para isso siga os mesmos passos que sigamos em nossa ultima aula, só alterando o nome do banco de "defaultdb" para "dinamica1".
- Conecte no banco pelo Dbeaver e aba uma nova janela de Script SQL com esse banco
- Gere o modelo físico pelo BRModelo , copie para a janela de scripts do Dbeaver e execute (como fizemos na última aula).
- Verifique se as tabelas foram geradas corretamente.

### Questões para análise

- Leia os comandos SQL executados. É possível inferir o que todos eles fazem? Algum detalhe chama atenção ou é mais difícil de entender?

- Abra as tabelas no modo de "dados" do DBeaver e insira registros. Tente inserir um animal informando um id_cliente inexistente. Foi possível?

- Insira agora 2 registros de clientes e 2 de animais (um relacionado a cada cliente). Em seguida tente excluir os dados de um dos clientes? O que aconteceu? O banco aceitou? Se sim, o que aconteceu com o registro do animal associado ao cliente excluído? Por que?

## Aula 2
Foco Conceitual - Discutir relacionamentos n para n sem atributos e com atributos, restrições de integridade,

## Aula 3
Foco Conceitual - Discutir a possibilidade de termos mais de um relacionamento entre duas entidades e a necessidade de dados históricos (snapshot vs. histórico)

## Aula 4
Foco Conceitual - Atributos compostos e multivalorados (conceitos e representação)

Discussão: Atributo composto ou entidade?

Foco Lógico - Como transformar atributos compostos e multivalorados do lógico para o conceitual (note que os multivalorados darão origem a tabelas, assim como uma entidade daria)


## Aula 5 
Foco Conceitual - Autorelacionamento e papeis (vamos colocar no modelo da aula 3 anterior uma autorelação "supervisor" 1 para n na classe funcionário). Ressaltar a importância dos papéis nesses casos.
Foco Lógico - Mostrar como a transformação se dá como se fossem duas tabelas Funcionario...


## Aula 6 (não teria no técnico)
Foco Conceitual - Herança
Foco Lógico - Como mapear herança

Fazer aqui um modelo grande...

## Aula 7 (Reflexões mais profundas)
Foco Conceitual - Entidade vs. atributos (usar o domínio da aula 1 - separamos cliente de animal ao inves de colocar os dados no cliente no animal (mesmo cada animal sendo de 1 cliente) mas colocamos tipo de animal e raça em animal, mesmo a raça dependendo unicamente do tipo e havendo repetições...)

Entidade vs. Relacionamento (usar o exemplo da aula 3 quando fizemos um relacionamento funcionario colabora em projeto, com atributos na colaboracao ao invés de criar a entidade colaboração.)

Foco Lógico - Falar de formas normais. No exemplo do tipo e raça de animal, a versão da aula 1 quebrava uma forma normal na medida que a raça dependia exclusivamente de um atributo que não era chave primária da tabela. 
Mostrar como a transformação de relacionamento com atributos é a mesma de uma classe quebrando o n para n em dois relacionamentos...

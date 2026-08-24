# Atividade de Modelo Lógico 1

**Atividade individual**

---

## Objetivo

Nesta atividade, você deve criar o modelo lógico a partir do modelo conceitual desenvolvido na atividade de MER da clínica veterinária. O objetivo é praticar a transformação do modelo conceitual para o modelo lógico, compreendendo as regras de mapeamento e a estrutura de tabelas, colunas, chaves primárias e chaves estrangeiras.

---

## Parte 1: Modelo lógico criado manualmente

### Instruções

Crie um modelo lógico no BRModelo a partir do modelo conceitual da [atividadeMER1.md](../AtividadesModeloConceitual/atividadeMER1.md), mas sem usar a funcionalidade de geração automática do BRModelo.

Faça o processo manualmente, seguindo este passo a passo:

1. Crie uma tabela para cada entidade do modelo conceitual.
2. Para cada entidade, inclua uma coluna para cada atributo da entidade.
3. Defina os relacionamentos entre as tabelas.
4. Para cada relacionamento, gere os atributos que serão chaves estrangeiras.
5. Defina os tipos dos atributos das tabelas.
6. Defina as chaves primárias e as chaves estrangeiras.

### Observações importantes

- Não use a função de geração automática do BRModelo para esta etapa.
- O objetivo é que você entenda o processo de conversão do modelo conceitual para o lógico.
- Nas tabelas, os atributos devem representar as colunas do banco.
- Os relacionamentos 1:N devem ser representados pela exportação da chave primária do lado 1 para o lado N.

### Recomendação importante sobre identificadores

Ao modelar a tabela `Cliente`, não defina o CPF como chave primária. Em vez disso, crie um atributo `id_cliente` do tipo inteiro.

- O CPF é um atributo do domínio do cliente e pode ser relevante para a identificação do cliente no mundo real.
- Mas, como identificador do banco, uma chave primária artificial como `id_cliente` é uma boa prática.
- Isso facilita a manutenção do banco caso haja alguma mudança no formato do CPF ou na regra de negócio relacionada a ele.

### Entregável

- Crie o modelo lógico no BRModelo de forma manual.
- Salve o diagrama no formato do BRModelo.
---

## Parte 2: Modelo lógico gerado automaticamente

Agora crie um novo modelo lógico no BRModelo usando a função de geração automática do próprio software.

### Instruções

1. Use o mesmo modelo conceitual da [atividadeMER1.md](../AtividadesModeloConceitual/atividadeMER1.md).
2. Gere o modelo lógico automaticamente no BRModelo.
3. Compare este modelo com o modelo lógico que você criou manualmente.

### Entregável

- Crie um segundo modelo lógico utilizando a geração automática do BRModelo.
- Salve o arquivo do diagrama.

---

## Questões para análise

### 1. Comparação dos dois processos

Compare o modelo lógico criado manualmente com o modelo lógico gerado automaticamente pelo BRModelo. Responda:

1. Quais foram as facilidades encontradas no processo manual?
2. Quais foram as dificuldades encontradas no processo manual?
3. Quais foram as facilidades encontradas na geração automática?
4. Quais foram as dificuldades encontradas na geração automática?
5. Houve diferenças entre os dois modelos? Quais foram?
6. O modelo automático refletiu corretamente as regras de negócio do cenário?

### 2. Análise sobre a chave primária

Refletindo sobre a definição de chave primária, responda:

1. Qual é a diferença entre usar um identificador do domínio, como o CPF, e usar uma chave primária artificial, como `id_cliente`?
2. Por que, em geral, é uma boa prática não usar atributos do domínio como chave primária?
3. Como uma mudança na regra de negócio, como a mudança na formação do CPF, afetaria o banco se o CPF fosse usado como chave primária?
4. O que aconteceria com todas as tabelas que armazenassem a chave do cliente transposta para outras tabelas?
5. Quais são os prós e contras de usar `id_cliente` do tipo inteiro como chave primária em vez de `cpf` do tipo varchar?

**Bom trabalho!**

[Voltar para o Arquivo Principal da Dinâmica 1](../dinamica1.md)
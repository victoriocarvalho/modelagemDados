# Atividade de Modelo Lógico 3

**Atividade individual**

---

## Objetivo

Nesta atividade, você deve transformar em um **modelo lógico** a versão final do modelo conceitual desenvolvido na [atividadeMER3.md](../AtividadesModeloConceitual/atividadeMER3.md), referente ao cenário da empresa de projetos.

O objetivo é analisar como o modelo conceitual é convertido em tabelas, colunas, chaves primárias e chaves estrangeiras quando existem mais de um relacionamento entre as mesmas entidades e quando é necessário armazenar dados históricos.

---

## Modelo conceitual de origem

Utilize como ponto de partida a versão final do modelo conceitual criada na [atividadeMER3.md](../AtividadesModeloConceitual/atividadeMER3.md). Nessa versão, o modelo representa:

- As entidades `Funcionario` e `Projeto`.
- O relacionamento de colaboração, com o atributo `funcao_colaborador` e os períodos de alocação.
- O relacionamento de coordenação, também com período de início e fim, para registrar o histórico de coordenadores.
- Dois relacionamentos diferentes entre as mesmas entidades, cada um com seu significado e seus próprios atributos.

Revise as entidades, os atributos, os identificadores, os nomes dos relacionamentos e as cardinalidades antes de iniciar a transformação.

---

## Tarefa: gerar o modelo lógico automaticamente

Crie o modelo lógico utilizando a **opção de geração automatizada do BRModelo**.

### Instruções

1. Abra no BRModelo a versão final do modelo conceitual desenvolvida na [atividadeMER3.md](../AtividadesModeloConceitual/atividadeMER3.md).
2. Confira se os dois relacionamentos entre `Funcionario` e `Projeto` estão presentes e possuem nomes diferentes.
3. Revise os atributos `data_inicio`, `data_fim` e `funcao_colaborador`, verificando a qual relacionamento cada um pertence.
4. Utilize a funcionalidade de geração automática do BRModelo para criar o modelo lógico.
5. Observe as tabelas, colunas, chaves primárias, chaves estrangeiras e tabelas associativas geradas.
6. Verifique se cada relacionamento foi mapeado individualmente, sem que um relacionamento seja confundido com o outro.
7. Analise como o BRModelo tratou os atributos dos relacionamentos e os períodos históricos.
8. Caso o BRModelo atribua nomes genéricos às tabelas associativas ou às chaves estrangeiras, renomeie-os para nomes que deixem claro o papel ou o significado da associação.
9. Salve o modelo lógico gerado no formato do BRModelo.

Nesta atividade, não é necessário criar uma versão manual. O foco é analisar o resultado da geração automatizada e relacioná-lo às regras de mapeamento do modelo conceitual.

### Entregável

- Um arquivo do BRModelo contendo o modelo lógico gerado automaticamente a partir da versão final da atividadeMER3.md.
- As respostas às questões de análise apresentadas a seguir.

---

## Questões para análise

### 1. Entidades, atributos e identificadores

Analise o modelo lógico gerado e responda:

1. Quais tabelas foram criadas a partir das entidades `Funcionario` e `Projeto`? Quais colunas foram criadas a partir dos atributos dessas entidades? Quais atributos identificadores se transformaram em chaves primárias?
2. Os atributos `data_inicio`, `data_fim` e `funcao_colaborador` aparecem em uma tabela de entidade ou em tabelas associativas? Explique.

### 2. Mais de um relacionamento entre as mesmas entidades

O modelo conceitual possui os relacionamentos `coordena` e `colabora`, ambos entre `Funcionario` e `Projeto`. Responda:

1. O BRModelo criou uma estrutura separada para cada relacionamento?
2. Como é possível identificar no modelo lógico qual tabela associativa representa a coordenação e qual representa a colaboração?
3. Por que os dois relacionamentos não devem ser misturados em uma única tabela?
4. Como os nomes das tabelas e das chaves estrangeiras podem deixar explícito o papel de cada associação?
5. Um mesmo funcionário pode ser coordenador de um projeto e colaborador de outro? Como o modelo lógico representa essa situação?
6. O fato de duas entidades possuírem mais de um relacionamento altera a regra geral de mapeamento? Justifique.

### 3. Mapeamento dos relacionamentos e chaves estrangeiras

Observe cada relacionamento separadamente e responda:

1. Quais tabelas associativas foram criadas para representar os relacionamentos N:N?
2. Quais chaves estrangeiras foram colocadas em cada tabela associativa?
3. Como cada chave estrangeira referencia a tabela de origem?
4. As chaves estrangeiras dos dois relacionamentos possuem nomes distintos ou genéricos? Que nomes você utilizaria para tornar o papel mais claro?
5. O relacionamento de coordenação da versão final continua sendo 1:N ou tornou-se N:N por causa do histórico? Explique.
6. O relacionamento de colaboração é 1:N ou N:N? Como as cardinalidades do modelo conceitual influenciaram essa decisão?

### 4. Atributos e dados históricos

Analise o tratamento dos períodos no modelo lógico e responda:

1. Por que os atributos `data_inicio` e `data_fim`  pertencem à relação entre funcionário e projeto, e não diretamente a `Funcionario` ou `Projeto`?
2. Como o modelo lógico permite registrar que funcionários diferentes coordenaram o mesmo projeto em períodos diferentes?
3. Qual é a diferença entre armazenar apenas o coordenador atual e armazenar o histórico de coordenadores?
4. Como uma consulta poderia descobrir quem coordenava determinado projeto em uma data específica?

### 5. Comparação com relacionamentos 1:N e 1:1

Compare os relacionamentos da atividade com os exemplos estudados na dinâmica e responda:

1. Em um relacionamento 1:1, por que é possível escolher para qual lado levar a chave estrangeira?
2. Considerando o exemplo de chefia atual entre `Funcionario` e `Departamento`, por que poderia ser conveniente colocar `id_chefe` em `Departamento`?

### 6. Conferência do modelo gerado

Faça uma revisão final do modelo lógico e responda:

1. Todas as entidades do modelo conceitual foram transformadas em tabelas?
2. Cada relacionamento entre `Funcionario` e `Projeto` foi representado separadamente?
3. As tabelas associativas possuem as chaves estrangeiras corretas?
4. Os atributos dos relacionamentos foram mantidos nas tabelas associativas correspondentes?
5. O modelo consegue representar mais de um coordenador para o mesmo projeto em períodos diferentes?
6. O modelo consegue representar vários colaboradores em um projeto?
7. O modelo consegue registrar a função e o período de cada colaboração?
8. Os nomes gerados automaticamente pelo BRModelo deixam claros os papéis exercidos? Se não, quais nomes devem ser ajustados?
9. Você identificou alguma decisão automática do BRModelo que precisaria ser revisada? Justifique.

---

## Conclusão

Quando duas entidades possuem mais de um relacionamento, cada associação deve ser mapeada individualmente. A existência de múltiplos relacionamentos não muda as estratégias de transformação, mas exige que seus significados, atributos e chaves sejam mantidos separados e identificáveis.

Quando é necessário armazenar histórico, uma relação que representava apenas o estado atual pode precisar registrar várias ocorrências ao longo do tempo. Os atributos de período, como `data_inicio` e `data_fim`, devem ser associados à ocorrência correspondente, permitindo consultar não apenas a situação atual, mas também as situações anteriores.

---

**Bom trabalho!**

[Voltar para o Arquivo Principal da Dinâmica 3](../dinamica3.md)

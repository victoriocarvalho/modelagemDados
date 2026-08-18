# Atividade de Modelagem Conceitual de Dados

## MER - Múltiplos Relacionamentos entre Mesmas Entidades e Necessidade de dados históricos (snapshot vs. histórico)

**Atividade Individual**

---

## Cenário: Empresa de Projetos

Uma empresa de consultoria e desenvolvimento deseja implementar um sistema para gerenciar seus projetos e a alocação de funcionários neles.

A empresa mantém um cadastro de seus **funcionários**. De cada funcionário deseja-se armazenar seu número de matrícula (que o identifica unicamente), nome completo, especialidade e email corporativo.

A empresa também gerencia vários **projetos**. De cada projeto deseja-se armazenar um código do projeto (que o identifica unicamente), nome do projeto, descrição e data de início.

Um **funcionário pode participar de um projeto de duas formas distintas**:

1. **Como coordenador**: Cada projeto **tem exatamente um funcionário como coordenador**. Um funcionário pode coordenar vários projetos ou não coordenar nenhum.

2. **Como colaborador**: Um projeto pode ter **vários funcionários como colaboradores** (além do coordenador). Um funcionário pode colaborar em vários projetos. Para cada colaboração, deseja-se registrar qual é a **função do funcionário no projeto** (por exemplo: "Desenvolvedor Backend", "Analista de Requisitos", "Testador", "Arquiteto", etc.).

**Importante**: Um funcionário que é coordenador de um projeto **também pode ser colaborador** em outros projetos .

---

## Tarefa

Desenvolva um **Modelo Entidade Relacionamento (MER)** para o cenário descrito acima utilizando a ferramenta **BRModelo**.

### Requisitos do Modelo:

1. **Identifique as 2 entidades** mencionadas no cenário
2. **Defina os atributos** de cada entidade
3. **Indique o atributo identificador** de cada entidade
4. **Represente os relacionamentos e indique corretamente as cardinalidades**

### Dicas:

- Existem dois relacionamentos entre as mesmas duas entidades! Ambos devem estar representados no diagrama
- O relacionamento de Colaboração possui um atributo: "função" ou "função_colaborador"
- Observe que as cardinalidades mínimas também são importantes: um projeto **deve** ter um coordenador, mas um funcionário **pode não** coordenar nenhum projeto

---

## Tarefa 2 - Histórico e Períodos de Alocação

Considere a seguinte evolução do cenário:

A empresa percebeu que **nem sempre um funcionário será o coordenador de um projeto por todo seu ciclo de vida**. Coordenadores podem ser alterados! Por exemplo:

- **João** foi coordenador do **Projeto A** de 01 de janeiro a 10 de março
- **José** foi coordenador do **Projeto A** de 11 de março até o final do projeto (atual)

Além disso, também queremos guardar **quando cada colaborador trabalhou** no projeto, não apenas quem trabalhou. Por exemplo:

- **Maria** foi "Desenvolvedora Frontend" no **Projeto A** de 01 de janeiro a 28 de fevereiro
- **Pedro** foi "Testador" no **Projeto A** de 01 de fevereiro até agora


### Questões Reflexivas:

1. **Limitação do Modelo Anterior**: Seu modelo anterior consegue armazenar **todo o histórico** de coordenadores de um projeto? Ou apenas o coordenador atual?

2. **Mudança Fundamental**: Para capturar o histórico completo, como você precisaria alterar o relacionamento de Coordenação?
   - **Dica**: O relacionamento de Coordenação deixaria de ser 1:N e passaria a ser N:N! Afinal, um projeto pode ter vários coordenadores (em períodos diferentes) e um funcionário pode ter coordenado vários projetos.

3. **Novos Atributos**: Se o relacionamento de Coordenação vira N:N, quais atributos ele precisaria ter para representar os períodos?



Considerando esses fatores Desenvolva uma **nova versão do seu modelo MER** que mapeie esse novo cenário.



---

## Para Refletir


1. **Reflita sobre as mudanças**: Como a adição de períodos afeta a compreensão do modelo? Quais consultas o sistema agora consegue fazer que não conseguia antes?


Analise o seu modelo original (primeira versão) e responda aos seguintes questionamentos:

1. **Visualização de Relacionamentos**: Como o BRModelo permite representar dois relacionamentos diferentes entre as mesmas duas entidades? Os relacionamentos ficam claramente distintos no diagrama?

2. **Atributo em N:N**: O relacionamento de Colaboração tem um atributo ("função"). Este atributo é importante porque:
   - Não é uma propriedade do Funcionário (um funcionário pode ter funções diferentes em projetos diferentes)
   - Não é uma propriedade do Projeto (um projeto pode ter funcionários em diferentes funções)
   - É uma propriedade específica **da relação entre funcionário e projeto**

3. **Caso Real**: Imagine o seguinte cenário:
   - **João** é o coordenador do **Projeto A**
   - **João** também colabora no **Projeto B** como "Arquiteto"
   - **Maria** colabora no **Projeto A** como "Desenvolvedora Frontend"

   Seu modelo MER consegue representar corretamente esta situação? Como?

4. **Cardinalidades Mínimas**: Discuta as cardinalidades mínimas:
   - Um projeto **sempre** precisa ter um coordenador? (cardinalidade mínima 1)
   - Um funcionário **precisa** coordenar pelo menos um projeto? (cardinalidade mínima 0)

5. **Evolução do Modelo**: Como seu modelo evoluiu entre a primeira e terceira versão? Quais foram as principais mudanças nas entidades e relacionamentos?

---

**Data de Entrega:** Conforme indicado no cronograma da disciplina

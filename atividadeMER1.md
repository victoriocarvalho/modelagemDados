# Atividade de Modelagem Conceitual de Dados

**Atividade Individual**

---

## Cenário: Clínica Veterinária

Uma pequena clínica veterinária deseja criar um sistema para gerenciar seus atendimentos. A clínica dispõe de vários veterinários e atende diversos clientes com seus animais de estimação.

Sobre cada **veterinário** deseja-se armazenar seu número de matrícula (que o identifica unicamente), nome completo, especialidade e telefone para contato.

A clínica precisa manter um cadastro de **clientes**. De cada cliente deseja-se registrar seu CPF (que o identifica unicamente), nome, endereço e telefone.

Os clientes levam seus **animais de estimação** para consultas. De cada animal deseja-se armazenar um número de registro (que o identifica unicamente), nome, tipo de animal (cão, gato, pássaro, etc.), raça e data de nascimento. Cada animal pertence a um único cliente.

Quando um cliente leva seu animal à clínica, é feito um **atendimento/consulta**. Sobre cada consulta deseja-se armazenar o número da consulta (que a identifica unicamente), a data e hora, o diagnóstico fornecido, o valor cobrado e o veterinário responsável. Cada consulta envolve um único veterinário e um único animal.

---

## Tarefa

Desenvolva um **Modelo Entidade Relacionamento (MER)** para o cenário descrito acima. Utilize a ferramenta **BRModelo** para criar seu diagrama.

### Requisitos do Modelo:

1. **Identifique todas as entidades** mencionadas no cenário
2. **Defina os atributos** de cada entidade com seus respectivos tipos
3. **Indique o atributo identificador** de cada entidade
4. **Represente os relacionamentos** entre as entidades com suas respectivas cardinalidades
5. **Verifique a consistência** do modelo em relação à descrição do cenário

## Para Refletir

Conceitos importantes sobre cardinalidade:

**Cardinalidade** é a quantidade de ocorrências de uma entidade que se relacionam com ocorrências de outra entidade. Cada relacionamento possui dois aspectos de cardinalidade:

- **Cardinalidade Mínima**: qual é a quantidade mínima de ocorrências relacionadas (normalmente é 0 ou 1)
- **Cardinalidade Máxima**: qual é a quantidade máxima de ocorrências relacionadas (normalmente é 1 ou n)

Assim, um relacionamento pode ser representado como (cardinalidade_mínima, cardinalidade_máxima) em cada lado.

### Questões para Análise:

1. **Análise de seus relacionamentos**: Examine todos os relacionamentos do seu modelo. Para cada um, escreva qual é a cardinalidade máxima de cada lado da relação.

2. **Padrão observado**: Qual padrão você observa? Em todos os relacionamentos, qual é a distribuição de cardinalidades máximas?

3. **Relacionamentos N:N**: É possível existir um relacionamento onde a cardinalidade máxima seja N (muitos) dos dois lados? Dê um exemplo conceptual.

4. **Caso de estudo**: No cenário da clínica, como seria se o relacionamento entre **Animal de Estimação** e **Consulta** fosse de muitos-para-muitos (N:N) em vez de um-para-muitos (1:N)? Qual seria o significado disso no mundo real? Faria sentido para o sistema da clínica?

**Bom trabalho!**
# Atividade de Modelo Físico de Dados

**Atividade Individual**

---

## Tarefa

A partir do modelo lógico produzido na atividade anterior, crie o **modelo físico** para este cenário. Utilize a ferramenta **BRModelo** para gerar o script SQL de criação do esquema e execute este script em um banco PostgreSQL no Aiven, utilizando o **DBeaver**.

### Requisitos do Modelo Físico:

1. **Crie o esquema do banco** em SQL usando DDL
2. **Defina as tabelas** correspondentes às entidades do modelo lógico
3. **Defina os tipos dos atributos** de cada tabela
4. **Crie as chaves primárias**
5. **Crie as chaves estrangeiras** e restrições de integridade referencial
6. **Verifique a consistência** do esquema em relação ao modelo lógico
7. **Execute o script** no banco PostgreSQL do Aiven pelo DBeaver

---

## Passo a passo sugerido

### 1. Criação do modelo físico no BRModelo

Use o BRModelo para gerar o script de criação do esquema a partir do modelo lógico. O objetivo desta etapa é transformar as tabelas e relacionamentos em instruções SQL.
O script SQL deve conter comandos de criação das tabelas e das restrições.

### 2. Criação do banco no Aiven

Crie o banco de dados no Aiven:
    1 - Faça login no aiven
    2 - Verifique que seu serviço esteja rodando
    3 - Clique sobre o nome do seu serviço para abrir os detalhes
    4 - Na barra do lado direito selecione a opção databases e depois clique em adicionar database.
    5 - Defina o nome "dinamica1" para seu banco de dados.

### 3. Criação do Esquema do banco pelo DBeaver
1 - Crie uma nova conexão no Dbeaver para se conectar com o banco que acabou de criar no aiven. Para isso siga os mesmos passos que sigamos em nossa ultima aula, só alterando o nome do banco de "defaultdb" para "dinamica1".
2 - Conecte no banco pelo Dbeaver e aba uma nova janela de Script SQL com esse banco.
3 - Gere o modelo físico pelo BRModelo , copie o sript gerado para a janela de scripts do Dbeaver e execute (como fizemos na última aula).
4 - Verifique se as tabelas foram geradas corretamente.

---

## Para Refletir

O modelo físico é a etapa em que o banco deixa de ser apenas um desenho conceitual e passa a existir como estrutura real no SGBD. Nessa fase, o que antes era uma representação lógica de entidades e relacionamentos se transforma em código SQL que o banco entende e executa.

### Questões para Análise:

1. **Estrutura do banco**: Leia os comandos SQL executados. É possível inferir o que todos eles fazem? Algum detalhe chama atenção ou é mais difícil de entender? Qual é a relação entre o modelo lógico e o modelo físico?

2. **Comparação com o modelo lógico**: O que mudou entre o modelo lógico e o modelo físico? O que foi acrescentado na fase física?

3. **Chaves primárias e estrangeiras**: Por que as chaves primárias e estrangeiras são fundamentais no modelo físico?

4. **Integridade de dados**: Como as restrições de integridade referencial ajudam a evitar dados inconsistentes?

5. **Testes Práticos**: Faça os seguintes testes e responda o que se pede:

- Abra as tabelas no modo de "dados" do DBeaver e insira registros. Tente inserir um animal informando um id_cliente inexistente. Foi possível? Por que?

- Insira agora 2 registros de clientes e 2 de animais (um relacionado a cada cliente). Em seguida tente excluir os dados de um dos clientes? O que aconteceu? O banco aceitou? Se sim, o que aconteceu com o registro do animal associado ao cliente excluído? Por que?

---

**Bom trabalho!**

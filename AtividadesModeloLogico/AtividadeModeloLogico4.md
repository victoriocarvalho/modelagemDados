# Atividade de Modelo Lógico 4

**Atividade individual**

---

## Objetivo

Nesta atividade, você deve transformar em um **modelo lógico** a versão final do modelo conceitual desenvolvido na [atividadeMER4.md](../AtividadesModeloConceitual/atividadeMER4.md), referente ao cenário da loja varejista.

O objetivo é observar como atributos compostos e multivalorados são convertidos para o modelo relacional. Verifique especialmente como o `endereco` e os `telefones` de `Cliente` e `Vendedor` são representados em tabelas, colunas, chaves primárias e chaves estrangeiras.

---

## Modelo conceitual de origem

Utilize como ponto de partida a versão final do modelo conceitual criada na [atividadeMER4.md](../AtividadesModeloConceitual/atividadeMER4.md). Antes de iniciar a transformação, confira se o modelo contém:

- As entidades `Cliente`, `Vendedor`, `Produto`, `Categoria` e `Venda`.
- Os atributos identificadores e demais atributos de cada entidade.
- O atributo composto `endereco` de `Cliente` e `Vendedor`, formado por tipo do logradouro, nome do logradouro, número, complemento, bairro, cidade e estado.
- O atributo multivalorado `telefones` de `Cliente` e `Vendedor`.
- O relacionamento entre `Venda` e `Produto`, com os atributos `quantidade` e `preco_vendido` ou outro nome equivalente definido no modelo conceitual.

Revise os nomes dos atributos, os identificadores, os relacionamentos e as cardinalidades antes de iniciar a geração do modelo lógico.

---

## Tarefa: gerar o modelo lógico automaticamente

Crie o modelo lógico utilizando a **opção de geração automatizada do BRModelo**.

### Instruções

1. Abra no BRModelo a versão final do modelo conceitual desenvolvida na [atividadeMER4.md](../AtividadesModeloConceitual/atividadeMER4.md).
2. Confira se os atributos compostos `endereco` e os atributos multivalorados `telefones` estão definidos corretamente para `Cliente` e `Vendedor`.
3. Utilize a funcionalidade de geração automática do BRModelo para criar o modelo lógico.
4. Observe as tabelas, colunas, chaves primárias, chaves estrangeiras e tabelas associativas geradas.
5. Verifique se as partes de `endereco` foram transformadas em colunas nas tabelas de `Cliente` e `Vendedor`, sem a criação de uma coluna única chamada `endereco`.
6. Verifique se `telefones` foi transformado em uma ou mais tabelas próprias, com uma linha para cada telefone e uma chave estrangeira para o respectivo cliente ou vendedor.
7. Analise as chaves primárias das tabelas de telefones. Verifique se elas impedem o cadastro repetido do mesmo telefone para a mesma pessoa.
8. Observe como o relacionamento entre `Venda` e `Produto` foi transformado e onde foram colocados os atributos `quantidade` e `preco_vendido`.
9. Confira se o preço atual de `Produto` e o preço praticado em cada venda foram mantidos em locais diferentes, preservando o histórico das vendas.
10. Caso o BRModelo atribua nomes genéricos às tabelas ou às chaves estrangeiras, renomeie-os para nomes que deixem claro seu significado.
11. Salve o modelo lógico gerado no formato do BRModelo.

Nesta atividade, não é necessário criar uma versão manual. O foco é analisar o resultado da geração automatizada e verificar se ele segue as regras de transformação discutidas na aula.

### Entregável

- Um arquivo do BRModelo contendo o modelo lógico gerado automaticamente a partir da versão final da atividadeMER4.md.
- As respostas às questões de análise apresentadas a seguir.

---

## Questões para análise

### 1. Transformação do atributo composto `endereco`

Observe o tratamento do endereço de `Cliente` e `Vendedor` e responda:

1. As partes `tipo_logradouro`, `nome_logradouro`, `numero`, `complemento`, `bairro`, `cidade` e `estado` foram transformadas em colunas?
2. Em quais tabelas essas colunas foram colocadas?
3. Foi criada uma coluna única chamada `endereco`? Por que essa coluna não é necessária no modelo relacional?
4. Por que o atributo composto não gerou, neste caso, uma tabela `Endereco`?
5. Se dois clientes tiverem o mesmo endereço, como os valores aparecem no modelo lógico? Essa repetição é um problema para o contexto da atividade? Justifique.

### 2. Transformação do atributo multivalorado `telefones`

Observe as tabelas geradas para os telefones e responda:

1. Quantas tabelas o BRModelo criou para armazenar os telefones de `Cliente` e de `Vendedor`? Duas ou apenas uma?
2. Verifique a transposição de chaves feita pelo BRModelo entre `Cliente` e a tabela de telefone. Está correta? CUIDADO NESTE PONTO! A VERSÃO DO BRMODELO QUE USEI NOS TESTES ERROU NA TRASNFORMAÇÃO! VERIFIQUE COM CUIDADO E INDIQUE AQUI O ERRO OBSERVADO (SE OCORREU)
3. Garanta que o modelo final permita que um mesmo número pode ser cadastrado para pessoas diferentes mas não possa haver o mesmo número para a mesma pessoa duas vezes.

### 3. Transformação dos relacionamentos e atributos da venda

Analise o relacionamento entre `Venda` e `Produto` e responda:

1. Foi criada uma tabela associativa para representar os produtos de cada venda? Qual é o nome dela?
2. Quais chaves estrangeiras essa tabela recebeu?
3. Onde foram colocados os atributos `quantidade` e `preco_vendido`?
4. Por que `quantidade` e `preco_vendido` pertencem à associação entre venda e produto, e não diretamente a `Venda` ou `Produto`?
5. Onde foi armazenado o preço atual de venda do produto? Por que ele não deve substituir `preco_vendido` nas vendas já realizadas?

---

## Conclusão

No modelo relacional, um atributo composto é representado por suas partes em colunas da tabela da entidade. Já um atributo multivalorado exige uma tabela própria, com uma linha para cada valor e uma chave estrangeira para a entidade de origem. A geração automática do BRModelo ajuda a realizar essa transformação, mas o modelo gerado deve ser conferido para garantir que ele preserve as regras e o significado do modelo conceitual.

---

**Bom trabalho!**

[Voltar para o Arquivo Principal da Dinâmica 4](../dinamica4.md)

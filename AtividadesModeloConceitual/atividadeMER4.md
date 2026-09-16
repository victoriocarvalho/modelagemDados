# Atividade de Modelagem Conceitual de Dados

**Atividade Individual**

---

## Cenário: Loja Varejista

Uma loja varejista deseja criar um sistema para gerenciar seus clientes, vendedores, produtos e vendas.

A loja mantém um cadastro de **clientes**. De cada cliente deseja-se saber seu CPF (que o identifica unicamente), nome completo, idade, endereço, telefones para contato e data em que se tornou cliente. Um cliente pode possuir mais de um telefone cadastrado.

Também existe um cadastro de **vendedores**. De cada vendedor deseja-se saber seu número de matrícula (que o identifica unicamente), CPF (que o identifica unicamente), nome completo, idade, endereço, telefones para contato, salario e percentual de comissão. Um vendedor pode possuir mais de um telefone cadastrado.

Os endereços devem ser formados por tipo do logradouro, nome do logradouro, número, complemento, bairro, cidade e estado.

A loja comercializa diversos **produtos**. De cada produto deseja-se armazenar seu código (que o identifica unicamente), nome, descrição, preço de venda, quantidade disponível em estoque e categoria. Cada categoria tem um nome e define o percentual de ICMS a ser recolhido na venda dos produtos.

A loja também precisa registrar suas **vendas**. Para cada venda deseja-se armazenar seu número (que a identifica unicamente), data, cliente comprador e vendedor responsável. Uma venda pode conter vários produtos e um produto pode participar de várias vendas. Para cada produto vendido em uma venda, deseja-se registrar a quantidade vendida e o preço pelo qual foi vendido.

## Tarefa

Desenvolva um **Modelo Entidade Relacionamento (MER)** para o cenário descrito acima utilizando a ferramenta **BRModelo**.

## Para Refletir: endereço como atributo ou entidade

No cenário da loja, o `endereco` deve ser modelado como um atributo composto de `Cliente` e `Vendedor` ou como uma entidade própria? Considere que o endereço é formado por tipo do logradouro, nome do logradouro, número, complemento, bairro, cidade e estado.

Ao representá-lo como um atributo composto, cada cliente terá seu próprio valor de endereço. Assim, se dois clientes morarem no mesmo endereço, as partes desse endereço serão mantidas de forma independente no cadastro de cada cliente. Essa duplicação não é um problema neste contexto, pois o endereço está sendo utilizado apenas como uma informação do cliente: não é necessário identificar endereços, relacioná-los com outras entidades ou acompanhar sua existência separadamente.

Reflita: que necessidade do domínio poderia justificar a criação de uma entidade `Endereco`? Por exemplo, seria diferente se o sistema precisasse cadastrar cada endereço uma única vez, associá-lo a vários clientes, registrar alterações históricas ou relacioná-lo a outras entidades. Nesse caso, o endereço teria maior importância e independência dentro do domínio, e poderia ser modelado como uma entidade.

## Para Refletir: atributo idade ou data de nascimento

Um dos requisitos descritos no cenário é de se saber a idade dos vendedores e dos clientes. Nesse contexto a solução mais direta seria criar um atributo para armazenar a idade. Mas, será que esta seria uma boa opção?
Pense: a idade é calculada com base na data de nascimento do indivíduo. Se a idade for armazenada, eventualmente a informação ficará desatualizada. Mas, se a data de nascimento for armazenada e utilizada para calcular a idade sempre que necessário, você não terá o problema de desatualização do dado.
Este caso ilustra uma boa prática: evitar atributos calculados. Prefira atributos que sejam a base para os cálculos.

### Para Refletir: preço atual e preço histórico

O produto precisa armazenar seu preço atual de venda, mas cada item vendido também deve guardar o preço praticado naquela venda. Assim, uma alteração no preço atual não modifica o valor de vendas passadas. Essa decisão retoma a discussão da dinâmica anterior sobre a necessidade de preservar dados históricos.
Reflita: seu modelo permite armazenar o preço atual de venda do produto sem perder o preço pelo qual foi vendido? Como isso é feito? Teria outras formas de modelar o domíno para atender a esse requisito?

# Atividade de Modelagem Conceitual 5

**Atividade Individual**

---

## Cenário: Loja Varejista

Utilize o mesmo cenário da [atividadeMER4.md](atividadeMER4.md) e a versão final do modelo conceitual desenvolvida naquela atividade.

---

## Tarefa

A partir do modelo conceitual da atividadeMER4, crie uma nova versão do MER no BRModelo aplicando os conceitos de **herança** e **autorrelacionamento**.

### 1. Generalização de clientes e vendedores

Crie a entidade pai `Pessoa` e faça `Cliente` e `Vendedor` herdarem dela.

- Coloque em `Pessoa` os atributos comuns a clientes e vendedores.
- Faça `Cliente` e `Vendedor` herdarem os atributos de `Pessoa`, sem repetir esses atributos nas entidades filhas.
- Mantenha em `Vendedor` e em  `Cliente` os atributos específicos de cada papel.
- Preserve os demais relacionamentos e atributos do cenário da atividadeMER4.
- Represente a generalização com a notação de herança do BRModelo, utilizando o triângulo entre `Pessoa`, `Cliente` e `Vendedor`.

Lembre-se de que toda instância de `Cliente` e toda instância de `Vendedor` também é uma instância de `Pessoa`. A mesma pessoa pode exercer os dois papéis e, nesse caso, participar simultaneamente das entidades `Cliente` e `Vendedor`.

### 2. Autorrelacionamento de tutoria

Acrescente ao modelo o relacionamento `tutoria` entre vendedores:

- Um vendedor pode ter nenhum ou um vendedor `tutor`.
- Um vendedor pode ser `tutor` de zero ou vários outros vendedores.
- O relacionamento ocorre entre duas instâncias da entidade `Vendedor`; não crie uma nova entidade para representar o tutor.
- Identifique as extremidades com os papéis `tutor` e `tutorado`.

## Entregável

- Um arquivo do BRModelo contendo a nova versão do modelo conceitual.
- A entidade pai `Pessoa`, com a generalização para `Cliente` e `Vendedor`.
- O autorrelacionamento `tutoria`, com os papéis e as cardinalidades corretos.

## Para Refletir

Reflita sobre as vantagens de identificar o conceito de `Pessoa` no modelo. Essa generalização torna mais fácil perceber, por exemplo, que uma mesma pessoa pode ser simultaneamente `Cliente` e `Vendedor`, sem que seja necessário tratá-la como duas pessoas diferentes. Pense também em como a identificação dos atributos comuns pode evitar repetições e tornar o modelo mais fiel ao domínio.

---

**Bom trabalho!**

[Voltar para o Arquivo Principal da Dinâmica 5](../dinamica5.md)

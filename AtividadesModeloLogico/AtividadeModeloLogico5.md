# Atividade de Modelo Lógico 5

**Atividade individual**

---

## Objetivo

Nesta atividade, você deve transformar em um **modelo lógico** a versão final do modelo conceitual desenvolvida na [atividadeMER5.md](../AtividadesModeloConceitual/atividadeMER5.md), referente ao cenário da loja varejista.

O foco será observar como o BRModelo transforma a hierarquia de herança entre `Pessoa`, `Cliente` e `Vendedor` e como mapeia o autorrelacionamento `tutoria` entre vendedores.

---

## Tarefa: gerar o modelo lógico automaticamente

Crie o modelo lógico utilizando a **opção de geração automatizada do BRModelo**.

### Instruções

1. Abra no BRModelo a versão final do modelo conceitual desenvolvida na [atividadeMER5.md](../AtividadesModeloConceitual/atividadeMER5.md).
2. Revise a entidade pai `Pessoa`, as entidades filhas `Cliente` e `Vendedor`, o relacionamento de herança e o autorrelacionamento `tutoria`.
3. Utilize a funcionalidade de geração automática do BRModelo para criar o modelo lógico.
4. Observe que o BRModelo apresenta três opções de transformação da hierarquia de herança. Escolha a opção que você considerar mais adequada ao cenário.
5. Observe as tabelas, colunas, chaves primárias e chaves estrangeiras geradas para a herança e para o autorrelacionamento.
6. Verifique se a transformação escolhida preservou os atributos comuns de `Pessoa`, os atributos específicos de `Cliente` e `Vendedor` e os papéis da tutoria.
7. Salve o modelo lógico gerado no formato do BRModelo.

Nesta atividade, não é necessário criar uma versão manual. O objetivo é analisar a estratégia escolhida pelo BRModelo e verificar se o resultado segue as regras discutidas na aula.

### Entregável

- Um arquivo do BRModelo contendo o modelo lógico gerado automaticamente a partir da versão final da atividadeMER5.md.
- As respostas às questões de análise apresentadas a seguir.

---

## Questões para análise

### 1. Herança

Analise a transformação da hierarquia `Pessoa`–`Cliente`–`Vendedor` e responda:

1. Qual das três opções de transformação de herança você escolheu no BRModelo?
2. Por que você considerou essa opção a mais adequada para o cenário da loja?
3. A transformação gerada pelo BRModelo foi feita corretamente, conforme esperado? Verifique se os atributos comuns, os atributos específicos e as chaves foram mapeados de acordo com a estratégia escolhida.
4. Faça novas transformações utilizando, separadamente, as outras duas estratégias de mapeamento de herança. Observe e compare os modelos lógicos gerados.

### 2. Autorrelacionamento

Analise a transformação do relacionamento `tutoria` e responda:

1. O BRModelo mapeou corretamente o autorrelacionamento? Observe especialmente a criação da chave estrangeira na própria tabela `Vendedor`, referenciando a chave primária dessa mesma tabela.

---

**Bom trabalho!**

[Voltar para o Arquivo Principal da Dinâmica 5](../dinamica5.md)

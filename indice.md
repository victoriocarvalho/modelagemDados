# Atividades de Modelagem Conceitual de Dados

## Índice de Atividades MER

Bem-vindo ao conjunto de atividades sobre Modelo Entidade-Relacionamento (MER)! Abaixo estão todas as atividades organizadas em ordem de complexidade incremental.

---

## [Atividade 1: Clínica Veterinária](AtividadesModeloConceitual/atividadeMER1.md)

**Conceitos abordados:**
- Identificação de entidades
- Definição de atributos simples e monovalorados
- Atributos identificadores (chaves primárias)
- Relacionamentos **1 para N** (um-para-muitos)
- Análise de cardinalidades

**Descrição:**
Nesta atividade você desenvolverá um modelo para uma clínica veterinária. O cenário apresenta entidades com relacionamentos simples, onde todos os relacionamentos são do tipo 1:N. A atividade inclui uma seção "Para Refletir" que o induz a pensar sobre cardinalidades máximas e a possibilidade de relacionamentos N:N.

---

## [Atividade 2: Escola de Línguas](AtividadesModeloConceitual/atividadeMER2.md)

**Conceitos abordados:**
- Relacionamentos **N para N** (muitos-para-muitos)
- Atributos em relacionamentos N:N
- Restrições de integridade
- Limitações do modelo MER

**Descrição:**
Nesta atividade você modelará um sistema para uma escola de idiomas. O foco principal é compreender relacionamentos N:N e como nem todas as regras de negócio podem ser capturadas diretamente no diagrama. A atividade também inclui uma segunda tarefa sobre como representar atributos nos relacionamentos N:N, consolidando o aprendizado sobre a importância de caracterizar relacionamentos adequadamente.

---

## [Atividade 3: Empresa de Projetos](AtividadesModeloConceitual/atividadeMER3.md)

**Conceitos abordados:**
- Múltiplos relacionamentos entre as mesmas duas entidades
- Relacionamentos com papéis distintos (coordenador vs. colaborador)
- Cardinalidades diferentes entre relacionamentos
- Atributos em relacionamentos
- Modelagem de cenários mais complexos

**Descrição:**
Nesta atividade você modelará um sistema de gerenciamento de projetos onde uma mesma empresa possui funcionários e projetos. A complexidade aqui é a existência de **dois relacionamentos distintos entre as mesmas entidades**: um funcionário pode ser coordenador de um projeto (relação 1:N) ou colaborador em um projeto (relação N:N com atributo de função). Este cenário consolidar o aprendizado sobre como representar múltiplos papéis que uma entidade pode ter em relação a outra.

---

## Orientações Gerais

### Ferramenta a Utilizar
Utilize a ferramenta **BRModelo** para criar todos os seus diagramas.

### Formato de Entrega
Para cada atividade, você deve:
1. Fazer uma cópia do arquivo de descrição
2. Incluir a imagem do seu modelo MER no arquivo
3. Gerar um PDF contendo o diagrama
4. Postar no AVA conforme cronograma

### Dicas para Sucesso
- Leia o cenário com atenção
- Identifique todas as entidades mencionadas
- Determine os atributos de cada entidade
- Indique claramente as chaves primárias
- Represente os relacionamentos com as cardinalidades corretas
- Responda às questões de reflexão para consolidar o aprendizado

---

**Bom trabalho!** 📚

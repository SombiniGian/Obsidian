# Tabela TB_PROD_CODIGO_BARRAS

**Módulo:** Cadastros / Estoque
Códigos de barras associados aos produtos, permitindo múltiplos códigos por produto, indicação do principal e controle de conversão de unidade.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRDC_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave de relacionamento. |
| `PRDC_PRODUTO` | INTEGER | Não | Identificador do produto (TB_PRODUTO.PRD_ID). |
| `PRDC_COD_BARRAS` | VARCHAR(20) | Não | Código de barras do produto. |
| `PRDC_SEQUENCIA` | INTEGER | Sim | Sequencial do código de barras para o produto. |
| `PRDC_PRINCIPAL` | VARCHAR(1) | Sim | Indica o principal código de barras do produto, usado em relatórios quando necessário (S/N). |
| `PRDC_CONVERSAO` | VARCHAR(1) | Sim | Indica se o código está associado a uma conversão de unidade (S/N). |

COMMENT ON COLUMN TB_PROD_CODIGO_BARRAS.PRDC_PRINCIPAL IS 'principal codigo de barras do produto
 aquele que sera impresso em relatorios qdo preciso';

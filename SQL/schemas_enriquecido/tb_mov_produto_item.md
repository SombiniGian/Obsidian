# Tabela TB_MOV_PRODUTO_ITEM

**Módulo:** Estoque
Itens de uma movimentação de produtos. Detalha o produto, a quantidade, os valores e se cada item representa entrada ou saída.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `MVPI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `MVPI_MOV_PRODUTO` | INTEGER | Não | Identificador da movimentação de produtos (TB_MOV_PRODUTO.MVP_ID). Parte da chave primária composta. |
| `MVPI_SEQUENCIA` | INTEGER | Não | Sequencial do item na movimentação. Parte da chave primária composta. |
| `MVPI_PRODUTO` | INTEGER | Sim | Identificador do produto movimentado (TB_PRODUTO.PRD_ID). |
| `MVPI_QUANTIDADE` | NUMERIC(15,4) | Sim | Quantidade movimentada do produto. |
| `MVPI_VALOR_UNITARIO` | NUMERIC(15,4) | Sim | Valor unitário do produto. |
| `MVPI_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do item. |
| `MVPI_UNIDADE` | VARCHAR(3) | Sim | Unidade de medida do item. |
| `MVPI_TIPO_MOV` | VARCHAR(1) | Sim | Tipo de movimento: E = Entrada, S = Saída. |
| `MVPI_OBSERVACAO` | VARCHAR(2000) | Sim | Observações do item. |

COMMENT ON COLUMN TB_MOV_PRODUTO_ITEM.MVPI_TIPO_MOV IS 'E - ENTRADA
S - SAIDA';

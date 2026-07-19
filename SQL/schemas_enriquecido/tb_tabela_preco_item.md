# Tabela TB_TABELA_PRECO_ITEM

**Módulo:** Comercial / Vendas
Itens da tabela de preço (TB_TABELA_PRECO) com o preço de venda específico por unidade de medida para cada produto.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TBP_TABELA_PRECO` | INTEGER | Não | FK para TB_TABELA_PRECO.TBP_ID. Parte da chave primária composta. |
| `TBP_SEQUENCIA` | INTEGER | Não | Sequencial do item dentro da tabela. Parte da chave primária composta. |
| `TBP_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID. Parte da chave primária composta. |
| `TBP_PRECO_VENDA` | NUMERIC(15,6) | Sim | Preço de venda do produto nesta tabela. |
| `TBP_UNIDADE` | VARCHAR(6) | Não | Unidade de medida à qual o preço se refere (UN, KG, LT, etc.). |
| `TBP_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção (S/N). |
| `TBP_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. Default: current_timestamp. |
| `TBP_EXTRA1` | VARCHAR(30) | Sim | Campo adicional para uso genérico/integrador. |

COMMENT ON COLUMN TB_TABELA_PRECO_ITEM.TBP_PRODUTO IS 'FK para TB_PRODUTO.PRD_ID — use JOIN com TB_PRODUTO para obter descrição do produto.';

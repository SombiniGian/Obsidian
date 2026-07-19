# Tabela TB_TABELA_PRECO_ITEM_GRUPO

**Módulo:** Comercial / Vendas
Permite aplicar valores/percentuais da tabela de preço por grupo/subgrupo de produtos, sem precisar cadastrar item a item. Complementa TB_TABELA_PRECO_ITEM.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TBP_TABELA_PRECO` | INTEGER | Não | FK para TB_TABELA_PRECO.TBP_ID. Parte da chave primária composta. |
| `TBP_SEQUENCIA` | INTEGER | Não | Sequencial do item dentro da tabela. Parte da chave primária composta. |
| `TBP_GRUPO` | INTEGER | Não | FK para TB_PROD_GRUPO.PGRU_ID. Parte da chave primária composta. |
| `TBP_VALOR` | NUMERIC(15,6) | Sim | Valor/percentual aplicado aos produtos do grupo/subgrupo. |
| `TBP_TIPO` | VARCHAR(1) | Não | Indica se o valor é percentual ou monetário (D=Desconto, A=Acréscimo, P=Percentual). |
| `TBP_SUBGRUPO` | INTEGER | Sim | FK para TB_PROD_SUB_GRUPO.PSGR_ID — opcional, restringe ao subgrupo. |

COMMENT ON COLUMN TB_TABELA_PRECO_ITEM_GRUPO.TBP_TIPO IS 'Tipo de aplicação da tabela para o grupo (ver TB_TABELA_PRECO.TBP_TIPO).';

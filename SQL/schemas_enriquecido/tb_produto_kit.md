# Tabela TB_PRODUTO_KIT

**Módulo:** Estoque / Vendas
Composição de kits de produtos: define quais produtos compõem um kit (TB_PRODUTO.PRD_ID), a quantidade, valor e data de início de validade da composição. Cada registro associa o produto-kit a um produto componente.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRDK_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PRDK_PRODUTO_KIT` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID — produto-kit (o kit vendido). Parte da chave primária composta. |
| `PRDK_PRODUTO_COMPOEM` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID — produto que compõe o kit. Parte da chave primária composta. |
| `PRDK_QUANTIDADE` | NUMERIC(15,4) | Sim | Quantidade do produto componente dentro do kit. |
| `PRDK_DT_INICIO` | DATE | Sim | Data de início da validade da composição do kit. |
| `PRDK_VALOR` | NUMERIC(15,4) | Sim | Valor do componente dentro do kit. |

COMMENT ON COLUMN TB_PRODUTO_KIT.PRDK_PRODUTO_KIT IS 'FK para TB_PRODUTO.PRD_ID — identifica o kit. Use JOIN com TB_PRODUTO para obter descrição do kit.';
COMMENT ON COLUMN TB_PRODUTO_KIT.PRDK_PRODUTO_COMPOEM IS 'FK para TB_PRODUTO.PRD_ID — identifica o produto componente. Use JOIN com TB_PRODUTO para obter descrição do componente.';

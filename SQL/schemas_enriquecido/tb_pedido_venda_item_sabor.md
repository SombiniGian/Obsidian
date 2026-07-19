# Tabela TB_PEDIDO_VENDA_ITEM_SABOR

**Módulo:** Vendas / Restaurante
Sabores selecionados em um item de pedido de venda do tipo pizza (TB_PEDIDO_VENDA_ITEM), registrando valor, quantidade e preço de venda por sabor para rateio e composição do valor total do item.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PVSB_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PVSB_PEDIDO_VENDA` | INTEGER | Não | Identificador do pedido de venda (TB_PEDIDO_VENDA.PEV_ID). Parte da chave primária composta. |
| `PVSB_ITEM` | INTEGER | Não | Sequencial do item do pedido ao qual o sabor pertence. Parte da chave primária composta. |
| `PVSB_SABOR` | INTEGER | Não | FK para TB_SABOR — sabor selecionado no item. Parte da chave primária composta. |
| `PVSB_VALOR` | NUMERIC(15,6) | Sim | Valor total do sabor no item. |
| `PVSB_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade do sabor aplicada ao item. |
| `PVSB_VALOR_UNITARIO` | NUMERIC(15,6) | Sim | Valor unitário do sabor. |
| `PVSB_PRECO_VENDA` | NUMERIC(15,6) | Sim | Preço de venda do sabor. |

COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM_SABOR.PVSB_PEDIDO_VENDA IS 'FK para TB_PEDIDO_VENDA.PEV_ID — use JOIN com TB_PEDIDO_VENDA para obter dados do pedido.';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM_SABOR.PVSB_SABOR IS 'FK para TB_SABOR — use JOIN com TB_SABOR para obter a descrição do sabor.';

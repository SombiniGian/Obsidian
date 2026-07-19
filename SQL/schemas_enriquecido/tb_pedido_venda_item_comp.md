# Tabela TB_PEDIDO_VENDA_ITEM_COMP

**Módulo:** Vendas / Restaurante
Complementos adicionais ou retiradas vinculadas a um item de pedido de venda (TB_PEDIDO_VENDA_ITEM). Permite registrar valor, quantidade e grupo de complemento aplicado ao item, replicando o comportamento de adicionais de pizza/itens personalizáveis.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PEVC_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PEVC_PEDIDO_VENDA` | INTEGER | Não | Identificador do pedido de venda (TB_PEDIDO_VENDA.PEV_ID). Parte da chave primária composta. |
| `PEVC_ITEM` | INTEGER | Não | Sequencial do item do pedido ao qual o complemento pertence. Parte da chave primária composta. |
| `PEVC_COMPLEMENTO` | INTEGER | Não | FK para TB_COMPLEMENTO.COM_ID — complemento aplicado ao item. Parte da chave primária composta. |
| `PEVC_TIPO` | VARCHAR(1) | Sim | Tipo do complemento (A = Adicionar, R = Retirar). |
| `PEVC_VALOR` | NUMERIC(15,4) | Sim | Valor total do complemento aplicado ao item. |
| `PEVC_QUANTIDADE` | NUMERIC(15,4) | Sim | Quantidade do complemento aplicada ao item. |
| `PEVC_GRUPO` | INTEGER | Sim | FK para o grupo de complemento ao qual o item pertence. |
| `PEVC_VALOR_UNITARIO` | NUMERIC(15,4) | Sim | Valor unitário do complemento. |

COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM_COMP.PEVC_COMPLEMENTO IS 'FK para TB_COMPLEMENTO.COM_ID — use JOIN com TB_COMPLEMENTO para obter descrição e tipo do complemento.';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM_COMP.PEVC_PEDIDO_VENDA IS 'FK para TB_PEDIDO_VENDA.PEV_ID — use JOIN com TB_PEDIDO_VENDA para obter dados do pedido.';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM_COMP.PEVC_TIPO IS 'A - ADICIONAR
R - RETIRAR';

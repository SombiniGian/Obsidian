# Tabela TB_CARGA_COLETA_ITEM

**Módulo:** Logística / Coleta
Itens (pedidos) vinculados a uma carga de coleta, com a ordem de coleta/entrega.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CARCI_EMPRESA` | INTEGER | Não | Identificador da empresa. |
| `CARCI_CARGA` | INTEGER | Não | FK para TB_CARGA_COLETA.CARC_ID. |
| `CARCI_PEDIDO` | INTEGER | Não | Identificador do pedido de coleta. |
| `CARCI_SEQUENCIA` | INTEGER | Não | Sequencial do item. |
| `CARCI_ORDEM_ENTREGA` | INTEGER | Sim | Ordem em que o pedido deve ser coletado. |

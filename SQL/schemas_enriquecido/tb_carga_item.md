# Tabela TB_CARGA_ITEM

**Módulo:** Cargas / Logística
Tabela de itens (pedidos) vinculados a uma carga para entrega/coleta. Define a ordem em que cada pedido deve ser entregue dentro da carga.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CARGI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `CARGI_CARGA` | INTEGER | Não | FK para TB_CARGA. Identificador da carga. Parte da chave primária composta. |
| `CARGI_PEDIDO` | INTEGER | Não | FK para TB_PEDIDO_VENDA (ou TB_PEDIDO_COMPRA) vinculado à carga. Parte da chave primária composta. |
| `CARGI_SEQUENCIA` | INTEGER | Não | Sequencial do item dentro da carga. Parte da chave primária composta. |
| `CARGI_ORDEM_ENTREGA` | INTEGER | Sim | Ordem em que o pedido deve ser entregue na rota. |

# Tabela TB_INVENTARIO_ITEM

**Módulo:** Estoque
Itens do inventário de estoque, com as quantidades e preços contados, os valores calculados pelo sistema e a variação do produto quando aplicável.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `INVI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `INVI_INVENTARIO` | INTEGER | Não | Identificador do inventário (TB_INVENTARIO.INV_ID). Parte da chave primária composta. |
| `INVI_SEQUENCIA` | INTEGER | Não | Sequencial do item no inventário. Parte da chave primária composta. |
| `INVI_PRODUTO` | INTEGER | Sim | Identificador do produto inventariado (TB_PRODUTO.PRD_ID). |
| `INVI_UNIDADE` | VARCHAR(6) | Sim | Unidade de medida utilizada no inventário. |
| `INVI_UNITARIO` | NUMERIC(15,4) | Sim | Valor unitário considerado no inventário. |
| `INVI_VALOR_INVENTARIO` | NUMERIC(15,2) | Sim | Valor do item conforme a contagem do inventário. |
| `INVI_VALOR_CALCULADO` | NUMERIC(15,2) | Sim | Valor calculado pelo sistema com base no estoque e preço selecionados. |
| `INVI_QTDE_INVENTARIO` | NUMERIC(15,4) | Sim | Quantidade contada no inventário. |
| `INVI_QTDE_CALCULADO` | NUMERIC(15,4) | Sim | Quantidade calculada pelo sistema para comparação. |
| `INVI_NOVO_PRECO_VENDA` | NUMERIC(15,6) | Sim | Novo preço de venda apurado ou informado no inventário. |
| `INVI_VARIACAO` | INTEGER | Sim | Identificador da variação do produto (TB_PRODUTO_VARIACAO.PRV_ID). |

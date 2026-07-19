# Tabela TB_PEDIDO_VENDA_ITEM_KIT

**Módulo:** Vendas / Estoque
Itens de composição de kits vinculados aos itens de um pedido de venda. Registra os produtos componentes, quantidades, valores, unidade, peso, metragem e rateios utilizados no faturamento e no controle de estoque.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PEVK_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PEVK_PEDIDO_VENDA` | INTEGER | Não | Identificador do pedido de venda (TB_PEDIDO_VENDA.PEV_ID). Parte da chave primária composta. |
| `PEVK_ITEM` | INTEGER | Não | Sequencial do item do pedido ao qual o componente pertence. Parte da chave primária composta. |
| `PEVK_SEQUENCIA` | INTEGER | Não | Sequencial do componente do kit dentro do item. Parte da chave primária composta. |
| `PEVK_PRODUTO` | INTEGER | Sim | Identificador do produto componente do kit (TB_PRODUTO.PRD_ID). |
| `PEVK_QUANTIDADE` | NUMERIC(15,4) | Sim | Quantidade do componente no kit. |
| `PEVK_QUANTIDADE_NF` | NUMERIC(15,6) | Sim | Quantidade do componente utilizada na nota fiscal. |
| `PEVK_VALOR_UNITARIO_NF` | NUMERIC(15,6) | Sim | Valor unitário do componente na nota fiscal. |
| `PEVK_VALOR_UNITARIO` | NUMERIC(15,6) | Sim | Valor unitário do componente no pedido. |
| `PEVK_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do componente no pedido. |
| `PEVK_VALOR_TOTAL_NF` | NUMERIC(15,4) | Sim | Valor total do componente na nota fiscal. |
| `PEVK_UN` | VARCHAR(6) | Sim | Unidade de medida do componente. |
| `PEVK_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo do produto componente. |
| `PEVK_QTDE_ESTOQUE` | NUMERIC(15,6) | Sim | Quantidade do componente considerada para baixa de estoque. |
| `PEVK_VALOR_DESCONTO` | NUMERIC(15,4) | Sim | Valor de desconto aplicado ao componente. |
| `PEVK_VALOR_ACRESCIMO` | NUMERIC(15,4) | Sim | Valor de acréscimo aplicado ao componente. |
| `PEVK_VALOR_DESCARTE` | NUMERIC(15,4) | Sim | Valor de descarte ou perda associado ao componente. |
| `PEVK_DESC_RATEADO` | NUMERIC(15,4) | Sim | Parcela do desconto do pedido rateada para o componente. |
| `PEVK_ACRES_RATEADO` | NUMERIC(15,4) | Sim | Parcela do acréscimo do pedido rateada para o componente. |
| `PEVK_PORCENTAGEM` | NUMERIC(15,4) | Sim | Percentual de participação do componente no kit. |
| `PEVK_PESO_BRUTO` | NUMERIC(15,3) | Sim | Peso bruto do componente. |
| `PEVK_PESO_LIQUIDO` | NUMERIC(15,3) | Sim | Peso líquido do componente. |
| `PEVK_METRAGEM` | NUMERIC(15,4) | Sim | Metragem cúbica ou dimensional do componente. |
| `PEVK_SUB_TOTAL` | NUMERIC(15,4) | Sim | Subtotal do componente antes dos ajustes. |
| `PEVK_QTDE_KIT` | NUMERIC(15,4) | Sim | Quantidade de kits considerada no cálculo do componente. |

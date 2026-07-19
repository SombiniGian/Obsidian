# Tabela TB_BORDERO_RECEBIMENTO_ITEM

**Módulo:** Financeiro
Itens que compõem um borderô de recebimento, vinculando cada recebimento baixado aos valores efetivamente recebidos no borderô (juros, multa, acréscimo, desconto e valor de recebimento).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BRI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `BRI_BORDERO_RECEBIMENTO` | INTEGER | Não | Identificador do borderô de recebimento (TB_BORDERO_RECEBIMENTO.BDR_ID). Parte da chave primária composta. |
| `BRI_SEQUENCIAL` | INTEGER | Não | Sequencial do item dentro do borderô. Parte da chave primária composta. |
| `BRI_RECEBIMENTO` | INTEGER | Sim | Identificador do recebimento (TB_RECEBIMENTO.REC_ID) que está sendo baixado neste item do borderô. |
| `BRI_VALOR_ABERTO` | NUMERIC(15,2) | Sim | Valor em aberto do recebimento no momento da baixa. |
| `BRI_VALOR_RECEBIDO` | NUMERIC(15,2) | Sim | Valor efetivamente recebido (pago) para o título neste item. |
| `BRI_VALOR_JUROS` | NUMERIC(15,2) | Sim | Juros recebido no item do borderô. |
| `BRI_VALOR_MULTA` | NUMERIC(15,2) | Sim | Valor de multa aplicado na baixa do título. |
| `BRI_VALOR_ACRESCIMO` | NUMERIC(15,2) | Sim | Valor de acréscimo aplicado na baixa do título. |
| `BRI_VALOR_DESCONTO` | NUMERIC(15,2) | Sim | Valor de desconto concedido na baixa do título. |
| `BRI_VALOR_RECEBIMENTO` | NUMERIC(15,2) | Sim | Valor total do recebimento (líquido) lançado para este item. |

COMMENT ON COLUMN TB_BORDERO_RECEBIMENTO_ITEM.BRI_VALOR_JUROS IS 'Juros Recebido no item do bordero';
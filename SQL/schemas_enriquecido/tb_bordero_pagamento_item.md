# Tabela TB_BORDERO_PAGAMENTO_ITEM

**Módulo:** Financeiro
Itens do borderô de pagamento, registrando cada pagamento (TB_PAGAMENTO) baixado no borderô com seus valores (aberto, pago, desconto, acréscimo, juros, multa).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BPI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `BPI_BORDERO_PAGAMENTO` | INTEGER | Não | Identificador do borderô de pagamento (FK para TB_BORDERO_PAGAMENTO.BDP_ID). Parte da chave primária composta. |
| `BPI_SEQUENCIAL` | INTEGER | Não | Sequencial do item dentro do borderô. Parte da chave primária composta. |
| `BPI_PAGAMENTO` | INTEGER | Sim | Identificador do pagamento baixado (FK para TB_PAGAMENTO.PAG_ID). |
| `BPI_VALOR_ABERTO` | NUMERIC(15,2) | Sim | Valor em aberto do pagamento antes da baixa. |
| `BPI_VALOR_PAGO` | NUMERIC(15,2) | Sim | Valor efetivamente pago no borderô. |
| `BPI_VALOR_DESCONTO` | NUMERIC(15,2) | Sim | Valor de desconto aplicado no borderô. |
| `BPI_VALOR_ACRESCIMO` | NUMERIC(15,2) | Sim | Valor de acréscimo aplicado no borderô. |
| `BPI_VALOR_PAGAMENTO` | NUMERIC(15,2) | Sim | Valor total do pagamento calculado (pago + acréscimo - desconto). |
| `BPI_VALOR_JUROS` | NUMERIC(15,2) | Sim | Valor de juros recebido no item do borderô. |
| `BPI_VALOR_MULTA` | NUMERIC(15,2) | Sim | Valor de multa aplicada no item do borderô. |

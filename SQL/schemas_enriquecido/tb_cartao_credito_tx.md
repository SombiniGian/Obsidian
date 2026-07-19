# Tabela TB_CARTAO_CREDITO_TX

**Módulo:** Financeiro / Cartão
Faixas de taxa de cartão de crédito/débito por bandeira e parcela, vinculadas a um cadastro de cartão (TB_CARTAO_CREDITO).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CTX_CARTAO` | INTEGER | Não | FK para o cadastro de cartão. |
| `CTX_SEQ` | INTEGER | Não | Sequencial da faixa de taxa. |
| `CTX_PARCELA_INI` | INTEGER | Sim | Parcela inicial da faixa (ex.: 1). |
| `CTX_PARCELA_FIM` | INTEGER | Sim | Parcela final da faixa (ex.: 6). |
| `CTX_TX_DEBITO` | NUMERIC(15,2) | Sim | Taxa (%) aplicada para transações de débito. |
| `CTX_TX_CREDITO` | NUMERIC(15,2) | Sim | Taxa (%) aplicada para transações de crédito. |
| `CTX_BANDEIRA` | VARCHAR(2) | Sim | Bandeira da faixa (Visa, Master, Elo etc.). |

# Tabela TB_BORDERO_RECEBIMENTO_VALORES

**Módulo:** Financeiro
Formas de moeda/recebimento e movimentos gerados em um borderô de recebimento (caixa, banco, cheque, cartão, crédito). Cada linha registra uma espécie de moeda utilizada e o movimento financeiro originado pelo borderô.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BRV_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `BRV_BORDERO_RECEBIMENTO` | INTEGER | Não | Identificador do borderô de recebimento (TB_BORDERO_RECEBIMENTO.BDR_ID). Parte da chave primária composta. |
| `BRV_SEQUENCIAL` | INTEGER | Não | Sequencial do lançamento dentro do borderô. Parte da chave primária composta. |
| `BRV_ESPECIE_MOEDA` | INTEGER | Sim | Identificador da espécie de moeda utilizada (TB_ESPECIE_MOEDA.ESP_ID). Define o tipo de pagamento (dinheiro, cartão, cheque, etc.). |
| `BRV_VALOR` | NUMERIC(15,2) | Sim | Valor recebido nesta espécie de moeda. |
| `BRV_MOVIMENTAR` | VARCHAR(2) | Sim | Tipo de movimentação financeira gerada pelo borderô: CX = Movimentar Conta Caixa; CB = Movimentar Conta Bancária; CH = Lançar Cheque Recebido; CE = Lançar Cheque Emitido; CC = Lançar Parcelas Cartão Crédito; CR = Crédito. |
| `BRV_ID_MOVIMENTO` | INTEGER | Sim | ID do movimento originado desse lançamento (referência lógica a TB_MOVIMENTO_CONTA ou TB_CHEQUE_RECEBIDO conforme BRV_MOVIMENTAR). |

COMMENT ON COLUMN TB_BORDERO_RECEBIMENTO_VALORES.BRV_MOVIMENTAR IS 'CX - Movimentar Conta Caixa
CB - Movimentar Conta Bancária
CH - Lançar Cheque Recebido
CE - Lançar Cheque Emitido
CC - Lançar Parcelas Cartão Crédito
CR - Crédito';
COMMENT ON COLUMN TB_BORDERO_RECEBIMENTO_VALORES.BRV_ID_MOVIMENTO IS 'id do movimento originado desse lançamento';
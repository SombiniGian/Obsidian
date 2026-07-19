# Tabela TB_BORDERO_PAGAMENTO_VALORES

**Módulo:** Financeiro / Borderô de Pagamento
Itens (valores/espécies) que compõem um borderô de pagamento (TB_BORDERO_PAGAMENTO). Permite registrar pagamentos em múltiplas espécies de moeda (dinheiro, cheque, cartão, crédito), indicando o tipo de movimentação financeira gerada (caixa, conta bancária, cheque recebido, cheque emitido, cartão ou crédito) e o movimento de conta originado.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BPV_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `BPV_BORDERO_PAGAMENTO` | INTEGER | Não | FK para TB_BORDERO_PAGAMENTO. Parte da chave primária composta. |
| `BPV_SEQUENCIAL` | INTEGER | Não | Sequencial do item dentro do borderô. Parte da chave primária composta. |
| `BPV_ESPECIE_MOEDA` | INTEGER | Sim | FK para TB_ESPECIE_MOEDA.ESP_ID — espécie/forma de pagamento. |
| `BPV_VALOR` | NUMERIC(15,2) | Sim | Valor pago nesta espécie de moeda. |
| `BPV_MOVIMENTAR` | VARCHAR(2) | Sim | Tipo de movimentação financeira gerada (CX/CB/CH/CE/CC/CR). |
| `BPV_ID_MOVIMENTO` | INTEGER | Sim | FK para TB_MOVIMENTO_CONTA.MOV_ID — movimento originado deste lançamento. |

COMMENT ON COLUMN TB_BORDERO_PAGAMENTO_VALORES.BPV_MOVIMENTAR IS 'CX - Movimentar Conta Caixa
CB - Movimentar Conta Bancária
CH - Lançar Cheque Recebido
CE - Lançar Cheque Emitido
CC - Lançar Parcelas Cartão Crédito
CR - Crédito';
COMMENT ON COLUMN TB_BORDERO_PAGAMENTO_VALORES.BPV_BORDERO_PAGAMENTO IS 'FK para TB_BORDERO_PAGAMENTO — use JOIN por BPV_BORDERO_PAGAMENTO.';

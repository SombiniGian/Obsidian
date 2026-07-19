# Tabela TB_BORDERO_DEPOSITO_VALORES

**Módulo:** Financeiro / Borderô de Depósito
Itens (valores/espécies) que compõem um borderô de depósito (TB_BORDERO_DEPOSITO). Permite registrar pagamentos em múltiplas espécies de moeda (dinheiro, cheque, cartão etc.), indicando se geram movimentação em conta caixa ou bancária e o vínculo com o movimento de conta gerado.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BDV_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `BDV_BORDERO_DEPOSITO` | INTEGER | Não | FK para TB_BORDERO_DEPOSITO. Parte da chave primária composta. |
| `BDV_SEQUENCIAL` | INTEGER | Não | Sequencial do item dentro do borderô. Parte da chave primária composta. |
| `BDV_ESPECIE_MOEDA` | INTEGER | Sim | FK para TB_ESPECIE_MOEDA.ESP_ID — espécie/forma de pagamento. |
| `BDV_VALOR` | NUMERIC(15,2) | Sim | Valor recebido nesta espécie de moeda. |
| `BDV_MOVIMENTAR` | VARCHAR(2) | Sim | Tipo de movimentação financeira gerada (CX=Caixa, CB=Conta Bancária). |
| `BDV_ID_MOVIMENTO` | INTEGER | Sim | FK para TB_MOVIMENTO_CONTA.MOV_ID — movimento originado deste lançamento. |
| `BDV_CONTA` | INTEGER | Sim | FK para TB_CONTA.CNT_ID — conta destino do movimento. |

COMMENT ON COLUMN TB_BORDERO_DEPOSITO_VALORES.BDV_MOVIMENTAR IS 'CX - Movimentar Conta Caixa
CB - Movimentar Conta Bancária';
COMMENT ON COLUMN TB_BORDERO_DEPOSITO_VALORES.BDV_ID_MOVIMENTO IS 'id do movimento originado desse lançamento';
COMMENT ON COLUMN TB_BORDERO_DEPOSITO_VALORES.BDV_BORDERO_DEPOSITO IS 'FK para TB_BORDERO_DEPOSITO — use JOIN com TB_BORDERO_DEPOSITO pelo ID do borderô.';

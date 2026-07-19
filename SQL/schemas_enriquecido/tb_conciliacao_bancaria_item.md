# Tabela TB_CONCILIACAO_BANCARIA_ITEM

**Módulo:** Financeiro / Conciliação Bancária
Itens (lançamentos) que compõem uma conciliação bancária (TB_CONCILIACAO_BANCARIA). Cada item representa um movimento a ser conciliado: extrato bancário, pagamento, recebimento, cheque etc., com tipo, valor, status e o vínculo com o lançamento conciliado.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CBI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `CBI_CONCILIACAO` | INTEGER | Não | FK para TB_CONCILIACAO_BANCARIA. Parte da chave primária composta. |
| `CBI_ID` | INTEGER | Não | Identificador único do item da conciliação. Parte da chave primária composta. |
| `CBI_DOCUMENTO` | VARCHAR(20) | Sim | Número do documento do lançamento (extrato, cheque, boleto). |
| `CBI_DT_MOVIMENTO` | DATE | Sim | Data do movimento no extrato/conciliação. |
| `CBI_TIPO` | VARCHAR(1) | Sim | Tipo do lançamento (C=Crédito, D=Débito). |
| `CBI_VALOR` | NUMERIC(15,2) | Sim | Valor do lançamento a conciliar. |
| `CBI_DESCRICAO` | VARCHAR(100) | Sim | Descrição/histórico do lançamento. |
| `CBI_STATUS` | VARCHAR(1) | Sim | Status do item (P=Pendente, C=Conciliado, etc.). |
| `CBI_USUARIO` | INTEGER | Sim | FK para TB_USUARIO — usuário responsável pela conciliação. |
| `CBI_ID_CONCILIADO` | INTEGER | Sim | Identificador do movimento conciliado (TB_MOVIMENTO_CONTA.MOV_ID ou similar). |

COMMENT ON COLUMN TB_CONCILIACAO_BANCARIA_ITEM.CBI_TIPO IS 'C - Crédito / D - Débito';
COMMENT ON COLUMN TB_CONCILIACAO_BANCARIA_ITEM.CBI_CONCILIACAO IS 'FK para TB_CONCILIACAO_BANCARIA — use JOIN por CBI_CONCILIACAO.';

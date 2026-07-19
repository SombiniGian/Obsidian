# Tabela TB_CONCILIACAO_BANCARIA

**Módulo:** Financeiro
Tabela de cabeçalho da conciliação bancária. Armazena o período de conciliação (data início/fim), a conta bancária conciliada, o arquivo OFX importado e o usuário responsável. Os itens (lançamentos) da conciliação ficam em TB_CONCILIACAO_BANCARIA_ITEM.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `COC_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `COC_ID` | INTEGER | Não | Identificador único da conciliação. Parte da chave primária composta. |
| `COC_CONTA` | INTEGER | Sim | FK para TB_CONTA.CNT_ID que está sendo conciliada. |
| `COC_DT_INICIO` | DATE | Sim | Data de início do período de conciliação. |
| `COC_DT_FIM` | DATE | Sim | Data de fim do período de conciliação. |
| `COC_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento da conciliação no sistema. |
| `COC_ARQUIVO_OFX` | BLOB SUB_TYPE BINARY | Sim | Arquivo OFX importado (extrato bancário) em formato binário. NUNCA selecione em queries SELECT. |
| `COC_USUARIO` | INTEGER | Sim | Identificador do usuário que realizou a conciliação. |
| `COC_STATUS` | VARCHAR(1) | Sim | Status da conciliação (A=Andamento, F=Finalizada, C=Cancelada). |

COMMENT ON COLUMN TB_CONCILIACAO_BANCARIA.COC_ARQUIVO_OFX IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

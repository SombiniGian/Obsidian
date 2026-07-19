# Tabela TB_CHEQUE_EMITIDO_ITEM

**Módulo:** Financeiro / Cheques Emitidos
Registra o histórico de ações (movimentações) realizadas com um cheque emitido (TB_CHEQUE_EMITIDO): emissão, compensação e cancelamento. Cada item guarda a ação, data, histórico, usuário e a origem do movimento (manual, borderô de recebimento ou borderô de pagamento).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CHEI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `CHEI_CHEQUE_EMITIDO` | INTEGER | Não | FK para TB_CHEQUE_EMITIDO. Parte da chave primária composta. |
| `CHEI_SEQUENCIAL` | INTEGER | Não | Sequencial do item dentro do histórico do cheque. Parte da chave primária composta. |
| `CHEI_ACAO` | VARCHAR(2) | Sim | Ação realizada com o cheque (CE/CP/CN). |
| `CHEI_DT_ACAO` | DATE | Sim | Data em que a ação foi executada. |
| `CHEI_HISTORICO` | VARCHAR(200) | Sim | Histórico/descrição da ação realizada. |
| `CHEI_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora do lançamento do item no sistema. |
| `CHEI_ORIGEM_MOVIMENTO` | VARCHAR(10) | Não | Origem da movimentação do cheque (MANUAL/BD.REC/BD.PAG). |
| `CHEI_ORIGEM_NUMERO` | INTEGER | Sim | Identificador (número) do documento de origem. |
| `CHEI_USUARIO` | INTEGER | Sim | FK para TB_USUARIO — usuário responsável pela ação. |

COMMENT ON COLUMN TB_CHEQUE_EMITIDO_ITEM.CHEI_ACAO IS 'CHRI_ACAO -> CAMPO PARA ARMAZENAR AS AÇÕES REALIZADAS COM O CHEQUE
------------------------------------------------------------------
CE -> CHEQUES EMITIDOS
CP -> CHEQUES COMPENSADOS
CN -> CANCELADO';
COMMENT ON COLUMN TB_CHEQUE_EMITIDO_ITEM.CHEI_ORIGEM_MOVIMENTO IS 'CHRI_ORIGEM_MOVIMENTO
--------------------
''MANUAL'' -> LANÇADO DIRETAMENTO NO RECEBIMENTO
''BD.REC'' -> ORIGEM É UM BORDERO DE RECEBIMENTO
''BD.PAG'' -> ORIGEM É UM BORDERÔ DE PAGAMENTO';
COMMENT ON COLUMN TB_CHEQUE_EMITIDO_ITEM.CHEI_CHEQUE_EMITIDO IS 'FK para TB_CHEQUE_EMITIDO — use JOIN por CHEI_CHEQUE_EMITIDO.';

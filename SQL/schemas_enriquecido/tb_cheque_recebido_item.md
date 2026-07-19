# Tabela TB_CHEQUE_RECEBIDO_ITEM

**Módulo:** Financeiro / Cheques Recebidos
Registra o histórico de ações (movimentações) realizadas com um cheque recebido (TB_CHEQUE_RECEBIDO): carteira, depósito, passagem, devoluções, cancelamento, fechamento de caixa e inadimplência. Cada item guarda a ação, data, histórico, usuário, origem e conta de depósito.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CHRI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `CHRI_CHEQUE_RECEBIDO` | INTEGER | Não | FK para TB_CHEQUE_RECEBIDO.CHR_ID. Parte da chave primária composta. |
| `CHRI_SEQUENCIAL` | INTEGER | Não | Sequencial do item dentro do histórico do cheque. Parte da chave primária composta. |
| `CHRI_ACAO` | VARCHAR(2) | Sim | Ação realizada com o cheque (CR/CD/CP/C1/C2/CI/CN/FC). |
| `CHRI_DT_ACAO` | DATE | Sim | Data em que a ação foi executada. |
| `CHRI_HISTORICO` | VARCHAR(200) | Sim | Histórico/descrição da ação realizada. |
| `CHRI_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora do lançamento do item no sistema. |
| `CHRI_ORIGEM_MOVIMENTO` | VARCHAR(10) | Não | Origem da movimentação do cheque (MANUAL/BD.REC/BD.PAG). |
| `CHRI_ORIGEM_NUMERO` | INTEGER | Sim | Identificador (número) do documento de origem. |
| `CHRI_USUARIO` | INTEGER | Sim | FK para TB_USUARIO — usuário responsável pela ação. |
| `CHRI_CONTA_DEPOSITO` | INTEGER | Sim | FK para TB_CONTA.CNT_ID — conta onde o cheque foi depositado. |
| `CHRI_DESTINATARIO` | INTEGER | Sim | FK para TB_PESSOA.PES_ID — destinatário (para cheques passados). |

COMMENT ON COLUMN TB_CHEQUE_RECEBIDO_ITEM.CHRI_ACAO IS 'CHRI_ACAO -> CAMPO PARA ARMAZENAR AS AÇÕES REALIZADAS COM O CHEQUE
------------------------------------------------------------------
CR -> CHEQUES EM CARTEIRA
CD -> CHEQUES DEPOSITADOS
CP -> CHEQUES PASSADO
C1 -> CHEQUES 1 DEVOLUÇÃO
C2 -> CHEQUES 2 DEVOLUÇÃO
CI -> INADIMPLÊNCIA
CN -> CANCELADO
FC -> FECHAMENTO CAIXA';
COMMENT ON COLUMN TB_CHEQUE_RECEBIDO_ITEM.CHRI_ORIGEM_MOVIMENTO IS 'CHRI_ORIGEM_MOVIMENTO
--------------------
''MANUAL'' -> LANÇADO DIRETAMENTO NO RECEBIMENTO
''BD.REC'' -> ORIGEM É UM BORDERO DE RECEBIMENTO
''BD.PAG'' -> ORIGEM É UM BORDERÔ DE PAGAMENTO';
COMMENT ON COLUMN TB_CHEQUE_RECEBIDO_ITEM.CHRI_CHEQUE_RECEBIDO IS 'FK para TB_CHEQUE_RECEBIDO.CHR_ID — use JOIN por CHRI_CHEQUE_RECEBIDO.';

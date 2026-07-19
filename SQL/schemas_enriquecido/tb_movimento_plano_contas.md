# Tabela TB_MOVIMENTO_PLANO_CONTAS

**Módulo:** Financeiro / Contábil
Movimentações financeiras vinculadas diretamente a contas de débito e crédito do plano de contas, usadas para registrar e acompanhar lançamentos contábeis.

## Quando usar esta tabela

Esta é a tabela de **escrituração contábil** (débito/crédito no plano de contas). Ela recebe os lançamentos originados em outras rotinas financeiras, como `TB_MOVIMENTO_CONTA` (movimentos de caixa e bancários). Use esta tabela para relatórios por plano de contas, razão contábil, partidas dobradas, fechamentos contábeis e rastreamento do espelho de operações de caixa já registradas em `TB_MOVIMENTO_CONTA`.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `MOV_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `MOV_ID` | INTEGER | Não | Identificador único do movimento. Parte da chave primária composta. |
| `MOV_CONTA_DEBITO` | INTEGER | Sim | Conta do plano de contas debitada no lançamento. |
| `MOV_CONTA_CREDITO` | INTEGER | Sim | Conta do plano de contas creditada no lançamento. |
| `MOV_DT_EMISSAO` | DATE | Sim | Data de emissão do movimento. |
| `MOV_VALOR` | NUMERIC(15,2) | Sim | Valor do lançamento. |
| `MOV_COMPENSADO` | VARCHAR(1) | Sim | Indica se o movimento foi compensado (S/N). |
| `MOV_DT_COMPENSADO` | DATE | Sim | Data de compensação do movimento. |
| `MOV_DT_AGENDADO` | DATE | Sim | Data agendada para compensação. |
| `MOV_USUARIO` | INTEGER | Sim | Identificador do usuário que lançou o movimento. |
| `MOV_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro. |
| `MOV_HISTORICO` | VARCHAR(100) | Sim | Histórico ou descrição do lançamento. |
| `MOV_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações do movimento em formato binário. NUNCA selecione em queries SELECT. |
| `MOV_STATUS` | VARCHAR(1) | Sim | Status do movimento: A = Agendado, P = Compensado, C = Cancelado. |
| `MOV_ORIGEM` | VARCHAR(30) | Sim | Sigla do módulo ou rotina que originou o movimento. |
| `MOV_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem. |
| `MOV_CENTRO_CUSTO` | INTEGER | Sim | Identificador do centro de custo (TB_CENTRO_CUSTO.CEN_ID). |

COMMENT ON COLUMN TB_MOVIMENTO_PLANO_CONTAS.MOV_COMPENSADO IS 'S - SIM
N - NAO';
COMMENT ON COLUMN TB_MOVIMENTO_PLANO_CONTAS.MOV_STATUS IS 'A - AGENDADO
P - COMPENSADO
C - CANCELADO';
COMMENT ON COLUMN TB_MOVIMENTO_PLANO_CONTAS.MOV_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

## Nota operacional — operações de caixa

Operações de caixa (saída/entrada de valores em caixa físico, transferências entre contas-corrente) são registradas primeiro em `TB_MOVIMENTO_CONTA` e só depois espelhadas para `TB_MOVIMENTO_PLANO_CONTAS` como lançamentos contábeis. Para perguntas cujo contexto seja operação de caixa, priorize `TB_MOVIMENTO_CONTA` — ela contém o registro original com detalhes de conta, tipo do movimento (D/C), fechamento, transferências e valores em caixa. `TB_MOVIMENTO_PLANO_CONTAS` permanece válida para razão contábil, partidas dobradas, fechamentos contábeis e para rastrear o espelho contábil de uma operação de caixa já registrada em `TB_MOVIMENTO_CONTA`.

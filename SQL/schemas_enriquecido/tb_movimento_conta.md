# Tabela TB_MOVIMENTO_CONTA

**Módulo:** Financeiro
Tabela central de movimentações financeiras do sistema: débitos/créditos, compensação, sangria, suprimento, vendas, recebimentos, boletos, PIX, TEF, transferência entre contas, fechamento de caixa e operações de caixa em geral. Todas as movimentações financeiras (caixa e bancárias) passam por aqui, sendo a fonte primária recomendada para qualquer consulta cujo contexto seja operação de caixa.

## Quando usar esta tabela

Use `TB_MOVIMENTO_CONTA` como fonte primária sempre que a pergunta envolver:

- **SANGRIA** (saída de valores do caixa) — operação cadastrada e registrada **nesta tabela**.
- **SUPRIMENTO** (entrada de valores no caixa) — operação cadastrada e registrada **nesta tabela**.
- Demais movimentações de caixa e bancárias: débitos, créditos, transferências entre contas, vendas, recebimentos, boletos, PIX, TEF, conciliações, fechamento de caixa, troco, etc.

A partir desta tabela, os lançamentos contábeis podem ser espelhados em `TB_MOVIMENTO_PLANO_CONTAS` (escrituração contábil). Por isso, para qualquer consulta cujo contexto seja **SANGRIA** ou **SUPRIMENTO**, priorize `TB_MOVIMENTO_CONTA` — ela contém o registro original e detalhado (conta, tipo, valor em caixa, fechamento, transferências, etc.).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `MOV_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `MOV_ID` | INTEGER | Não | Identificador único do movimento. Parte da chave primária composta. |
| `MOV_DT_EMISSAO` | DATE | Sim | Data de emissão do movimento. |
| `MOV_VALOR` | NUMERIC(15,2) | Sim | Valor do movimento. |
| `MOV_COMPENSADO` | VARCHAR(1) | Sim | Indica se o movimento está compensado: S = Sim, N = Não. |
| `MOV_DT_COMPENSADO` | DATE | Sim | Data em que o movimento foi compensado. |
| `MOV_DT_AGENDADO` | DATE | Sim | Data agendada para compensação. |
| `MOV_USUARIO` | INTEGER | Sim | Identificador do usuário que lançou o movimento. |
| `MOV_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro no sistema. |
| `MOV_HISTORICO` | VARCHAR(100) | Sim | Histórico/descrição do movimento. |
| `MOV_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações em formato binário. NUNCA selecione em queries SELECT. |
| `MOV_STATUS` | VARCHAR(1) | Sim | Status do movimento: A = Agendado, P = Compensado, C = Cancelado. |
| `MOV_ORIGEM` | VARCHAR(30) | Sim | Sigla do módulo/rotina de origem (ex.: RECEBIMENTO, VENDA, SUPRIMENTO). |
| `MOV_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem do movimento. |
| `MOV_CONTA` | INTEGER | Sim | Identificador da conta (TB_CONTA.CNT_ID) na qual o movimento foi lançado. |
| `MOV_PLANO_CONTAS` | INTEGER | Sim | Identificador do plano de contas contábil do movimento. |
| `MOV_TIPO` | VARCHAR(1) | Sim | Tipo do movimento: D = Débito, C = Crédito. |
| `MOV_ESPECIE_MOEDA` | INTEGER | Sim | Identificador da espécie de moeda (TB_ESPECIE_MOEDA.ESP_ID). |
| `MOV_FECHAMENTO` | INTEGER | Sim | Identificador do fechamento de caixa ao qual o movimento pertence. |
| `MOV_TROCO` | VARCHAR(1) | Sim | Indica se o movimento representa um troco (S/N). |
| `MOV_CONTA_TRANSF` | INTEGER | Sim | Conta destino da transferência (quando MOV_TIPO_TRANSF indica transferência). |
| `MOV_ID_TRANSF` | INTEGER | Sim | Identificador do movimento pareado na transferência. |
| `MOV_TIPO_TRANSF` | VARCHAR(1) | Sim | Tipo da transferência (ex.: E = Entrada, S = Saída). |
| `MOV_VALOR_CAIXA` | NUMERIC(15,2) | Sim | Valor lançado no caixa (quando diferente do valor total). |
| `MOV_CODIGO_PSP` | VARCHAR(50) | Sim | Código do provedor (PSP) para PIX/TEF. |
| `MOV_TEF_NSU` | VARCHAR(100) | Sim | NSU da transação TEF. |
| `MOV_ID_CARTEIRA_DIGITAL` | VARCHAR(50) | Sim | ID da carteira digital (integração). |
| `MOV_NOME_CARTEIRA_DIGITAL` | VARCHAR(100) | Sim | Nome da carteira digital. |
| `MOV_PIX` | INTEGER | Sim | Identificador do PIX vinculado. |
| `MOV_ID_PAGARME` | VARCHAR(100) | Sim | ID do movimento no Pagar.me. |
| `MOV_BANDEIRA` | VARCHAR(2) | Sim | Bandeira do cartão (quando aplicável). |
| `MOV_ID_CONCILIADO` | INTEGER | Sim | Identificador da conciliação bancária. |
| `MOV_CENTRO_CUSTO` | INTEGER | Sim | Identificador do centro de custo (TB_CENTRO_CUSTO.CEN_ID). |

COMMENT ON COLUMN TB_MOVIMENTO_CONTA.MOV_COMPENSADO IS 'S - SIM
N - NAO';
COMMENT ON COLUMN TB_MOVIMENTO_CONTA.MOV_STATUS IS 'A - AGENDADO
P - COMPENSADO
C - CANCELADO';
COMMENT ON COLUMN TB_MOVIMENTO_CONTA.MOV_TIPO IS 'D - DEBITO
C - CREDITO';
COMMENT ON COLUMN TB_MOVIMENTO_CONTA.MOV_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
# Tabela TB_LOTE_PROD_MOV

**Módulo:** Estoque / Lotes
Tabela de movimentações de estoque por lote de produto. Registra entradas, saídas e acertos de estoque informando o lote, quantidade, conversões de unidade e a origem do movimento.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `LMOV_LOTE` | INTEGER | Não | FK para TB_LOTE_PRODUTO. Identificador do lote movimentado. Parte da chave primária composta. |
| `LMOV_SEQUENCIA` | INTEGER | Não | Sequencial do movimento dentro do lote. Parte da chave primária composta. |
| `LMOV_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `LMOV_TIPO` | VARCHAR(3) | Sim | Tipo do movimento de estoque. |
| `LMOV_DT_MOVIMENTO` | DATE | Sim | Data em que o movimento de estoque foi efetivado. |
| `LMOV_UN` | VARCHAR(6) | Sim | Unidade de medida utilizada no movimento. |
| `LMOV_FATOR_CONVERSAO` | VARCHAR(1) | Sim | Fator de conversão entre a unidade de movimentação e a unidade de estoque (M=Multiplica, D=Divide). |
| `LMOV_QTDE_CONVERSAO` | NUMERIC(15,4) | Sim | Fator numérico de conversão de unidade. |
| `LMOV_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade movimentada na unidade do movimento. |
| `LMOV_QTDE_ESTOQUE` | NUMERIC(18,6) | Sim | Quantidade equivalente na unidade de estoque. |
| `LMOV_ORIGEM` | VARCHAR(10) | Sim | Tabela/documento de origem do movimento (ex.: NF, PED, INV). |
| `LMOV_ID_ORIGEM` | INTEGER | Sim | Identificador do registro de origem do movimento. |
| `LMOV_ORIGEM_ITEM` | INTEGER | Sim | Sequência do item de origem do movimento. |
| `LMOV_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de gravação do movimento. |
| `LMOV_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que lançou o movimento. |
| `LMOV_HISTORICO` | VARCHAR(100) | Sim | Histórico/descrição do movimento. |
| `LMOV_PESSOA` | INTEGER | Sim | FK para TB_PESSOA (cliente/fornecedor) relacionada ao movimento. |
| `LMOV_NOTA_FISCAL` | INTEGER | Sim | FK para TB_NOTA_FISCAL de origem do movimento, quando aplicável. |

COMMENT ON COLUMN TB_LOTE_PROD_MOV.LMOV_TIPO IS 'ENT - ENTRADA NO ESTOQUE
  SAI - SAIDA DO ESTOQUE
  ACE - ACERTO DE ESTOQUE';

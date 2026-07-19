# Tabela TB_ORDEM_PRODUCAO_PERDAS

**Módulo:** Produção / Estoque
Registra as perdas (quebras, desperdícios, sobras) ocorridas durante uma ordem de produção (TB_ORDEM_PRODUCAO). Permite controlar produto, quantidade, valor, motivo, situação e usuário responsável pelo lançamento da perda.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `OPP_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `OPP_ID` | INTEGER | Não | Identificador único da perda de produção. Parte da chave primária composta. |
| `OPP_ORDEM_PRODUCAO` | INTEGER | Não | FK para TB_ORDEM_PRODUCAO.OP_ID — ordem de produção relacionada. |
| `OPP_PRODUTO` | INTEGER | Sim | FK para TB_PRODUTO.PRD_ID — produto da perda. |
| `OPP_DT_EMISSAO` | DATE | Sim | Data de emissão/lançamento da perda. |
| `OPP_COLABORADOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID — colaborador que registrou a perda. |
| `OPP_QUANTIDADE` | NUMERIC(15,4) | Sim | Quantidade perdida do produto. |
| `OPP_VALOR_UNITARIO` | NUMERIC(15,4) | Sim | Valor unitário do produto perdido. |
| `OPP_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total da perda (quantidade × valor unitário). |
| `OPP_UNIDADE` | VARCHAR(6) | Sim | Unidade de medida da perda (UN, KG, LT etc.). |
| `OPP_MOTIVO` | INTEGER | Sim | Identificador do motivo da perda (TB_DEVOLUCAO_MOTIVO ou cadastro equivalente). |
| `OPP_SEQ_SITUACAO` | INTEGER | Sim | Sequencial da situação dentro da ordem de produção. |
| `OPP_SITUACAO` | INTEGER | Sim | Situação operacional da perda. |
| `OPP_USUARIO` | INTEGER | Sim | FK para TB_USUARIO — usuário que lançou a perda. |
| `OPP_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora do lançamento da perda. |

COMMENT ON COLUMN TB_ORDEM_PRODUCAO_PERDAS.OPP_ORDEM_PRODUCAO IS 'FK para TB_ORDEM_PRODUCAO.OP_ID — use JOIN por OPP_ORDEM_PRODUCAO.';
COMMENT ON COLUMN TB_ORDEM_PRODUCAO_PERDAS.OPP_PRODUTO IS 'FK para TB_PRODUTO.PRD_ID — use JOIN por PRD_ID para obter descrição do produto.';

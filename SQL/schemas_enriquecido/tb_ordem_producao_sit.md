# Tabela TB_ORDEM_PRODUCAO_SIT

**Módulo:** Produção / Estoque
Histórico de situações (movimentações de status) de uma ordem de produção (TB_ORDEM_PRODUCAO). Cada registro representa uma mudança de situação com usuário, colaborador, data/hora e observação.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `OPS_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `OPS_ORDEM_PRODUCAO` | INTEGER | Não | FK para TB_ORDEM_PRODUCAO.OP_ID. Parte da chave primária composta. |
| `OPS_SEQUENCIA` | INTEGER | Não | Sequencial da mudança de situação. Parte da chave primária composta. |
| `OPS_USUARIO` | INTEGER | Sim | FK para TB_USUARIO — usuário que registrou a mudança. |
| `OPS_SITUACAO` | INTEGER | Sim | Identificador da nova situação da ordem de produção. |
| `OPS_COLABORADOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID — colaborador responsável. |
| `OPS_DATA` | DATE | Sim | Data da mudança de situação. |
| `OPS_HORA` | TIME | Sim | Hora da mudança de situação. |
| `OPS_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações da mudança de situação em formato binário. NUNCA selecione em queries SELECT. |

COMMENT ON COLUMN TB_ORDEM_PRODUCAO_SIT.OPS_ORDEM_PRODUCAO IS 'FK para TB_ORDEM_PRODUCAO.OP_ID — use JOIN por OPS_ORDEM_PRODUCAO.';
COMMENT ON COLUMN TB_ORDEM_PRODUCAO_SIT.OPS_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização.';

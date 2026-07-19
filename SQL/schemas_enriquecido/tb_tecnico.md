# Tabela TB_TECNICO

**Módulo:** Cadastros / Ordem de Serviço
Dados do técnico vinculados a TB_PESSOA.PES_ID. Armazena percentual de comissão por execução de ordens de serviço.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TEC_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `TEC_OBSERVACAO` | VARCHAR(100) | Sim | Observações gerais do técnico. |
| `TEC_COMISSAO_PERC` | NUMERIC(15,2) | Sim | Percentual de comissão do técnico em ordens de serviço. |
| `TEC_PESSOA` | INTEGER | Não | FK para TB_PESSOA.PES_ID. Parte da chave primária composta. Use SEMPRE por PES_ID. |

COMMENT ON COLUMN TB_TECNICO.TEC_PESSOA IS 'FK para TB_PESSOA.PES_ID — SEMPRE faça JOIN com TB_PESSOA por PES_ID. Para filtrar técnicos utilize WHERE PES_TECNICO = ''S'' em TB_PESSOA.';

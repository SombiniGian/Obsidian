# Tabela TB_DEFEITO

**Módulo:** Ordem de Serviço / Cadastros
Cadastro de defeitos/constatações utilizadas em ordens de serviço. Permite padronizar descrições de problemas diagnosticados e armazenar observações em texto longo.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `DEF_ID` | INTEGER | Não | Identificador único do defeito. |
| `DEF_EMPRESA` | INTEGER | Sim | Identificador da empresa à qual o defeito pertence. |
| `DEF_DESCRICAO` | VARCHAR(100) | Sim | Descrição do defeito. |
| `DEF_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações detalhadas sobre o defeito (texto longo). |

COMMENT ON COLUMN TB_DEFEITO.DEF_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização';
# Tabela TB_ORDEM_SERVICO_SIT

**Módulo:** Ordem de Serviço
Tabela de situações/status percorridos por uma ordem de serviço. Registra o histórico de mudanças de status, com usuário, técnico responsável, data, hora e observações.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `OSS_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `OSS_ORDEM_SERVICO` | INTEGER | Não | FK para TB_ORDEM_SERVICO. Parte da chave primária composta. |
| `OSS_SEQUENCIA` | INTEGER | Não | Sequencial do registro de situação. Parte da chave primária composta. |
| `OSS_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que registrou a mudança de situação. |
| `OSS_SITUACAO` | INTEGER | Sim | Código/identificador da situação aplicada à OS. |
| `OSS_TECNICO` | INTEGER | Sim | FK para TB_PESSOA (PES_TECNICO=S). Técnico responsável pela OS no momento. |
| `OSS_DATA` | DATE | Sim | Data em que a situação foi aplicada. |
| `OSS_HORA` | TIME | Sim | Hora em que a situação foi aplicada. |
| `OSS_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações da mudança de situação em formato binário/texto longo. |

COMMENT ON COLUMN TB_ORDEM_SERVICO_SIT.OSS_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização';

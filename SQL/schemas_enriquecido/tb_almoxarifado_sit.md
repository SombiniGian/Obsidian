# Tabela TB_ALMOXARIFADO_SIT

**Módulo:** Estoque / Movimentações
Tabela de situações/status percorridos por um movimento de almoxarifado. Registra o histórico de mudanças com usuário, colaborador, data, hora e observações.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `ALMS_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `ALMS_ALMOXARIFADO` | INTEGER | Não | FK para TB_ALMOXARIFADO. Identificador do movimento. Parte da chave primária composta. |
| `ALMS_SEQUENCIA` | INTEGER | Não | Sequencial do registro de situação. Parte da chave primária composta. |
| `ALMS_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que registrou a mudança de situação. |
| `ALMS_SITUACAO` | INTEGER | Sim | Código/identificador da situação aplicada ao movimento. |
| `ALMS_COLABORADOR` | INTEGER | Sim | FK para TB_PESSOA (PES_COLABORADOR=S). Colaborador relacionado à situação. |
| `ALMS_DATA` | DATE | Sim | Data em que a situação foi aplicada. |
| `ALMS_HORA` | TIME | Sim | Hora em que a situação foi aplicada. |
| `AMLS_OBSERCACAO` | BLOB SUB_TYPE BINARY | Sim | Observações da mudança de situação. |

COMMENT ON COLUMN TB_ALMOXARIFADO_SIT.AMLS_OBSERCACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização';

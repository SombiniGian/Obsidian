# Tabela TB_LOTE_PRODUCAO

**Módulo:** Produção / Lotes
Tabela de lotes de produção. Controla o ciclo de produção com status, datas (emissão, início, produção, previsão), usuário, colaborador responsável, observações, origem e campos genéricos reservados.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `LOT_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `LOT_ID` | INTEGER | Não | Identificador único do lote de produção. Parte da chave primária composta. |
| `LOT_STATUS` | VARCHAR(1) | Sim | Status do lote (A=Aberto, P=Produzindo, F=Finalizado, C=Cancelado). |
| `LOT_DT_EMISSAO` | DATE | Sim | Data de emissão do lote. |
| `LOT_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de gravação do registro. |
| `LOT_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que criou o lote. |
| `LOT_DT_PRODUCAO` | DATE | Sim | Data em que a produção foi efetivamente realizada. |
| `LOT_DT_INICIO` | DATE | Sim | Data de início da produção. |
| `LOT_DT_PREVISAO` | DATE | Sim | Data prevista para conclusão da produção. |
| `LOT_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações do lote (texto longo). |
| `LOT_COLABORADOR` | INTEGER | Sim | FK para TB_PESSOA (PES_COLABORADOR=S). Colaborador responsável pelo lote. |
| `LOT_ORIGEM` | VARCHAR(20) | Sim | Tabela/documento que originou o lote (ex.: ORDEM_PRODUCAO, INVENTARIO). |
| `LOT_ID_ORIGEM` | INTEGER | Sim | Identificador do registro de origem do lote. |
| `CAMPO_6` | VARCHAR(70) | Sim | Campo genérico reservado (uso conforme customização do cliente). |
| `CAMPO_13` | VARCHAR(10) | Sim | Campo genérico reservado (uso conforme customização do cliente). |
| `CAMPO_14` | VARCHAR(10) | Sim | Campo genérico reservado (uso conforme customização do cliente). |

COMMENT ON COLUMN TB_LOTE_PRODUCAO.LOT_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização';
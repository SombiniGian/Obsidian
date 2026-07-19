# Tabela TB_SITUACAO

**Módulo:** Ordens de Serviço / Produção
Cadastro de situações (status customizados) utilizadas em ordens de serviço, ordens de produção e outros documentos. Cada situação possui descrição, cor, status, observação e flags de uso em OS/OP/almoxarifado, além de suporte a notificação por WhatsApp.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `SIT_ID` | INTEGER | Não | Identificador único da situação. |
| `SIT_EMPRESA` | INTEGER | Sim | Identificador da empresa à qual a situação pertence. |
| `SIT_DESCRICAO` | VARCHAR(100) | Sim | Descrição da situação. |
| `SIT_STATUS` | VARCHAR(1) | Sim | Status da situação (A = Ativa, I = Inativa). |
| `SIT_COR` | VARCHAR(20) | Sim | Cor associada à situação (para destaque em telas e relatórios). |
| `SIT_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações da situação em formato binário. NUNCA selecione em queries SELECT. |
| `SIT_ARQUIVO_IMP` | VARCHAR(20) | Sim | Nome do arquivo de impressão associado à situação. |
| `SIT_USAR_OS` | VARCHAR(1) | Sim | Indica se a situação é usada em ordens de serviço (S/N). |
| `SIT_USAR_OP` | VARCHAR(1) | Sim | Indica se a situação é usada em ordens de produção (S/N). |
| `SIT_WHATSUP` | VARCHAR(1) | Sim | Indica se a situação dispara notificação via WhatsApp (S/N). |
| `SIT_ALMOXARIFADO` | VARCHAR(1) | Sim | Indica se a situação é usada no almoxarifado (S/N). |

COMMENT ON COLUMN TB_SITUACAO.SIT_STATUS IS 'A - ATIVA
I - INATIVA';
COMMENT ON COLUMN TB_SITUACAO.SIT_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

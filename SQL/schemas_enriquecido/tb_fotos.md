# Tabela TB_FOTOS

**Módulo:** Cadastros / Genérico
Tabela genérica de fotos anexadas a registros de qualquer tabela do sistema. Armazena a imagem binária ou URLs (BBImg/manual) e metadados de quem/when cadastrou.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `FOT_ID` | INTEGER | Não | Identificador único da foto. |
| `FOT_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `FOT_TABELA` | VARCHAR(50) | Sim | Nome da tabela à qual a foto está vinculada. |
| `FOT_REGISTRO` | INTEGER | Sim | Identificador do registro na tabela de origem. |
| `FOT_SEQ` | INTEGER | Sim | Sequência da foto dentro do registro. |
| `FOT_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que anexou a foto. |
| `FOT_DESCRICAO` | VARCHAR(100) | Sim | Descrição/legenda da foto. |
| `FOT_FOTO` | BLOB SUB_TYPE BINARY | Sim | Conteúdo binário da imagem. |
| `FOT_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de cadastro da foto. |
| `FOT_URL_BBIMG` | VARCHAR(2000) | Sim | URL pública da imagem hospedada no BBImg (quando aplicável). |
| `FOT_URL_MANUAL` | VARCHAR(1000) | Sim | URL manual informada pelo usuário. |

COMMENT ON COLUMN TB_FOTOS.FOT_FOTO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização';
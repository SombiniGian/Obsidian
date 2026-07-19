# Tabela TB_PESSOA_FOTOS

**Módulo:** Cadastros
Fotos/documentos digitalizados vinculados a uma pessoa (TB_PESSOA). Permite armazenar múltiplas fotos e imagens de documentos (frente/verso) por cadastro, com controle de exibição no PDV.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PEF_PESSOA` | INTEGER | Não | FK para TB_PESSOA.PES_ID — pessoa dona da foto. Parte da chave primária composta. |
| `PEF_SEQUENCIA` | INTEGER | Não | Sequencial da foto dentro da pessoa. Parte da chave primária composta. |
| `PEF_DESCRICAO` | VARCHAR(100) | Sim | Descrição da foto (ex.: Foto do Rosto, Documento RG Frente). |
| `PEF_FOTO` | BLOB SUB_TYPE BINARY | Sim | Arquivo binário da foto/documento. NUNCA selecione em queries SELECT. |
| `PEF_ID` | INTEGER | Não | Identificador único do registro de foto. |
| `PEF_ORDEM_PDV` | INTEGER | Sim | Ordem de exibição no PDV. |
| `PEF_EXIBIR_PDV` | VARCHAR(1) | Sim | Indica se exibe a foto no PDV (S/N). |
| `PEF_TODOS_PDV` | VARCHAR(1) | Sim | Indica se exibe em todos os PDVs (S/N). |
| `PEF_DOC_FRENTE` | VARCHAR(1) | Sim | Indica se é a foto da frente do documento (S/N). |
| `PEF_DOC_VERSO` | VARCHAR(1) | Sim | Indica se é a foto do verso do documento (S/N). |

COMMENT ON COLUMN TB_PESSOA_FOTOS.PEF_PESSOA IS 'FK para TB_PESSOA.PES_ID — use JOIN com TB_PESSOA por PES_ID';
COMMENT ON COLUMN TB_PESSOA_FOTOS.PEF_FOTO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização';

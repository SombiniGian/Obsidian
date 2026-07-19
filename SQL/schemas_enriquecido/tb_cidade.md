# Tabela TB_CIDADE

**Módulo:** Cadastros
Cadastro de cidades/municípios brasileiros utilizados em endereços, notas fiscais e regras tributárias (IBS/CBS, código IBGE).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CID_ID` | INTEGER | Não | Identificador único da cidade. |
| `CID_NOME` | VARCHAR(80) | Sim | Nome do município. |
| `CID_CODIGO_MUNICIPIO` | VARCHAR(10) | Sim | Código do município (IBGE). |
| `CID_CEP` | VARCHAR(10) | Sim | CEP genérico da cidade. |
| `CID_ESTADO` | INTEGER | Sim | FK para TB_ESTADO.EST_ID. |
| `CID_REGIAO` | INTEGER | Sim | FK para TB_REGIAO.REG_ID. |
| `CID_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. Default: current_timestamp. |
| `CID_COD_NFSE` | VARCHAR(10) | Sim | Código do município na NFS-e. |
| `CID_IBS` | NUMERIC(15,2) | Sim | Alíquota de IBS do município (reforma tributária). |
| `CID_GOV_REDUTOR` | NUMERIC(15,2) | Sim | Redutor governamental aplicado ao IBS municipal. |

COMMENT ON COLUMN TB_CIDADE.CID_ESTADO IS 'FK para TB_ESTADO.EST_ID — use JOIN com TB_ESTADO para obter UF/sigla';

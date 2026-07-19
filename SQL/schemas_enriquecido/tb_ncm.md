# Tabela TB_NCM

**Módulo:** Fiscal
Tabela de NCM (Nomenclatura Comum do Mercosul) utilizada na classificação fiscal de produtos, determinação de alíquotas de ICMS (estadual e municipal), IPI nacional e de importação, e na validação de regras tributárias na emissão de NF-e/NFC-e.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `NCM_CODIGO` | VARCHAR(10) | Não | Código NCM (chave primária). Formato 8 dígitos com possíveis sufixos (ex.: 8471.30.12 ou 84713012). |
| `NCM_DESCRICAO` | VARCHAR(2000) | Sim | Descrição do NCM. |
| `NCM_TIPO` | VARCHAR(1) | Sim | Tipo do NCM (uso interno/classificação). |
| `NCM_ALIQ_NAC` | NUMERIC(15,2) | Sim | Alíquota de IPI nacional. |
| `NCM_ALIQ_IMP` | NUMERIC(15,2) | Sim | Alíquota de IPI para produtos importados. |
| `NCM_GENERO` | VARCHAR(2) | Sim | Gênero do item (tabela IBGE). |
| `NCM_ALIQ_EST` | NUMERIC(15,2) | Sim | Alíquota de ICMS estadual. |
| `NCM_ALIQ_MUN` | NUMERIC(15,2) | Sim | Alíquota de ICMS municipal. |
| `NCM_STATUS` | VARCHAR(1) | Sim | Status do NCM (A=Ativo, I=Inativo). |
| `NCM_VERSAO` | VARCHAR(10) | Sim | Versão da tabela NCM utilizada. |
| `NCM_DT_INICIO` | DATE | Sim | Data de início da vigência do NCM. |
| `NCM_DT_FIM` | DATE | Sim | Data de fim da vigência do NCM. |

COMMENT ON COLUMN TB_NCM.NCM_CODIGO IS 'Chave primária da tabela. Use SEMPRE JOIN por NCM_CODIGO. Em TB_PRODUTO o campo de ligação é o NCM do produto (mesmo conteúdo, apenas o nome do campo muda).';
COMMENT ON COLUMN TB_NCM.NCM_STATUS IS 'A - ATIVO
I - INATIVO';

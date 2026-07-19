# Tabela TB_CST

**Módulo:** Fiscal
Tabela de CST (Código de Situação Tributária) do ICMS, utilizada na emissão de NF-e/NFC-e. Define se há tributação, redução de base/alíquota, transferência de crédito, diferimento, monofásica e regras de IBS/CBS (reforma tributária).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CST_CODIGO` | VARCHAR(3) | Não | Código CST de 3 dígitos (chave primária). Ex.: 000, 010, 020, 040, 060, 090. |
| `CST_DESCRICAO` | VARCHAR(500) | Sim | Descrição do CST. |
| `CST_EXIGE_TRIBUTACAO` | VARCHAR(1) | Sim | Indica se o CST exige tributação (S/N). |
| `CST_REDUCAO_BC` | VARCHAR(1) | Sim | Indica se o CST permite redução de base de cálculo (S/N). |
| `CST_REDUCAO_ALIQUOTA` | VARCHAR(1) | Sim | Indica se o CST permite redução de alíquota (S/N). |
| `CST_TRANSFERENCIA_CREDITO` | VARCHAR(1) | Sim | Indica se o CST permite transferência de crédito (S/N). |
| `CST_DIFERIMENTO` | VARCHAR(1) | Sim | Indica se o CST permite diferimento (S/N). |
| `CST_MONOFASICA` | VARCHAR(1) | Sim | Indica se o CST é monofásico sobre combustíveis (S/N). |
| `CST_STATUS` | VARCHAR(1) | Sim | Status do CST (A=Ativo, I=Inativo). |
| `CST_CPRES_IBS_ZFM` | VARCHAR(1) | Sim | CST CBS/IBS para Zona Franca de Manaus (reforma tributária). |
| `CST_AJUSTE_CREDITO` | VARCHAR(1) | Sim | Indica se permite ajuste de crédito (S/N). |

COMMENT ON COLUMN TB_CST.CST_CODIGO IS 'Chave primária. Use SEMPRE JOIN por CST_CODIGO. No XML da NF-e este código é referenciado como orig+CST ou CST isolado dependendo da tag.';
COMMENT ON COLUMN TB_CST.CST_EXIGE_TRIBUTACAO IS 'S - SIM
N - NAO';
COMMENT ON COLUMN TB_CST.CST_STATUS IS 'A - ATIVO
I - INATIVO';

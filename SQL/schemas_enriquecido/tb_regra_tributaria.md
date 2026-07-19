# Tabela TB_REGRA_TRIBUTARIA

**Módulo:** Fiscal (IBS/CBS)
Cadastro de regras tributárias da Reforma Tributária (IBS/CBS/IS). Define CST, classificação tributária, alíquotas, reduções, diferimentos e desonerações aplicáveis por estado, natureza de operação e regime do destinatário.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `RTB_ID` | INTEGER | Não | Identificador único da regra tributária. |
| `RTB_DESCRICAO` | VARCHAR(100) | Sim | Descrição da regra. |
| `RTB_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `RTB_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. |
| `RTB_CST_CBS_IBS` | VARCHAR(3) | Sim | CST unificada CBS/IBS. |
| `RTB_CLASS_TRIB` | VARCHAR(20) | Sim | Classificação tributária (cClassTrib). |
| `RTB_IBS_UF_ALIQ` | NUMERIC(15,2) | Sim | Alíquota IBS estadual. |
| `RTB_IBS_UF_DIF` | NUMERIC(15,2) | Sim | Diferimento IBS estadual. |
| `RTB_IBS_UF_RED` | NUMERIC(15,2) | Sim | Redução IBS estadual. |
| `RTB_IBS_UF_DESON` | NUMERIC(15,2) | Sim | Desoneração IBS estadual. |
| `RTB_IBS_MUN_ALIQ` | NUMERIC(15,2) | Sim | Alíquota IBS municipal. |
| `RTB_IBS_MUN_DIF` | NUMERIC(15,2) | Sim | Diferimento IBS municipal. |
| `RTB_IBS_MUN_RED` | NUMERIC(15,2) | Sim | Redução IBS municipal. |
| `RTB_IBS_MUN_DESON` | NUMERIC(15,2) | Sim | Desoneração IBS municipal. |
| `RTB_IBS_CPRES_COD` | VARCHAR(2) | Sim | Código de situação tributária da CBS/IBS em operação com crédito presumido. |
| `RTB_IBS_CPRES_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do crédito presumido IBS. |
| `RTB_CBS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota CBS. |
| `RTB_CBS_DIF` | NUMERIC(15,2) | Sim | Diferimento CBS. |
| `RTB_CBS_RED` | NUMERIC(15,2) | Sim | Redução CBS. |
| `RTB_CBS_DESON` | NUMERIC(15,2) | Sim | Desoneração CBS. |
| `RTB_CBD_CPRES_COD` | VARCHAR(2) | Sim | Código CBS em crédito presumido. |
| `RTB_CBS_CPRES_ALIQ` | NUMERIC(15,2) | Sim | Alíquota de crédito presumido CBS. |
| `RTB_MONO_CBS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota monofásica CBS. |
| `RTB_MONO_IBS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota monofásica IBS. |
| `RTB_MONO_CBS_RETEN` | NUMERIC(15,2) | Sim | Alíquota retida monofásica CBS. |
| `RTB_MONO_IBS_RETEN` | NUMERIC(15,2) | Sim | Alíquota retida monofásica IBS. |
| `RTB_MONO_CBS_RET` | NUMERIC(15,2) | Sim | Alíquota retida monofásica CBS (detalhada). |
| `RTB_MONO_IBS_RET` | NUMERIC(15,2) | Sim | Alíquota retida monofásica IBS (detalhada). |
| `RTB_MONO_CBS_DIF` | NUMERIC(15,2) | Sim | Diferimento monofásico CBS. |
| `RTB_MONO_IBS_DIF` | NUMERIC(15,2) | Sim | Diferimento monofásico IBS. |
| `RTB_REG_CST` | VARCHAR(3) | Sim | CST no regime específico. |
| `RTB_REG_CLASS_TRIB` | VARCHAR(20) | Sim | Classificação tributária no regime específico. |
| `RTB_REG_IBS_UF_ALIQ` | NUMERIC(15,2) | Sim | Alíquota IBS UF no regime específico. |
| `RTB_REG_IBS_MUN_ALIQ` | NUMERIC(15,2) | Sim | Alíquota IBS MUN no regime específico. |
| `RTB_REG_CBS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota CBS no regime específico. |
| `RTB_IS_CST` | VARCHAR(3) | Sim | CST do Imposto Seletivo (IS). |
| `RTB_IS_CLASS_TRIB` | VARCHAR(20) | Sim | Classificação tributária do IS. |
| `RTB_IS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do IS. |
| `RTB_IS_ESP_ALIQ` | NUMERIC(15,2) | Sim | Alíquota específica do IS. |
| `RTB_REGRA_TRIBUTARIA` | INTEGER | Sim | FK para outra regra tributária (encadeamento). |
| `RTB_NATUREZA_OPERACAO` | INTEGER | Sim | FK para TB_NATUREZA_OPERACAO vinculada. |
| `RTB_ESTADO` | INTEGER | Sim | FK para TB_ESTADO (UF de aplicação). |
| `RTB_REGIME_DEST` | VARCHAR(2) | Sim | Regime tributário do destinatário (1=Contribuinte, 2=Não contribuinte). |
| `RTB_ZONA_FRANCA` | VARCHAR(1) | Sim | Aplicável a zona franca (S/N). |

COMMENT ON COLUMN TB_REGRA_TRIBUTARIA.RTB_REGIME_DEST IS '1 - CONTRIBUINTE
2 - NAO CONTRIBUINTE';
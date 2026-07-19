# Tabela TB_GRUPO_TRIB_ITEM

**Módulo:** Fiscal / Tributação
Tabela de itens (regras) de um grupo de tributação. Define por estado/natureza de operação/CFOP as alíquotas, CST/CSOSN, MVA, ICMS-ST, FCP, ICMS monofásico, difal, benefício fiscal e ajustes aplicados.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TRBI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `TRBI_GRUPO_TRIBUTACAO` | INTEGER | Não | FK para TB_GRUPO_TRIBUTACAO. Grupo de tributação. Parte da chave primária composta. |
| `TRBI_SEQUENCIA` | INTEGER | Não | Sequencial da regra dentro do grupo. Parte da chave primária composta. |
| `TRBI_ESTADO` | INTEGER | Sim | FK para TB_ESTADO. Estado (UF) destinatário da regra. |
| `TRBI_NATUREZA_OPERACAO` | INTEGER | Sim | FK para TB_NATUREZA_OPERACAO. Natureza de operação. |
| `TRBI_CFOP` | VARCHAR(4) | Sim | CFOP aplicável à regra. |
| `TRBI_TIPO_PRODUTO` | VARCHAR(2) | Sim | Tipo de produto (Mercadoria, Serviço, etc.). |
| `TRBI_REGIME_DEST` | VARCHAR(2) | Sim | Regime tributário do destinatário. |
| `TRBI_ICMS_ORIGEM` | VARCHAR(1) | Sim | Origem da mercadoria (0=Nacional, 1=Importada etc.). |
| `TRBI_ICMS_CST` | VARCHAR(4) | Sim | CST do ICMS. |
| `TRBI_ICMS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do ICMS. |
| `TRBI_ICMS_MOD_BC` | INTEGER | Sim | Modalidade de base de cálculo do ICMS. |
| `TRBI_ICMS_ST_MVA` | NUMERIC(15,2) | Sim | MVA (Margem de Valor Agregado) para ICMS-ST. |
| `TRBI_ICMS_ST_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do ICMS-ST. |
| `TRBI_ICMS_ST_MOD_BC` | INTEGER | Sim | Modalidade de base de cálculo do ICMS-ST. |
| `TRBI_FCP_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do FCP (Fundo de Combate à Pobreza). |
| `TRBI_MSG_FISCAL` | INTEGER | Sim | Código da mensagem fiscal aplicada. |
| `TRBI_FCP_ST_ALIQ` | NUMERIC | Sim | Alíquota do FCP-ST. |
| `TRBI_ICMS_CSOSN` | VARCHAR(4) | Sim | CSOSN para optantes do Simples Nacional. |
| `TRBI_ICMS_BC_VALOR` | INTEGER | Sim | Indica se a base de cálculo é por valor (1) ou percentual (0). |
| `TRBI_COD_BENEF` | VARCHAR(10) | Sim | Código de benefício fiscal. |
| `TRBI_MOT_DESON` | INTEGER | Sim | Motivo da desoneração do ICMS. |
| `TRBI_DIF_ALIQ` | NUMERIC(15,2) | Sim | Alíquota de diferencial de alíquota (DIFAL). |
| `TRBI_ICMS_RED_BC` | NUMERIC(15,4) | Sim | Percentual de redução da base de cálculo do ICMS. |
| `TRBI_ICMS_ST_RED_BC` | NUMERIC(15,4) | Sim | Percentual de redução da base de cálculo do ICMS-ST. |
| `TRBI_ICMS_MONO` | NUMERIC(15,4) | Sim | Alíquota do ICMS monofásico (sobre operação própria). |
| `TRBI_ICMS_MONO_RETEN` | NUMERIC(15,4) | Sim | Alíquota do ICMS monofásico retido anteriormente. |
| `TRBI_ICMS_RED_MONO` | NUMERIC(15,4) | Sim | Percentual de redução da alíquota monofásica. |
| `TRBI_ICMS_MOT_RED_MONO` | VARCHAR(1) | Sim | Motivo da redução monofásica (1=Operação interestadual, etc.). |
| `TRBI_ICMS_MONO_RET` | NUMERIC(15,4) | Sim | Valor/alíquota do ICMS monofásico retido. |
| `TRBI_MONO_DIF_ALIQ` | NUMERIC(15,4) | Sim | Diferencial de alíquota monofásica. |
| `TRBI_AJUSTE_FISCAL` | INTEGER | Sim | FK para TB_AJUSTE_FISCAL aplicado na regra. |
| `TRBI_ALIQ_AJUSTE` | NUMERIC(15,2) | Sim | Alíquota do ajuste fiscal. |
| `TRBI_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. Default: current_timestamp. |
| `TRBI_COD_CRED_PRESUMIDO` | VARCHAR(10) | Sim | Código do crédito presumido. |
| `TRBI_CRED_PRESUMIDO_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do crédito presumido. |

COMMENT ON COLUMN TB_GRUPO_TRIB_ITEM.TRBI_DIF_ALIQ IS '0 - NÃO POSSUI
  1 - TÁXI
  2 - DEFICIENTE FÍSICO
  3 - PRODUTOR AGROPECUÁRIO;
  4 - FROTISTA/LOCADORA
  5 - DIPLOMÁTICO/CONSULAR
  6 - AMAZÔNIA E ÁREAS DE LIVRE COMÉRCIO
  7 - SUFRAMA
  8 - VENDA A ÓRGÃO PÚBLICO
  9 - OUTROS
  10 - DEFICIENTE CONDUTOR
  11 - DEFICIENTE NÃO CONDUTOR
  12 - ORGÃO FOMENTO
  90 - SOLICITAÇÃO FISCO';
# Tabela TB_PRODUTO_TRIBUTO

**Módulo:** Fiscal
Configuração tributária detalhada do produto por empresa (ICMS, IPI, PIS, COFINS, ICMS-ST, FCP, IBS, CBS etc.). Permite parametrizar CSTs, alíquotas, origens, MVA, reduções de base de cálculo e regras da reforma tributária.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRDT_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PRDT_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID. Parte da chave primária composta. |
| `PRDT_TIPO_PRODUTO` | VARCHAR(2) | Sim | Tipo do produto conforme SPED (00=Revenda, 01=MP, 02=Embalagem, 03=Processo, 04=Acabado, 05=Subproduto, 06=Intermediário, 07=Uso/Consumo, 08=Ativo, 09=Serviços, 10=Outros, 99=Outras). |
| `PRDT_ICMS_CST` | VARCHAR(2) | Sim | CST de ICMS (saída). |
| `PRDT_ICMS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota de ICMS (saída). |
| `PRDT_IPI_CST` | VARCHAR(2) | Sim | CST de IPI (saída). |
| `PRDT_IPI_ALIQ` | NUMERIC(15,2) | Sim | Alíquota de IPI (saída). |
| `PRDT_PIS_CST_SAI` | VARCHAR(2) | Sim | CST de PIS (saída). |
| `PRDT_PIS_NAT` | VARCHAR(3) | Sim | Código de natureza da receita (PIS). |
| `PRDT_PIS_ALIQ_SAI` | NUMERIC(15,2) | Sim | Alíquota de PIS (saída). |
| `PRDT_PIS_CST_ENT` | VARCHAR(2) | Sim | CST de PIS (entrada). |
| `PRDT_PIS_ALIQ_ENT` | NUMERIC(15,2) | Sim | Alíquota de PIS (entrada). |
| `PRDT_CONFINS_CST_SAI` | VARCHAR(2) | Sim | CST de COFINS (saída). |
| `PRDT_CONFINS_NAT` | VARCHAR(3) | Sim | Código de natureza da receita (COFINS). |
| `PRDT_CONFINS_ALIQ_SAI` | NUMERIC(15,2) | Sim | Alíquota de COFINS (saída). |
| `PRDT_CONFINS_CST_ENT` | VARCHAR(2) | Sim | CST de COFINS (entrada). |
| `PRDT_CONFINS_ALIQ_ENT` | NUMERIC(15,2) | Sim | Alíquota de COFINS (entrada). |
| `PRDT_ICMS_ORIGEM` | VARCHAR(1) | Sim | Origem da mercadoria (0=Nacional, 1=Importação direta, 2=Adquirida no mercado interno, 3/4/5=Nacional c/ conteúdo importado, 6/7=Sem similar nacional, 8=Nacional > 70%). |
| `PRDT_ICMS_CSOSN` | VARCHAR(4) | Sim | CSOSN para Simples Nacional. |
| `PRDT_ICMS_ALIQ_CRED` | NUMERIC(15,2) | Sim | Alíquota de crédito de ICMS no Simples Nacional. |
| `PRDT_ICMS_MVA` | NUMERIC(15,2) | Sim | MVA (Margem de Valor Agregado) ou pauta para cálculo de ICMS-ST. |
| `PRDT_TRIBUTACAO_ECF` | VARCHAR(1) | Sim | Tributação em ECF (T=Tributado, F=Substituição, I=Isento, N=Não incidência, S=ISS Tributado). |
| `PRDT_ICMS_MOD_BC` | INTEGER | Sim | Modalidade de BC do ICMS (0=MVA%, 1=Pauta, 2=Preço tabelado, 3=Valor da operação). |
| `PRDT_ICMS_ST_MOD_BC` | INTEGER | Sim | Modalidade de BC do ICMS-ST (0=Preço tabelado, 1=Lista Negativa, 2=Lista Positiva, 3=Lista Neutra, 4=MVA%, 5=Pauta). |
| `PRDT_ICMS_ST_ALIQ` | NUMERIC(15,2) | Sim | Alíquota de ICMS-ST. |
| `PRDT_GRUPO_TRIB` | INTEGER | Sim | FK para grupo tributário. |
| `PRDT_CEST` | VARCHAR(7) | Sim | Código CEST (Substituição Tributária). |
| `PRDT_CEST_NCM` | VARCHAR(8) | Sim | NCM relacionado ao CEST. |
| `PRDT_IPI_CST_ENT` | VARCHAR(2) | Sim | CST de IPI (entrada). |
| `PRDT_IPI_ALIQ_ENT` | NUMERIC(15,2) | Sim | Alíquota de IPI (entrada). |
| `PRDT_IPI_ENQ` | VARCHAR(3) | Sim | Código de enquadramento do IPI. |
| `PRDT_FCP_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do Fundo de Combate à Pobreza (FCP). |
| `PRDT_FCP_ST_ALIQ` | NUMERIC(15,2) | Sim | Alíquota de FCP-ST. |
| `PRDT_FCP_ST_BC_RET` | NUMERIC(15,2) | Sim | Base de cálculo FCP-ST retido. |
| `PRDT_FCP_ST_VALOR_RET` | NUMERIC(15,2) | Sim | Valor do FCP-ST retido. |
| `PRDT_ST_BC_RET` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS-ST retido. |
| `PRDT_ST_VALOR_RET` | NUMERIC(15,2) | Sim | Valor do ICMS-ST retido. |
| `PRDT_ICMS_VALOR_RET` | NUMERIC(15,2) | Sim | Valor do ICMS retido. |
| `PRDT_FCP_ST_ALIQ_RET` | INTEGER | Sim | Alíquota de FCP-ST retido. |
| `PRDT_MOT_DESON` | INTEGER | Sim | Motivo da desoneração (1=Táxi, 2=Deficiente, 3=Produtor, 9=Outros, etc.). |
| `PRDT_COD_BENEF` | VARCHAR(10) | Sim | Código de benefício fiscal. |
| `PRDT_DIF_ALIQ` | NUMERIC(15,2) | Sim | Percentual de DIFAL. |
| `PRDT_ICMS_BC` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS fixa para a modalidade. |
| `PRDT_TIPO_CREDITO` | VARCHAR(3) | Sim | Tipo de crédito de ICMS (outorgado/presumido). |
| `PRDT_CONTRIB_SOCIAL` | VARCHAR(2) | Sim | Código de contribuição social. |
| `PRDT_ICMS_RED_BC` | NUMERIC(15,4) | Sim | Percentual de redução de BC do ICMS. |
| `PRDT_ICMS_ST_RED_BC` | NUMERIC(15,4) | Sim | Percentual de redução de BC do ICMS-ST. |
| `PRDT_ICMS_MONO` | NUMERIC(15,4) | Sim | Alíquota de ICMS monofásico. |
| `PRDT_ICMS_MONO_RETEN` | NUMERIC(15,4) | Sim | Alíquota de ICMS monofásico retido. |
| `PRDT_ICMS_RED_MONO` | NUMERIC(15,4) | Sim | Redução de alíquota do ICMS monofásico. |
| `PRDT_ICMS_MOT_RED_MONO` | VARCHAR(1) | Sim | Motivo da redução do ICMS monofásico. |
| `PRDT_ICMS_MONO_RET` | NUMERIC(15,4) | Sim | Alíquota de ICMS monofásico retido anteriormente. |
| `PRDT_MONO_DIF_ALIQ` | NUMERIC(15,4) | Sim | DIFAL do ICMS monofásico. |
| `PRDT_AMPARO_LEGAL_IMENDES` | BLOB SUB_TYPE BINARY | Sim | Amparo legal iMendes em formato binário. NUNCA selecione em queries SELECT. |
| `PRDT_COD_CRED_PRESUMIDO` | VARCHAR(10) | Sim | Código de crédito presumido (IBS/CBS). |
| `PRDT_CRED_PRESUMIDO_ALIQ` | NUMERIC(15,2) | Sim | Alíquota de crédito presumido. |
| `PRDT_REGRA_TRIBUTARIA` | INTEGER | Sim | Regra tributária aplicada (IBS/CBS). |

COMMENT ON COLUMN TB_PRODUTO_TRIBUTO.PRDT_ICMS_BC IS 'Valor para calcula BC do ICMS de acordo com a modalidade definida em PRDT_ICMS_MOD_BC.';
COMMENT ON COLUMN TB_PRODUTO_TRIBUTO.PRDT_AMPARO_LEGAL_IMENDES IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

# Tabela TB_NOTA_FISCAL_ITEM_TRIB

**Módulo:** Fiscal
Tributos detalhados dos itens da nota fiscal, incluindo IBS, CBS, FCP, tributação monofásica, regimes especiais, valores devolvidos e regras tributárias aplicadas.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `NFT_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `NFT_NOTA_FISCAL` | INTEGER | Não | Identificador da nota fiscal (TB_NOTA_FISCAL.NF_ID). Parte da chave primária composta. |
| `NFT_SEQUENCIA` | INTEGER | Não | Sequencial do item tributário na nota fiscal. Parte da chave primária composta. |
| `NFT_IS_CST` | VARCHAR(3) | Sim | Código de Situação Tributária do imposto seletivo. |
| `NFT_IS_CLASS_TRIB` | VARCHAR(20) | Sim | Classificação tributária do imposto seletivo. |
| `NFT_IS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do imposto seletivo. |
| `NFT_IS_ESP_ALIQ` | NUMERIC(15,2) | Sim | Alíquota específica do imposto seletivo. |
| `NFT_IS_VALOR` | NUMERIC(15,2) | Sim | Valor do imposto seletivo. |
| `NFT_IBS_CBS_BC` | NUMERIC(15,2) | Sim | Base de cálculo conjunta do IBS e da CBS. |
| `NFT_IBS_UF_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do IBS da UF. |
| `NFT_IBS_UF_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS da UF. |
| `NFT_IBS_UF_DIF_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do diferimento do IBS da UF. |
| `NFT_IBS_UF_DIF_VALOR` | NUMERIC(15,2) | Sim | Valor diferido do IBS da UF. |
| `NFT_IBS_UF_RED` | NUMERIC(15,2) | Sim | Percentual de redução do IBS da UF. |
| `NFT_IBS_UF_EFET_ALIQ` | NUMERIC(15,2) | Sim | Alíquota efetiva do IBS da UF. |
| `NFT_IBS_UF_VALOR_DEV` | NUMERIC(15,2) | Sim | Valor devolvido do IBS da UF. |
| `NFT_IBS_MUN_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do IBS municipal. |
| `NFT_IBS_MUN_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS municipal. |
| `NFT_IBS_MUN_DIF_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do diferimento do IBS municipal. |
| `NFT_IBS_MUN_DIF_VALOR` | NUMERIC(15,2) | Sim | Valor diferido do IBS municipal. |
| `NFT_IBS_MUN_RED` | NUMERIC(15,2) | Sim | Percentual de redução do IBS municipal. |
| `NFT_IBS_MUN_EFET_ALIQ` | NUMERIC(15,2) | Sim | Alíquota efetiva do IBS municipal. |
| `NFT_IBS_MUN_VALOR_DEV` | NUMERIC(15,2) | Sim | Valor devolvido do IBS municipal. |
| `NFT_IBS_VALOR` | NUMERIC(15,2) | Sim | Valor total do IBS. |
| `NFT_CBS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota da CBS. |
| `NFT_CBS_VALOR` | NUMERIC(15,2) | Sim | Valor da CBS. |
| `NFT_CBS_DIF_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do diferimento da CBS. |
| `NFT_CBS_DIF_VALOR` | NUMERIC(15,2) | Sim | Valor diferido da CBS. |
| `NFT_CBS_RED` | NUMERIC(15,2) | Sim | Percentual de redução da CBS. |
| `NFT_CBS_EFET_ALIQ` | NUMERIC(15,2) | Sim | Alíquota efetiva da CBS. |
| `NFT_CBS_VALOR_DEV` | NUMERIC(15,2) | Sim | Valor devolvido da CBS. |
| `NFT_REG_CST` | VARCHAR(3) | Sim | Código de Situação Tributária do regime regular. |
| `NFT_REG_CLASS_TRIB` | VARCHAR(20) | Sim | Classificação tributária do regime regular. |
| `NFT_REG_IBS_UF_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do IBS da UF no regime regular. |
| `NFT_REG_IBS_UF_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS da UF no regime regular. |
| `NFT_REG_IBS_MUN_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do IBS municipal no regime regular. |
| `NFT_REG_IBS_MUN_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS municipal no regime regular. |
| `NFT_REG_CBS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota da CBS no regime regular. |
| `NFT_REG_CBS_VALOR` | NUMERIC(15,2) | Sim | Valor da CBS no regime regular. |
| `NFT_IBS_CPRES_COD` | VARCHAR(2) | Sim | Código do crédito presumido do IBS. |
| `NFT_IBS_CPRES_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do crédito presumido do IBS. |
| `NFT_IBS_CPRES_VALOR` | NUMERIC(15,2) | Sim | Valor do crédito presumido do IBS. |
| `NFT_IBS_CPRES_VALOR_SUSP` | NUMERIC(15,2) | Sim | Valor suspenso do crédito presumido do IBS. |
| `NFT_CBS_CPRES_COD` | VARCHAR(2) | Sim | Código do crédito presumido da CBS. |
| `NFT_CBS_CPRES_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do crédito presumido da CBS. |
| `NFT_CBS_CPRES_VALOR` | NUMERIC(15,2) | Sim | Valor do crédito presumido da CBS. |
| `NFT_CBS_CPRES_VALOR_SUSP` | NUMERIC(15,2) | Sim | Valor suspenso do crédito presumido da CBS. |
| `NFT_GOV_IBS_UF_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do IBS da UF para operação com ente governamental. |
| `NFT_GOV_IBS_UF_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS da UF para ente governamental. |
| `NFT_GOV_IBS_MUN_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do IBS municipal para ente governamental. |
| `NFT_GOV_IBS_MUN_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS municipal para ente governamental. |
| `NFT_GOV_CBS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota da CBS para ente governamental. |
| `NFT_GOV_CBS_VALOR` | NUMERIC(15,2) | Sim | Valor da CBS para ente governamental. |
| `NFT_MONO_BC_QTDE` | NUMERIC(15,6) | Sim | Base de cálculo quantitativa da tributação monofásica. |
| `NFT_MONO_IBS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota monofásica do IBS. |
| `NFT_MONO_IBS_VALOR` | NUMERIC(15,2) | Sim | Valor monofásico do IBS. |
| `NFT_MONO_CBS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota monofásica da CBS. |
| `NFT_MONO_CBS_VALOR` | NUMERIC(15,2) | Sim | Valor monofásico da CBS. |
| `NFT_MONO_RETEN_BC_QTDE` | NUMERIC(15,6) | Sim | Base quantitativa da tributação monofásica retida. |
| `NFT_MONO_CBS_RETEN_ALIQ` | NUMERIC(15,2) | Sim | Alíquota da CBS monofásica retida. |
| `NFT_MONO_CBS_RETEN_VALOR` | NUMERIC(15,2) | Sim | Valor da CBS monofásica retida. |
| `NFT_MONO_IBS_RETEN_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do IBS monofásico retido. |
| `NFT_MONO_IBS_RETEN_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS monofásico retido. |
| `NFT_MONO_RET_BC_QTDE` | NUMERIC(15,6) | Sim | Base quantitativa da tributação monofásica a reter. |
| `NFT_MONO_CBS_RET_ALIQ` | NUMERIC(15,2) | Sim | Alíquota da CBS monofásica a reter. |
| `NFT_MONO_CBS_RET_VALOR` | NUMERIC(15,2) | Sim | Valor da CBS monofásica a reter. |
| `NFT_MONO_IBS_RET_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do IBS monofásico a reter. |
| `NFT_MONO_IBS_RET_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS monofásico a reter. |
| `NFT_MONO_CBS_DIF` | NUMERIC(15,2) | Sim | Percentual de diferimento da CBS monofásica. |
| `NFT_MONO_CBS_DIF_VALOR` | NUMERIC(15,2) | Sim | Valor diferido da CBS monofásica. |
| `NFT_MONO_IBS_DIF` | NUMERIC(15,2) | Sim | Percentual de diferimento do IBS monofásico. |
| `NFT_MONO_IBS_DIF_VALOR` | NUMERIC(15,2) | Sim | Valor diferido do IBS monofásico. |
| `NFT_MONO_CBS_TOTAL` | NUMERIC(15,2) | Sim | Valor total da CBS monofásica. |
| `NFT_MONO_IBS_TOTAL` | NUMERIC(15,2) | Sim | Valor total do IBS monofásico. |
| `NFT_TRANSF_CRED_IBS_VALOR` | NUMERIC(15,2) | Sim | Valor de crédito de IBS transferido. |
| `NFT_TRANSF_CRED_CBS_VALOR` | NUMERIC(15,2) | Sim | Valor de crédito de CBS transferido. |
| `NFT_CPRES_ZFM_IBS_TIPO` | VARCHAR(1) | Sim | Tipo do crédito presumido de IBS da Zona Franca de Manaus. |
| `NFT_CPRES_ZFM_IBS_VALOR` | NUMERIC(15,2) | Sim | Valor do crédito presumido de IBS da Zona Franca de Manaus. |
| `NFT_IS_BC` | NUMERIC(15,2) | Sim | Base de cálculo do imposto seletivo. |
| `NFT_IBS_CBS_CST` | VARCHAR(3) | Sim | Código de Situação Tributária do IBS e CBS. |
| `NFT_IBS_CBS_CLASS_TRIB` | VARCHAR(20) | Sim | Classificação tributária do IBS e da CBS. |
| `NFT_REGRA_APLICADA` | INTEGER | Sim | Identificador da regra tributária aplicada ao item. |
| `NFT_REGRA_PRODUTO` | INTEGER | Sim | Identificador da regra tributária definida para o produto. |

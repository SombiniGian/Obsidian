# Tabela TB_PEDIDO_VENDA_ITEM_NF

**Módulo:** Fiscal / Vendas
Dados fiscais dos itens de pedido de venda preparados para emissão da nota fiscal. Mantém produto, valores, códigos fiscais e bases, alíquotas e valores dos tributos calculados para o faturamento.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PVNF_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PVNF_PEDIDO_VENDA` | INTEGER | Não | Identificador do pedido de venda (TB_PEDIDO_VENDA.PEV_ID). Parte da chave primária composta. |
| `PVNF_SEQUENCIA` | INTEGER | Não | Sequencial do item fiscal dentro do pedido. Parte da chave primária composta. |
| `PVNF_PRODUTO` | INTEGER | Sim | Identificador do produto (TB_PRODUTO.PRD_ID). |
| `PVNF_DESCRICAO` | VARCHAR(100) | Sim | Descrição do produto no item fiscal. |
| `PVNF_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade faturada do item. |
| `PVNF_VALOR_UNITARIO` | NUMERIC(15,10) | Sim | Valor unitário do item para faturamento. |
| `PVNF_VALOR_SUB_TOTAL` | NUMERIC(15,4) | Sim | Subtotal do item antes de descontos e despesas. |
| `PVNF_VALOR_DESCONTO` | NUMERIC(15,4) | Sim | Valor de desconto aplicado ao item. |
| `PVNF_VALOR_DESPESAS` | NUMERIC(15,4) | Sim | Despesas rateadas para o item. |
| `PVNF_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do item fiscal. |
| `PVNF_CFOP` | VARCHAR(4) | Sim | Código Fiscal de Operações e Prestações do item. |
| `PVNF_NCM` | VARCHAR(8) | Sim | Código NCM do produto. |
| `PVNF_VALOR_IMPOSTOS` | NUMERIC(15,2) | Sim | Valor total dos impostos do item. |
| `PVNF_ICMS_ORIGEM` | VARCHAR(1) | Sim | Origem da mercadoria para cálculo do ICMS. |
| `PVNF_ICMS_CSOSN` | VARCHAR(4) | Sim | Código de Situação da Operação no Simples Nacional. |
| `PVNF_ICMS_CST` | VARCHAR(3) | Sim | Código de Situação Tributária do ICMS. |
| `PVNF_ICMS_MOD_BC` | INTEGER | Sim | Modalidade de determinação da base de cálculo do ICMS. |
| `PVNF_ICMS_BC_FIXO` | NUMERIC(15,2) | Sim | Base de cálculo fixa do ICMS. |
| `PVNF_ICMS_BC` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS. |
| `PVNF_ICMS_VALOR` | NUMERIC(15,2) | Sim | Valor do ICMS. |
| `PVNF_ICMS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do ICMS. |
| `PVNF_ICMS_CRED_ALIQ` | NUMERIC(15,2) | Sim | Alíquota de crédito de ICMS. |
| `PVNF_ICMS_CRED_VALOR` | NUMERIC(15,2) | Sim | Valor do crédito de ICMS. |
| `PVNF_ICMS_ST_BC_FIXO` | INTEGER | Sim | Base de cálculo fixa do ICMS por substituição tributária. |
| `PVNF_ICMS_ST_BC` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS por substituição tributária. |
| `PVNF_ICMS_ST_VALOR` | NUMERIC(15,2) | Sim | Valor do ICMS por substituição tributária. |
| `PVNF_ICMS_ST_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do ICMS por substituição tributária. |
| `PVNF_ICMS_ST_MOD_BC` | INTEGER | Sim | Modalidade de determinação da base do ICMS-ST. |
| `PVNF_IPI_CST` | VARCHAR(2) | Sim | Código de Situação Tributária do IPI. |
| `PVNF_IPI_VALOR` | NUMERIC(15,2) | Sim | Valor do IPI. |
| `PVNF_IPI_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do IPI. |
| `PVNF_IPI_ENQ` | VARCHAR(3) | Sim | Código de enquadramento do IPI. |
| `PVNF_PIS_CST` | VARCHAR(2) | Sim | Código de Situação Tributária do PIS. |
| `PVNF_PIS_BC` | NUMERIC(15,2) | Sim | Base de cálculo do PIS. |
| `PVNF_PIS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do PIS. |
| `PVNF_PIS_VALOR` | NUMERIC(15,2) | Sim | Valor do PIS. |
| `PVNF_CONFINS_CST` | VARCHAR(2) | Sim | Código de Situação Tributária da COFINS. |
| `PVNF_CONFINS_BC` | NUMERIC(15,2) | Sim | Base de cálculo da COFINS. |
| `PVNF_CONFINS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota da COFINS. |
| `PVNF_CONFINS_VALOR` | NUMERIC(15,2) | Sim | Valor da COFINS. |
| `PVNF_ICMS_MVA` | NUMERIC(15,2) | Sim | Margem de Valor Agregado utilizada no ICMS-ST. |
| `PVNF_CEST` | VARCHAR(7) | Sim | Código Especificador da Substituição Tributária. |
| `PVNF_ICMS_ALIQ_UF_DEST` | NUMERIC(15,2) | Sim | Alíquota do ICMS para a UF de destino. |
| `PVNF_ICMS_PARTILHA` | NUMERIC(15,2) | Sim | Percentual de partilha do ICMS entre origem e destino. |
| `PVNF_ICMS_VALOR_DIFAL` | NUMERIC(15,2) | Sim | Valor do diferencial de alíquotas do ICMS. |
| `PVNF_ICMS_VALOR_UF_DEST` | NUMERIC(15,2) | Sim | Valor do ICMS destinado à UF de destino. |
| `PVNF_ICMS_VALOR_UF_ORIGEM` | NUMERIC(15,2) | Sim | Valor do ICMS pertencente à UF de origem. |
| `PVNF_FCP_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do Fundo de Combate à Pobreza. |
| `PVNF_FCP_ALIQ_UF_DEST` | NUMERIC(15,2) | Sim | Alíquota do FCP da UF de destino. |
| `PVNF_FCP_VALOR` | NUMERIC(15,2) | Sim | Valor do FCP. |
| `PVNF_ICMS_BC_UF_DEST` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS da UF de destino. |
| `PVNF_FCP_BC_UF_DEST` | NUMERIC(15,2) | Sim | Base de cálculo do FCP da UF de destino. |
| `PVNF_FCP_VALOR_UF_DEST` | NUMERIC(15,2) | Sim | Valor do FCP da UF de destino. |
| `PVNF_ICMS_ALIQ_INTER` | NUMERIC(15,2) | Sim | Alíquota interestadual do ICMS. |
| `PVNF_CONFINS_NAT_REC` | VARCHAR(3) | Sim | Natureza da receita da COFINS. |
| `PVNF_PIS_NAT_REC` | VARCHAR(3) | Sim | Natureza da receita do PIS. |
| `PVNF_IPI_BC` | NUMERIC(15,2) | Sim | Base de cálculo do IPI. |
| `PVNF_CODIGO_FCI` | VARCHAR(50) | Sim | Código da Ficha de Conteúdo de Importação. |
| `PVNF_CONTEUDO_IMPORTACAO` | NUMERIC(15,2) | Sim | Percentual de conteúdo de importação. |
| `PVNF_FCP_BC` | NUMERIC(15,2) | Sim | Base de cálculo do FCP. |
| `PNNF_FCP_ICMS_BC` | NUMERIC(15,2) | Sim | Base de cálculo do FCP relacionado ao ICMS. |
| `PVNF_FCP_ICMS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do FCP relacionado ao ICMS. |
| `PVNF_FCP_ICMS_VALOR` | NUMERIC(15,2) | Sim | Valor do FCP relacionado ao ICMS. |
| `PVNF_FCP_ST_BC` | NUMERIC(15,2) | Sim | Base de cálculo do FCP-ST. |
| `PVNF_FCP_ST_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do FCP-ST. |
| `PVNF_FCP_ST_VALOR` | NUMERIC(15,2) | Sim | Valor do FCP-ST. |
| `PVNF_FCP_ST_RET_BC` | NUMERIC(15,2) | Sim | Base de cálculo do FCP-ST retido. |
| `PVNF_FCP_ST_RET_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do FCP-ST retido. |
| `PVNF_FCP_ST_RET_VALOR` | NUMERIC(15,2) | Sim | Valor do FCP-ST retido. |
| `PVNF_PERC_ST` | NUMERIC(15,2) | Sim | Percentual aplicado à substituição tributária. |
| `PVNF_COD_BENEF` | VARCHAR(10) | Sim | Código do benefício fiscal. |
| `PVNF_MOT_DESON` | INTEGER | Sim | Motivo da desoneração do ICMS. |
| `PVNF_ICMS_DESON_VALOR` | NUMERIC(15,2) | Sim | Valor do ICMS desonerado. |
| `PVNF_ICMS_DIF_ALIQ` | NUMERIC(15,2) | Sim | Diferencial de alíquota do ICMS. |
| `PVNF_ICMS_EFET_BC` | NUMERIC(15,2) | Sim | Base efetiva do ICMS. |
| `PVNF_ICMS_EFET_ALIQ` | NUMERIC(15,2) | Sim | Alíquota efetiva do ICMS. |
| `PVNF_ICMS_EFET_VALOR` | NUMERIC(15,2) | Sim | Valor efetivo do ICMS. |
| `PVNF_ICMS_EFET_RED_BC` | NUMERIC(15,2) | Sim | Redução da base efetiva do ICMS. |
| `PVNF_QTDE_ESTOQUE` | NUMERIC(15,6) | Sim | Quantidade do item considerada no estoque. |
| `PVNF_ICMS_RED_BC` | NUMERIC(15,4) | Sim | Percentual de redução da base de cálculo do ICMS. |
| `PVNF_ICMS_ST_RED_BC` | NUMERIC(15,4) | Sim | Percentual de redução da base de cálculo do ICMS-ST. |
| `PVNF_ICMS_ALIQ_NORMAL` | NUMERIC(15,2) | Sim | Alíquota normal do ICMS antes de reduções ou ajustes. |

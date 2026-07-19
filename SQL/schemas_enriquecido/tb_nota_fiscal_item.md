# Tabela TB_NOTA_FISCAL_ITEM

**Módulo:** Fiscal
Itens (produtos) que compõem uma nota fiscal (TB_NOTA_FISCAL). Reúne dados de quantidade, valor, ICMS/IPI/PIS/COFINS, ST, DIFAL, IBS/CBS, informações de importação e referência ao pedido de venda/compra.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `NFI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `NFI_NOTA_FISCAL` | INTEGER | Não | FK para TB_NOTA_FISCAL.NF_ID. Parte da chave primária composta. |
| `NFI_SEQUENCIA` | INTEGER | Não | Sequencial do item dentro da NF. Parte da chave primária composta. |
| `NFI_PRODUTO` | INTEGER | Sim | FK para TB_PRODUTO.PRD_ID. |
| `NFI_DESCRICAO` | VARCHAR(100) | Sim | Descrição do produto na NF (denominação). |
| `NFI_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção (S/N). |
| `NFI_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade do item. |
| `NFI_VALOR_UNITARIO` | NUMERIC(15,10) | Sim | Valor unitário. |
| `NFI_VALOR_SUB_TOTAL` | NUMERIC(15,4) | Sim | Valor do subtotal do item. |
| `NFI_VALOR_DESCONTO` | NUMERIC(15,4) | Sim | Valor do desconto aplicado ao item. |
| `NFI_VALOR_DESPESAS` | NUMERIC(15,4) | Sim | Despesas acessórias do item. |
| `NFI_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do item. |
| `NFI_CFOP` | VARCHAR(4) | Sim | CFOP do item. |
| `NFI_NCM` | VARCHAR(8) | Sim | NCM do produto. |
| `NFI_UNIDADE` | VARCHAR(6) | Sim | Unidade de medida. |
| `NFI_VALOR_IMPOSTOS` | NUMERIC(15,2) | Sim | Valor aproximado dos impostos do item. |
| `NFI_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo específico do produto (S=Simples, V=Veículo). |
| `NFI_ICMS_ORIGEM` | VARCHAR(1) | Sim | Origem da mercadoria (0..8). |
| `NFI_ICMS_CSOSN` | VARCHAR(4) | Sim | CSOSN do ICMS (Simples Nacional). |
| `NFI_ICMS_CST` | VARCHAR(3) | Sim | CST do ICMS. |
| `NFI_ICMS_BC` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS. |
| `NFI_ICMS_VALOR` | NUMERIC(15,2) | Sim | Valor do ICMS. |
| `NFI_ICMS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do ICMS. |
| `NFI_ICMS_CRED_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do crédito de ICMS. |
| `NFI_ICMS_CRED_VALOR` | NUMERIC(15,2) | Sim | Valor do crédito de ICMS. |
| `NFI_ICMS_ST_BC` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS ST. |
| `NFI_ICMS_ST_VALOR` | NUMERIC(15,2) | Sim | Valor do ICMS ST. |
| `NFI_ICMS_ST_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do ICMS ST. |
| `NFI_IPI_CST` | VARCHAR(2) | Sim | CST do IPI. |
| `NFI_IPI_VALOR` | NUMERIC(15,2) | Sim | Valor do IPI. |
| `NFI_IPI_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do IPI. |
| `NFI_PIS_CST` | VARCHAR(2) | Sim | CST do PIS. |
| `NFI_PIS_BC` | NUMERIC(15,2) | Sim | Base de cálculo do PIS. |
| `NFI_PIS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do PIS. |
| `NFI_PIS_VALOR` | NUMERIC(15,2) | Sim | Valor do PIS. |
| `NFI_CONFINS_CST` | VARCHAR(2) | Sim | CST do COFINS. |
| `NFI_CONFINS_BC` | NUMERIC(15,2) | Sim | Base de cálculo do COFINS. |
| `NFI_CONFINS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do COFINS. |
| `NFI_CONFINS_VALOR` | NUMERIC(15,2) | Sim | Valor do COFINS. |
| `NFI_QTDE_ESTOQUE` | NUMERIC(15,6) | Sim | Quantidade a movimentar no estoque. |
| `NFI_FATOR_CONVERSAO` | VARCHAR(1) | Sim | Fator de conversão (M=Multiplicar, D=Dividir). |
| `NFI_QTDE_CONVERSAO` | NUMERIC(15,4) | Sim | Quantidade do fator de conversão. |
| `NFI_VALOR_FRETE` | NUMERIC(15,2) | Sim | Valor do frete rateado no item. |
| `NFI_VALOR_SEGURO` | NUMERIC(15,2) | Sim | Valor do seguro rateado no item. |
| `NFI_ICMS_MVA` | NUMERIC(15,2) | Sim | MVA (Margem de Valor Agregado) usado no cálculo de ST. |
| `NFI_CALCULA_IMPOSTO` | VARCHAR(1) | Sim | Calcula imposto sobre o item (S/N). |
| `NFI_PESO_BRUTO` | NUMERIC(15,3) | Sim | Peso bruto do item (kg). |
| `NFI_PESO_LIQUIDO` | NUMERIC(15,3) | Sim | Peso líquido do item (kg). |
| `NFI_METRAGEM_CUBICA` | NUMERIC(15,4) | Sim | Metragem cúbica do item. |
| `NFI_CEST` | VARCHAR(7) | Sim | CEST do produto. |
| `NFI_ICMS_ALIQ_UF_DEST` | NUMERIC(15,2) | Sim | Alíquota de ICMS na UF de destino. |
| `NFI_ICMS_PARTILHA` | NUMERIC(15,2) | Sim | Percentual de partilha para UF destino. |
| `NFI_ICMS_VALOR_DIFAL` | NUMERIC(15,2) | Sim | Valor do DIFAL. |
| `NFI_ICMS_VALOR_UF_DEST` | NUMERIC(15,2) | Sim | Valor do ICMS para UF destino. |
| `NFI_ICMS_VALOR_UF_ORIGEM` | NUMERIC(15,2) | Sim | Valor do ICMS para UF origem. |
| `NFI_FCP_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do FCP. |
| `NFI_FCP_VALOR` | NUMERIC(15,2) | Sim | Valor do FCP. |
| `NFI_ICMS_BC_UF_DEST` | NUMERIC(15,2) | Sim | BC do ICMS na UF destino. |
| `NFI_ICMS_ALIQ_INTER` | NUMERIC(15,2) | Sim | Alíquota de ICMS interestadual. |
| `NFI_FCP_BC` | NUMERIC(15,2) | Sim | BC do FCP. |
| `NFI_FCP_ST_BC` | NUMERIC(15,2) | Sim | BC do FCP ST. |
| `NFI_FCP_ST_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do FCP ST. |
| `NFI_FCP_ST_VALOR` | NUMERIC(15,2) | Sim | Valor do FCP ST. |
| `NFI_FCP_ST_RET_BC` | NUMERIC(15,2) | Sim | BC do FCP ST retido. |
| `NFI_FCP_ST_RET_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do FCP ST retido. |
| `NFI_FCP_ST_RET_VALOR` | NUMERIC(15,2) | Sim | Valor do FCP ST retido. |
| `NFI_PERC_ST` | NUMERIC(15,2) | Sim | Percentual de ICMS ST suportado pelo consumidor (tag pST). |
| `NFI_FCP_BC_UF_DEST` | NUMERIC(15,2) | Sim | BC do FCP na UF destino. |
| `NFI_FCP_ALIQ_UF_DEST` | NUMERIC(15,2) | Sim | Alíquota do FCP na UF destino. |
| `NFI_FCP_VALOR_UF_DEST` | NUMERIC(15,2) | Sim | Valor do FCP na UF destino. |
| `NFI_QTDE_TRIB` | NUMERIC(15,6) | Sim | Quantidade tributável. |
| `NFI_VALOR_UNIT_TRIB` | NUMERIC(15,10) | Sim | Valor unitário tributável. |
| `NFI_UNIDADE_TRIB` | VARCHAR(6) | Sim | Unidade tributável. |
| `NFI_DEV_PERC` | NUMERIC(15,2) | Sim | Percentual de devolução. |
| `NFI_DEV_VALOR_IPI` | NUMERIC(15,2) | Sim | Valor de IPI devolvido. |
| `NFI_INF_ADICIONAIS` | VARCHAR(500) | Sim | Informações adicionais do item. |
| `NFI_PEDIDO_COMPRA` | VARCHAR(15) | Sim | Número do pedido de compra relacionado (controle B2B). |
| `NFI_PEDIDO_COMPRA_ITEM` | INTEGER | Sim | Sequencial do item do pedido de compra. |
| `NFI_CODIGO_FCI` | VARCHAR(50) | Sim | Código FCI (importação). |
| `NFI_CONTEUDO_IMPORTACAO` | NUMERIC(15,2) | Sim | Conteúdo de importação. |
| `NFI_BC_II` | NUMERIC(15,2) | Sim | Base de cálculo do Imposto de Importação. |
| `NFI_ALIQ_II` | NUMERIC(15,2) | Sim | Alíquota do II. |
| `NFI_VALOR_II` | NUMERIC(15,2) | Sim | Valor do II. |
| `NFI_DESP_ADUANEIRAS` | NUMERIC(15,2) | Sim | Despesas aduaneiras. |
| `NFI_VALOR_IOF` | NUMERIC(15,2) | Sim | Valor do IOF. |
| `NFI_FATOR_VOLUME` | VARCHAR(1) | Sim | Fator de volume (M/D). |
| `NFI_VOLUME` | INTEGER | Sim | Quantidade de volumes do item. |
| `NFI_VOLUME_ITEM` | INTEGER | Sim | Quantidade de itens por volume. |
| `NFI_ICMS_SUBSTITUO` | NUMERIC(15,2) | Sim | Valor de ICMS substituído. |
| `NFI_ICMS_ST_BC_RET` | NUMERIC(15,2) | Sim | BC do ICMS ST retido. |
| `NFI_ICMS_ST_VALOR_RET` | NUMERIC(15,2) | Sim | Valor do ICMS ST retido. |
| `NFI_ICMS_EFET_BC` | NUMERIC(15,2) | Sim | BC do ICMS efetivo. |
| `NFI_ICMS_EFET_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do ICMS efetivo. |
| `NFI_ICMS_EFET_VALOR` | NUMERIC(15,2) | Sim | Valor do ICMS efetivo. |
| `NFI_ICMS_EFET_RED_BC` | NUMERIC(15,2) | Sim | Redução de BC do ICMS efetivo. |
| `NFI_IPI_ENQ` | VARCHAR(3) | Sim | Enquadramento do IPI. |
| `NFI_MOT_DESON` | INTEGER | Sim | Motivo da desoneração do ICMS (0..11, 90). |
| `NFI_ICMS_DESON_VALOR` | NUMERIC(15,2) | Sim | Valor do ICMS desonerado. |
| `NFI_COD_BENEF` | VARCHAR(10) | Sim | Código de benefício fiscal. |
| `NFI_ICMS_MOD_BC` | INTEGER | Sim | Modalidade de BC do ICMS (0..3). |
| `NFI_ICMS_BC_FIXO` | NUMERIC(15,2) | Sim | BC fixa do ICMS (vinda do produto/grupo). |
| `NFI_ICMS_ST_BC_FIXO` | NUMERIC(15,2) | Sim | BC fixa do ICMS ST (MVA ou Pauta). |
| `NFI_ICMS_ST_MOD_BC` | INTEGER | Sim | Modalidade de BC do ICMS ST (0..5). |
| `NFI_ICMS_DIF_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do DIFAL. |
| `NFI_ICMS_VALOR_OP` | NUMERIC(15,2) | Sim | Valor como se não tivesse diferimento. |
| `NFI_ICMS_DIF_VALOR` | NUMERIC(15,2) | Sim | Valor do diferimento. |
| `NFI_QTDE_TRIB_UN` | NUMERIC(15,6) | Sim | Quantidade tributável por unidade. |
| `NFI_PEDIDO_VENDA` | INTEGER | Sim | FK para TB_PEDIDO_VENDA.PEV_ID. |
| `NFI_PEDIDO_ITEM` | INTEGER | Sim | Sequencial do item do pedido de venda. |
| `NFI_STATUS_PROD` | VARCHAR(1) | Sim | Status: P=Pendente, I=Informado, S=Sugerido, V=Vendido, C=Produto Contábil. |
| `NFI_IPI_BC` | NUMERIC(15,2) | Sim | BC do IPI. |
| `NFI_TX_SISCOMEX` | NUMERIC(15,2) | Sim | Taxa SISCOMEX. |
| `NFI_ICMS_ALIQ_ORIG` | NUMERIC(15,2) | Sim | Alíquota original do ICMS. |
| `NFI_FCP_ALIQ_ORIG` | NUMERIC(15,2) | Sim | Alíquota original do FCP. |
| `NFI_ST_ALIQ_ORIG` | NUMERIC(15,2) | Sim | Alíquota original do ICMS ST. |
| `NFI_FCP_ST_ALIQ_ORIG` | NUMERIC(15,2) | Sim | Alíquota original do FCP ST. |
| `NFI_MVA_ORIG` | NUMERIC(15,2) | Sim | MVA original. |
| `NFI_CST_ORIG` | VARCHAR(2) | Sim | CST original. |
| `NFI_CSOSN_ORIG` | VARCHAR(3) | Sim | CSOSN original. |
| `NFI_ICMS_BC_ORGI` | NUMERIC(15,2) | Sim | BC original do ICMS. |
| `NFI_ICMS_VALOR_ORIG` | NUMERIC(15,2) | Sim | Valor original do ICMS. |
| `NFI_FCP_BC_ORIG` | NUMERIC(15,2) | Sim | BC original do FCP. |
| `NFI_FCP_VALOR_ORIG` | NUMERIC(15,2) | Sim | Valor original do FCP. |
| `NFI_ST_BC_ORIG` | NUMERIC(15,2) | Sim | BC original do ICMS ST. |
| `NFI_ST_VALOR_ORIG` | NUMERIC(15,2) | Sim | Valor original do ICMS ST. |
| `NFI_FCP_ST_BC_ORIG` | NUMERIC(15,2) | Sim | BC original do FCP ST. |
| `NFI_FCP_ST_VALOR_ORIG` | NUMERIC(15,2) | Sim | Valor original do FCP ST. |
| `NFI_IPI_BC_ORIG` | NUMERIC(15,2) | Sim | BC original do IPI. |
| `NFI_IPI_VALOR_ORIG` | NUMERIC(15,2) | Sim | Valor original do IPI. |
| `NFI_IPI_ALIQ_ORIG` | NUMERIC(15,2) | Sim | Alíquota original do IPI. |
| `NFI_PIS_BC_ORIG` | NUMERIC(15,2) | Sim | BC original do PIS. |
| `NFI_PIS_ALIQ_ORIG` | NUMERIC(15,2) | Sim | Alíquota original do PIS. |
| `NFI_PIS_VALOR_ORIG` | NUMERIC(15,2) | Sim | Valor original do PIS. |
| `NFI_COFINS_BC_ORIG` | NUMERIC(15,2) | Sim | BC original do COFINS. |
| `NFI_COFINS_ALIQ_ORIG` | NUMERIC(15,2) | Sim | Alíquota original do COFINS. |
| `NFI_COFINS_VALOR_ORIG` | NUMERIC(15,2) | Sim | Valor original do COFINS. |
| `NFI_SEGURO_ORIG` | NUMERIC(15,2) | Sim | Valor original do seguro. |
| `NFI_FRETE_ORIG` | NUMERIC(15,2) | Sim | Valor original do frete. |
| `NFI_ICMS_DESON_ORIG` | NUMERIC(15,2) | Sim | Valor original do ICMS desonerado. |
| `NFI_ICMS_RED_BC` | NUMERIC(15,4) | Sim | Redução de BC do ICMS. |
| `NFI_ICMS_ST_RED_BC` | NUMERIC(15,4) | Sim | Redução de BC do ICMS ST. |
| `NFI_ICMS_RED_ORIG` | NUMERIC(15,4) | Sim | Redução original de BC. |
| `NFI_ST_RED_ORIG` | NUMERIC(15,4) | Sim | Redução original de BC ST. |
| `NFI_ISS_BC` | NUMERIC(15,2) | Sim | BC do ISS (serviços). |
| `NFI_ISS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do ISS. |
| `NFI_ISS_RETIDO` | VARCHAR(1) | Sim | ISS retido (S/N). |
| `NFI_ISS_VALOR` | NUMERIC(15,2) | Sim | Valor do ISS. |
| `NFI_ISS_VALOR_RETENCAO` | NUMERIC(15,2) | Sim | Valor retido do ISS. |
| `NFI_ISS_VALOR_DEDUCAO` | NUMERIC(15,2) | Sim | Valor de dedução do ISS. |
| `NFI_ISS_VALOR_OUTRAS_RET` | NUMERIC(15,2) | Sim | Valor de outras retenções (ISS). |
| `NFI_ISS_VALOR_DESC_INCOND` | NUMERIC(15,2) | Sim | Desconto incondicional sobre ISS. |
| `NFI_ISS_VALOR_DESC_CONDIC` | NUMERIC(15,2) | Sim | Desconto condicional sobre ISS. |
| `NFI_ISS_COD_MUNICIPIO` | VARCHAR(10) | Sim | Código do município de incidência do ISS. |
| `NFI_ISS_COD_SERV_NACIONAL` | VARCHAR(10) | Sim | Código do serviço nacional (LC116). |
| `NFI_ISS_COD_SERV_MUNICIPAL` | VARCHAR(20) | Sim | Código do serviço municipal. |
| `NFI_ISS_COD_MUN_FG` | VARCHAR(10) | Sim | Código do município de FG (ISS). |
| `NFI_ISS_COD_PAIS` | INTEGER | Sim | Código do país (ISS). |
| `NFI_ISS_IND_EXIGIBILIDADE` | VARCHAR(1) | Sim | Indicador de exigibilidade do ISS. |
| `NFI_ISS_NR_PROCESSO` | VARCHAR(30) | Sim | Número do processo (suspensão ISS). |
| `NFI_ISS_IND_INCENTIVO` | VARCHAR(1) | Sim | Indicador de incentivo cultural (S/N). |
| `NFI_CIDADE_INCIDENCIA` | INTEGER | Sim | FK para TB_CIDADE — cidade de incidência do ISS. |
| `NFI_CIDADE_FG` | INTEGER | Sim | FK para TB_CIDADE — cidade de FG. |
| `NFI_OS` | INTEGER | Sim | FK para ordem de serviço. |
| `NFI_OS_ITEM` | INTEGER | Sim | Item da OS. |
| `NFI_ISS_COD_SIT_TRIB` | VARCHAR(1) | Sim | Código da situação tributária do ISS. |
| `NFI_ICMS_ALIQ_NORMAL` | NUMERIC(15,2) | Sim | Alíquota normal (não simples) do ICMS. |
| `NFI_OP` | INTEGER | Sim | FK para TB_ORDEM_PRODUCAO.OP_ID. |
| `NFI_OP_ITEM` | INTEGER | Sim | Item da OP. |
| `NFI_ICMS_BC_MONO` | NUMERIC(15,4) | Sim | BC do ICMS monofásico. |
| `NFI_ICMS_ALIQ_MONO` | NUMERIC(15,4) | Sim | Alíquota do ICMS monofásico. |
| `NFI_ICMS_VALOR_MONO` | NUMERIC(15,4) | Sim | Valor do ICMS monofásico. |
| `NFI_ICMS_BC_MONO_RETEN` | NUMERIC(15,4) | Sim | BC do ICMS monofásico retido. |
| `NFI_ICMS_ALIQ_MONO_RETEN` | NUMERIC(15,4) | Sim | Alíquota do ICMS monofásico retido. |
| `NFI_ICMS_VALOR_MONO_RETEN` | NUMERIC(15,4) | Sim | Valor do ICMS monofásico retido. |
| `NFI_ICMS_RED_MONO` | NUMERIC(15,4) | Sim | Redução de BC do ICMS monofásico. |
| `NFI_MOT_RED_MONO` | VARCHAR(1) | Sim | Motivo da redução do ICMS monofásico. |
| `NFI_ICMS_VALOR_MONO_OP` | NUMERIC(15,4) | Sim | Valor do ICMS monofásico na operação. |
| `NFI_ICMS_DIF_MONO` | NUMERIC(15,4) | Sim | Diferimento do ICMS monofásico. |
| `NFI_ICMS_VALOR_DIF_MONO` | NUMERIC(15,4) | Sim | Valor do diferimento do ICMS monofásico. |
| `NFI_ICMS_BC_MONO_RET` | NUMERIC(15,4) | Sim | BC do ICMS monofásico por retenção. |
| `NFI_ICMS_ALIQ_MONO_RET` | NUMERIC(15,4) | Sim | Alíquota do ICMS monofásico por retenção. |
| `NFI_ICMS_VALOR_MONO_RET` | NUMERIC(15,4) | Sim | Valor do ICMS monofásico por retenção. |
| `NFI_VALOR_DESC_RETIDO` | NUMERIC(15,4) | Sim | Valor do desconto retido. |
| `NFI_COD_SABORES` | VARCHAR(20) | Sim | Código dos sabores (pizzas etc.). |
| `NFI_CFOP_XML` | VARCHAR(4) | Sim | CFOP original do XML importado. |
| `NFI_VARIACAO` | INTEGER | Sim | Variação do produto (grade). |
| `NFI_DESCONTO_ORIG` | NUMERIC(15,4) | Sim | Desconto original. |
| `NFI_DEV_TOTAL` | NUMERIC(15,4) | Sim | Devolução total. |
| `NFI_OUTRAS_DESP_ORIG` | NUMERIC(15,4) | Sim | Outras despesas originais. |
| `NFI_COD_CRED_PRESUMIDO` | VARCHAR(10) | Sim | Código do crédito presumido. |
| `NFI_CRED_PRESUMIDO_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do crédito presumido. |
| `NFI_CRED_PRESUMIDO_VALOR` | NUMERIC(15,2) | Sim | Valor do crédito presumido. |
| `NFI_TABELA_PRECO` | INTEGER | Sim | FK para TB_TABELA_PRECO.TBP_ID usada. |
| `NFI_TABELA_PRECO_DESC_ACRE` | NUMERIC(15,2) | Sim | Desconto/Acréscimo da tabela de preço. |
| `NFI_TIPO_TABELA_PRECO` | VARCHAR(1) | Sim | Tipo da tabela (D=Desconto, A=Acréscimo). |
| `NFI_LOCAL_ESTOQUE` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE.LOC_ID. |

COMMENT ON COLUMN TB_NOTA_FISCAL_ITEM.NFI_TIPO_PRODUTO IS 'NFI_PRODUTO_ESPECIFICO
S - SIMPLES
V - VEICULO';
COMMENT ON COLUMN TB_NOTA_FISCAL_ITEM.NFI_ICMS_PARTILHA IS 'Porcentagem que vai ficar com UF Destino';
COMMENT ON COLUMN TB_NOTA_FISCAL_ITEM.NFI_PERC_ST IS 'pST - tag pST para informar o percentual do ICMS-ST suportado pelo consumidor nas operações com ICMS retido por ST (CST=60 e CSOSN=500).';
COMMENT ON COLUMN TB_NOTA_FISCAL_ITEM.NFI_PEDIDO_COMPRA IS 'Informação de interesse do emissor para controle do B2B.';
COMMENT ON COLUMN TB_NOTA_FISCAL_ITEM.NFI_PEDIDO_COMPRA_ITEM IS 'Informação de interesse do emissor para controle do B2B.';
COMMENT ON COLUMN TB_NOTA_FISCAL_ITEM.NFI_ICMS_BC_FIXO IS 'Base de cálculo vinda do produto/grupo de tributação quando a modalidade não for 3 (Valor Operação).';
COMMENT ON COLUMN TB_NOTA_FISCAL_ITEM.NFI_ICMS_ST_BC_FIXO IS 'Base de cálculo ST vinda do produto/grupo (pode ser MVA ou Pauta).';
COMMENT ON COLUMN TB_NOTA_FISCAL_ITEM.NFI_ICMS_VALOR_OP IS 'Valor como se não tivesse o diferimento';
COMMENT ON COLUMN TB_NOTA_FISCAL_ITEM.NFI_STATUS_PROD IS 'P - PENDENTE
I - INFORMADO
S - SUGERIDO
V - VENDIDO
C - PRODUTO CONTABIL';
COMMENT ON COLUMN TB_NOTA_FISCAL_ITEM.NFI_NOTA_FISCAL IS 'FK para TB_NOTA_FISCAL.NF_ID — use SEMPRE JOIN com TB_NOTA_FISCAL';
COMMENT ON COLUMN TB_NOTA_FISCAL_ITEM.NFI_PRODUTO IS 'FK para TB_PRODUTO.PRD_ID — use JOIN com TB_PRODUTO por PRD_ID';

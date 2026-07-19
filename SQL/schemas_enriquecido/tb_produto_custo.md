# Tabela TB_PRODUTO_CUSTO

**Módulo:** Estoque / Compras
Histórico de movimentação de custo de um produto. Armazena preços de custo e venda, fornecedor, origem do movimento (compra, inventário, etc.), lucro aplicado, ICMS ST, despesas, fórmulas de cálculo de custo/venda e sugestões de preço para reajuste.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRDC_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PRDC_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID. Parte da chave primária composta. |
| `PRDC_SEQUENCIA` | INTEGER | Não | Sequencial do registro de custo. Parte da chave primária composta. |
| `PRDC_DT_MOVIMENTO` | DATE | Sim | Data do movimento que originou/atualizou o custo. |
| `PRDC_FORNECEDOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (apenas fornecedores) — fornecedor da operação. |
| `PRDC_PRECO_CUSTO` | NUMERIC(15,6) | Sim | Preço de custo do produto no movimento. |
| `PRDC_CUSTO_ADICIONAL` | NUMERIC(15,6) | Sim | Custo adicional (frete, seguro, outras despesas) somado ao custo. |
| `PRDC_LUCRO` | NUMERIC(15,2) | Sim | Percentual de lucro aplicado sobre o custo. |
| `PRDC_PRECO_VENDA` | NUMERIC(15,6) | Sim | Preço de venda calculado. |
| `PRDC_ORIGEM` | VARCHAR(10) | Sim | Sigla do módulo/rotina de origem do movimento de custo (ex.: COMPRA, INVENTARIO). |
| `PRDC_ORIGEM_ID` | INTEGER | Sim | Identificador do documento de origem. |
| `PRDC_ORIGEM_ITEM` | INTEGER | Sim | Item do documento de origem. |
| `PRDC_ALTERAR_PRECO` | VARCHAR(1) | Sim | Indica se o preço de venda deve ser alterado (S/N). |
| `PRDC_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção em listagens (S/N). |
| `PRDC_PRECO_VENDA_NOVO` | NUMERIC(15,6) | Sim | Sugestão de novo preço de venda. |
| `PRDC_PRECO_CUSTO_NOVO` | NUMERIC(15,6) | Sim | Sugestão de novo preço de custo. |
| `PRDC_PRECO_VENDA_SUG` | NUMERIC(15,6) | Sim | Preço de venda sugerido pelo cálculo. |
| `PRDC_LUCRO_NOVO` | NUMERIC(15,2) | Sim | Percentual de lucro sugerido. |
| `PRDC_GONDOLA` | VARCHAR(1) | Sim | Indica se o item está em gôndola (S/N). |
| `PRDC_PRECO_CUSTO_LIQ` | NUMERIC(15,6) | Sim | Preço de custo líquido (após descontos). |
| `PRDC_PRECO_CUSTO_COMPRA` | NUMERIC(15,6) | Sim | Preço de custo de compra. |
| `PRDC_UN_COMPRA` | VARCHAR(6) | Sim | Unidade de compra do produto. |
| `PRDC_CUSTO_UN` | NUMERIC(15,6) | Sim | Custo unitário do produto. |
| `PRDC_VALOR_ST` | NUMERIC(15,2) | Sim | Valor de ICMS-ST aplicado ao custo. |
| `PRDC_BC_ST` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS-ST. |
| `PRDC_BC_FCP_ST` | NUMERIC(15,2) | Sim | Base de cálculo do FCP-ST. |
| `PRDC_VALOR_FCP_ST` | NUMERIC(15,2) | Sim | Valor do FCP-ST. |
| `PRDC_BASE_CUSTO` | VARCHAR(1) | Sim | Tipo de base utilizada no cálculo do custo. |
| `PRDC_TIPO_DESC_CUSTO` | VARCHAR(1) | Sim | Tipo do desconto aplicado no custo (P=Percentual, V=Valor). |
| `PRDC_DESCONTO_CUSTO` | NUMERIC(15,6) | Sim | Desconto aplicado ao custo. |
| `PRDC_TIPO_DESP_CUSTO` | VARCHAR(1) | Sim | Tipo das despesas aplicadas no custo (P=Percentual, V=Valor). |
| `PRDC_DESPESAS_CUSTO` | NUMERIC(15,6) | Sim | Despesas aplicadas ao custo. |
| `PRDC_TIPO_ST_CUSTO` | VARCHAR(1) | Sim | Tipo do ICMS-ST aplicado no custo (P=Percentual, V=Valor). |
| `PRDC_ICMS_ST_CUSTO` | NUMERIC(15,6) | Sim | ICMS-ST aplicado no custo. |
| `PRDC_TIPO_IPI_CUSTO` | VARCHAR(1) | Sim | Tipo do IPI aplicado no custo (P=Percentual, V=Valor). |
| `PRDC_IPI_CUSTO` | NUMERIC(15,6) | Sim | IPI aplicado no custo. |
| `PRDC_TIPO_FCP_CUSTO` | VARCHAR(1) | Sim | Tipo do FCP-ST aplicado no custo (P=Percentual, V=Valor). |
| `PRDC_FCP_ST_CUSTO` | NUMERIC(15,6) | Sim | FCP-ST aplicado no custo. |
| `PRDC_BASE_PRECO` | VARCHAR(1) | Sim | Tipo de base utilizada no cálculo do preço de venda. |
| `PRDC_DESCONTO_PRECO` | NUMERIC(15,6) | Sim | Desconto aplicado no preço de venda. |
| `PRDC_IMPOSTOS_PRECO` | NUMERIC(15,6) | Sim | Impostos aplicados no preço de venda. |
| `PRDC_DESPESAS_PRECO` | NUMERIC(15,6) | Sim | Despesas aplicadas no preço de venda. |
| `PRDC_COMISSAO_VENDA` | NUMERIC(15,6) | Sim | Comissão de venda aplicada no preço. |
| `PRDC_LUCRO_DESEJADO` | NUMERIC(15,6) | Sim | Lucro desejado aplicado no cálculo do preço. |
| `PRDC_TIPO_CALCULO` | VARCHAR(1) | Sim | Tipo de cálculo utilizado (C=Custo, V=Venda). |
| `PRDC_TIPO_IMPOSTO_CUSTO` | VARCHAR(1) | Sim | Tipo do imposto aplicado no custo (P=Percentual, V=Valor). |
| `PRDC_IMPOSTO_CUSTO` | NUMERIC(15,6) | Sim | Imposto aplicado no custo. |
| `PRDC_ICMS_VENDA` | NUMERIC(15,6) | Sim | ICMS de venda aplicado no cálculo. |
| `PRDC_CASAS_DECIMAIS` | INTEGER | Sim | Casas decimais usadas no cálculo. |
| `PRDC_BASE_CUSTO_VALOR` | NUMERIC(15,6) | Sim | Valor da base de custo. |
| `PRDC_DESC_CUSTO_VALOR` | NUMERIC(15,6) | Sim | Valor de desconto de custo. |
| `PRDC_DESP_CUSTO_VALOR` | NUMERIC(15,6) | Sim | Valor de despesas de custo. |
| `PRDC_ICMS_ST_CUSTO_VALOR` | NUMERIC(15,6) | Sim | Valor do ICMS-ST de custo. |
| `PRDC_IPI_CUSTO_VALOR` | NUMERIC(15,6) | Sim | Valor do IPI de custo. |
| `PRDC_FCP_ST_CUSTO_VALOR` | NUMERIC(15,6) | Sim | Valor do FCP-ST de custo. |
| `PRDC_DESC_PRECO_VALOR` | NUMERIC(15,6) | Sim | Valor de desconto aplicado no preço. |
| `PRDC_IMPOSTO_PRECO_VALOR` | NUMERIC(15,6) | Sim | Valor de imposto aplicado no preço. |
| `PRDC_DESP_PRECO_VALOR` | NUMERIC(15,6) | Sim | Valor de despesas aplicadas no preço. |
| `PRDC_COMISSAO_VENDA_VALOR` | NUMERIC(15,6) | Sim | Valor da comissão de venda. |
| `PRDC_LUCRO_VALOR` | NUMERIC(15,6) | Sim | Valor de lucro desejado. |
| `PRDC_IMPOSTO_CUSTO_VALOR` | NUMERIC(15,6) | Sim | Valor do imposto de custo. |
| `PRDC_ICMS_VENDA_VALOR` | NUMERIC(15,6) | Sim | Valor do ICMS de venda. |
| `PRDC_MOEDA` | INTEGER | Sim | FK para TB_ESPECIE_MOEDA.ESP_ID — moeda do custo. |
| `PRDC_VARIACAO` | INTEGER | Sim | FK para TB_PRODUTO_VARIACAO.PRV_ID — variação do produto. |
| `PRDC_ICMS_COMPRA` | NUMERIC(15,6) | Sim | Percentual de ICMS na compra. |
| `PRDC_ICMS_COMPRA_VALOR` | NUMERIC(15,6) | Sim | Valor do ICMS na compra. |
| `PRDC_PIS_COMPRA` | NUMERIC(15,6) | Sim | Percentual de PIS na compra. |
| `PRDC_PIS_COMPRA_VALOR` | NUMERIC(15,6) | Sim | Valor do PIS na compra. |
| `PRDC_PIS_VENDA` | NUMERIC(15,6) | Sim | Percentual de PIS na venda. |
| `PRDC_PIS_VENDA_VALOR` | NUMERIC(15,6) | Sim | Valor do PIS na venda. |
| `PRDC_COFINS_COMPRA` | NUMERIC(15,6) | Sim | Percentual de COFINS na compra. |
| `PRDC_COFINS_COMPRA_VALOR` | NUMERIC(15,6) | Sim | Valor da COFINS na compra. |
| `PRDC_COFINS_VENDA` | NUMERIC(15,6) | Sim | Percentual de COFINS na venda. |
| `PRDC_COFINS_VENDA_VALOR` | NUMERIC(15,6) | Sim | Valor da COFINS na venda. |
| `PRDC_TIPO_ICMS_COMPRA` | VARCHAR(1) | Sim | Tipo do ICMS de compra (P=Percentual, V=Valor). |
| `PRDC_TIPO_PIS_COMPRA` | VARCHAR(1) | Sim | Tipo do PIS de compra (P=Percentual, V=Valor). |
| `PRDC_TIPO_COFINS_COMPRA` | VARCHAR(1) | Sim | Tipo da COFINS de compra (P=Percentual, V=Valor). |
| `PRDC_PRECO_COMPRA` | NUMERIC(15,6) | Sim | Preço de compra do produto. |
| `PRDC_CUSTO_CONTABIL` | NUMERIC(15,6) | Sim | Custo contábil do produto. |
| `PRDC_CUSTO_AQUISICAO` | NUMERIC(15,6) | Sim | Custo de aquisição do produto. |
| `PRDC_TOTAL_IMPOSTOS` | NUMERIC(15,6) | Sim | Total de impostos considerados no custo. |
| `PRDC_BASE_PRECO_VALOR` | NUMERIC(15,6) | Sim | Valor da base de preço. |
| `PRDC_UF_COMPRA` | VARCHAR(2) | Sim | UF de origem da compra. |
| `PRDC_ESTADO_COMPRA` | INTEGER | Sim | FK para TB_ESTADO.EST_ID — estado de origem da compra. |
| `PRDC_ICMS_ALIQ_ENT` | NUMERIC(15,2) | Sim | Alíquota de ICMS de entrada. |
| `PRDC_PIS_ALIQ_ENT` | NUMERIC(15,2) | Sim | Alíquota de PIS de entrada. |
| `PRDC_COFINS_ALIQ_ENT` | NUMERIC(15,2) | Sim | Alíquota de COFINS de entrada. |
| `PRDC_TIPO_ICMS_VENDA` | VARCHAR(1) | Sim | Tipo do ICMS de venda (P=Percentual, V=Valor). |
| `PRDC_TIPO_PIS_VENDA` | VARCHAR(1) | Sim | Tipo do PIS de venda (P=Percentual, V=Valor). |
| `PRDC_TIPO_COFINS_VENDA` | VARCHAR(1) | Sim | Tipo da COFINS de venda (P=Percentual, V=Valor). |
| `PRDC_TIPO_IMPOSTOS_PRECO` | VARCHAR(1) | Sim | Tipo dos impostos aplicados no preço (P=Percentual, V=Valor). |
| `PRDC_TIPO_DESPESAS_PRECO` | VARCHAR(1) | Sim | Tipo das despesas aplicadas no preço (P=Percentual, V=Valor). |
| `PRDC_TIPO_COMISSAO_VENDA` | VARCHAR(1) | Sim | Tipo da comissão de venda (P=Percentual, V=Valor). |
| `PRDC_TIPO_LUCRO_DESEJADO` | VARCHAR(1) | Sim | Tipo do lucro desejado (P=Percentual, V=Valor). |
| `PRDC_DESCRICAO_CUSTO_1` | VARCHAR(50) | Sim | Descrição do componente de custo 1. |
| `PRDC_TIPO_CUSTO_1` | VARCHAR(1) | Sim | Tipo do componente de custo 1 (P=Percentual, V=Valor). |
| `PRDC_VALOR_CUSTO_1` | NUMERIC(15,6) | Sim | Valor do componente de custo 1. |
| `PRDC_TOTAL_CUSTO_1` | NUMERIC(15,6) | Sim | Total calculado do componente de custo 1. |
| `PRDC_DESCRICAO_CUSTO_2` | VARCHAR(50) | Sim | Descrição do componente de custo 2. |
| `PRDC_TIPO_CUSTO_2` | VARCHAR(1) | Sim | Tipo do componente de custo 2 (P=Percentual, V=Valor). |
| `PRDC_VALOR_CUSTO_2` | NUMERIC(15,6) | Sim | Valor do componente de custo 2. |
| `PRDC_TOTAL_CUSTO_2` | NUMERIC(15,6) | Sim | Total calculado do componente de custo 2. |
| `PRDC_DESCRICAO_CUSTO_3` | VARCHAR(50) | Sim | Descrição do componente de custo 3. |
| `PRDC_TIPO_CUSTO_3` | VARCHAR(1) | Sim | Tipo do componente de custo 3 (P=Percentual, V=Valor). |
| `PRDC_VALOR_CUSTO_3` | NUMERIC(15,6) | Sim | Valor do componente de custo 3. |
| `PRDC_TOTAL_CUSTO_3` | NUMERIC(15,6) | Sim | Total calculado do componente de custo 3. |
| `PRDC_DESCRICAO_VENDA_1` | VARCHAR(50) | Sim | Descrição do componente de venda 1. |
| `PRDC_TIPO_VENDA_1` | VARCHAR(1) | Sim | Tipo do componente de venda 1 (P=Percentual, V=Valor). |
| `PRDC_VALOR_VENDA_1` | NUMERIC(15,6) | Sim | Valor do componente de venda 1. |
| `PRDC_TOTAL_VENDA_1` | NUMERIC(15,6) | Sim | Total calculado do componente de venda 1. |
| `PRDC_DESCRICAO_VENDA_2` | VARCHAR(50) | Sim | Descrição do componente de venda 2. |
| `PRDC_TIPO_VENDA_2` | VARCHAR(1) | Sim | Tipo do componente de venda 2 (P=Percentual, V=Valor). |
| `PRDC_VALOR_VENDA_2` | NUMERIC(15,6) | Sim | Valor do componente de venda 2. |
| `PRDC_TOTAL_VENDA_2` | NUMERIC(15,6) | Sim | Total calculado do componente de venda 2. |
| `PRDC_DESCRICAO_VENDA_3` | VARCHAR(50) | Sim | Descrição do componente de venda 3. |
| `PRDC_TIPO_VENDA_3` | VARCHAR(1) | Sim | Tipo do componente de venda 3 (P=Percentual, V=Valor). |
| `PRDC_VALOR_VENDA_3` | NUMERIC(15,6) | Sim | Valor do componente de venda 3. |
| `PRDC_TOTAL_VENDA_3` | NUMERIC(15,6) | Sim | Total calculado do componente de venda 3. |
| `PRDC_FORMULA_CUSTO_1` | INTEGER | Sim | FK para TB_FORMULA — fórmula aplicada no componente de custo 1. |
| `PRDC_FORMULA_CUSTO_2` | INTEGER | Sim | FK para TB_FORMULA — fórmula aplicada no componente de custo 2. |
| `PRDC_FORMULA_CUSTO_3` | INTEGER | Sim | FK para TB_FORMULA — fórmula aplicada no componente de custo 3. |
| `PRDC_FORMULA_VENDA_1` | INTEGER | Sim | FK para TB_FORMULA — fórmula aplicada no componente de venda 1. |
| `PRDC_FORMULA_VENDA_2` | INTEGER | Sim | FK para TB_FORMULA — fórmula aplicada no componente de venda 2. |
| `PRDC_FORMULA_VENDA_3` | INTEGER | Sim | FK para TB_FORMULA — fórmula aplicada no componente de venda 3. |

COMMENT ON COLUMN TB_PRODUTO_CUSTO.PRDC_PRODUTO IS 'FK para TB_PRODUTO.PRD_ID — use JOIN com TB_PRODUTO para obter descrição do produto.';
COMMENT ON COLUMN TB_PRODUTO_CUSTO.PRDC_FORNECEDOR IS 'FK para TB_PESSOA.PES_ID — use JOIN com TB_PESSOA para obter nome do fornecedor.';

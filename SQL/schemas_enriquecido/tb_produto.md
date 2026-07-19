# Tabela TB_PRODUTO

**Módulo:** Cadastros
Catálogo de produtos do ERP: descrição, preços (custo e venda), unidades, tipo de produto (Revenda, Restaurante, Matéria Prima, Variação, Uso ou Consumo, Serviço, Veículo, Arma, Kit), estoque, promoções, dados fiscais (NCM), variações, atributos para e-commerce (iFood, Mercado Livre, Tray, WooCommerce) e dados específicos para restaurante (pizza, sabores, cashback, complemento).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRD_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `PRD_ID` | INTEGER | Não | Identificador único do produto. |
| `PRD_STATUS` | VARCHAR(1) | Sim | Status do produto: 'A' = Ativo, 'I' = Inativo. |
| `PRD_DESCRICAO` | VARCHAR(100) | Sim | Descrição do produto. |
| `PRD_GRUPO` | INTEGER | Sim | Identificador do grupo do produto. |
| `PRD_SUBGRUPO` | INTEGER | Sim | Identificador do subgrupo do produto. |
| `PRD_MARCA` | INTEGER | Sim | Identificador da marca do produto. |
| `PRD_UN_COMPRA` | VARCHAR(6) | Sim | Unidade de compra (UN, PCT, CX, KG, PC, GR, M, M2, M3, LT, DUZ, SAC, HR, CEN, MIM, MT, TON, CNJ, KIT, MIL, JOG, GAL, RSM, FRD, BLO). |
| `PRD_PRECO_CUSTO` | NUMERIC(15,6) | Sim | Preço de custo do produto. |
| `PRD_UN_VENDA` | VARCHAR(6) | Sim | Unidade de venda (mesma lista de códigos de PRD_UN_COMPRA). |
| `PRD_LUCRO` | NUMERIC(15,2) | Sim | Percentual de lucro aplicado sobre o preço de custo. |
| `PRD_PRECO_VENDA` | NUMERIC(15,6) | Sim | Preço de venda do produto. |
| `PRD_FOTO` | VARCHAR(500) | Sim | Caminho/URL da foto principal do produto. |
| `PRD_NCM` | VARCHAR(10) | Sim | Código NCM do produto (fiscal). |
| `PRD_LIGACAO` | INTEGER | Sim | Identificador de produto ligado/equivalente. |
| `PRD_PESO_LIQUIDO` | NUMERIC(15,3) | Sim | Peso líquido do produto (em kg). |
| `PRD_PESO_BRUTO` | NUMERIC(15,3) | Sim | Peso bruto do produto (em kg). |
| `PRD_CONTROLA_ESTOQUE` | VARCHAR(1) | Sim | Indica se controla estoque (S/N). |
| `PRD_ESTOQUE_MINIMO` | INTEGER | Sim | Estoque mínimo permitido. |
| `PRD_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo do produto: N = Normal, V = Veículo, S = Serviços, G = Grade, U = Uso Consumo, M = Matéria Prima, E = Embalagem, R = Produto em Processo, B = Balanca, P = Produto Acabado. |
| `PRD_LOCAL` | VARCHAR(30) | Sim | Local padrão de armazenagem do produto. |
| `PRD_COMISSAO_PERC` | NUMERIC(15,2) | Sim | Percentual de comissão sobre o produto. |
| `PRD_CALCULA_COMISSAO` | VARCHAR(1) | Sim | Indica se calcula comissão (S/N). |
| `PRD_EDITADO` | VARCHAR(1) | Sim | Indica se o produto foi editado e precisa ser atualizado no PDV (S = Sim, N = Não). |
| `PRD_APLICA_DESCONTO` | VARCHAR(10) | Sim | Indica se aplica desconto (S = Sim, N = Não). |
| `PRD_COD_FILIAL` | VARCHAR(20) | Sim | Código do produto na filial (Minas Rio). |
| `PRD_COD_BARRAS_CAIXA` | VARCHAR(20) | Sim | Código de barras da caixa. |
| `PRD_COD_ATACADO` | VARCHAR(20) | Sim | Código do produto na matriz (Minas Rio). |
| `PRD_EXPORTAR` | VARCHAR(1) | Sim | Indica se o produto pode ser exportado para tablet (S = Sim, N = Não). |
| `PRD_ESTOQUE_MINIMO_NF` | NUMERIC(15,2) | Sim | Estoque mínimo do produto no sistema 'S'. |
| `PRD_DT_CADASTRO` | DATE | Sim | Data de cadastro do produto. |
| `PRD_REFERENCIA` | VARCHAR(20) | Sim | Referência/código auxiliar do produto. |
| `PRD_DT_ULTIMO_LANCAMENTO` | DATE | Sim | Data do último lançamento (entrada/saída) do produto. |
| `PRD_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações do produto em formato binário. NUNCA selecione em queries SELECT. |
| `PRD_METRAGEM_CUBICA` | NUMERIC(15,4) | Sim | Metragem cúbica do produto. |
| `PRD_DT_INI_PROM` | DATE | Sim | Data de início da promoção. |
| `PRD_DT_FIM_PROM` | DATE | Sim | Data de fim da promoção. |
| `PRD_VALOR_PROM` | NUMERIC(15,6) | Sim | Valor promocional do produto. |
| `PRD_BALANCA_TECLA` | INTEGER | Sim | Tecla da balança associada ao produto. |
| `PRD_BALANCA_VALIDADE` | INTEGER | Sim | Validade (em dias) enviada à balança. |
| `PRD_BALANCA_TIPO` | INTEGER | Sim | Tipo de informação da balança: 0 = Peso, 1 = Unidade, 2 = EAN. |
| `PRD_BALANCA_CODIGO` | INTEGER | Sim | Código do produto enviado para a balança. |
| `PRD_PRECO_CUSTO_LIQ` | NUMERIC(15,6) | Sim | Preço de custo líquido (após deduções). |
| `PRD_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção do produto (S/N). |
| `PRD_CODIGO` | VARCHAR(20) | Sim | Código interno do produto. |
| `PRD_FRACIONADO` | VARCHAR(1) | Sim | Indica se o produto é vendido fracionado (S/N). |
| `PRD_FATOR_VOLUME` | VARCHAR(1) | Sim | Fator de volume do produto. |
| `PRD_VOLUME` | INTEGER | Sim | Quantidade de volumes por unidade. |
| `PRD_IMAGEM` | BLOB SUB_TYPE BINARY | Sim | Imagem do produto em formato binário. NUNCA selecione em queries SELECT. |
| `PRD_GERENCIAL` | VARCHAR(1) | Sim | Produto gerencial — não valida informações fiscais e não pode ser inserido em documentos fiscais (S/N). |
| `PRD_INFORMAR_TOTAL` | VARCHAR(1) | Sim | Indica se o vendedor informa o valor total no item (S/N). |
| `PRD_SISTEMA` | VARCHAR(1) | Sim | Indica se é produto de uso interno do sistema (S/N). |
| `PRD_SETOR` | INTEGER | Sim | Identificador do setor de produção/expedição. |
| `PRD_IMPRIMIR_RESTAURANTE` | VARCHAR(1) | Sim | Como imprimir no restaurante: N = Não, S = Setor, P = Produto. |
| `PRD_STATUS_RESTAURANTE` | VARCHAR(1) | Sim | Status do produto no restaurante. |
| `PRD_INCLUSAO_MASSA` | VARCHAR(1) | Sim | Indica se o produto foi incluído em massa (S/N). |
| `PRD_FORNECEDOR` | INTEGER | Sim | Identificador do fornecedor principal (TB_PESSOA.PES_ID). |
| `PRD_ATUAL_FORN` | VARCHAR(1) | Sim | Indica se atualiza o fornecedor padrão (S/N). |
| `PRD_OBS_RESUMIDA` | VARCHAR(200) | Sim | Observação resumida do produto. |
| `PRD_ALTERAR_PRECO` | VARCHAR(1) | Sim | Permite alterar o preço na venda (S/N). |
| `PRD_CONTROLA_LOTE` | VARCHAR(1) | Sim | Controle de lote: N = Não, E = Entrada, S = Saída, A = Ambos. |
| `PRD_OBRIGAR_VALIDADE_LOTE` | VARCHAR(1) | Sim | Obriga informar validade no lote (S/N). |
| `PRD_VALIDAR_QTDE_LOTE` | VARCHAR(1) | Sim | Valida a quantidade informada no lote (S/N). |
| `PRD_USAR_LIGACAO` | VARCHAR(1) | Sim | Indica se usa o produto de ligação na venda (S/N). |
| `PRD_PRODUTO_NF` | INTEGER | Sim | Produto utilizado na NF (caso seja diferente do produto de venda). |
| `PRD_VASILHAME` | INTEGER | Sim | Identificador do vasilhame associado (garrafas, botijões etc.). |
| `PRD_STATUS_VASILHAME` | VARCHAR(1) | Sim | Status do vasilhame (A=Ativo, I=Inativo). |
| `PRD_MOEDA` | INTEGER | Sim | Identificador da moeda/preço alternativo do produto. |
| `PRD_IFOOD` | VARCHAR(1) | Sim | Indica se o produto é publicado no iFood (S/N). |
| `PRD_WORDPRESS` | VARCHAR(1) | Sim | Indica se o produto é publicado no WooCommerce (S/N). |
| `PRD_PRECO_MINIMO` | NUMERIC(15,6) | Sim | Preço mínimo permitido para venda. |
| `PRD_FAVORITO` | VARCHAR(1) | Sim | Produto favorito no PDV (S/N). |
| `PRD_TIPO_VALIDADE` | VARCHAR(1) | Sim | Tipo da validade informada no lote. |
| `PRD_VALOR_VALIDADE` | INTEGER | Sim | Valor (em dias) da validade padrão. |
| `PRD_FORN_LOTE` | VARCHAR(1) | Sim | Indica se exige fornecedor no lote (S/N). |
| `PRD_INFADPROD` | VARCHAR(500) | Sim | Informações adicionais do produto (NF-e). |
| `PRD_TIPO_VALOR_PROM` | VARCHAR(1) | Sim | Tipo do valor promocional (V=Valor, P=Percentual). |
| `PRD_CASAS_DECIMAIS_PRECO` | INTEGER | Sim | Quantidade de casas decimais do preço. |
| `PRD_ID_IFOOD` | VARCHAR(100) | Sim | Identificador do produto no iFood. |
| `PRD_PRECO_MINIMO_PERC` | NUMERIC(15,2) | Sim | Percentual mínimo permitido sobre o preço de venda. |
| `PRD_CODIGO_FISCAL` | VARCHAR(60) | Sim | Código fiscal atual do produto. |
| `PRD_DT_CODIGO` | DATE | Sim | Data de vigência do código fiscal atual. |
| `PRD_CODIGO_FISCAL_ANT` | VARCHAR(60) | Sim | Código fiscal anterior do produto. |
| `PRD_DT_CODIGO_ANT` | DATE | Sim | Data de vigência do código fiscal anterior. |
| `PRD_VENDER_AREA_VOLUME` | VARCHAR(1) | Sim | Indica se vende por área/volume (S/N). |
| `PRD_QUARENTENA_AO_PRODUZIR` | VARCHAR(1) | Sim | Aplica quarentena ao produzir (S/N). |
| `PRD_QUARENTENA_DIAS` | INTEGER | Sim | Quantidade de dias de quarentena. |
| `PRD_TRAY` | VARCHAR(100) | Sim | Identificador do produto na Tray. |
| `CAMPO_55` | VARCHAR(20) | Sim | Campo legado/reservado. |
| `PRD_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. Default: current_timestamp. |
| `PRD_LARGURA` | NUMERIC(15,6) | Sim | Largura do produto (dimensões). |
| `PRD_ALTURA` | NUMERIC(15,6) | Sim | Altura do produto (dimensões). |
| `PRD_PROFUNDIDADE` | NUMERIC(15,6) | Sim | Profundidade do produto (dimensões). |
| `PRD_PIZZA` | VARCHAR(1) | Sim | Indica se o produto é uma pizza (S/N). |
| `PRD_NR_PEDACOS` | INTEGER | Sim | Número de pedaços em que a pizza é cortada. |
| `PRD_MAX_SABORES` | INTEGER | Sim | Quantidade máxima de sabores da pizza. |
| `PRD_MONTAR_PRECO_SABORES` | VARCHAR(1) | Sim | Monta o preço pelos sabores escolhidos (S/N). |
| `PRD_TIPO_CASHBACK` | VARCHAR(1) | Sim | Tipo de cashback aplicado ao produto. |
| `PRD_VALOR_CASHBACK` | NUMERIC(15,2) | Sim | Valor de cashback do produto. |
| `PRD_SOLICITA_COD_DEV_VASILHAME` | VARCHAR(1) | Sim | Solicita código de devolução do vasilhame (S/N). |
| `PRD_AREA_CAIXA` | NUMERIC(15,6) | Sim | Área da caixa do produto. |
| `PRD_ID_WORDPRESS` | VARCHAR(100) | Sim | Identificador do produto no WooCommerce. |
| `PRD_URL_BBIMG` | VARCHAR(2000) | Sim | URL da imagem no BackBlaze/B2. |
| `PRD_APLICAR_TX_SERVICO` | VARCHAR(1) | Sim | Aplica taxa de serviço na venda do produto (S/N). |
| `PRD_TIPO_VARIACAO` | INTEGER | Sim | Identificador do tipo de variação (TB_TIPO_ATRIBUTO). |
| `PRD_ID_MELI` | VARCHAR(50) | Sim | Identificador do produto no Mercado Livre. |
| `PRD_SKU` | VARCHAR(100) | Sim | SKU do produto (marketplaces). |
| `PRD_ULTIMO_ENVIO_ECOMMERCE` | TIMESTAMP | Sim | Data e hora do último envio ao e-commerce. |
| `PRD_CONTROLE_IMENDES` | INTEGER | Sim | Controle de envio ao Imendes. |
| `PRD_DT_CONSULTA_IMENDES` | DATE | Sim | Data da última consulta ao Imendes. |
| `PRD_HR_CONSULTA_IMENDES` | TIME | Sim | Hora da última consulta ao Imendes. |
| `PRD_STATUS_CONSULTA_IMENDES` | VARCHAR(2000) | Sim | Status/erro retornado pelo Imendes. |
| `PRD_CODIGO_IMENDES` | INTEGER | Sim | Código retornado pelo Imendes. |
| `PRD_IFOOD_SERVES` | VARCHAR(1) | Sim | Indica se o produto serves (servir) no iFood (S/N). |
| `PRD_QTD_MAX_SENHA` | NUMERIC(15,6) | Sim | Quantidade máxima para a senha/fila. |
| `PRD_PRECO_COMPRA` | NUMERIC(15,6) | Sim | Preço de compra atual do produto. |
| `PRD_CUSTO_AQUISICAO` | NUMERIC(15,6) | Sim | Custo de aquisição do produto. |
| `PRD_CUSTO_CONTABIL` | NUMERIC(15,6) | Sim | Custo contábil do produto. |
| `PRD_INF_ADC_C177` | VARCHAR(30) | Sim | Informações adicionais para o campo C177 da NF-e (combustíveis). |

COMMENT ON COLUMN TB_PRODUTO.PRD_STATUS IS 'PRD_STATUS
============
''A'' -> ATIVO
''I'' -> INATIVO';
COMMENT ON COLUMN TB_PRODUTO.PRD_UN_COMPRA IS '      UNIDADE(UN)
PACOTE(PCT)
CAIXA(CX)
KILO(KG)
PEÇA(PC)
GRAMA(GR)
METRO(M)
METRO QUADRADO(M2)
METRO CÚBICO(M3)
LITRO(LT)
DÚZIA(DUZ)
SACO(SAC)
HORA(HR)
CENTÍMETRO(CEN)
MILÍMETRO(MIM)
METROS(MT)
TONELADA(TON)
CONJUNTO(CNJ)
KIT(KIT)
MILHEIRO(MIL)
JOGO(JOG)
GALÃO(GAL)
RESMA(RSM)
FARDO(FRD)
BLOCO(BLO)';
COMMENT ON COLUMN TB_PRODUTO.PRD_UN_VENDA IS 'UNIDADE(UN)
PACOTE(PCT)
CAIXA(CX)
KILO(KG)
PEÇA(PC)
GRAMA(GR)
METRO(M)
METRO QUADRADO(M2)
METRO CÚBICO(M3)
LITRO(LT)
DÚZIA(DUZ)
SACO(SAC)
HORA(HR)
CENTÍMETRO(CEN)
MILÍMETRO(MIM)
METROS(MT)
TONELADA(TON)
CONJUNTO(CNJ)
KIT(KIT)
MILHEIRO(MIL)
JOGO(JOG)
GALÃO(GAL)
RESMA(RSM)
FARDO(FRD)
BLOCO(BLO)';
COMMENT ON COLUMN TB_PRODUTO.PRD_TIPO_PRODUTO IS 'PRD_TIPO_PRODUTO
   N - NORMAL
   V - VEICULO
   S - SERVIÇOS
   G - GRADE
   U - USO CONSUMO
   M - MATERIA PRIMA
   E - EMBALAGEM
   R - PRODUTO EM PROCESSO
   B - BALANCA
   P - PRODUTO ACABADO';
COMMENT ON COLUMN TB_PRODUTO.PRD_EDITADO IS 'S - SIM (Foi editado precisa ser atualizado no PDV)
N - NÃO (Não foi editado depois de ter sido atualizado)';
COMMENT ON COLUMN TB_PRODUTO.PRD_APLICA_DESCONTO IS 'S - SIM
N - NAO';
COMMENT ON COLUMN TB_PRODUTO.PRD_COD_FILIAL IS ' Código Filial Minas Rio';
COMMENT ON COLUMN TB_PRODUTO.PRD_COD_ATACADO IS 'Código Matriz Minas Rio';
COMMENT ON COLUMN TB_PRODUTO.PRD_EXPORTAR IS 'Verificar se produto poderá ser exportado para tablet.
S - SIM
N - NÃO';
COMMENT ON COLUMN TB_PRODUTO.PRD_ESTOQUE_MINIMO_NF IS 'Estoque minimo de produto sistema ''S''';
COMMENT ON COLUMN TB_PRODUTO.PRD_BALANCA_TIPO IS '0 - Peso
1 - Unidade
2 - EAN';
COMMENT ON COLUMN TB_PRODUTO.PRD_BALANCA_CODIGO IS 'Código do produto para enviar para balança';
COMMENT ON COLUMN TB_PRODUTO.PRD_GERENCIAL IS 'Produto Gerencial não vai validar informações fiscais e não vai poder ser inserido em documentos fiscais';
COMMENT ON COLUMN TB_PRODUTO.PRD_IMPRIMIR_RESTAURANTE IS 'N - NÃO
    S - SETOR
    P - PRODUTO';
COMMENT ON COLUMN TB_PRODUTO.PRD_CONTROLA_LOTE IS 'N - Não
  E - Entrada
  S - Saída
  A - Ambos';
COMMENT ON COLUMN TB_PRODUTO.PRD_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_PRODUTO.PRD_IMAGEM IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_PRODUTO.PRD_STATUS IS 'Para filtrar produtos ativos utilize WHERE PRD_STATUS = ''A''';
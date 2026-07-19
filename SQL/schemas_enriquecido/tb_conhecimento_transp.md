# Tabela TB_CONHECIMENTO_TRANSP

**Módulo:** Fiscal / Transporte
Conhecimento de Transporte Eletrônico (CT-e). Documento fiscal emitido para prestação de serviço de transporte de cargas. Contém dados do tomador, remetente, destinatário, veículo, valores, ICMS, impostos retidos e informações do modal.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CTE_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `CTE_ID` | INTEGER | Não | Identificador único do CT-e. Parte da chave primária composta. |
| `CTE_STATUS` | VARCHAR(1) | Sim | Status do CT-e (A=Aberto, F=Fechado, C=Cancelado, T=Em trânsito). |
| `CTE_EMITIR_RECEBER` | VARCHAR(1) | Sim | Operação: E=Emitir, R=Receber. |
| `CTE_MODELO` | VARCHAR(2) | Sim | Modelo do documento (57=CT-e, 67=CT-e OS). |
| `CTE_SERIE` | INTEGER | Sim | Série do CT-e. |
| `CTE_NUMERO` | INTEGER | Sim | Número do CT-e. |
| `CTE_NATUREZA_OPERACAO` | INTEGER | Sim | FK para TB_NATUREZA_OPERACAO. |
| `CTE_DESC_NAT_OP` | VARCHAR(100) | Sim | Descrição da natureza de operação. |
| `CTE_CFOP` | VARCHAR(4) | Sim | CFOP do CT-e. |
| `CTE_DT_EMISSAO` | DATE | Sim | Data de emissão. |
| `CTE_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento. |
| `CTE_DT_EMISSAO_ANUL` | DATE | Sim | Data de emissão do CT-e de anulação. |
| `CTE_DT_HR_VIAGEM` | TIMESTAMP | Sim | Data e hora de início da viagem. |
| `CTE_TIPO` | INTEGER | Sim | Tipo do CT-e (0=Normal, 1=Complemento, 2=Anulação, 3=Substituição). |
| `CTE_MODALIDADE` | INTEGER | Sim | Modalidade (1=Rodoviário, 2=Aéreo, 3=Aquaviário, 4=Ferroviário, 5=Dutoviário). |
| `CTE_REMETENTE` | INTEGER | Sim | FK para TB_PESSOA (remetente). |
| `CTE_DESTINATARIO` | INTEGER | Sim | FK para TB_PESSOA (destinatário). |
| `CTE_EXPEDIDOR` | INTEGER | Sim | FK para TB_PESSOA (expedidor). |
| `CTE_RECEBEDOR` | INTEGER | Sim | FK para TB_PESSOA (recebedor). |
| `CTE_IND_TOMADOR` | INTEGER | Sim | Indicador do tomador (0=Remetente, 1=Expedidor, 2=Recebedor, 3=Destinatário, 4=Outros). |
| `CTE_TOMARDOR` | INTEGER | Sim | FK para TB_PESSOA (tomador do serviço). |
| `CTE_IND_LOTACAO` | INTEGER | Sim | Indicador de lotação. |
| `CTE_TIPO_SERV` | INTEGER | Sim | Tipo de serviço (0=Normal, 1=Redespacho, 2=Redespacho intermediário, 3=Vinculado à multimodal, 4=Reentrega, 5=Devolução, 6=Retorno). |
| `CTE_TIPO_FRETAMENTO` | INTEGER | Sim | Tipo de fretamento (1=Contínuo, 2=Eventual). |
| `CTE_CIDADE_EMIT` | INTEGER | Sim | FK para TB_CIDADE (cidade de emissão). |
| `CTE_COD_MUN_EMIT` | VARCHAR(10) | Sim | Código IBGE do município de emissão. |
| `CTE_DESC_CIDADE_EMIT` | VARCHAR(60) | Sim | Descrição da cidade de emissão. |
| `CTE_UF_EMIT` | VARCHAR(2) | Sim | UF de emissão. |
| `CTE_CIDADE_ORIG` | INTEGER | Sim | FK para TB_CIDADE (origem da prestação). |
| `CTE_COD_MUN_ORIG` | VARCHAR(10) | Sim | Código IBGE do município de origem. |
| `CTE_DESC_CIDADE_ORIG` | VARCHAR(60) | Sim | Descrição da cidade de origem. |
| `CTE_UF_ORIG` | VARCHAR(2) | Sim | UF de origem. |
| `CTE_CIDADE_DEST` | INTEGER | Sim | FK para TB_CIDADE (destino da prestação). |
| `CTE_COD_MUN_DEST` | VARCHAR(10) | Sim | Código IBGE do município de destino. |
| `CTE_DESC_CIDADE_DEST` | VARCHAR(60) | Sim | Descrição da cidade de destino. |
| `CTE_UF_DEST` | VARCHAR(2) | Sim | UF de destino. |
| `CTE_RETIRA` | INTEGER | Sim | Indica se retira (0=Sim, 1=Não). |
| `CTE_DETALHE_RETIRA` | VARCHAR(160) | Sim | Detalhes do retira. |
| `CTE_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações em formato binário. NUNCA selecione em queries SELECT. |
| `CTE_VALOR_CARGA` | NUMERIC(15,2) | Sim | Valor da carga transportada. |
| `CTE_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total do serviço. |
| `CTE_VALOR_RECEBER` | NUMERIC(15,2) | Sim | Valor a receber do tomador. |
| `CTE_VALOR_RECEBIDO` | NUMERIC(15,2) | Sim | Valor efetivamente recebido. |
| `CTE_VALOR_PARCELADO` | NUMERIC(15,2) | Sim | Valor parcelado. |
| `CTE_VALOR_DIFERENCA` | NUMERIC(15,2) | Sim | Diferença de valor (recebido vs. a receber). |
| `CTE_VALOR_RETENCAO` | NUMERIC(15,2) | Sim | Valor de retenção. |
| `CTE_ICMS_CST` | VARCHAR(2) | Sim | CST de ICMS. |
| `CTE_ICMS_BC` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS. |
| `CTE_ICMS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota de ICMS. |
| `CTE_ICMS_VALOR` | NUMERIC(15,2) | Sim | Valor do ICMS. |
| `CTE_ICMS_RED_ALIQ` | NUMERIC(15,2) | Sim | Redução de alíquota de ICMS. |
| `CTE_ICMS_CRED_ALIQ` | NUMERIC(15,2) | Sim | Alíquota de crédito de ICMS. |
| `CTE_ICMS_CRED_VALOR` | NUMERIC(15,2) | Sim | Valor do crédito de ICMS. |
| `CTE_ICMS_BC_DEST` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS na operação interestadual. |
| `CTE_ICMS_ALIQ_DEST` | NUMERIC(15,2) | Sim | Alíquota do ICMS destino. |
| `CTE_ICMS_ALIQ_INTER` | NUMERIC(15,2) | Sim | Alíquota interestadual. |
| `CTE_ICMS_PARTILHA` | NUMERIC(15,2) | Sim | Percentual de partilha do DIFAL. |
| `CTE_ICMS_VALOR_DEST` | NUMERIC(15,2) | Sim | Valor do ICMS destino. |
| `CTE_ICMS_VALOR_ORIGEM` | NUMERIC(15,2) | Sim | Valor do ICMS origem. |
| `CTE_ICMS_VALOR_DIFAL` | NUMERIC(15,2) | Sim | Valor do DIFAL. |
| `CTE_FCP_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do FCP. |
| `CTE_FCP_VALOR` | NUMERIC(15,2) | Sim | Valor do FCP. |
| `CTE_VALOR_PIS` | NUMERIC(15,2) | Sim | Valor do PIS. |
| `CTE_VALOR_COFINS` | NUMERIC(15,2) | Sim | Valor do COFINS. |
| `CTE_VALOR_IR` | NUMERIC(15,2) | Sim | Valor do IR retido. |
| `CTE_VALOR_INSS` | NUMERIC(15,2) | Sim | Valor do INSS retido. |
| `CTE_VALOR_CSLL` | NUMERIC(15,2) | Sim | Valor do CSLL retido. |
| `CTE_ALIQ_PIS` | NUMERIC(15,2) | Sim | Alíquota PIS. |
| `CTE_RETER_PIS` | VARCHAR(1) | Sim | Indica se retém PIS (S/N). |
| `CTE_ALIQ_COFINS` | NUMERIC(15,2) | Sim | Alíquota COFINS. |
| `CTE_RETER_COFINS` | VARCHAR(1) | Sim | Indica se retém COFINS (S/N). |
| `CTE_ALIQ_IR` | NUMERIC(15,2) | Sim | Alíquota IR. |
| `CTE_RETER_IR` | VARCHAR(1) | Sim | Indica se retém IR (S/N). |
| `CTE_ALIQ_INSS` | NUMERIC(15,2) | Sim | Alíquota INSS. |
| `CTE_RETER_INSS` | VARCHAR(1) | Sim | Indica se retém INSS (S/N). |
| `CTE_ALIQ_CSLL` | NUMERIC(15,2) | Sim | Alíquota CSLL. |
| `CTE_RETER_CSLL` | VARCHAR(1) | Sim | Indica se retém CSLL (S/N). |
| `CTE_CALCULAR_MANUAL` | VARCHAR(1) | Sim | Cálculo manual de impostos (S/N). |
| `CTE_RNTRC` | VARCHAR(8) | Sim | RNTRC do transportador. |
| `CTE_VEICULO` | INTEGER | Sim | FK para TB_VEICULO. |
| `CTE_PLACA` | VARCHAR(8) | Sim | Placa do veículo. |
| `CTE_PLACA_UF` | VARCHAR(2) | Sim | UF da placa. |
| `CTE_RENAVAM` | VARCHAR(20) | Sim | RENAVAM do veículo. |
| `CTE_TARA` | NUMERIC(15,2) | Sim | Tara do veículo em Kg. |
| `CTE_CAPACIDADE_KG` | INTEGER | Sim | Capacidade em Kg. |
| `CTE_CAPACIDADE_M3` | INTEGER | Sim | Capacidade em M3. |
| `CTE_TIPO_VEICULO` | INTEGER | Sim | Tipo do veículo (tração). |
| `CTE_TIPO_CARROCERIA` | INTEGER | Sim | Tipo de carroceria. |
| `CTE_PROD_PRED` | VARCHAR(60) | Sim | Produto predominante. |
| `CTE_OUT_CAT` | VARCHAR(30) | Sim | Outras características da carga. |
| `CTE_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção (S/N). |
| `CTE_GERA_FINANCEIRO` | VARCHAR(1) | Sim | Gera financeiro (S/N). |
| `CTE_FORMA_PAGTO` | INTEGER | Sim | FK para TB_FORMA_PAGTO. |
| `CTE_EMAIL_ENVIADO` | VARCHAR(1) | Sim | Indica se e-mail foi enviado (S/N). |
| `CTE_EMAIL_DEST` | VARCHAR(100) | Sim | E-mail do destinatário. |
| `CTE_CARGA` | INTEGER | Sim | FK para TB_CARGA. |
| `CTE_CARGA_ORDEM` | INTEGER | Sim | Ordem do CT-e dentro da carga. |
| `CTE_PROPRIETARIO` | VARCHAR(1) | Sim | Indica se é veículo próprio (T=Tac Agregado, P=Próprio). |
| `CTE_PROP_CNPJ_CPF` | VARCHAR(14) | Sim | CNPJ/CPF do proprietário do veículo. |
| `CTE_PROP_RNTRC` | VARCHAR(8) | Sim | RNTRC do proprietário. |
| `CTE_PROP_NOME` | VARCHAR(60) | Sim | Nome do proprietário. |
| `CTE_PROP_IE` | VARCHAR(14) | Sim | IE do proprietário. |
| `CTE_PROP_UF` | VARCHAR(2) | Sim | UF do proprietário. |
| `CTE_PROP_TIPO` | INTEGER | Sim | Tipo do proprietário (1=TAC, 2=Agregado, 3=Independente). |
| `CTE_SEGURADORA` | INTEGER | Sim | FK para TB_PESSOA (seguradora). |
| `CTE_SEG_NOME` | VARCHAR(100) | Sim | Nome da seguradora. |
| `CTE_SEG_CNPJ` | VARCHAR(14) | Sim | CNPJ da seguradora. |
| `CTE_SEG_APOLICE` | VARCHAR(20) | Sim | Número da apólice. |
| `CTE_SEG_AVERBACAO` | VARCHAR(10) | Sim | Número da averbação. |
| `CTE_SEG_RESP` | INTEGER | Sim | Tipo de responsabilidade do seguro. |
| `CTE_PESO_BRUTO` | NUMERIC(15,2) | Sim | Peso bruto total. |
| `CTE_PESO_LIQUIDO` | NUMERIC(15,2) | Sim | Peso líquido total. |
| `CTE_VOLUMES` | INTEGER | Sim | Quantidade de volumes. |
| `CTE_OS_TAF` | VARCHAR(12) | Sim | TAF do CT-e OS. |
| `CTE_OS_REG_ESTADUAL` | VARCHAR(25) | Sim | Registro Estadual do CT-e OS. |
| `CTE_PROP_TAF` | VARCHAR(12) | Sim | TAF do proprietário. |
| `CTE_PROP_REG_EST` | VARCHAR(25) | Sim | Registro Estadual do proprietário. |
| `CTE_OS_DESC_SERVICO` | VARCHAR(30) | Sim | Descrição do serviço do CT-e OS. |
| `CTE_OS_QTDE` | NUMERIC(15,4) | Sim | Quantidade do CT-e OS. |
| `CTE_CHAVE_ANUL_COMPL` | VARCHAR(44) | Sim | Chave do CT-e de anulação/complemento referenciado. |
| `CTE_SUBST_CHAVE` | VARCHAR(44) | Sim | Chave do CT-e substituído. |
| `CTE_SUBST_CHAVE_ANUL` | VARCHAR(44) | Sim | Chave do CT-e de anulação da substituição. |
| `CTE_SUBST_ALT_TOMADOR` | VARCHAR(1) | Sim | Alteração de tomador na substituição (S/N). |
| `CTE_SUBS_MODELO_DOC_TOMADOR` | VARCHAR(2) | Sim | Modelo do documento do tomador na substituição. |
| `CTE_SUBST_CHAVE_TOMADOR` | VARCHAR(44) | Sim | Chave do documento do tomador na substituição. |
| `CTE_NOTA_FISCAL` | INTEGER | Sim | FK para TB_NOTA_FISCAL vinculada. |
| `CTE_REGRA_APLICADA` | INTEGER | Sim | Regra tributária aplicada (IBS/CBS). |
| `CTE_REGRA_NAT` | INTEGER | Sim | Natureza regra IBS/CBS. |

COMMENT ON COLUMN TB_CONHECIMENTO_TRANSP.CTE_STATUS IS 'A - ABERTO
F - FECHADO
C - CANCELADO
T - EM TRANSITO';
COMMENT ON COLUMN TB_CONHECIMENTO_TRANSP.CTE_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
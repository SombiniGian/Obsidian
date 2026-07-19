# Tabela TB_CLIENTE

**Módulo:** Cadastros
Dados comerciais e fiscais do cliente vinculados a TB_PESSOA.PES_ID. Contém limite de crédito, regime tributário, tabela de preço, regras de desconto, mensalidade e configurações para NFS-e.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CLI_PESSOA` | INTEGER | Não | FK para TB_PESSOA.PES_ID. Parte da chave primária. Use SEMPRE por PES_ID. |
| `CLI_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `CLI_OBSERVACAO` | VARCHAR(2000) | Sim | Observações do cliente. |
| `CLI_DT_CADASTRO` | DATE | Sim | Data de cadastro do cliente. |
| `CLI_STATUS` | VARCHAR(1) | Sim | Status do cliente: A=Ativo, I=Inativo. |
| `CLI_LIMITE_CREDITO` | NUMERIC(15,2) | Sim | Limite de crédito do cliente — não deve ser vazio para venda no PDV. |
| `CLI_FORMA_PGTO` | INTEGER | Sim | FK para TB_FORMA_PAGTO.FPG_ID — forma de pagamento padrão. |
| `CLI_AJUSTE` | NUMERIC(15,2) | Sim | Valor de ajuste no momento do faturamento. |
| `CLI_VENDEDOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (vendedor padrão do cliente). |
| `CLI_AJUSTAR` | VARCHAR(1) | Sim | Permite ajustar valor da venda no faturamento (S/N). |
| `CLI_REGIME` | VARCHAR(2) | Sim | Regime tributário (R=Real, P=Presumido, S=Simples Nacional, N=Normal, M=Micro, C=Consumidor Final, I=Indústria, etc.). |
| `CLI_ALTERAR_FORMA_PAGTO` | VARCHAR(1) | Sim | Permite alterar forma de pagamento padrão (S/N). |
| `CLI_TABELA_PRECO` | INTEGER | Sim | FK para TB_TABELA_PRECO.TBP_ID — tabela de preço padrão. |
| `CLI_GRUPO` | INTEGER | Sim | FK para TB_CLIENTE_GRUPO.CLIG_ID — grupo do cliente. |
| `CLI_NR_PARCELAS` | INTEGER | Sim | Número padrão de parcelas. |
| `CLI_REGIAO` | INTEGER | Sim | FK para TB_REGIAO.REG_ID — região de entrega. |
| `CLI_PERMITE_DESCONTO` | VARCHAR(1) | Sim | Permite vendedor aplicar desconto (S/N). |
| `CLI_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção (S/N). |
| `CLI_PLANO_CONTAS` | INTEGER | Sim | FK para plano de contas padrão do cliente. |
| `CLI_MENSAGEM_ALERTA` | VARCHAR(2000) | Sim | Mensagem de alerta exibida em tela de venda. |
| `CLI_OBS_NOTA` | VARCHAR(2000) | Sim | Observação padrão para nota fiscal do cliente. |
| `CLI_TRIBUTA_ICMS` | VARCHAR(1) | Sim | Indica se o cliente tributa ICMS (S/N). |
| `CLI_TRIBUTA_IPI` | VARCHAR(1) | Sim | Indica se o cliente tributa IPI (S/N). |
| `CLI_TRANSPORTADOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (transportador padrão). |
| `CLI_REDESPACHO` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (redespacho padrão). |
| `CLI_TIPO_FRETE` | INTEGER | Sim | Tipo de frete padrão: 0=CIF, 1=FOB, 2=Terceiros, 9=Sem Frete. |
| `CLI_TIPO_FRETE_RED` | INTEGER | Sim | Tipo de frete do redespacho. |
| `CLI_ENDERECO_ENTREGA` | INTEGER | Sim | FK para TB_ENDERECO.END_ID (entrega padrão). |
| `CLI_ENDERECO_COBRANCA` | INTEGER | Sim | FK para TB_ENDERECO.END_ID (cobrança padrão). |
| `CLI_PRECO_VENDA_CUSTO` | VARCHAR(1) | Sim | Define se usa preço de venda ou de custo. |
| `CLI_SERV_RESP_RETENCAO` | INTEGER | Sim | Responsável pela retenção do ISS (1=Tomador, 2=Intermediário). |
| `CLI_SERV_EXIGENCIA_ISS` | INTEGER | Sim | Exigibilidade do ISS (1=Exigível, 2=Não incidência, 3=Isenção, 4=Exportação, 5=Imunidade, etc.). |
| `CLI_SERV_NR_PROCESSO` | VARCHAR(30) | Sim | Número do processo judicial/administrativo (suspensão de ISS). |
| `CLI_SERV_ALIQ_ISS` | NUMERIC(15,2) | Sim | Alíquota do ISS. |
| `CLI_SERV_ISS_RETIDO` | VARCHAR(1) | Sim | Indica se o ISS é retido (S/N). |
| `CLI_SERV_ALIQ_PIS` | NUMERIC(15,2) | Sim | Alíquota do PIS. |
| `CLI_SERV_PIS_RETIDO` | VARCHAR(1) | Sim | Indica se o PIS é retido (S/N). |
| `CLI_SERV_ALIQ_COFINS` | NUMERIC(15,2) | Sim | Alíquota do COFINS. |
| `CLI_SERV_COFINS_RETIDO` | VARCHAR(1) | Sim | Indica se o COFINS é retido (S/N). |
| `CLI_SERV_ALIQ_CSLL` | NUMERIC(15,2) | Sim | Alíquota da CSLL. |
| `CLI_SERV_CSLL_RETIDO` | VARCHAR(1) | Sim | Indica se a CSLL é retida (S/N). |
| `CLI_SERV_ALIQ_IR` | NUMERIC(15,2) | Sim | Alíquota do IR. |
| `CLI_SERV_IR_RETIDO` | VARCHAR(1) | Sim | Indica se o IR é retido (S/N). |
| `CLI_SERV_ALIQ_INSS` | NUMERIC(15,2) | Sim | Alíquota do INSS. |
| `CLI_SERV_INSS_RETIDO` | VARCHAR(1) | Sim | Indica se o INSS é retido (S/N). |
| `CLI_INCENTIVADOR_CULTURAL` | VARCHAR(1) | Sim | Indica se é incentivador cultural (S/N). |
| `CLI_EXPORTAR_TABLET` | VARCHAR(1) | Sim | Indica se exporta para tablet (S/N). |
| `CLI_SERV_BUSCAR` | VARCHAR(1) | Sim | Indica se serviço é de busca/coleta (S/N). |
| `CLI_MENSALIADE` | NUMERIC(15,2) | Sim | Valor da mensalidade. |
| `CLI_VALOR_MENSALIDADE` | NUMERIC(15,2) | Sim | Valor aplicado da mensalidade. |
| `CLI_INSTALACAO` | NUMERIC(15,2) | Sim | Valor de instalação. |
| `CLI_VALOR_INSTAL` | NUMERIC(15,2) | Sim | Valor aplicado de instalação. |
| `CLI_DIA_MENSALIDADE` | INTEGER | Sim | Dia de vencimento da mensalidade. |
| `CLI_GERAR_BOLETO` | VARCHAR(1) | Sim | Indica se gera boleto da mensalidade (S/N). |
| `CLI_INICIO_ATIVIDADE` | DATE | Sim | Data de início da atividade do cliente. |
| `CLI_DIA_INSTLACAO` | INTEGER | Sim | Dia de vencimento da instalação. |
| `CLI_MENSALISTA` | VARCHAR(1) | Sim | Indica se o cliente é mensalista (S/N). |
| `CLI_ESPECIE_MOEDA_MENSALISTA` | INTEGER | Sim | Espécie de moeda da mensalidade. |
| `CLI_MODALIDADE_COBRANCA` | INTEGER | Sim | Modalidade de cobrança. |
| `CLI_SERV_PRODUTO` | INTEGER | Sim | FK para TB_PRODUTO — produto/serviço da mensalidade. |
| `CLI_DESC_DIAS` | INTEGER | Sim | Dias para o primeiro desconto. |
| `CLI_DESC_VALOR` | NUMERIC(15,2) | Sim | Valor do primeiro desconto. |
| `CLI_DESC_TIPO` | VARCHAR(1) | Sim | Tipo do primeiro desconto (V=Valor, P=Porcentagem). |
| `CLI_DESC_DIAS_2` | INTEGER | Sim | Dias para o segundo desconto. |
| `CLI_DESC_VALOR_2` | NUMERIC(15,2) | Sim | Valor do segundo desconto. |
| `CLI_DESC_TIPO_2` | VARCHAR(1) | Sim | Tipo do segundo desconto. |
| `CLI_DESC_DIAS_3` | INTEGER | Sim | Dias para o terceiro desconto. |
| `CLI_DESC_VALOR_3` | NUMERIC(15,2) | Sim | Valor do terceiro desconto. |
| `CLI_DESC_TIPO_3` | VARCHAR(1) | Sim | Tipo do terceiro desconto. |
| `CLI_NUMERO_CONSIGNADOS` | INTEGER | Sim | Quantidade de itens consignados. |
| `CLI_VALIDAR_LIMITE_CREDITO` | VARCHAR(1) | Sim | Se deve validar limite de crédito (S/N). |
| `CLI_FIM_ATIVIDADE` | DATE | Sim | Data de fim da atividade do cliente. |
| `CLI_PIS_RET` | NUMERIC(15,4) | Sim | Alíquota de retenção do PIS. |
| `CLI_COFINS_RET` | NUMERIC(15,4) | Sim | Alíquota de retenção do COFINS. |
| `CLI_CSLL_RET` | NUMERIC(15,4) | Sim | Alíquota de retenção da CSLL. |
| `CLI_IR_RET` | NUMERIC(15,4) | Sim | Alíquota de retenção do IR. |
| `CLI_PREV_RET` | NUMERIC(15,4) | Sim | Alíquota de retenção da Previdência. |
| `CLI_DESCONTAR_RETENCAO_TRIBUTOS` | VARCHAR(1) | Sim | Indica se desconta retenção de tributos (S/N). |
| `CLI_IPI_INTEGRA_BC_ICMS` | VARCHAR(1) | Sim | Indica se o IPI integra a BC do ICMS (S/N). |
| `CLI_SERV_ALIQ_DEDUCAO` | NUMERIC(15,4) | Sim | Alíquota de dedução para ISS. |

COMMENT ON COLUMN TB_CLIENTE.CLI_PESSOA IS 'FK para TB_PESSOA.PES_ID — Chave primária. SEMPRE faça JOIN com TB_PESSOA por PES_ID. Para filtrar clientes utilize WHERE PES_CLIENTE = ''S'' em TB_PESSOA.';
COMMENT ON COLUMN TB_CLIENTE.CLI_STATUS IS 'CLI_STATUS
''A'' -> ATIVO
''I'' -> INATIVO';
COMMENT ON COLUMN TB_CLIENTE.CLI_LIMITE_CREDITO IS 'Limite de crédito do cliente — não deve ser vazio, é necessário para a venda no PDV.';
COMMENT ON COLUMN TB_CLIENTE.CLI_AJUSTAR IS 'S - SIM
N - NAO';
COMMENT ON COLUMN TB_CLIENTE.CLI_REGIME IS 'MINAS RIO
R - REAL
P - PRESUMIDO
S - SIMPLES NACIONAL

RETAGUARDA
N - NORMAL
S - SIMPLES NACIONAL
M - MICRO EMPREENDEDOR
C - CONSUMIDOR FINAL
I - INDÚSTRIA
P - PRODUTOR RURAL';
COMMENT ON COLUMN TB_CLIENTE.CLI_ALTERAR_FORMA_PAGTO IS 'S - SIM
N - NAO';
COMMENT ON COLUMN TB_CLIENTE.CLI_NR_PARCELAS IS 'Número de parcelas';
COMMENT ON COLUMN TB_CLIENTE.CLI_PERMITE_DESCONTO IS 'Permite Vendedor Aplicar desconto SIM ou NÃO';

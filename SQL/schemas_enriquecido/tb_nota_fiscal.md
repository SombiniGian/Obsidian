# Tabela TB_NOTA_FISCAL

**Módulo:** Fiscal
Tabela principal de notas fiscais (NF-e, NFC-e, NF de serviço/importação etc.). Reúne dados do documento fiscal, totais, impostos, informações do destinatário, transportador e dados de IBS/CBS.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `NF_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `NF_ID` | INTEGER | Não | Identificador único da nota fiscal. Parte da chave primária composta. |
| `NF_ENTRADA_SAIDA` | VARCHAR(1) | Sim | Tipo da nota: E=Entrada, S=Saída. |
| `NF_MODELO` | VARCHAR(2) | Sim | Modelo do documento fiscal (ex.: 55=NF-e, 65=NFC-e). |
| `NF_SERIE` | INTEGER | Sim | Série da nota fiscal. |
| `NF_SUBSERIE` | VARCHAR(2) | Sim | Subsérie da nota fiscal. |
| `NF_NUMERO` | INTEGER | Sim | Número da nota fiscal. |
| `NF_DT_EMISSAO` | DATE | Sim | Data de emissão da nota. |
| `NF_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro no sistema. |
| `NF_NATUREZA_OPERACAO` | INTEGER | Sim | FK para TB_NATUREZA_OPERACAO.NOP_ID. |
| `NF_PEDIDO_VENDA` | INTEGER | Sim | FK para TB_PEDIDO_VENDA.PEV_ID — pedido de venda que originou a nota. |
| `NF_PEDIDO_COMPRA` | INTEGER | Sim | FK para TB_PEDIDO_COMPRA.PDC_ID — pedido de compra relacionado. |
| `NF_DATA_SAIDA` | DATE | Sim | Data de saída da mercadoria. |
| `NF_HORA_SAIDA` | TIME | Sim | Hora de saída da mercadoria. |
| `NF_VOLUME` | INTEGER | Sim | Quantidade de volumes da nota. |
| `NF_ESPECIE` | VARCHAR(60) | Sim | Espécie dos volumes. |
| `NF_MARCA` | VARCHAR(60) | Sim | Marca dos volumes. |
| `NF_NUMERACAO` | VARCHAR(60) | Sim | Numeração dos volumes. |
| `NF_PESO_LIQUIDO` | NUMERIC(15,3) | Sim | Peso líquido total da nota (kg). |
| `NF_PESO_BRUTO` | NUMERIC(15,3) | Sim | Peso bruto total da nota (kg). |
| `NF_TRANSPORTADOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (transportador). |
| `NF_PLACA` | VARCHAR(8) | Sim | Placa do veículo. |
| `NF_UF_PLACA` | VARCHAR(2) | Sim | UF da placa do veículo. |
| `NF_TIPO_FRETE` | INTEGER | Sim | Tipo do frete: 0=CIF, 1=FOB, 2=Terceiros, 9=Sem Frete. |
| `NF_FORMA_PAGTO` | INTEGER | Sim | FK para TB_FORMA_PAGTO.FPG_ID — forma de pagamento. |
| `NF_DADOS_ADICIONAIS` | BLOB SUB_TYPE BINARY | Sim | Dados adicionais (texto longo) em binário. NUNCA selecione em queries SELECT. |
| `NF_VALOR_BC_ICMS_FRETE` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS do frete. |
| `NF_ALIQ_ICMS_FRETE` | NUMERIC(15,2) | Sim | Alíquota de ICMS do frete. |
| `NF_VALOR_ICMS_FRETE` | NUMERIC(15,2) | Sim | Valor do ICMS do frete. |
| `NF_VALOR_PRODUTOS` | NUMERIC(15,2) | Sim | Valor total dos produtos. |
| `NF_VALOR_BC_ICMS` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS. |
| `NF_VALOR_ICMS` | NUMERIC(15,2) | Sim | Valor do ICMS. |
| `NF_VALOR_BC_ST` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS ST. |
| `NF_VALOR_ST` | NUMERIC(15,2) | Sim | Valor do ICMS ST. |
| `NF_VALOR_BC_IPI` | NUMERIC(15,2) | Sim | Base de cálculo do IPI. |
| `NF_VALOR_IPI` | NUMERIC(15,2) | Sim | Valor do IPI. |
| `NF_VALOR_DESPESAS` | NUMERIC(15,2) | Sim | Valor de despesas acessórias (frete, seguro etc.). |
| `NF_VALOR_DESCONTO` | NUMERIC(15,2) | Sim | Valor total de descontos. |
| `NF_VALOR_FRETE` | NUMERIC(15,2) | Sim | Valor do frete. |
| `NF_VALOR_SEGURO` | NUMERIC(15,2) | Sim | Valor do seguro. |
| `NF_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total da nota. |
| `NF_USUARIO` | INTEGER | Sim | Identificador do usuário que emitiu/recebeu a nota. |
| `NF_STATUS` | VARCHAR(1) | Sim | Status: D=Digitada, G=Gerada, A=Assinada, T=Transmitida, E=Enviada por email, C=Cancelada, P=Pendente de retorno, S=Enviada para SEFAZ. |
| `NF_VALOR_RECEBER_AVISTA` | NUMERIC(15,2) | Sim | Valor a receber à vista. |
| `NF_VALOR_RECEBER_APRAZO` | NUMERIC(15,2) | Sim | Valor a receber a prazo. |
| `NF_VALOR_RECEBIDO_CHEQUE` | NUMERIC(15,2) | Sim | Valor recebido em cheque. |
| `NF_VALOR_TOTAL_RECEBIDO` | NUMERIC(15,2) | Sim | Valor total recebido. |
| `NF_VALOR_TOTAL_RECEBER` | NUMERIC(15,2) | Sim | Valor total a receber — base para cálculo de comissão. |
| `NF_VALOR_PIS` | NUMERIC(15,2) | Sim | Valor do PIS. |
| `NF_VALOR_COFINS` | NUMERIC(15,2) | Sim | Valor do COFINS. |
| `NF_FINALIDADE` | INTEGER | Sim | Finalidade: 1=Normal, 2=Complementar, 3=Ajuste, 4=Devolução/Retorno. |
| `NF_NFE_REFERENCIADA` | VARCHAR(44) | Sim | Chave de acesso da NF-e referenciada. |
| `NF_NOTA_FISCAL_IMPORTADA` | INTEGER | Sim | ID da NF importada que originou esta nota. |
| `NF_CUSTO_ADICIONAL` | NUMERIC(15,2) | Sim | Custo adicional lançado. |
| `NF_TOTAL_CUSTO` | NUMERIC(15,2) | Sim | Custo total da nota. |
| `NF_CARGA` | INTEGER | Sim | FK para carga vinculada. |
| `NF_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção (S/N). |
| `NF_DADOS_FISCAIS` | BLOB SUB_TYPE BINARY | Sim | Dados fiscais em binário. NUNCA selecione em queries SELECT. |
| `NF_VALOR_FCP` | NUMERIC(15,2) | Sim | Valor do Fundo de Combate à Pobreza (FCP). |
| `NF_VALOR_ICMS_UF_ORIGEM` | NUMERIC(15,2) | Sim | Valor do ICMS partilhado para a UF de origem. |
| `NF_VALOR_ICMS_UF_DEST` | NUMERIC(15,2) | Sim | Valor do ICMS partilhado para a UF de destino. |
| `NF_CONTA_DEBITO` | INTEGER | Sim | Conta contábil de débito. |
| `NF_CONTA_CREDITO` | INTEGER | Sim | Conta contábil de crédito. |
| `NF_RNTRC` | VARCHAR(20) | Sim | RNTRC do transportador. |
| `NF_EMITIR_RECEBER` | VARCHAR(1) | Sim | Indica se a nota emite ou recebe financeiro (E=Emitir, R=Receber). |
| `NF_PESSOA` | INTEGER | Sim | FK para TB_PESSOA.PES_ID — cliente/fornecedor da nota. |
| `NF_DEST_CNPJ_CPF` | VARCHAR(14) | Sim | CNPJ/CPF do destinatário (somente números). |
| `NF_DEST_IE` | VARCHAR(18) | Sim | IE do destinatário. |
| `NF_DEST_IND_IE` | VARCHAR(1) | Sim | Indicador da IE do destinatário: C=Contribuinte, I=Isento, N=Não Contribuinte. |
| `NF_DEST_CONS_FINAL` | VARCHAR(1) | Sim | Indica se o destinatário é consumidor final (S/N). |
| `NF_DEST_NOME` | VARCHAR(100) | Sim | Nome/Razão Social do destinatário. |
| `NF_DEST_LOGRADOURO` | VARCHAR(100) | Sim | Logradouro do destinatário. |
| `NF_DEST_NUMERO` | VARCHAR(10) | Sim | Número do endereço do destinatário. |
| `NF_DEST_COMPLEMENTO` | VARCHAR(20) | Sim | Complemento do endereço do destinatário. |
| `NF_DEST_CIDADE` | INTEGER | Sim | FK para TB_CIDADE.CID_ID do destinatário. |
| `NF_DEST_BAIRRO` | VARCHAR(50) | Sim | Bairro do destinatário. |
| `NF_DEST_COD_MUNICIPIO` | INTEGER | Sim | Código do município do destinatário (IBGE). |
| `NF_DEST_UF` | VARCHAR(2) | Sim | UF do destinatário. |
| `NF_DEST_CEP` | VARCHAR(10) | Sim | CEP do destinatário. |
| `NF_DEST_FONE` | VARCHAR(20) | Sim | Telefone do destinatário. |
| `NF_TRANSP_CNPJ_CPF` | VARCHAR(14) | Sim | CNPJ/CPF do transportador. |
| `NF_TRANSP_IE` | VARCHAR(18) | Sim | IE do transportador. |
| `NF_TRANSP_NOME` | VARCHAR(100) | Sim | Nome/Razão Social do transportador. |
| `NF_TRANSP_ENDERECO` | VARCHAR(100) | Sim | Endereço do transportador. |
| `NF_TRANSP_CIDADE` | VARCHAR(80) | Sim | Cidade do transportador. |
| `NF_TRANSP_UF` | VARCHAR(2) | Sim | UF do transportador. |
| `NF_IND_PAGTO` | VARCHAR(1) | Sim | Indicador de pagamento: 0=À vista, 1=À prazo, 2=Outros. |
| `NF_VALOR_TOTAL_PARCELADO` | NUMERIC(15,2) | Sim | Valor total parcelado. |
| `NF_VALOR_DIFERENCA` | NUMERIC(15,2) | Sim | Valor da diferença para crédito. |
| `NF_VEICULO` | INTEGER | Sim | FK para veículo (TB_VEICULO). |
| `NF_GERA_FINANCEIRO` | VARCHAR(1) | Sim | Indica se a nota gera financeiro (S/N). |
| `NF_VERSAO_EXE` | VARCHAR(20) | Sim | Versão do executável que gerou a nota. |
| `NF_TABELA_PRECO` | INTEGER | Sim | FK para TB_TABELA_PRECO.TBP_ID usada na nota. |
| `NF_TAB_TIPO` | VARCHAR(1) | Sim | Tipo da tabela: A=Acréscimo, D=Desconto. |
| `NF_TAB_VALOR` | NUMERIC(15,2) | Sim | Valor do acréscimo/desconto da tabela. |
| `NF_PRECO_UTILIZAR` | VARCHAR(1) | Sim | Define se o preço é de Venda ou Custo. |
| `NF_EMAIL_ENVIADO` | VARCHAR(1) | Sim | Indica se o e-mail foi enviado (S/N). |
| `NF_EMAIL_DEST` | VARCHAR(1000) | Sim | E-mail(s) de destino da nota. |
| `NF_CARGA_ORDEM` | INTEGER | Sim | Ordem dentro da carga. |
| `NF_DEST_CIDADE_NOME` | VARCHAR(80) | Sim | Nome da cidade do destinatário (cópia). |
| `NF_VALOR_COFERENCIA` | NUMERIC(15,2) | Sim | Valor de conferência. |
| `NF_IND_PRES` | INTEGER | Sim | Indicador de presença: 0=Não se aplica, 1=Presencial, 2=Internet, 3=Teleatendimento, 4=NFC-e entrega a domicílio, 5=Presencial fora do estabelecimento, 9=Outros. |
| `NF_VALOR_FCP_UF_DEST` | NUMERIC(15,2) | Sim | Valor do FCP para UF de destino. |
| `NF_VALOR_FCP_ST` | NUMERIC(15,2) | Sim | Valor do FCP ST. |
| `NF_VALOR_FCP_ST_RET` | NUMERIC(15,2) | Sim | Valor do FCP ST retido. |
| `NF_VALOR_IPI_DEV` | NUMERIC(15,2) | Sim | Valor do IPI devolvido. |
| `NF_VALOR_TRIB_MUNICIPAIS` | NUMERIC(15,2) | Sim | Valor aproximado dos tributos municipais. |
| `NF_VALOR_TRIB_ESTADUAIS` | NUMERIC(15,2) | Sim | Valor aproximado dos tributos estaduais. |
| `NF_VALOR_TRIB_FEDERAIS` | NUMERIC(15,2) | Sim | Valor aproximado dos tributos federais. |
| `NF_VALOR_TOTAL_TRIB` | NUMERIC(15,2) | Sim | Valor aproximado total dos tributos. |
| `NF_ALIQ_CRED_ICMS` | NUMERIC(15,2) | Sim | Alíquota de crédito de ICMS. |
| `NF_VALOR_CRED_ICMS` | NUMERIC(15,2) | Sim | Valor do crédito de ICMS. |
| `NF_MOV_EST_GERENCIAL` | VARCHAR(1) | Sim | Indica se movimenta estoque gerencial (S/N). |
| `NF_ATUALIZAR_CUSTO` | VARCHAR(1) | Sim | Indica se atualiza custo dos produtos (S/N). |
| `NF_CUSTO_TOTAL` | NUMERIC(15,2) | Sim | Custo total dos produtos. |
| `NF_ORDEM_SERVICO` | INTEGER | Sim | FK para ordem de serviço relacionada. |
| `NF_GRUPO_FATURA` | VARCHAR(1) | Sim | Indica se pertence a grupo de fatura (S/N). |
| `NF_GRUPO_FORMA_PAGTO` | VARCHAR(1) | Sim | Indica se pertence a grupo de forma de pagamento (S/N). |
| `NF_FORMA_PAGTO_OBS` | VARCHAR(1) | Sim | Indica se a forma de pagamento deve ir para a observação da nota (S/N). |
| `NF_SUBSTITUIDA` | VARCHAR(1) | Sim | Indica se foi substituída (S/N). |
| `NF_SUBSTITUTA` | INTEGER | Sim | ID da nota fiscal substituta. |
| `NF_VALOR_BC_II` | NUMERIC(15,2) | Sim | Base de cálculo do Imposto de Importação. |
| `NF_VALOR_II` | NUMERIC(15,2) | Sim | Valor do Imposto de Importação. |
| `NF_IMPORTACAO` | VARCHAR(1) | Sim | Indica se é nota de importação (S/N). |
| `NF_CANCELA_PEDIDO` | VARCHAR(1) | Sim | Comportamento ao cancelar a nota: N=Nada, F=Cancela faturamento, V=Cancela faturamento e pedido. |
| `NF_METRAGEM_CUBICA` | NUMERIC(15,4) | Sim | Metragem cúbica total da nota. |
| `NF_ALTERAR_VOLUME` | VARCHAR(1) | Sim | Permite alterar volume (S/N). |
| `NF_GRUPO_REPASSE_ICMS` | VARCHAR(1) | Sim | Repasse de ICMS entre UFs (S/N). |
| `NF_GRUPO_ICMS_EFETIVO` | VARCHAR(1) | Sim | ICMS efetivo (S/N). |
| `NF_MOV_ESTOQUE` | VARCHAR(1) | Sim | Indica se movimenta estoque (S/N). |
| `NF_VALOR_ICMS_DESON` | NUMERIC(15,2) | Sim | Valor do ICMS desonerado. |
| `NF_DEST_NAO_REG` | VARCHAR(1) | Sim | Destinatário não registrado (S/N). |
| `NF_TIPO_DESCONTO` | VARCHAR(1) | Sim | Tipo do desconto (V=Valor, P=Porcentagem, T=Total). |
| `NF_DESCONTO` | NUMERIC(15,2) | Sim | Valor do desconto aplicado. |
| `NF_TIPO_ACRESCIMO` | VARCHAR(1) | Sim | Tipo do acréscimo (V=Valor, P=Porcentagem). |
| `NF_ACRESCIMO` | NUMERIC(15,2) | Sim | Valor do acréscimo aplicado. |
| `NF_ORIGEM` | VARCHAR(10) | Sim | Sigla da rotina de origem da nota. |
| `NF_REMETENTE` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (remetente). |
| `NF_DESTINATARIO` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (destinatário). |
| `NF_EXPEDIDOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (expedidor). |
| `NF_RECEBEDOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (recebedor). |
| `NF_VENDEDOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (vendedor). |
| `NF_VENDEDOR_OBS` | VARCHAR(1) | Sim | Indica se o vendedor vai para a observação (S/N). |
| `NF_LOTE_PRODUCAO` | INTEGER | Sim | FK para lote de produção relacionado. |
| `NF_DESMEMBRAR` | VARCHAR(1) | Sim | Indica se deve desmembrar a nota (S/N). |
| `NF_NOTA_IMP` | INTEGER | Sim | ID da nota que importou a nota atual. |
| `NF_PEDIDO_OBS` | VARCHAR(1) | Sim | Indica se a observação do pedido vai para a nota (S/N). |
| `NF_ZERAR_BC` | VARCHAR(1) | Sim | Indica se zera base de cálculo (S/N). |
| `NF_DOC_EXTERIOR` | VARCHAR(20) | Sim | Documento para pessoas do exterior. |
| `NF_DEST_PAIS` | VARCHAR(50) | Sim | País do destinatário. |
| `NF_DEST_COD_PAIS` | INTEGER | Sim | Código do país do destinatário. |
| `NF_VALOR_SISCOMEX` | NUMERIC(15,2) | Sim | Valor do SISCOMEX. |
| `NF_VALOR_AFRMM` | NUMERIC(15,2) | Sim | Valor do AFRMM. |
| `NF_DESP_ADUANEIRAS` | NUMERIC(15,2) | Sim | Despesas aduaneiras. |
| `NF_COD_REF_INF` | VARCHAR(1) | Sim | Código de referência de informação. |
| `NF_LOCAL_ESTOQUE` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE.LOC_ID. |
| `NF_PEDIDO_CLIENTE` | VARCHAR(15) | Sim | Número do pedido do cliente. |
| `NF_AVULSA` | VARCHAR(1) | Sim | Indica se é nota avulsa (S/N). |
| `NF_EXPORTACAO` | VARCHAR(1) | Sim | Indica se é nota de exportação (S/N). |
| `NF_EXP_UF_SAIDA` | VARCHAR(2) | Sim | UF de saída da exportação. |
| `NF_EXP_LOC_EXP` | VARCHAR(60) | Sim | Local de exportação. |
| `NF_EXP_LOC_DESPACHO` | VARCHAR(60) | Sim | Local de despacho da exportação. |
| `NF_ENTREGA_FUTURA` | VARCHAR(1) | Sim | Indica se é entrega futura (S/N). |
| `NF_TIPO_DIFAL` | VARCHAR(1) | Sim | Tipo do DIFAL. |
| `NF_ICMS_DESON_TOTAL` | VARCHAR(1) | Sim | Indica se há ICMS desonerado total (S/N). |
| `NF_LOCAL` | INTEGER | Sim | FK para TB_LOCAL. |
| `NF_TIPO_LOCAL` | VARCHAR(1) | Sim | Tipo do local. |
| `NF_GNRE` | INTEGER | Sim | Identificador da GNRE. |
| `NF_VALOR_SERVICOS` | NUMERIC(15,2) | Sim | Valor dos serviços (NFS-e). |
| `NF_VALOR_ISS_BC` | NUMERIC(15,2) | Sim | Base de cálculo do ISS. |
| `NF_VALOR_ISS` | NUMERIC(15,2) | Sim | Valor do ISS. |
| `NF_VALOR_PIS_SERVICO` | NUMERIC(15,2) | Sim | Valor do PIS sobre serviços. |
| `NF_VALOR_COFINS_SERVICO` | NUMERIC(15,2) | Sim | Valor do COFINS sobre serviços. |
| `NF_VALOR_DEDUCAO_ISS` | NUMERIC(15,2) | Sim | Valor de dedução do ISS. |
| `NF_VALOR_RETENCAO_ISS` | NUMERIC(15,2) | Sim | Valor de retenção do ISS. |
| `NF_VALOR_DESC_COND_ISS` | NUMERIC(15,2) | Sim | Desconto condicional sobre ISS. |
| `NF_VALOR_DESC_INCOND_ISS` | NUMERIC(15,2) | Sim | Desconto incondicional sobre ISS. |
| `NF_VALOR_ISS_RETIDO` | NUMERIC(15,2) | Sim | Valor do ISS retido. |
| `NF_ISS_REGIME_TRIBUTACAO` | INTEGER | Sim | Regime especial de tributação do ISS. |
| `NF_DT_PRESTACAO_SERVICO` | DATE | Sim | Data da prestação do serviço. |
| `NF_IND_INTERMEDIADOR` | INTEGER | Sim | Indicador de intermediador. |
| `NF_INTERMEDIADOR` | INTEGER | Sim | FK para intermediador. |
| `NF_INTERM_CNPJ` | VARCHAR(14) | Sim | CNPJ do intermediador. |
| `NF_INTERM_IDENT_USUARIO` | VARCHAR(60) | Sim | Identificação do usuário no intermediador. |
| `NF_NAO_IMPRIMIR_LOTE_DETALHADO` | VARCHAR(1) | Sim | Indica se não imprime lote detalhado (S/N). |
| `NF_NUMERO_DAV` | INTEGER | Sim | Número do DAV (Documento Auxiliar de Venda). |
| `NF_NUMERO_RE` | INTEGER | Sim | Número do RE. |
| `NF_COD_INDENTIFICACAO_RE` | VARCHAR(100) | Sim | Código de identificação do RE. |
| `NF_DEST_SUFRAMA` | VARCHAR(10) | Sim | SUFRAMA do destinatário. |
| `NF_CONSIGNADO` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (consignado). |
| `NF_ORDEM_PRODUCAO` | INTEGER | Sim | FK para TB_ORDEM_PRODUCAO.OP_ID. |
| `NF_VALOR_BC_ICMS_MONO` | NUMERIC(15,2) | Sim | BC do ICMS monofásico. |
| `NF_VALOR_ICMS_MONO` | NUMERIC(15,2) | Sim | Valor do ICMS monofásico. |
| `NF_VALOR_BC_ICMS_MONO_RETEN` | NUMERIC(15,2) | Sim | BC do ICMS monofásico retido. |
| `NF_VALOR_ICMS_MONO_RETEN` | NUMERIC(15,2) | Sim | Valor do ICMS monofásico retido. |
| `NF_VALOR_BC_ICMS_MONO_RET` | NUMERIC(15,2) | Sim | BC do ICMS monofásico por retenção. |
| `NF_VALOR_ICMS_MONO_RET` | NUMERIC(15,2) | Sim | Valor do ICMS monofásico por retenção. |
| `NF_DESCONTAR_RETENCAO_TRIBUTOS` | VARCHAR(1) | Sim | Indica se desconta retenção de tributos (S/N). |
| `NF_ALIQ_PIS_RET` | NUMERIC(15,4) | Sim | Alíquota do PIS retido. |
| `NF_VALOR_PIS_RET` | NUMERIC(15,2) | Sim | Valor do PIS retido. |
| `NF_ALIQ_COFINS_RET` | NUMERIC(15,4) | Sim | Alíquota do COFINS retido. |
| `NF_VALOR_COFINS_RET` | NUMERIC(15,2) | Sim | Valor do COFINS retido. |
| `NF_BC_IR_RET` | NUMERIC(15,2) | Sim | Base de cálculo do IR retido. |
| `NF_ALIQ_IR_RET` | NUMERIC(15,4) | Sim | Alíquota do IR retido. |
| `NF_VALOR_IR_RET` | NUMERIC(15,2) | Sim | Valor do IR retido. |
| `NF_BC_PREV_RET` | NUMERIC(15,2) | Sim | Base de cálculo da Previdência retida. |
| `NF_ALIQ_PREV_RET` | NUMERIC(15,4) | Sim | Alíquota da Previdência retida. |
| `NF_VALOR_PREV_RET` | NUMERIC(15,2) | Sim | Valor da Previdência retida. |
| `NF_ALIQ_CSLL_RET` | NUMERIC(15,4) | Sim | Alíquota da CSLL retida. |
| `NF_VALOR_CSLL_RET` | NUMERIC(15,2) | Sim | Valor da CSLL retida. |
| `NF_VALOR_DESC_RETIDO` | NUMERIC(15,2) | Sim | Valor do desconto retido. |
| `NF_IPI_INTEGRA_BC_ICMS` | VARCHAR(1) | Sim | Indica se IPI integra BC do ICMS (S/N). |
| `NF_GUID` | VARCHAR(50) | Sim | GUID para integração. |
| `NF_ID_SERVIDOR` | INTEGER | Sim | FK para TB_SERVIDOR de origem. |
| `NF_ID_LOCAL` | INTEGER | Sim | FK para TB_LOCAL. |
| `NF_BORDERO_REC` | INTEGER | Sim | FK para TB_BORDERO_RECEBIMENTO. |
| `NF_PAG_ELETRONICO` | VARCHAR(1) | Sim | Indica se o pagamento é eletrônico (S/N). |
| `NF_SOMAR_II` | VARCHAR(1) | Sim | Indica se soma II no total da nota (S/N). |
| `NF_SOMAR_ICMS` | VARCHAR(1) | Sim | Indica se soma ICMS no total da nota (S/N). |
| `NF_SOMAR_PIS_COFINS` | VARCHAR(1) | Sim | Indica se soma PIS/COFINS no total da nota (S/N). |
| `NF_ZERAR_BC_PIS_COFINS` | VARCHAR(1) | Sim | Indica se zera BC de PIS/COFINS (S/N). |
| `NF_ZERAR_IPI` | VARCHAR(1) | Sim | Indica se zera IPI (S/N). |
| `NF_OUTRAS_MOV` | INTEGER | Sim | Identificador de outras movimentações. |
| `NF_TIPO_TABELA_PRECO` | VARCHAR(1) | Sim | Tipo da tabela de preço usada (D/A). |
| `NF_TABELA_DESC_ACRES` | NUMERIC(15,2) | Sim | Valor de desconto/acréscimo da tabela. |
| `NF_RECEBIDA_CTE` | INTEGER | Sim | CTE recebido relacionado. |
| `NF_DEST_REGIME` | VARCHAR(2) | Sim | Regime tributário do destinatário. |
| `NF_IS_VALOR` | NUMERIC(15,2) | Sim | Valor do IS (IBS/CBS). |
| `NF_IBS_CBS_BC` | NUMERIC(15,2) | Sim | Base de cálculo do IBS/CBS. |
| `NF_CBS_VALOR` | NUMERIC(15,2) | Sim | Valor do CBS. |
| `NF_CBS_DIF_VALOR` | NUMERIC(15,2) | Sim | Valor do CBS por diferimento. |
| `NF_CBS_DEV_VALOR` | NUMERIC(15,2) | Sim | Valor do CBS devolvido. |
| `NF_CBS_CPRES_VALOR` | NUMERIC(15,2) | Sim | Valor do CBS com crédito presumido. |
| `NF_CBS_CPRES_VALOR_SUSP` | NUMERIC(15,2) | Sim | Valor do CBS com crédito presumido suspenso. |
| `NF_IBS_UF_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS UF. |
| `NF_IBS_UF_DIF_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS UF por diferimento. |
| `NF_IBS_UF_DEV_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS UF devolvido. |
| `NF_IBS_MUN_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS municipal. |
| `NF_IBS_MUN_DIF_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS municipal por diferimento. |
| `NF_IBS_MUN_DEV_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS municipal devolvido. |
| `NF_IBS_CPRES_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS com crédito presumido. |
| `NF_IBS_CPRES_VALOR_SUSP` | NUMERIC(15,2) | Sim | Valor do IBS com crédito presumido suspenso. |
| `NF_IBS_VALOR` | NUMERIC(15,2) | Sim | Valor total do IBS. |
| `NF_CBS_MONO_VALOR` | NUMERIC(15,2) | Sim | Valor do CBS monofásico. |
| `NF_CBS_MONO_RETEN_VALOR` | NUMERIC(15,2) | Sim | Valor do CBS monofásico retido. |
| `NF_CBS_MONO_RET_VALOR` | NUMERIC(15,2) | Sim | Valor do CBS monofásico por retenção. |
| `NF_IBS_MONO_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS monofásico. |
| `NF_IBS_MONO_RETEN_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS monofásico retido. |
| `NF_IBS_MONO_RET_VALOR` | NUMERIC(15,2) | Sim | Valor do IBS monofásico por retenção. |
| `NF_ENTE_GOV` | VARCHAR(1) | Sim | Indica se é ente governamental (S/N). |
| `NF_GOV_REDUTOR` | NUMERIC(15,2) | Sim | Redutor do ente governamental. |
| `NF_GOV_TIPO` | VARCHAR(1) | Sim | Tipo do redutor governamental. |
| `NF_TIPO_DEBITO` | VARCHAR(2) | Sim | Tipo do débito. |
| `NF_TIPO_CREDITO` | VARCHAR(2) | Sim | Tipo do crédito. |
| `NF_COD_MUN_CONSUMO` | INTEGER | Sim | Código do município de consumo (IBS). |
| `NF_REGRA_TRIBUTARIA` | INTEGER | Sim | Regra tributária aplicada. |

COMMENT ON COLUMN TB_NOTA_FISCAL.NF_TIPO_FRETE IS 'NF_TIPO_FRETE
0 - CIF
1 - FOB
2 - TERCEIROS
9 - SEM FRETE';
COMMENT ON COLUMN TB_NOTA_FISCAL.NF_STATUS IS 'NF_STATUS
NOTAS EMITIDAS
D - DIGITADA
G - GERADA
A - ASSINADA
T - TRANSMITIDA
E - ENVIADA POR EMAIL
C - CANCELADA
P - PENDENTE DE RETORNO
NOTAS RECEBIDAS
D - DIGITADA
S - ENVIADA PARA SEFAZ';
COMMENT ON COLUMN TB_NOTA_FISCAL.NF_VALOR_TOTAL_RECEBER IS 'Valor que realmente o cliente vai receber daquela nota (Valor da Nota - descontos + acrescimos - Tx Cartão). Utilizado como base de cálculo para comissão.';
COMMENT ON COLUMN TB_NOTA_FISCAL.NF_FINALIDADE IS '1 - NORMAL
2 - COMPLEMENTAR
3 - AJUSTE
4 - DEVOLUCAO / RETORNO';
COMMENT ON COLUMN TB_NOTA_FISCAL.NF_NFE_REFERENCIADA IS 'CHAVE DE ACESSO DA NFE REFERENCIADA';
COMMENT ON COLUMN TB_NOTA_FISCAL.NF_NOTA_FISCAL_IMPORTADA IS 'ID da Nota Fiscal que foi importada';
COMMENT ON COLUMN TB_NOTA_FISCAL.NF_DEST_IND_IE IS 'C - CONTRIBUINTE
I - ISENTO
N - NÃO CONTRIBUINTE';
COMMENT ON COLUMN TB_NOTA_FISCAL.NF_DEST_CONS_FINAL IS 'S - SIM
N - NAO';
COMMENT ON COLUMN TB_NOTA_FISCAL.NF_TAB_TIPO IS 'A - Acrescimo
D - Desconto';
COMMENT ON COLUMN TB_NOTA_FISCAL.NF_EMAIL_ENVIADO IS 'S - SIM
N - NÃO';
COMMENT ON COLUMN TB_NOTA_FISCAL.NF_PESSOA IS 'FK para TB_PESSOA.PES_ID — use JOIN com TB_PESSOA por PES_ID';
COMMENT ON COLUMN TB_NOTA_FISCAL.NF_PEDIDO_VENDA IS 'FK para TB_PEDIDO_VENDA.PEV_ID';
COMMENT ON COLUMN TB_NOTA_FISCAL.NF_DADOS_ADICIONAIS IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_NOTA_FISCAL.NF_DADOS_FISCAIS IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

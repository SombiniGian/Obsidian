# Tabela TB_ORDEM_SERVICO

**Módulo:** Serviços / Ordem de Serviço
Tabela principal de Ordens de Serviço (OS). Controla o ciclo de vida da OS desde a abertura até a entrega, com dados de cliente, técnico, vendedor, equipamento, defeito, laudo, serviços, produtos, valores (total, desconto, acréscimo, comissão,ISS, retenções), movimentação de estoque, dados para NF-e/NFS-e, garantia, liberações (senha) e fechamentos. É a tabela central do módulo de assistência técnica/serviços.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `OS_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `OS_ID` | INTEGER | Não | Identificador único da OS. Parte da chave primária composta. |
| `OS_STATUS` | VARCHAR(1) | Sim | Status da OS (A=Aberto, T=Executando, E=Entregue). |
| `OS_CLIENTE` | INTEGER | Sim | FK para TB_PESSOA.PES_ID do cliente. Use JOIN por PES_ID. |
| `OS_TECNICO` | INTEGER | Sim | FK para TB_TECNICO responsável. |
| `OS_VENDEDOR` | INTEGER | Sim | FK para TB_VENDEDOR. |
| `OS_DT_EMISSAO` | DATE | Sim | Data de emissão da OS. |
| `OS_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento no sistema. |
| `OS_DT_PREVISTA` | DATE | Sim | Data prevista para execução/entrega. |
| `OS_HR_PREVISTA` | TIME | Sim | Hora prevista para execução/entrega. |
| `OS_DT_ENTREGA` | DATE | Sim | Data efetiva de entrega. |
| `OS_HR_ENTREGA` | TIME | Sim | Hora efetiva de entrega. |
| `OS_DT_FATURAMENTO` | DATE | Sim | Data de faturamento da OS. |
| `OS_USUARIO` | INTEGER | Sim | Identificador do usuário que abriu a OS. |
| `OS_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total da OS. |
| `OS_VALOR_DESCONTO` | NUMERIC(15,2) | Sim | Valor de desconto aplicado. |
| `OS_VALOR_ACRESCIMO` | NUMERIC(15,2) | Sim | Valor de acréscimo aplicado. |
| `OS_VALOR_SERVICO` | NUMERIC(15,2) | Sim | Valor dos serviços. |
| `OS_VALOR_PRODUTOS` | NUMERIC(15,2) | Sim | Valor dos produtos. |
| `OS_SUB_TOTAL` | NUMERIC(15,2) | Sim | Subtotal da OS. |
| `OS_TEMPO_PREVISTO` | INTEGER | Sim | Tempo previsto de execução em minutos. |
| `OS_TEMPO_GASTO` | INTEGER | Sim | Tempo gasto em minutos. |
| `OS_FORMA_PAGTO` | INTEGER | Sim | FK para TB_FORMA_PAGTO. |
| `OS_TIPO_FORMA_PAGTO` | VARCHAR(1) | Sim | Tipo da forma de pagamento (A=À vista, P=A prazo). |
| `OS_FORMA_PAGTO_DESC_ACRES` | NUMERIC(15,2) | Sim | Desconto/acréscimo da forma de pagamento. |
| `OS_VALOR_RECEBIDO_CHEQUE` | NUMERIC(15,2) | Sim | Valor recebido em cheque. |
| `OS_VALOR_TOTAL_RECEBIDO` | NUMERIC(15,2) | Sim | Valor total já recebido. |
| `OS_VALOR_TOTAL_RECEBER` | NUMERIC(15,2) | Sim | Valor total a receber. |
| `OS_VALOR_RECEBER_AVISTA` | NUMERIC(15,2) | Sim | Valor a receber à vista. |
| `OS_VALOR_RECEBER_APRAZO` | NUMERIC(15,2) | Sim | Valor a receber a prazo. |
| `OS_VALOR_TOTAL_PARCELADO` | NUMERIC(15,2) | Sim | Valor total parcelado. |
| `OS_VALOR_DIFERENCA` | NUMERIC(15,2) | Sim | Valor de diferença (troco). |
| `OS_VALOR_COMISSAO` | NUMERIC(15,2) | Sim | Valor de comissão total. |
| `OS_COMISSAO_TECNICO` | NUMERIC(15,2) | Sim | Comissão do técnico. |
| `OS_COMISSAO_VENDEDOR` | NUMERIC(15,2) | Sim | Comissão do vendedor. |
| `OS_VALOR_COMISSAO_VEND` | NUMERIC(15,2) | Sim | Valor de comissão do vendedor (cálculo separado). |
| `OS_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações em formato binário. NUNCA selecione em queries SELECT. |
| `OS_LAUDO_TECNICO` | BLOB SUB_TYPE BINARY | Sim | Laudo técnico em formato binário. NUNCA selecione em queries SELECT. |
| `OS_OBS_DEFEITO` | BLOB SUB_TYPE BINARY | Sim | Observações do defeito. NUNCA selecione em queries SELECT. |
| `OS_MENSAGEM_ALERTA` | BLOB SUB_TYPE BINARY | Sim | Mensagem de alerta da OS. NUNCA selecione em queries SELECT. |
| `OS_OBS_NFE` | BLOB SUB_TYPE BINARY | Sim | Observações para NF-e. NUNCA selecione em queries SELECT. |
| `OS_OBS_NFSE` | BLOB SUB_TYPE BINARY | Sim | Observações para NFS-e. NUNCA selecione em queries SELECT. |
| `OS_OBS_GARANTIA` | BLOB SUB_TYPE BINARY | Sim | Observações da garantia. NUNCA selecione em queries SELECT. |
| `OS_PEDIDO_VENDA` | INTEGER | Sim | FK para TB_PEDIDO_VENDA vinculado. |
| `OS_TABELA_PRECO` | INTEGER | Sim | FK para TB_TABELA_PRECO aplicada. |
| `OS_TIPO_TABELA_PRECO` | VARCHAR(1) | Sim | Tipo da tabela (A=Acrescimo, D=Desconto). |
| `OS_TABELA_DESC_ACRES` | NUMERIC(15,2) | Sim | Percentual/valor da tabela. |
| `OS_GERA_FINANCEIRO` | VARCHAR(1) | Sim | Indica se a OS gera financeiro (S/N). |
| `OS_LIMITE_CREDITO` | NUMERIC(15,2) | Sim | Limite de crédito do cliente nesta OS. |
| `OS_LIMITE_DISPONIVEL` | NUMERIC(15,2) | Sim | Limite disponível do cliente nesta OS. |
| `OS_LIMITE_UTILIZADO` | NUMERIC(15,2) | Sim | Limite utilizado nesta OS. |
| `OS_CAIXA` | INTEGER | Sim | FK para TB_FECHAMENTO_CAIXA. |
| `OS_ISS_PERC` | NUMERIC(15,2) | Sim | Percentual de ISS. |
| `OS_ISS_VALOR` | NUMERIC(15,2) | Sim | Valor de ISS. |
| `OS_NATUREZA_OPERACAO` | INTEGER | Sim | FK para TB_NATUREZA_OPERACAO. |
| `OS_PRIORIDADE` | VARCHAR(1) | Sim | Prioridade da OS (B=Baixa, N=Normal, A=Alta, U=Urgente). |
| `OS_DESCRICAO_DEFEITO` | VARCHAR(100) | Sim | Descrição do defeito. |
| `OS_DEFEITO` | INTEGER | Sim | FK para TB_DEFEITO. |
| `OS_CLASSIFICACAO` | INTEGER | Sim | FK para TB_CLASSIFICACAO. |
| `OS_TIPO_EQUIPAMENTO` | INTEGER | Sim | FK para TB_TIPO_EQUIPAMENTO. |
| `OS_EQUIPAMENTO` | INTEGER | Sim | FK para TB_EQUIPAMENTO. |
| `OS_EQUIP_DESC_1` | VARCHAR(100) | Sim | Descrição do equipamento - campo 1 (DESCRIÇÃO EQUIPAMENTO). |
| `OS_EQUIP_DESC_2` | VARCHAR(100) | Sim | Modelo do equipamento. |
| `OS_EQUIP_DESC_3` | VARCHAR(100) | Sim | Número de série do equipamento. |
| `OS_EQUIP_MARCA` | INTEGER | Sim | FK para TB_PROD_MARCA do equipamento. |
| `OS_NR_PARCELAS` | INTEGER | Sim | Quantidade de parcelas. |
| `OS_PLANO_CONTAS` | INTEGER | Sim | FK para TB_PLANO_CONTA. |
| `OS_TIPO_DESCONTO` | VARCHAR(1) | Sim | Tipo do desconto (P=Percentual, V=Valor). |
| `OS_DESCONTO` | NUMERIC(15,2) | Sim | Percentual/valor de desconto. |
| `OS_TIPO_ACRESCIMO` | VARCHAR(1) | Sim | Tipo do acréscimo (P=Percentual, V=Valor). |
| `OS_ACRESCIMO` | NUMERIC(15,2) | Sim | Percentual/valor de acréscimo. |
| `OS_USUARIO_LIBERACAO` | INTEGER | Sim | FK para TB_USUARIO que liberou (desconto/acréscimo). |
| `OS_DT_LIBERACAO` | TIMESTAMP | Sim | Data e hora da liberação. |
| `OS_SENHA_LIBERACAO` | INTEGER | Sim | FK para TB_SENHA_LIBERACAO. |
| `OS_VALOR_CUSTO_MEDIO` | NUMERIC(15,2) | Sim | Valor de custo médio dos produtos/serviços. |
| `OS_MOV_ESTOQUE` | VARCHAR(1) | Sim | Indica se a OS gera movimento de estoque (S/N). |
| `OS_SITUACAO` | INTEGER | Sim | FK para TB_ORDEM_SERVICO_SIT (situação da OS). |
| `OS_ENDERECO_ENTREGA` | INTEGER | Sim | FK para TB_ENDERECO.END_ID de entrega. |
| `OS_NOTA_FISCAL_PROD` | INTEGER | Sim | FK para TB_NOTA_FISCAL de produtos. |
| `OS_NOTA_FISCAL_SERV` | INTEGER | Sim | FK para TB_NOTA_SERVICO. |
| `OS_VOLUME` | INTEGER | Sim | Quantidade de volumes. |
| `OS_PESO_LIQUIDO` | NUMERIC(15,2) | Sim | Peso líquido (kg). |
| `OS_PESO_BRUTO` | NUMERIC(15,2) | Sim | Peso bruto (kg). |
| `OS_LOCAL_ESTOQUE` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE.LOC_ID de saída. |
| `OS_GARANTIDOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID do garantidor. |
| `OS_DT_VENDA_GARANTIA` | DATE | Sim | Data da venda da garantia. |
| `OS_NF_GARANTIA` | VARCHAR(20) | Sim | Número da NF da garantia. |
| `OS_CERTIFICADO_GARANTIA` | VARCHAR(100) | Sim | Número do certificado de garantia. |
| `OS_REVENDEDOR_GARANTIA` | VARCHAR(100) | Sim | Nome do revendedor da garantia. |
| `OS_GARANTIA_TERCEIROS` | VARCHAR(1) | Sim | Indica se é garantia de terceiros (S/N). |
| `OS_DT_GARANTIA` | DATE | Sim | Data de início da garantia. |
| `OS_DIAS_GARANTIA` | INTEGER | Sim | Quantidade de dias de garantia. |
| `OS_FINANCEIRO_GARANTIDOR` | VARCHAR(1) | Sim | Indica se o garantidor gera financeiro (S/N). |
| `OS_AVISAR_GARANTIA` | VARCHAR(1) | Sim | Indica se deve avisar sobre a garantia (S/N). |
| `OS_ALIQ_PIS` | NUMERIC(15,2) | Sim | Alíquota PIS. |
| `OS_VALOR_PIS` | NUMERIC(15,2) | Sim | Valor PIS. |
| `OS_PIS_RETIDO` | VARCHAR(1) | Sim | PIS retido (S/N). |
| `OS_ALIQ_COFINS` | NUMERIC(15,2) | Sim | Alíquota COFINS. |
| `OS_VALOR_COFINS` | NUMERIC(15,2) | Sim | Valor COFINS. |
| `OS_COFINS_RETIDO` | VARCHAR(1) | Sim | COFINS retido (S/N). |
| `OS_ALIQ_INSS` | NUMERIC(15,2) | Sim | Alíquota INSS. |
| `OS_VALOR_INSS` | NUMERIC(15,2) | Sim | Valor INSS. |
| `OS_INSS_RETIDO` | VARCHAR(1) | Sim | INSS retido (S/N). |
| `OS_ALIQ_IR` | NUMERIC(15,2) | Sim | Alíquota IR. |
| `OS_VALOR_IR` | NUMERIC(15,2) | Sim | Valor IR. |
| `OS_IR_RETIDO` | VARCHAR(1) | Sim | IR retido (S/N). |
| `OS_ALIQ_CSLL` | NUMERIC(15,2) | Sim | Alíquota CSLL. |
| `OS_VALOR_CSLL` | NUMERIC(15,2) | Sim | Valor CSLL. |
| `OS_CSLL_RETIDO` | VARCHAR(1) | Sim | CSLL retido (S/N). |
| `OS_VALOR_DESC_CONDIC` | NUMERIC(15,2) | Sim | Valor de desconto condicional. |
| `OS_VALOR_DESC_INCOND` | NUMERIC(15,2) | Sim | Valor de desconto incondicional. |
| `OS_VALOR_RETENCAO` | NUMERIC(15,2) | Sim | Valor de retenção. |
| `OS_VALOR_OUT_RETENCOES` | NUMERIC(15,2) | Sim | Valor de outras retenções. |
| `OS_VALOR_DEDUCOES` | NUMERIC(15,2) | Sim | Valor de deduções. |
| `OS_VALOR_BC_SERV` | NUMERIC(15,2) | Sim | Base de cálculo do serviço. |
| `OS_VALOR_NFSE` | NUMERIC(15,2) | Sim | Valor da NFS-e. |
| `OS_ALIQ_ISS` | NUMERIC(15,2) | Sim | Alíquota ISS. |
| `OS_VALOR_ISS` | NUMERIC(15,2) | Sim | Valor ISS. |
| `OS_ISS_RETIDO` | VARCHAR(1) | Sim | ISS retido (S/N). |
| `OS_CALCULAR_MANUAL` | VARCHAR(1) | Sim | Indica se o cálculo é manual (S/N). |
| `OS_SUB_TOTAL_SERV` | NUMERIC(15,2) | Sim | Subtotal dos serviços. |
| `OS_SERV_COD_NACIONAL` | VARCHAR(10) | Sim | Código nacional do serviço. |
| `OS_NBS` | VARCHAR(10) | Sim | Código NBS (Nomenclatura Brasileira de Serviços). |
| `OS_SERV_COD_MUNICIPAL` | VARCHAR(10) | Sim | Código municipal do serviço. |
| `OS_SERV_CNAE` | VARCHAR(10) | Sim | Código CNAE do serviço. |
| `OS_CIDADE_SERV` | INTEGER | Sim | FK para TB_CIDADE.CID_ID de prestação do serviço. |
| `OS_CIDADE_INCID` | INTEGER | Sim | FK para TB_CIDADE.CID_ID de incidência. |
| `OS_REGIME_TRIBUTACAO` | INTEGER | Sim | Regime de tributação. |
| `OS_RESP_RETENCAO` | INTEGER | Sim | Responsável pela retenção. |
| `OS_EXIGENCIA_ISS` | INTEGER | Sim | Exigibilidade do ISS. |
| `OS_NR_PROCESSO` | VARCHAR(30) | Sim | Número do processo judicial/admin. |
| `OS_INCENTIVADOR_CULTURAL` | VARCHAR(1) | Sim | Indica se é incentivador cultural (S/N). |
| `OS_LOCAL_TRIB_NFSE` | VARCHAR(1) | Sim | De onde veio a tributação da NFS-e (C=Cliente, P=Produto). |
| `OS_FECHAMENTO` | INTEGER | Sim | Identificador do fechamento de caixa. |
| `OS_TIPO_TROCO` | VARCHAR(1) | Sim | Tipo de troco (D=Devolver, C=Creditar). |
| `OS_GUID` | VARCHAR(50) | Sim | GUID para integração. |
| `OS_GUID_CLIENTE` | VARCHAR(50) | Sim | GUID do cliente (integração). |
| `OS_GUID_FECHAMENTO` | VARCHAR(50) | Sim | GUID do fechamento (integração). |
| `OS_ORDEM_UNIFICADO` | INTEGER | Sim | Identificador unificado (integração entre lojas). |
| `OS_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. |
| `OS_CODIGO_APP` | INTEGER | Sim | Código da OS no app. |
| `OS_VALOR_IMPOSTO` | NUMERIC(15,2) | Sim | Valor do imposto aproximado. |
| `OS_ICMS_DESON_TOTAL` | VARCHAR(1) | Sim | Indica se aplica desoneração total de ICMS (S/N). |
| `OS_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção em listagens (S/N). |
| `OS_BORDERO_COMISSAO` | INTEGER | Sim | FK para TB_BORDERO_COMISSAO. |

COMMENT ON COLUMN TB_ORDEM_SERVICO.OS_STATUS IS 'A - ABERTO
T - EXECUTANDO
E - ENTREGUE';
COMMENT ON COLUMN TB_ORDEM_SERVICO.OS_TEMPO_PREVISTO IS 'Tempo previsto em minutos';
COMMENT ON COLUMN TB_ORDEM_SERVICO.OS_TEMPO_GASTO IS 'Tempo gasto em minutos';
COMMENT ON COLUMN TB_ORDEM_SERVICO.OS_EQUIP_DESC_1 IS 'DESCRIÇÃO EQUIPAMENTO';
COMMENT ON COLUMN TB_ORDEM_SERVICO.OS_EQUIP_DESC_2 IS 'MODELO';
COMMENT ON COLUMN TB_ORDEM_SERVICO.OS_EQUIP_DESC_3 IS 'N SERIE';
COMMENT ON COLUMN TB_ORDEM_SERVICO.OS_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_ORDEM_SERVICO.OS_LAUDO_TECNICO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

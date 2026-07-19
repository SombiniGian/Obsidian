# Tabela TB_NOTA_SERVICO

**Módulo:** Fiscal / Serviços
Cabeçalho da Nota Fiscal de Serviço eletrônica (NFS-e) e do Recibo Provisório de Serviço (RPS). Consolida dados do serviço, retenções, ISS, tomador, municípios, integração, cobrança e situação do documento.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `NS_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `NS_ID` | INTEGER | Não | Identificador único da nota de serviço. Parte da chave primária composta. |
| `NS_SERIE` | VARCHAR(10) | Sim | Série da NFS-e ou do RPS. |
| `NS_NUMERO` | VARCHAR(20) | Sim | Número da nota de serviço ou do RPS. |
| `NS_TIPO` | INTEGER | Sim | Tipo de RPS: 1 = RPS, 2 = Nota Fiscal Conjugada, 3 = Cupom. |
| `NS_DT_EMISSAO` | TIMESTAMP | Sim | Data e hora de emissão da nota de serviço. |
| `NS_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento no sistema. |
| `NS_USUARIO` | INTEGER | Sim | Identificador do usuário que lançou a nota. |
| `NS_NATUREZA_OPERACAO` | INTEGER | Sim | Identificador da natureza de operação (TB_NATUREZA_OPERACAO). |
| `NS_NAT_OP_NFSE` | VARCHAR(10) | Sim | Código da natureza da operação na NFS-e. |
| `NS_STATUS_RPS` | VARCHAR(1) | Sim | Status do RPS: 1 = Normal, 2 = Cancelado. |
| `NS_STATUS_NFSE` | VARCHAR(1) | Sim | Status da NFS-e: 1 = Normal, 2 = Cancelado. |
| `NS_EXIGIBILIDADE_ISS` | INTEGER | Sim | Natureza da operação do ISS: 1 = Exigível, 2 = Não incidência, 3 = Isenção, 4 = Exportação, 5 = Imunidade, 6 = Suspensa por decisão judicial, 7 = Suspensa por processo administrativo. |
| `NS_NR_PROCESSO` | VARCHAR(30) | Sim | Número do processo judicial ou administrativo de suspensão da exigibilidade. |
| `NS_REGIME_TRIBUTACAO` | INTEGER | Sim | Regime especial de tributação da NFS-e. |
| `NS_ISS_RETIDO` | VARCHAR(1) | Sim | Indica se o ISS foi retido (S/N). |
| `NS_RESP_RETENCAO` | INTEGER | Sim | Responsável pela retenção do ISS: 1 = Tomador, 2 = Intermediário. |
| `NS_AMBIENTE_PRODUCAO` | INTEGER | Sim | Ambiente de emissão da NFS-e, como produção ou homologação. |
| `NS_CIDADE_SERVICO` | INTEGER | Sim | Identificador da cidade onde o serviço foi prestado. |
| `NS_CIDADE_SERV_NOME` | VARCHAR(80) | Sim | Nome da cidade onde o serviço foi prestado. |
| `NS_COD_MUNICIPIO_SERV` | INTEGER | Sim | Código do município onde o serviço foi prestado. |
| `NS_CIDADE_INCIDENCIA` | INTEGER | Sim | Identificador da cidade de incidência do ISS. |
| `NS_CIDADE_INCID_NOME` | VARCHAR(80) | Sim | Nome da cidade de incidência do ISS. |
| `NS_COD_MUNICIPIO_INCID` | INTEGER | Sim | Código do município de incidência do ISS. |
| `NS_VALOR_SERVICOS` | NUMERIC(15,2) | Sim | Valor bruto dos serviços. |
| `NS_VALOR_DEDUCOES` | NUMERIC(15,2) | Sim | Valor total das deduções da base de cálculo. |
| `NS_ALIQ_PIS` | NUMERIC(15,2) | Sim | Alíquota do PIS. |
| `NS_VALOR_PIS` | NUMERIC(15,2) | Sim | Valor do PIS. |
| `NS_ALIQ_COFINS` | NUMERIC(15,2) | Sim | Alíquota da COFINS. |
| `NS_VALOR_COFINS` | NUMERIC(15,2) | Sim | Valor da COFINS. |
| `NS_ALIQ_INSS` | NUMERIC(15,2) | Sim | Alíquota do INSS. |
| `NS_VALOR_INSS` | NUMERIC(15,2) | Sim | Valor do INSS. |
| `NS_ALIQ_IR` | NUMERIC(15,2) | Sim | Alíquota do Imposto de Renda retido. |
| `NS_VALOR_IR` | NUMERIC(15,2) | Sim | Valor do Imposto de Renda retido. |
| `NS_ALIQ_CSLL` | NUMERIC(15,2) | Sim | Alíquota da CSLL. |
| `NS_VALOR_CSLL` | NUMERIC(15,2) | Sim | Valor da CSLL. |
| `NS_VALOR_OUT_RETENCOES` | NUMERIC(15,2) | Sim | Valor de outras retenções. |
| `NS_VALOR_BC_ISS` | NUMERIC(15,2) | Sim | Base de cálculo do ISS. |
| `NS_VALOR_ISS` | NUMERIC(15,2) | Sim | Valor do ISS. |
| `NS_ALIQ_ISS` | NUMERIC(18,4) | Sim | Alíquota do ISS. |
| `NS_VALOR_DESC_CONDIC` | NUMERIC(15,2) | Sim | Valor do desconto condicional. |
| `NS_VALOR_DESC_INCOND` | NUMERIC(15,2) | Sim | Valor do desconto incondicional. |
| `NS_SUB_TOTAL` | NUMERIC(15,2) | Sim | Subtotal da nota de serviço. |
| `NS_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total da nota de serviço. |
| `NS_SERVICO_COD_MUNICIPAL` | VARCHAR(10) | Sim | Código municipal do serviço. |
| `NS_SERVICO_COD_NACIONAL` | VARCHAR(10) | Sim | Código nacional do serviço conforme LC 116. |
| `NS_SERVICO_CNAE` | VARCHAR(10) | Sim | Código CNAE do serviço. |
| `NS_SERVICO_DESCRICAO` | VARCHAR(2000) | Sim | Descrição dos serviços prestados. |
| `NS_PESSOA` | INTEGER | Sim | Identificador da pessoa/tomador (TB_PESSOA.PES_ID). |
| `NS_DEST_CNPJ_CPF` | VARCHAR(14) | Sim | CPF ou CNPJ do tomador/destinatário. |
| `NS_DEST_IE` | VARCHAR(18) | Sim | Inscrição Estadual do tomador/destinatário. |
| `NS_DEST_NOME` | VARCHAR(100) | Sim | Nome ou razão social do tomador/destinatário. |
| `NS_DEST_LOGRADOURO` | VARCHAR(100) | Sim | Logradouro do tomador/destinatário. |
| `NS_DEST_NUMERO` | VARCHAR(10) | Sim | Número do endereço do tomador/destinatário. |
| `NS_DEST_COMPLEMENTO` | VARCHAR(10) | Sim | Complemento do endereço do tomador/destinatário. |
| `NS_DEST_CIDADE` | INTEGER | Sim | Identificador da cidade do tomador/destinatário. |
| `NS_DEST_CIDADE_NOME` | VARCHAR(80) | Sim | Nome da cidade do tomador/destinatário. |
| `NS_DEST_BAIRRO` | VARCHAR(50) | Sim | Bairro do tomador/destinatário. |
| `NS_DEST_COD_MUNICIPIO` | INTEGER | Sim | Código do município do tomador/destinatário. |
| `NS_DEST_UF` | VARCHAR(2) | Sim | Unidade federativa do tomador/destinatário. |
| `NS_DEST_CEP` | VARCHAR(10) | Sim | CEP do tomador/destinatário. |
| `NS_DEST_FONE` | VARCHAR(20) | Sim | Telefone do tomador/destinatário. |
| `NS_NUMERO_RPS` | INTEGER | Sim | Número do RPS que originou a nota. |
| `NS_PIS_RETIDO` | VARCHAR(1) | Sim | Indica se o PIS foi retido (S/N). |
| `NS_COFINS_RETIDO` | VARCHAR(1) | Sim | Indica se a COFINS foi retida (S/N). |
| `NS_INSS_RETIDO` | VARCHAR(1) | Sim | Indica se o INSS foi retido (S/N). |
| `NS_IR_RETIDO` | VARCHAR(1) | Sim | Indica se o IR foi retido (S/N). |
| `NS_CSLL_RETIDO` | VARCHAR(1) | Sim | Indica se a CSLL foi retida (S/N). |
| `NS_CALCULAR_MANUAL` | VARCHAR(1) | Sim | Indica se os valores tributários devem ser calculados manualmente (S/N). |
| `NS_VALOR_RETENCAO` | NUMERIC(15,2) | Sim | Valor total das retenções. |
| `NS_MONTAR_DESCRICAO` | VARCHAR(1) | Sim | Indica se a descrição deve ser montada a partir dos itens da NFS-e (S/N). |
| `NS_NBS` | VARCHAR(10) | Sim | Código da Nomenclatura Brasileira de Serviços. |
| `NS_ORDEM_SERVICO` | INTEGER | Sim | Identificador da ordem de serviço vinculada. |
| `NS_EMAIL_ENVIADO` | VARCHAR(1) | Sim | Indica se a nota foi enviada por e-mail (S/N). |
| `NS_EMAIL_DEST` | VARCHAR(100) | Sim | E-mail do destinatário da nota. |
| `NS_BORDERO_COBRANCA` | INTEGER | Sim | Identificador do borderô de cobrança vinculado. |
| `NS_RECEBIMENTO` | INTEGER | Sim | Identificador do recebimento financeiro vinculado. |
| `NS_DEST_INSC_MUNICIPAL` | VARCHAR(20) | Sim | Inscrição Municipal do tomador/destinatário. |
| `NS_DEST_DOC_EXTERIOR` | VARCHAR(20) | Sim | Documento do tomador/destinatário do exterior. |
| `NS_FECHAMENTO_UP` | INTEGER | Sim | Identificador do fechamento financeiro relacionado. |
| `NS_HOSPEDAGEM` | INTEGER | Sim | Identificador da hospedagem relacionada ao serviço. |
| `NS_ALIQ_DEDUCAO` | NUMERIC(15,4) | Sim | Alíquota de dedução aplicada aos serviços. |
| `NS_LOCAL_TRIB_NFSE` | VARCHAR(1) | Sim | Indicador do local de tributação da NFS-e. |
| `NS_OUTRAS_INFORMACOES` | VARCHAR(2000) | Sim | Outras informações da nota de serviço. |
| `NS_INCENTIVADOR_CULTURAL` | VARCHAR(1) | Sim | Indica se o prestador é incentivador cultural (S/N). |

COMMENT ON COLUMN TB_NOTA_SERVICO.NS_TIPO IS 'Código de tipo de RPS
1 - RPS
2 - Nota Fiscal Conjugada (Mista)
3 - Cupom';
COMMENT ON COLUMN TB_NOTA_SERVICO.NS_STATUS_RPS IS 'Código de status do RPS
1 - Normal
2 - Cancelado';
COMMENT ON COLUMN TB_NOTA_SERVICO.NS_STATUS_NFSE IS 'Código de status da NFS-e
1 - Normal
2 - Cancelado';
COMMENT ON COLUMN TB_NOTA_SERVICO.NS_EXIGIBILIDADE_ISS IS 'Código de natureza da operação
1 - Exigível
2 - Não incidência
3 - Isenção
4 - Exportação
5 - Imunidade
6 - Exigibilidade Suspensa por Decisão Judicial
7 - Exigibilidade Suspensa por Processo Administrativo';
COMMENT ON COLUMN TB_NOTA_SERVICO.NS_NR_PROCESSO IS 'Número do processo judicial ou administrativo de suspensão da exigibilidade';
COMMENT ON COLUMN TB_NOTA_SERVICO.NS_REGIME_TRIBUTACAO IS 'Código de identificação do regime especial de tributação
0 - Nenhum
1 - Microempresa municipal
2 - Estimativa
3 - Sociedade de profissionais
4 - Cooperativa
5 - Microempresário Individual (MEI)
6 - Microempresário e Empresa de Pequeno Porte (ME EPP)';
COMMENT ON COLUMN TB_NOTA_SERVICO.NS_RESP_RETENCAO IS 'Identificação do responsável pela retenção do ISS
1 - Tomador
2 - Intermediário';
COMMENT ON COLUMN TB_NOTA_SERVICO.NS_SERVICO_COD_NACIONAL IS 'LC116';
COMMENT ON COLUMN TB_NOTA_SERVICO.NS_MONTAR_DESCRICAO IS 'Percorrer Itens e montar a descrição do serviço na Capa da NFS-e';

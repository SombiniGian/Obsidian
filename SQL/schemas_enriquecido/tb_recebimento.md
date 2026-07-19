# Tabela TB_RECEBIMENTO

**Módulo:** Financeiro
Títulos a receber do ERP: vencimentos, baixas, juros, multa, comissões, cartão de crédito/débito, créditos de clientes e toda a movimentação financeira de vendas e ordens de serviço passa por aqui.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `REC_ID` | INTEGER | Não | Identificador único do recebimento. |
| `REC_EMPRESA` | INTEGER | Não | Identificador da empresa. |
| `REC_TIPO` | VARCHAR(2) | Sim | Tipo do título: CR = Crédito, DP = Duplicata, JR = Juros. |
| `REC_STATUS` | VARCHAR(2) | Sim | Status do título: AB = Aberto, PB = Parcialmente Aberto, BX = Baixado, CN = Cancelado. |
| `REC_CLIENTE` | INTEGER | Sim | Identificador do cliente (TB_PESSOA.PES_ID). |
| `REC_DT_EMISSAO` | DATE | Sim | Data de emissão do título. |
| `REC_DT_VENCIMENTO` | DATE | Sim | Data de vencimento do título. |
| `REC_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro no sistema. |
| `REC_DOCUMENTO` | VARCHAR(20) | Sim | Número do documento (NF, duplicata, fatura). |
| `REC_VALOR` | NUMERIC(15,2) | Sim | Valor original do título. |
| `REC_VALOR_DESCONTO` | NUMERIC(15,2) | Sim | Valor de desconto concedido na baixa. |
| `REC_VALOR_ACRESCIMO` | NUMERIC(15,2) | Sim | Valor de acréscimo aplicado na baixa. |
| `REC_USUARIO` | INTEGER | Sim | Identificador do usuário que lançou o título. |
| `REC_ABERTO` | VARCHAR(1) | Sim | Indicador rápido: S = Documento em Aberto, N = Documento Quitado. |
| `REC_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção do título (auxílio em processos, ex.: borderô). S = Selecionado; NULL ou outra letra = Não Selecionado. |
| `REC_OBSERVACAO` | BLOB SUB_TYPE BINARY SEGMENT SIZE 1000 | Sim | Observações do título em formato binário. NUNCA selecione em queries SELECT. |
| `REC_ORIGEM` | VARCHAR(30) | Não | Sigla/módulo de origem do título (Vendas, OS, Borderô, Manual etc.). |
| `REC_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem. |
| `REC_SERIE` | VARCHAR(1) | Sim | Série do documento fiscal. S = Sim, N = Não. |
| `REC_VALOR_DESC_CARTAO` | NUMERIC(15,2) | Sim | Valor de desconto aplicado pela administradora de cartão. |
| `REC_PAGO_CARTAO` | VARCHAR(1) | Sim | Indica se o título foi pago via cartão: S = Sim, N = Não. |
| `REC_SISTEMA` | VARCHAR(10) | Sim | Indica se é um título gerado pelo sistema (S/N). |
| `REC_BOLETO` | INTEGER | Sim | Identificador do boleto vinculado. |
| `REC_VENDA` | INTEGER | Sim | Identificador do pedido de venda vinculado. |
| `REC_PLANO_CONTAS` | INTEGER | Sim | Identificador do plano de contas contábil. |
| `REC_CAIXA` | INTEGER | Sim | Identificador do caixa (TB_CONTA.CNT_ID) onde foi recebido. |
| `REC_NOSSO_NUMERO` | INTEGER | Sim | Nosso número do boleto bancário. |
| `REC_VALOR_JUROS` | NUMERIC(15,2) | Sim | Valor de juros recebido na baixa. |
| `REC_DIAS_ATRASO` | INTEGER | Sim | Quantidade de dias em atraso na baixa. |
| `REC_COBRAR_JUROS` | VARCHAR(1) | Sim | Indica se cobra juros (S = Sim, N = Não). |
| `REC_JUROS` | NUMERIC(17,4) | Sim | Percentual de juros aplicado (%). |
| `REC_MULTA` | NUMERIC(17,4) | Sim | Percentual/valor de multa aplicado. |
| `REC_VALOR_MULTA` | NUMERIC(15,2) | Sim | Valor final de multa cobrada. |
| `REC_PERC_COMISSAO` | NUMERIC(15,2) | Sim | Percentual de comissão do vendedor sobre o título. |
| `REC_VALOR_COMISSAO` | NUMERIC(15,2) | Sim | Valor calculado da comissão. |
| `REC_VENDEDOR` | INTEGER | Sim | Identificador do vendedor (TB_PESSOA.PES_ID). |
| `REC_VENC_ORIGINAL` | DATE | Sim | Data de vencimento original (antes de renegociações). |
| `REC_BOLETO_ANTECIPADO` | VARCHAR(1) | Sim | Indica se o boleto foi antecipado (S/N). |
| `REC_CONTA_DEBITO` | INTEGER | Sim | Conta contábil de débito do título. |
| `REC_CONTA_CREDITO` | INTEGER | Sim | Conta contábil de crédito do título. |
| `REC_PESSOA` | INTEGER | Sim | Identificador da pessoa (TB_PESSOA.PES_ID) — referência alternativa ao cliente. |
| `REC_ESPECIE_MOEDA` | INTEGER | Sim | Identificador da espécie de moeda (TB_ESPECIE_MOEDA.ESP_ID). |
| `REC_MOVIMENTAR` | VARCHAR(2) | Sim | Tipo de movimentação financeira gerada (CX, CB, CH, CE, CC, CR). |
| `REC_ID_MOVIMENTO` | INTEGER | Sim | Identificador do movimento financeiro gerado (TB_MOVIMENTO_CONTA.MOV_ID). |
| `REC_PARCELA` | VARCHAR(3) | Sim | Identificador da parcela (ex.: 001). |
| `REC_NR_PARCELAS` | INTEGER | Sim | Número total de parcelas do título. |
| `REC_TIPO_MULTA` | VARCHAR(1) | Sim | Tipo da multa: 1 = Valor, 2 = Porcentagem. |
| `REC_TIPO_JUROS` | VARCHAR(1) | Sim | Tipo dos juros: 1 = Valor, 2 = Porcentagem. |
| `REC_QTDE_REPLICAR` | INTEGER | Sim | Quantidade de vezes que o título foi replicado (parcelamento). |
| `REC_INTERVALO_DIAS` | INTEGER | Sim | Intervalo em dias entre as parcelas. |
| `REC_OS_TIPO` | VARCHAR(1) | Sim | Tipo da ordem de serviço: S = Serviços, P = Produtos. |
| `REC_NOTA_FISCAL` | INTEGER | Sim | ID do documento fiscal atrelado ao financeiro. |
| `REC_DESTACAR_DEDUCOES` | VARCHAR(1) | Sim | Indica se destaca deduções na impressão (S/N). |
| `REC_OBS_BOLETO` | VARCHAR(1) | Sim | Indica se imprime observações do boleto (S/N). |
| `REC_CARTAO_CREDITO` | INTEGER | Sim | Identificador da administradora de cartão de crédito. |
| `REC_AVALISTA` | INTEGER | Sim | Identificador do avalista (TB_PESSOA.PES_ID). |
| `REC_CESSAO_TITULO` | VARCHAR(1) | Sim | Indica se o título foi cedido (S/N). |
| `REC_ORDEM_SERVICO` | INTEGER | Sim | Identificador da ordem de serviço vinculada. |
| `REC_NOTA_SERVICO` | INTEGER | Sim | Identificador da nota de serviço vinculada. |
| `REC_TAXA_CARTAO` | NUMERIC(15,2) | Sim | Taxa administrativa do cartão. |
| `REC_BORDERO_COMISSAO` | INTEGER | Sim | Identificador do borderô de comissão ao qual o título pertence. |
| `REC_FECHAMENTO` | INTEGER | Sim | Identificador do fechamento de caixa. |
| `REC_INTEGRACAO` | INTEGER | Sim | Identificador do processo de integração relacionado. |
| `REC_CNPJ_CREDENCIADORA` | VARCHAR(14) | Sim | CNPJ da credenciadora do cartão. |
| `REC_BANDEIRA` | VARCHAR(2) | Sim | Bandeira do cartão. |
| `REC_TEF_NSU` | VARCHAR(100) | Sim | NSU da transação TEF. |
| `REC_CREDENCIADORA` | VARCHAR(100) | Sim | Nome da credenciadora do cartão. |
| `CAMPO_8` | VARCHAR(25) | Sim | Campo legado/reservado. |
| `REC_SEM_BX_ADM` | VARCHAR(1) | Sim | Indica se o título não passa pela baixa administrativa (S/N). |
| `REC_CENTRO_CUSTO` | INTEGER | Sim | Identificador do centro de custo (TB_CENTRO_CUSTO.CEN_ID). |
| `REC_ID_CARTEIRA_DIGITAL` | VARCHAR(50) | Sim | ID da carteira digital. |
| `REC_NOME_CARTEIRA_DIGITAL` | VARCHAR(100) | Sim | Nome da carteira digital. |
| `REC_CODIGO_PSP` | VARCHAR(50) | Sim | Código do PSP (provedor de pagamento). |
| `REC_PIX` | INTEGER | Sim | Identificador do PIX vinculado. |
| `REC_GUID` | VARCHAR(50) | Sim | GUID para integração. |
| `REC_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. Default: current_timestamp. |
| `REC_ID_PAGARME` | VARCHAR(100) | Sim | ID do título no Pagar.me. |
| `REC_STONE_CODE` | VARCHAR(100) | Sim | Código do título na Stone. |
| `REC_ID_SERVIDOR` | INTEGER | Sim | Identificador do servidor de origem. |
| `REC_ID_LOCAL` | INTEGER | Sim | Identificador do local/loja de origem. |
| `REC_ESTACAO_PDV` | INTEGER | Sim | Estação PDV de origem. |
| `REC_CODIGO_AUT` | VARCHAR(200) | Sim | Código de autorização da transação. |

COMMENT ON COLUMN TB_RECEBIMENTO.REC_TIPO IS 'REC_TIPO
--------
CR -> CRÉDITO
DP -> DUPLICATA
JR -> JUROS';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_STATUS IS 'REC_STATUS
------------
AB -> ABERTO
PB -> PARCIAMENTE ABERTO
BX -> BAIXADO
CN -> CANCELADO';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_DT_LANCAMENTO IS 'REC_DT_LANCAMENTO
-----------------
DATA E HORA DE LANÇAMENTO DO REGISTRO NO SISTEMA';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_ABERTO IS 'REC_ABERTO
----------
S -> DOCUMENTO EM ABERTO
N -> DOCUMENTO QUITADO';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_SELECIONADO IS 'REC_SELECIONA
-------------
CAMPO UTILIZADO PARA AUXILIAR OS PROCESSOS
DE SELEÇÃO DE DOCUMENTOS PARA PROCESSAR BORDERÔ
''S'' -> SELECIONADO
NULL OU QUALQUER OUTRA LETRA -> NÃO SELECIONADO';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_SERIE IS 'REC_SERIE
S - SIM
N - NÃO';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_PAGO_CARTAO IS 'REC_PAGO_CARTAO
---------
''S'' -> SIM
''N'' -> NÃO';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_SISTEMA IS 'REC_SISTEMA
''S'' -> SIM
''N'' -> NÃO';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_NOSSO_NUMERO IS 'Campo pelo qual Boleto';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_COBRAR_JUROS IS 'S - SIM
N - NAO';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_JUROS IS 'Porcentagem (%)';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_TIPO_MULTA IS '1 - VALOR
2 - PORCENTAGEM';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_TIPO_JUROS IS '1 - VALOR
2 - PORCENTAGEM';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_OS_TIPO IS 'S - SERVIÇOS
  p - PRODUTOS';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_NOTA_FISCAL IS 'ID do documento fiscal atrelado ao financeiro';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_RECEBIMENTO.REC_ORIGEM IS 'Para localizar títulos de venda utilize WHERE REC_ORIGEM = ''VENDA'' e JOIN com TB_PEDIDO_VENDA via REC_ID_ORIGEM = PEV_ID';
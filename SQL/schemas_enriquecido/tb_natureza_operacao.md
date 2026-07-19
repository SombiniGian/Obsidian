# Tabela TB_NATUREZA_OPERACAO

**Módulo:** Fiscal
Natureza de operação utilizada em notas fiscais de entrada/saída, pedido de venda, ordem de serviço, pedido de compra. Define CFOP, CST, regras de cálculo de impostos, geração de financeiro/estoque, finalidade e comportamento em produção.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `NOP_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `NOP_ID` | INTEGER | Não | Identificador único da natureza de operação. Parte da chave primária composta. |
| `NOP_DESCRICAO` | VARCHAR(100) | Sim | Descrição interna da natureza de operação. |
| `NOP_DESCRICAO_NF` | VARCHAR(100) | Sim | Descrição exibida na nota fiscal. |
| `NOP_TIPO` | VARCHAR(1) | Sim | Tipo da natureza: E=Entrada, S=Saída. |
| `NOP_EMITIR_RECEBER` | VARCHAR(1) | Sim | Operação: E=Emitir, R=Receber. |
| `NOP_CFOP` | VARCHAR(4) | Sim | CFOP principal (estadual). |
| `NOP_CST` | VARCHAR(4) | Sim | CST de ICMS. |
| `NOP_DESTINATARIO_REMETENTE` | VARCHAR(1) | Sim | Indica destinatário/remetente padrão: C=Cliente, F=Fornecedor. |
| `NOP_GERA_FINANCEIRO` | VARCHAR(1) | Sim | Gera financeiro (contas a pagar/receber) (S/N). |
| `NOP_MOVIMENTA_ESTOQUE` | VARCHAR(1) | Sim | Movimenta estoque (S/N). |
| `NOP_MENSAGEM` | BLOB SUB_TYPE BINARY SEGMENT SIZE 1000 | Sim | Mensagem/corpo adicional em binário. NUNCA selecione em queries SELECT. |
| `NOP_STATUS` | VARCHAR(1) | Sim | Status: A=Ativo, I=Inativo. |
| `NOP_CALCULA_ICMS` | VARCHAR(1) | Sim | Calcula ICMS (S/N). |
| `NOP_PADRAO` | VARCHAR(1) | Sim | Indica se é a natureza padrão (S/N). |
| `NOP_EXPORTAR` | VARCHAR(1) | Sim | Indica se é exportada para integrações (S/N). |
| `NOP_CFOP_GRUPO` | INTEGER | Sim | FK para grupo de CFOP. |
| `NOP_ALIQ_CREDITO_ICMS` | NUMERIC(15,2) | Sim | Alíquota de crédito de ICMS. |
| `NOP_PEDIR_LIBERACAO` | VARCHAR(1) | Sim | Exige liberação para uso (S/N). |
| `NOP_PRECO_UTILIZAR` | VARCHAR(1) | Sim | Preço a utilizar: V=Venda, C=Custo. |
| `NOP_FINALIDADE` | INTEGER | Sim | Finalidade da NF: 1=Normal, 2=Complementar, 3=Ajuste, 4=Devolução/Retorno. |
| `NOP_MODELO` | VARCHAR(2) | Sim | Modelo do documento (55, 65 etc.). |
| `NOP_SERIE` | INTEGER | Sim | Série da NF. |
| `NOP_PLANO_CONTAS` | INTEGER | Sim | FK para plano de contas. |
| `NOP_IND_PRESENCA` | INTEGER | Sim | Indicador de presença na NF: 0=Não se aplica, 1=Presencial, 2=Internet, 3=Teleatendimento, 4=NFC-e entrega, 5=Presencial fora, 9=Outros. |
| `NOP_CFOP_INTERESTADUAL` | VARCHAR(4) | Sim | CFOP para operações interestaduais. |
| `NOP_MSG_FISCAL` | INTEGER | Sim | Mensagem fiscal aplicável. |
| `NOP_MOV_EST_GERENCIAL` | VARCHAR(1) | Sim | Movimenta estoque gerencial (S/N). |
| `NOP_ATUALIZAR_CUSTO` | VARCHAR(1) | Sim | Atualiza custo dos produtos (S/N). |
| `NOP_PADRAO_COMPRA` | VARCHAR(1) | Sim | Indica se é a natureza padrão de compras (S/N). |
| `NOP_CTE_MODALIDADE` | INTEGER | Sim | Modalidade do CT-e. |
| `NOP_CTE_TIPO` | INTEGER | Sim | Tipo do CT-e. |
| `NOP_CTE_TIPO_SERV` | INTEGER | Sim | Tipo de serviço do CT-e. |
| `NOP_GRUPO_FATURA` | VARCHAR(1) | Sim | Inclui no grupo de dados de cobrança (S/N). |
| `NOP_GRUPO_FORMA_PAGTO` | VARCHAR(1) | Sim | Inclui no grupo de forma de pagamento (S/N). |
| `NOP_FORMA_PAGTO_OBS` | VARCHAR(1) | Sim | Exibe forma de pagamento na observação da NF (S/N). |
| `NOP_GRUPO_REPASSE` | VARCHAR(1) | Sim | Grupo de repasse de ICMS (S/N). |
| `NOP_GRUPO_ICMS_EFETIVO` | VARCHAR(1) | Sim | Grupo de ICMS efetivo (S/N). |
| `NOP_GERAR_OP` | VARCHAR(1) | Sim | Gera ordem de produção (S/N). |
| `NOP_NFSE_TRIBUTACAO` | INTEGER | Sim | Regime de tributação da NFS-e (0=Nenhum, 1=Micro municipal, 2=Estimativa, 3=Sociedade, 4=Cooperativa, 5=MEI, 6=ME/EPP). |
| `NOP_NFSE_COD_NACIONAL` | VARCHAR(10) | Sim | Código nacional do serviço (LC116). |
| `NOP_NFSE_COD_MUNICIPAL` | VARCHAR(10) | Sim | Código municipal do serviço. |
| `NOP_TIPO_PADRAO_ENT` | VARCHAR(2) | Sim | Tipo padrão de entrada (00=Revenda, 01=MP, 02=Embalagem, 03=Processo, 04=Acabado, 05=Subproduto, 06=Intermediário, 07=Uso Consumo, 08=Ativo, 09=Serviços, 10=Outros, 99=Outras). |
| `NOP_MARKUP_PADRAO_ENT` | NUMERIC(15,2) | Sim | Markup padrão aplicado na entrada. |
| `NOP_IPI_ENT` | VARCHAR(1) | Sim | Considera IPI na entrada (S/N). |
| `NOP_ABRIR_TELA_NF` | VARCHAR(1) | Sim | Abre tela de NF automaticamente (S/N). |
| `NOP_VENDEDOR_OBS` | VARCHAR(1) | Sim | Inclui vendedor na observação (S/N). |
| `NOP_PROD_REVENDA` | VARCHAR(1) | Sim | Tipo de produto: Revenda (S/N). |
| `NOP_PROD_SERVICO` | VARCHAR(1) | Sim | Tipo de produto: Serviço (S/N). |
| `NOP_PROD_MAT_PRIMA` | VARCHAR(1) | Sim | Tipo de produto: Matéria-prima (S/N). |
| `NOP_PROD_USO_CONSUMO` | VARCHAR(1) | Sim | Tipo de produto: Uso e consumo (S/N). |
| `NOP_PROD_BALANCA` | VARCHAR(1) | Sim | Tipo de produto: Balança (S/N). |
| `NOP_PROD_ACABADO` | VARCHAR(1) | Sim | Tipo de produto: Acabado (S/N). |
| `NOP_PROD_COMB` | VARCHAR(1) | Sim | Tipo de produto: Combustível (S/N). |
| `NOP_PROD_PROCESSO` | VARCHAR(1) | Sim | Tipo de produto: Em processo (S/N). |
| `NOP_PROD_EMBALAGEM` | VARCHAR(1) | Sim | Tipo de produto: Embalagem (S/N). |
| `NOP_PROD_RESTAURANTE` | VARCHAR(1) | Sim | Tipo de produto: Restaurante (S/N). |
| `NOP_PROD_KIT` | VARCHAR(1) | Sim | Tipo de produto: Kit (S/N). |
| `NOP_PROD_ATIVO` | VARCHAR(1) | Sim | Tipo de produto: Ativo imobilizado (S/N). |
| `NOP_PROD_DESMEMBRAVEL` | VARCHAR(1) | Sim | Tipo de produto: desmembrável (S/N). |
| `NOP_PEDIDO_OBS` | VARCHAR(1) | Sim | Leva a observação do pedido para a NF (S/N). |
| `NOP_ESPECIE_MOEDA_ENT` | INTEGER | Sim | Espécie de moeda da entrada. |
| `NOP_ZERAR_BC` | VARCHAR(1) | Sim | Zera base de cálculo (S/N). |
| `NOP_IMPORTACAO` | VARCHAR(1) | Sim | Indica se é natureza de importação (S/N). |
| `NOP_CST_IMPORTADOS` | VARCHAR(2) | Sim | CST para produtos importados. |
| `NOP_ORIGEM_IMPORTADOS` | INTEGER | Sim | Origem da mercadoria importada (0 a 8). |
| `NOP_ICMS_ALIQ_IMP` | NUMERIC(15,2) | Sim | Alíquota de ICMS para importados. |
| `NOP_FCP_ALIQ_IMP` | NUMERIC(15,2) | Sim | Alíquota de FCP para importados. |
| `NOP_COD_REF_INF` | VARCHAR(1) | Sim | Código de referência de informação. |
| `NOP_LOCAL_ESTOQUE` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE.LOC_ID. |
| `NOP_VALOR_MAXIMO` | NUMERIC(15,2) | Sim | Valor máximo permitido para esta natureza. |
| `NOP_MAX_ITENS` | INTEGER | Sim | Quantidade máxima de itens permitidos. |
| `NOP_CALCULAR_IMPOSTO_PEDIDO` | VARCHAR(1) | Sim | Calcula imposto no pedido (S/N). |
| `NOP_ENTREGA_FUTURA` | VARCHAR(1) | Sim | Indica se é entrega futura (S/N). |
| `NOP_CALCULAR_DIFAL` | VARCHAR(1) | Sim | Calcula DIFAL (S/N). |
| `NOP_ICMS_DESON_TOTAL` | VARCHAR(1) | Sim | ICMS desonerado total (S/N). |
| `NOP_TIPO_DT_ENTRADA` | VARCHAR(1) | Sim | Define o tipo da data de entrada. |
| `NOP_ENVIA_INFADPROD` | VARCHAR(1) | Sim | Envia infAdProd no XML (S/N). Default 'N'. |
| `NOP_IND_INTERMEDIADOR` | INTEGER | Sim | Indicador de intermediador (NFS-e). |
| `NOP_INTERMEDIDOR` | INTEGER | Sim | Intermediador configurado. |
| `NOP_PROD_MEDICAMENTO` | VARCHAR(1) | Sim | Tipo de produto: Medicamento (S/N). Default 'S'. |
| `NOP_PERMITE_DESC_CONDICIONAL` | VARCHAR(1) | Sim | Permite desconto condicional (S/N). |
| `NOP_NAO_IMPRIMIR_LOTE_DETALHADO` | VARCHAR(1) | Sim | Não imprime lote detalhado (S/N). |
| `NOP_CTE_REMETENTE` | VARCHAR(3) | Sim | Tipo do remetente no CT-e. |
| `NOP_CTE_DESTINATARIO` | VARCHAR(3) | Sim | Tipo do destinatário no CT-e. |
| `NOP_CTE_EXPEDIDOR` | VARCHAR(3) | Sim | Tipo do expedidor no CT-e. |
| `NOP_CTE_RECEBEDOR` | VARCHAR(3) | Sim | Tipo do recebedor no CT-e. |
| `NOP_VALOR_MAX_SEM_ID` | NUMERIC(15,4) | Sim | Valor máximo permitido sem identificação do destinatário. |
| `NOP_GERA_CASHBACK` | VARCHAR(1) | Sim | Gera cashback (S/N). |
| `NOP_TIPO_CASHBACK` | VARCHAR(1) | Sim | Tipo do cashback gerado. |
| `NOP_VALOR_CASHBACK` | NUMERIC(15,1) | Sim | Valor do cashback. |
| `NOP_VOLUME_INF_ADICIONAL` | VARCHAR(1) | Sim | Inclui volume em infAdicional (S/N). |
| `NOP_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. |
| `NOP_PROD_ARMA` | VARCHAR(1) | Sim | Tipo de produto: Armamento (S/N). |
| `NOP_PROD_VEICULO` | VARCHAR(1) | Sim | Tipo de produto: Veículo (S/N). |
| `NOP_SITUACAO_DOCUMENTO` | VARCHAR(2) | Sim | Situação do documento fiscal. |
| `NOP_SOMAR_II` | VARCHAR(1) | Sim | Soma II no total (S/N). |
| `NOP_SOMAR_PIS_COFINS` | VARCHAR(1) | Sim | Soma PIS/COFINS no total (S/N). |
| `NOP_SOMAR_ICMS` | VARCHAR(1) | Sim | Soma ICMS no total (S/N). |
| `NOP_ZERAR_BC_PIS_COFINS` | VARCHAR(1) | Sim | Zera BC PIS/COFINS (S/N). |
| `NOP_ZERAR_IPI` | VARCHAR(1) | Sim | Zera IPI (S/N). |
| `NOP_ICMS_RED_IMP` | NUMERIC(15,2) | Sim | Redução de ICMS na importação. |
| `NOP_ICMS_DIF_IMP` | NUMERIC(15,2) | Sim | DIFAL de ICMS na importação. |
| `NOP_NAO_VALIDAR_VALIDADE_LOTE` | VARCHAR(1) | Sim | Não valida validade do lote (S/N). |
| `NOP_REGRA_TRIBUTARIA` | INTEGER | Sim | Regra tributária aplicada (IBS/CBS). |

COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_TIPO IS 'NOP_TIPO
E - ENTRADA
S - SAÍDA';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_EMITIR_RECEBER IS 'NOP_EMITIR_RECEBER  
E - EMITIR
R - RECEBER';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_DESTINATARIO_REMETENTE IS 'NOP_DESTINATARIO_REMETENTE
C - CLIENTE
F - FORNECEDOR';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_GERA_FINANCEIRO IS 'S - SIM
N - NÃO';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_MOVIMENTA_ESTOQUE IS 'S - SIM
N - NÃO';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_STATUS IS 'A - ATIVO
I - INATIVO';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_CALCULA_ICMS IS 'S - SIM
N - NÃO';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_PADRAO IS 'S - SIM
N - NAO';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_PEDIR_LIBERACAO IS 'S - SIM
N - NÃO';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_PRECO_UTILIZAR IS 'V - VENDA
C - CUSTO';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_FINALIDADE IS '1 - NORMAL
2 - COMPLEMENTAR
3 - AJUSTE
4 - DEVOLUCAO / RETORNO';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_IND_PRESENCA IS '0=Não se aplica; 1=Presencial; 2=Não presencial Internet; 3=Teleatendimento; 4=NFC-e com entrega a domicílio; 5=Presencial fora do estabelecimento; 9=Outros.';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_GRUPO_FATURA IS 'Dados Cobrança';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_FORMA_PAGTO_OBS IS 'Sair forma pagto na observação da nota fiscal';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_NFSE_TRIBUTACAO IS 'Código de identificação do regime especial de tributação:
0 - Nenhum
1 - Microempresa municipal
2 - Estimativa
3 - Sociedade de profissionais
4 - Cooperativa
5 - Microempreendedor Individual (MEI)
6 - ME/EPP';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_TIPO_PADRAO_ENT IS '00 - MERCADORIA PARA REVENDA
01 - MATÉRIA-PRIMA
02 - EMBALAGEM
03 - PRODUTO EM PROCESSO
04 - PRODUTO ACABADO
05 - SUBPRODUTO
06 - PRODUTO INTERMEDIÁRIO
07 - MATERIAL DE USO E CONSUMO
08 - ATIVO IMOBILIZADO
09 - SERVIÇOS
10 - OUTROS INSUMOS
99 - OUTRAS';
COMMENT ON COLUMN TB_NATUREZA_OPERACAO.NOP_MENSAGEM IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

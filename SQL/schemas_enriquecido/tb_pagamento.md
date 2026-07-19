# Tabela TB_PAGAMENTO

**Módulo:** Financeiro / Contas a Pagar
Tabela principal de títulos/contas a pagar. Armazena duplicatas, juros e créditos gerados a partir de diversas origens (NF-e, OS, pedido de compra, movimento manual). Suporta replicação em N parcelas com intervalo de dias, controle de juros/multa, vínculo com borderôs de pagamento, cartão de crédito, plano de contas, espécie de moeda e movimentação financeira (gera movimento em TB_MOVIMENTO_CONTA).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PAG_ID` | INTEGER | Não | Identificador único do pagamento. |
| `PAG_EMPRESA` | INTEGER | Não | Identificador da empresa. |
| `PAG_TIPO` | VARCHAR(2) | Sim | Tipo do título (DP=Duplicata, JR=Juros, CR=Crédito). |
| `PAG_STATUS` | VARCHAR(2) | Sim | Status do título (AB=Aberto, PB=Parcialmente Aberto, BX=Baixado, CN=Cancelado). |
| `PAG_DT_EMISSAO` | DATE | Sim | Data de emissão do título. |
| `PAG_DT_VENCIMENTO` | DATE | Sim | Data de vencimento do título. |
| `PAG_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro no sistema. |
| `PAG_DT_COMPETENCIA` | DATE | Sim | Data de competência contábil. |
| `PAG_DOCUMENTO` | VARCHAR(20) | Sim | Número do documento/título. |
| `PAG_VALOR` | NUMERIC(15,2) | Sim | Valor do título. |
| `PAG_VALOR_DESCONTO` | NUMERIC(15,2) | Sim | Valor de desconto. |
| `PAG_VALOR_ACRESCIMO` | NUMERIC(15,2) | Sim | Valor de acréscimo. |
| `PAG_VALOR_JUROS` | NUMERIC(15,2) | Sim | Valor de juros. |
| `PAG_VALOR_MULTA` | NUMERIC(15,2) | Sim | Valor de multa. |
| `PAG_JUROS` | NUMERIC(17,4) | Sim | Percentual/valor base de juros. |
| `PAG_MULTA` | NUMERIC(17,4) | Sim | Percentual/valor base de multa. |
| `PAG_TIPO_MULTA` | VARCHAR(1) | Sim | Tipo de multa (P=Percentual, V=Valor). |
| `PAG_TIPO_JUROS` | VARCHAR(1) | Sim | Tipo de juros (P=Percentual, V=Valor). |
| `PAG_USUARIO` | INTEGER | Sim | Identificador do usuário que lançou o título. |
| `PAG_ABERTO` | VARCHAR(1) | Sim | Indica se o documento está em aberto (S=Sim, N=Não/Quitado). |
| `PAG_SELECIONADO` | VARCHAR(1) | Sim | Marcador para seleção em processos (S/N). |
| `PAG_OBSERVACAO` | BLOB SUB_TYPE BINARY SEGMENT SIZE 1000 | Sim | Observações em formato binário. NUNCA selecione em queries SELECT. |
| `PAG_ORIGEM` | VARCHAR(30) | Não | Sigla do módulo/rotina de origem (ex.: NOTAFISCAL, COMPRA, MANUAL). |
| `PAG_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem. |
| `PAG_PLANO_CONTAS` | INTEGER | Sim | FK para TB_PLANO_CONTA. |
| `PAG_CAIXA` | INTEGER | Sim | FK para TB_FECHAMENTO_CAIXA. |
| `PAG_SISTEMA` | VARCHAR(1) | Sim | Indica se é um título gerado pelo sistema (S/N). |
| `PAG_CONTA_DEBITO` | INTEGER | Sim | FK para TB_CONTA.CNT_ID de débito (conta contábil). |
| `PAG_CONTA_CREDITO` | INTEGER | Sim | FK para TB_CONTA.CNT_ID de crédito (conta contábil). |
| `PAG_QTDE_REPLICAR` | INTEGER | Sim | Quantidade de parcelas para replicar (geração de N títulos). |
| `PAG_INTERVALO_DIAS` | INTEGER | Sim | Intervalo em dias entre as parcelas replicadas. |
| `PAG_PARCELA` | INTEGER | Sim | Número da parcela atual. |
| `PAG_NR_PARCELAS` | INTEGER | Sim | Quantidade total de parcelas. |
| `PAG_PESSOA` | INTEGER | Sim | FK para TB_PESSOA.PES_ID do fornecedor/credor. Use JOIN por PES_ID. |
| `PAG_ESPECIE_MOEDA` | INTEGER | Sim | FK para TB_ESPECIE_MOEDA.ESP_ID. |
| `PAG_MOVIMENTAR` | VARCHAR(2) | Sim | Indica se deve gerar movimento financeiro e tipo (S=Sim, N=Não). |
| `PAG_ID_MOVIMENTO` | INTEGER | Sim | FK para TB_MOVIMENTO_CONTA gerada. |
| `PAG_ORIGEM_ITEM` | INTEGER | Sim | FK para o item de origem (quando aplicável). |
| `PAG_CARTAO_CREDITO` | INTEGER | Sim | FK para TB_CARTAO_CREDITO_PLANILHA. |
| `PAG_BANDEIRA` | VARCHAR(2) | Sim | Bandeira do cartão (quando aplicável). |
| `PAG_CENTRO_CUSTO` | INTEGER | Sim | FK para TB_CENTRO_CUSTO.CEN_ID. |
| `PAG_LINHA_DIGITAVEL` | VARCHAR(100) | Sim | Linha digitável do boleto (quando gerado). |
| `PAG_COBRAR_JUROS` | VARCHAR(1) | Sim | Indica se cobra juros após vencimento (S/N). |
| `PAG_DIAS_ATRASO` | INTEGER | Sim | Dias de atraso do título. |
| `PAG_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. |

COMMENT ON COLUMN TB_PAGAMENTO.PAG_TIPO IS 'DP -> DUPLICATA
JR -> JUROS
CR -> CRÉDITO';
COMMENT ON COLUMN TB_PAGAMENTO.PAG_STATUS IS 'AB -> ABERTO
PB -> PARCIALMENTE ABERTO
BX -> BAIXADO
CN -> CANCELADO';
COMMENT ON COLUMN TB_PAGAMENTO.PAG_ABERTO IS 'S -> DOCUMENTO EM ABERTO
N -> DOCUMENTO QUITADO';
COMMENT ON COLUMN TB_PAGAMENTO.PAG_SELECIONADO IS 'CAMPO UTILIZADO PARA AUXILIAR OS PROCESSOS DE SELEÇÃO DE DOCUMENTOS PARA PROCESSAR BORDERÔ
''S'' -> SELECIONADO
NULL OU QUALQUER OUTRA LETRA -> NÃO SELECIONADO';
COMMENT ON COLUMN TB_PAGAMENTO.PAG_QTDE_REPLICAR IS 'Qtde de Parcelas para replicar';
COMMENT ON COLUMN TB_PAGAMENTO.PAG_INTERVALO_DIAS IS 'Intervalo de Dias para vencimento ao replicar';
COMMENT ON COLUMN TB_PAGAMENTO.PAG_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

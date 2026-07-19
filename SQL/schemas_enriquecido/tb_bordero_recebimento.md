# Tabela TB_BORDERO_RECEBIMENTO

**Módulo:** Financeiro
Gera um borderô com os recebimentos que foram baixados em lote, consolidando totais de cheques, créditos, juros e descontos, vinculando-se a um caixa, fechamento e conta. É o cabeçalho do borderô; seus itens vivem em TB_BORDERO_RECEBIMENTO_ITEM e as formas de pagamento em TB_BORDERO_RECEBIMENTO_VALORES.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BDR_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `BDR_ID` | INTEGER | Não | Identificador único do borderô de recebimento. Parte da chave primária composta. |
| `BDR_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do borderô no sistema. |
| `BDR_DT_EMISSAO` | DATE | Sim | Data de emissão do borderô. |
| `BDR_QUANTIDADE_CHEQUE` | INTEGER | Sim | Quantidade de cheques incluídos no borderô. |
| `BDR_VALOR_CHEQUE` | NUMERIC(15,2) | Sim | Valor total dos cheques incluídos no borderô. |
| `BDR_QUANTIDADE_RECEBIMENTO` | INTEGER | Sim | Quantidade de títulos (recebimentos) baixados no borderô. |
| `BDR_VALOR_RECEBIMENTO` | NUMERIC(15,2) | Sim | Valor total dos recebimentos baixados. |
| `BDR_QUANTIDADE_CREDITO` | INTEGER | Sim | Quantidade de créditos gerados pelo borderô. |
| `BDR_VALOR_CREDITO` | NUMERIC(15,2) | Sim | Valor total dos créditos gerados. |
| `BDR_QUANTIDADE_JUROS` | INTEGER | Sim | Quantidade de títulos que receberam juros. |
| `BDR_VALOR_JUROS` | NUMERIC(15,2) | Sim | Valor total de juros recebidos nos itens do borderô. |
| `BDR_VALOR_TOTAL_RECEBER` | NUMERIC(15,2) | Sim | Valor total a receber (soma dos títulos baixados). |
| `BDR_VALOR_RECEBIDO_DINHEIRO` | NUMERIC(15,2) | Sim | Valor recebido em dinheiro. |
| `BDR_VALOR_RECEBIDO_CARTAO` | NUMERIC(15,2) | Sim | Valor recebido em cartão. |
| `BDR_VALOR_RECEBIDO_TOTAL` | NUMERIC(15,2) | Sim | Valor total recebido no borderô. |
| `BDR_USUARIO` | INTEGER | Sim | Identificador do usuário responsável pelo lançamento do borderô. |
| `BDR_STATUS` | VARCHAR(2) | Não | Status do borderô: 'A' = Ativo; 'C' = Cancelado. |
| `BDR_GERA_CREDITO` | VARCHAR(1) | Sim | Indica se o borderô gera crédito para o cliente (S = Sim, N = Não). |
| `BDR_VALOR_MOV_BANCARIA` | NUMERIC(15,2) | Sim | Valor da movimentação bancária gerada pelo borderô. |
| `BDR_CAIXA` | INTEGER | Sim | Identificador do caixa (TB_CONTA.CNT_ID) associado ao borderô. |
| `BDR_FECHAMENTO` | INTEGER | Sim | Identificador do fechamento de caixa ao qual o borderô pertence. |
| `BDR_CONTA` | INTEGER | Sim | Identificador do plano de contas para contra partida de outros movimentos. |
| `BDR_PESSOA` | INTEGER | Sim | Identificador do cliente/pessoa (TB_PESSOA.PES_ID) principal do borderô. |
| `BDR_ORIGEM` | VARCHAR(10) | Sim | Sigla do módulo de origem do borderô (ex.: Vendas, OS). |
| `BDR_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem (ex.: pedido de venda, ordem de serviço). |
| `BDR_TIPO_ACRESCIMO` | VARCHAR(1) | Sim | Tipo do acréscimo aplicado (V = Valor, P = Percentual). |
| `BDR_ACRESCIMO` | NUMERIC(15,2) | Sim | Valor do acréscimo aplicado ao borderô. |
| `BDR_TIPO_DESCONTO` | VARCHAR(1) | Sim | Tipo do desconto aplicado (V = Valor, P = Percentual). |
| `BDR_DESCONTO` | NUMERIC(15,2) | Sim | Valor do desconto aplicado ao borderô. |
| `BDR_TIPO_TROCO` | VARCHAR(1) | Sim | Destino do troco (T = Lançou Troco, C = Lançou Crédito, D = Descartou). |
| `BDR_CAIXA_TROCO` | INTEGER | Sim | Identificador do caixa de destino do troco. |
| `BDR_VALOR_PAGAMENTOS` | NUMERIC(15,2) | Sim | Valor total dos pagamentos (espécies de moeda) associados ao borderô. |
| `BDR_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações gerais do borderô em formato binário. NUNCA selecione em queries SELECT. |
| `BDR_ID_SERVIDOR` | INTEGER | Sim | Identificador do servidor de origem (TB_SERVIDOR). |
| `BDR_GUID` | VARCHAR(50) | Sim | GUID para integração. |
| `BDR_ID_LOCAL` | INTEGER | Sim | Identificador do local/loja de origem (TB_LOCAL). |
| `BDR_NOTA_FISCAL` | INTEGER | Sim | Identificador da nota fiscal relacionada ao borderô. |
| `BDR_CONCILIACAO` | INTEGER | Sim | Identificador do processo de conciliação bancária ao qual o borderô está vinculado. |

COMMENT ON COLUMN TB_BORDERO_RECEBIMENTO.BDR_STATUS IS 'BDR_STATUS
------------
''A'' -> Ativo
''C'' -> Cancelado';
COMMENT ON COLUMN TB_BORDERO_RECEBIMENTO.BDR_GERA_CREDITO IS 'S - SIM
N - NÃO';
COMMENT ON COLUMN TB_BORDERO_RECEBIMENTO.BDR_CONTA IS 'Plano de contas para contra partida para outros movimentos';
COMMENT ON COLUMN TB_BORDERO_RECEBIMENTO.BDR_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização';
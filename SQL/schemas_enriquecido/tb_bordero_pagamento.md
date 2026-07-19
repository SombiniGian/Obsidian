# Tabela TB_BORDERO_PAGAMENTO

**Módulo:** Financeiro / Contas a Pagar
Gera um borderô com os pagamentos (contas a pagar) baixados em lote, consolidando totais de cheques emitidos, cheques recebidos passados, créditos, juros, valores em dinheiro e cartão, vinculando-se a um caixa, fechamento e plano de contas. É o cabeçalho do borderô de pagamento.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BDP_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `BDP_ID` | INTEGER | Não | Identificador único do borderô de pagamento. Parte da chave primária composta. |
| `BDP_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do borderô no sistema. |
| `BDP_DT_EMISSAO` | DATE | Sim | Data de emissão do borderô. |
| `BDP_QTDE_CHEQUE_EMITIDO` | INTEGER | Sim | Quantidade de cheques emitidos incluídos no borderô. |
| `BDP_VALOR_CHEQUE_EMITIDO` | NUMERIC(15,2) | Sim | Valor total dos cheques emitidos no borderô. |
| `BDP_QUANTIDADE_PAGAMENTO` | INTEGER | Sim | Quantidade de títulos (pagamentos) baixados no borderô. |
| `BDP_VALOR_PAGAMENTO` | NUMERIC(15,2) | Sim | Valor total dos pagamentos baixados. |
| `BDP_QUANTIDADE_CREDITO` | INTEGER | Sim | Quantidade de créditos gerados pelo borderô. |
| `BDP_VALOR_CREDITO` | NUMERIC(15,2) | Sim | Valor total dos créditos gerados. |
| `BDP_QUANTIDADE_JUROS` | INTEGER | Sim | Quantidade de títulos que receberam juros. |
| `BDP_VALOR_JUROS` | NUMERIC(15,2) | Sim | Valor total de juros pagos nos itens do borderô. |
| `BDP_VALOR_TOTAL_PAGAR` | NUMERIC(15,2) | Sim | Valor total a pagar (soma dos títulos baixados). |
| `BDP_VALOR_PAGO_DINHEIRO` | NUMERIC(15,2) | Sim | Valor pago em dinheiro no borderô. |
| `BDP_VALOR_PAGO_CARTAO` | NUMERIC(15,2) | Sim | Valor pago em cartão no borderô. |
| `BDP_QTDE_CHEQUE_REC` | INTEGER | Sim | Quantidade de cheques recebidos passados no borderô. |
| `BDP_VALOR_PAGO_CHEQUE_REC` | NUMERIC(15,2) | Sim | Valor pago em cheques recebidos passados no borderô. |
| `BDP_VALOR_PAGO_TOTAL` | NUMERIC(15,2) | Sim | Valor total pago no borderô. |
| `BDP_USUARIO` | INTEGER | Sim | Identificador do usuário responsável pelo lançamento do borderô. |
| `BDP_STATUS` | VARCHAR(1) | Sim | Status do borderô de pagamento. |
| `BDP_VALOR_MOV_BANCARIA` | NUMERIC(15,2) | Sim | Valor da movimentação bancária gerada pelo borderô. |
| `BDP_CAIXA` | INTEGER | Sim | Identificador do caixa (TB_CONTA.CNT_ID) associado ao borderô. |
| `BDP_FECHAMENTO` | INTEGER | Sim | Identificador do fechamento de caixa ao qual o borderô pertence. |
| `BDP_CONTA` | INTEGER | Sim | Identificador do plano de contas onde os pagamentos do borderô se encontram. |
| `BDP_PESSOA` | INTEGER | Sim | Identificador do fornecedor/pessoa (TB_PESSOA.PES_ID) principal do borderô. |
| `BDP_GERA_CREDITO` | VARCHAR(1) | Sim | Indica se o borderô gera crédito (S = Sim, N = Não). |
| `BDP_TIPO_TROCO` | VARCHAR(1) | Sim | Destino do troco (T = Lançou Troco, C = Lançou Crédito, D = Descartou). |
| `BDP_CAIXA_TROCO` | INTEGER | Sim | Identificador do caixa de destino do troco. |
| `BDP_TIPO_DESCONTO` | VARCHAR(1) | Sim | Tipo do desconto aplicado (V = Valor, P = Percentual). |
| `BDP_DESCONTO` | NUMERIC(15,2) | Sim | Valor do desconto aplicado ao borderô. |
| `BDP_TIPO_ACRESCIMO` | VARCHAR(1) | Sim | Tipo do acréscimo aplicado (V = Valor, P = Percentual). |
| `BDP_ACRESCIMO` | NUMERIC(15,2) | Sim | Valor do acréscimo aplicado ao borderô. |
| `BDP_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações gerais do borderô em formato binário. NUNCA selecione em queries SELECT. |
| `BDP_CONCILIACAO` | INTEGER | Sim | Identificador do processo de conciliação bancária ao qual o borderô está vinculado. |

COMMENT ON COLUMN TB_BORDERO_PAGAMENTO.BDP_STATUS IS 'BDP_STATUS
------------
''A'' -> Ativo
''C'' -> Cancelado';
COMMENT ON COLUMN TB_BORDERO_PAGAMENTO.BDP_CONTA IS 'Plano de contas que os pagamentos do bordero se encontram';
COMMENT ON COLUMN TB_BORDERO_PAGAMENTO.BDP_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização';
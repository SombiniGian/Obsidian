# Tabela TB_PEDIDO_VENDA_FIN

**Módulo:** Vendas
Formas de pagamento e lançamentos financeiros vinculados ao pedido de venda. Registra o troco, valores por espécie de moeda e o vínculo com TB_ESPECIE_MOEDA para indicar como o pedido foi pago.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PEVF_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PEVF_PEDIDO_VENDA` | INTEGER | Não | Identificador do pedido de venda (TB_PEDIDO_VENDA.PEV_ID). Parte da chave primária composta. |
| `PEVF_SEQUENCIA` | INTEGER | Não | Sequencial do lançamento financeiro dentro do pedido. Parte da chave primária composta. |
| `PEVF_ESPECIE_MOEDA` | INTEGER | Sim | Identificador da espécie de moeda (TB_ESPECIE_MOEDA.ESP_ID) — define como o pagamento foi feito (dinheiro, cartão, cheque, PIX etc.). |
| `PEVF_VALOR` | NUMERIC(15,2) | Sim | Valor pago nesta forma de pagamento. |
| `PEVF_TROCO` | NUMERIC(15,2) | Sim | Valor do troco devolvido ao cliente neste lançamento. |
| `PEVF_VALOR_VENDA` | NUMERIC(15,2) | Sim | Valor da venda associado a este lançamento. |
| `PEVF_DT_EMISSAO` | DATE | Sim | Data de emissão do lançamento financeiro. |
| `PEVF_DT_VECTO` | DATE | Sim | Data de vencimento (para pagamentos parcelados). |
| `PEVF_USUARIO` | INTEGER | Sim | Identificador do usuário que registrou o pagamento. |
| `PEVF_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro. |
| `PEVF_MOVIMENTAR` | VARCHAR(10) | Sim | Tipo de movimentação gerada (CX = Caixa, CB = Conta Bancária, CH = Cheque, CC = Cartão Crédito, CR = Crédito, TD = Tipo Documento). |
| `PEVF_CAIXA` | INTEGER | Sim | Identificador do caixa (TB_CONTA.CNT_ID) onde o pagamento foi recebido. |
| `PEVF_INTEGRACAO` | INTEGER | Sim | Identificador do processo de integração relacionado (ex.: TEF, Pagar.me). |
| `PEVF_CNPJ_CREDENCIADORA` | VARCHAR(14) | Sim | CNPJ da credenciadora do cartão. |
| `PEVF_BANDEIRA` | VARCHAR(2) | Sim | Bandeira do cartão (quando pagamento em cartão). |
| `PEVF_CREDENCIADORA` | VARCHAR(100) | Sim | Nome da credenciadora do cartão. |
| `PEVF_DOCUMENTO` | VARCHAR(20) | Sim | Número do documento (comprovante, NSU, cheque). |
| `PEVF_PARCELA` | VARCHAR(3) | Sim | Identificador da parcela (ex.: 001). |
| `PEVF_NR_PARCELAS` | INTEGER | Sim | Quantidade total de parcelas deste pagamento. |
| `PEVF_TEF` | VARCHAR(1) | Sim | Indica se o pagamento foi feito via TEF (S/N). |
| `PEVF_ID_MOVIMENTO` | INTEGER | Sim | Identificador do movimento financeiro gerado (TB_MOVIMENTO_CONTA.MOV_ID). |
| `PEVF_ADM_CARTAO` | INTEGER | Sim | Identificador da administradora de cartão (TB_PESSOA.PES_ID onde PES_ADM_CARTAO = 'S'). |
| `PEVF_TIPO` | VARCHAR(2) | Sim | Tipo do lançamento (ex.: DP = Duplicata, CR = Crédito, JR = Juros). |
| `PEVF_SEM_BX_ADM` | VARCHAR(1) | Sim | Indica se o título não passa pela baixa administrativa do cartão (S/N). |
| `PEVF_CONTA` | INTEGER | Sim | Identificador da conta (TB_CONTA.CNT_ID) associada ao recebimento. |
| `PEVF_PAGADOR` | INTEGER | Sim | Identificador do pagador (TB_PESSOA.PES_ID). |
| `PEVF_FECHAMENTO` | INTEGER | Sim | Identificador do fechamento de caixa ao qual o lançamento pertence. |
| `PEVF_CODIGO_PSP` | VARCHAR(50) | Sim | Código do PSP (provedor) — PIX/TEF. |
| `PEVF_ID_CARTEIRA_DIGITAL` | VARCHAR(50) | Sim | ID da carteira digital. |
| `PEVF_NOME_CARTEIRA_DIGITAL` | VARCHAR(100) | Sim | Nome da carteira digital. |
| `PEVF_TEF_NSU` | VARCHAR(100) | Sim | NSU da transação TEF. |
| `PEVF_PIX` | INTEGER | Sim | Identificador do PIX vinculado. |
| `PEVF_ID_PAGARME` | VARCHAR(100) | Sim | ID do lançamento no Pagar.me. |
| `PEVF_NR_CARTAO` | VARCHAR(20) | Sim | Número do cartão (mascarado) utilizado. |
| `PEVF_STONE_CODE` | VARCHAR(100) | Sim | Código da transação na Stone. |
| `PEVF_TEF_COMPROVANTE_1` | BLOB SUB_TYPE TEXT | Sim | Comprovante 1 do TEF em formato texto. NUNCA selecione em queries SELECT. |
| `PEVF_TEF_COMPROVANTE_2` | BLOB SUB_TYPE TEXT | Sim | Comprovante 2 do TEF em formato texto. NUNCA selecione em queries SELECT. |
| `PEVF_BIN` | VARCHAR(10) | Sim | BIN do cartão (6 primeiros dígitos). |
| `PEVF_ULT_DIGITOS` | VARCHAR(10) | Sim | Últimos dígitos do cartão. |
| `PEVF_CODIGO_AUT` | VARCHAR(200) | Sim | Código de autorização da transação TEF/cartão. |

COMMENT ON COLUMN TB_PEDIDO_VENDA_FIN.PEVF_ESPECIE_MOEDA IS 'FK para TB_ESPECIE_MOEDA.ESP_ID — use JOIN com TB_ESPECIE_MOEDA para descobrir a forma de pagamento (dinheiro, cartão, PIX, cheque, etc.)';
COMMENT ON COLUMN TB_PEDIDO_VENDA_FIN.PEVF_TEF_COMPROVANTE_1 IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_PEDIDO_VENDA_FIN.PEVF_TEF_COMPROVANTE_2 IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
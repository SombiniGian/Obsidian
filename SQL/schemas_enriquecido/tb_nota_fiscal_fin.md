# Tabela TB_NOTA_FISCAL_FIN

**Módulo:** Fiscal / Financeiro
Itens financeiros da nota fiscal (TB_NOTA_FISCAL): registram as formas de pagamento (parcelas) da NF, integrando com o financeiro (TB_RECEBIMENTO/TB_MOVIMENTO_CONTA) e com adquirentes/administradoras de cartão (CNPJ, bandeira, TEF, PIX).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `NFF_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `NFF_NOTA_FISCAL` | INTEGER | Não | FK para TB_NOTA_FISCAL.NF_ID. Parte da chave primária composta. |
| `NFF_SEQUENCIA` | INTEGER | Não | Sequencial do lançamento financeiro dentro da NF. Parte da chave primária composta. |
| `NFF_ESPECIE_MOEDA` | INTEGER | Sim | FK para TB_ESPECIE_MOEDA.ESP_ID — espécie de pagamento utilizada. |
| `NFF_VALOR` | NUMERIC(15,2) | Sim | Valor recebido nesta forma de pagamento. |
| `NFF_TROCO` | NUMERIC(15,2) | Sim | Valor do troco (quando houver). |
| `NFF_VALOR_VENDA` | NUMERIC(15,2) | Sim | Valor de venda associado a esta forma (com taxas). |
| `NFF_DT_EMISSAO` | DATE | Sim | Data de emissão do título/parcela. |
| `NFF_DT_VECTO` | DATE | Sim | Data de vencimento do título/parcela. |
| `NFF_USUARIO` | INTEGER | Sim | FK para TB_USUARIO — usuário que lançou. |
| `NFF_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento. |
| `NFF_MOVIMENTAR` | VARCHAR(10) | Sim | Tipo de movimentação financeira gerada (CX/CB/CH/CC/CR/TD). |
| `NFF_CAIXA` | INTEGER | Sim | FK para TB_CONTA.CNT_ID — caixa relacionado. |
| `NFF_INTEGRACAO` | INTEGER | Sim | Identificador da integração (Stone, Pagar.me etc.). |
| `NFF_CNPJ_CREDENCIADORA` | VARCHAR(14) | Sim | CNPJ da credenciadora/adquirente (apenas números). |
| `NFF_BANDEIRA` | VARCHAR(2) | Sim | Bandeira do cartão (Visa, Master, Elo, Hiper etc.). |
| `NFF_CREDENCIADORA` | VARCHAR(100) | Sim | Nome da credenciadora. |
| `NFF_DOCUMENTO` | VARCHAR(20) | Sim | Número do documento/título gerado. |
| `NFF_PARCELA` | VARCHAR(3) | Sim | Identificador da parcela (ex.: 01/03). |
| `NFF_NR_PARCELAS` | INTEGER | Sim | Número total de parcelas. |
| `NFF_TEF` | VARCHAR(1) | Sim | Indica se foi paga via TEF (S/N). |
| `NFF_ID_MOVIMENTO` | INTEGER | Sim | FK para TB_MOVIMENTO_CONTA.MOV_ID — movimento gerado. |
| `NFF_ADM_CARTAO` | INTEGER | Sim | FK para TB_PESSOA.PES_ID — administradora de cartão. |
| `NFF_TIPO` | VARCHAR(2) | Sim | Tipo do título (DP=Duplicata, CR=Crédito, JR=Juros etc.). |
| `NFF_SEM_BX_ADM` | VARCHAR(1) | Sim | Indica se não passa pela baixa administrativa do cartão (S/N). |
| `NFF_CONTA` | INTEGER | Sim | FK para TB_CONTA.CNT_ID — conta destino do movimento. |
| `NFF_TEF_NSU` | VARCHAR(100) | Sim | NSU da transação TEF. |
| `NFF_PIX` | INTEGER | Sim | Identificador do PIX gerado. |
| `NFF_CODIGO_AUT` | VARCHAR(200) | Sim | Código de autorização (cartão/TEF). |

COMMENT ON COLUMN TB_NOTA_FISCAL_FIN.NFF_NOTA_FISCAL IS 'FK para TB_NOTA_FISCAL.NF_ID — use JOIN com TB_NOTA_FISCAL por NF_ID.';
COMMENT ON COLUMN TB_NOTA_FISCAL_FIN.NFF_MOVIMENTAR IS 'CX = Caixa, CB = Conta Bancária, CH = Cheque, CC = Cartão Crédito, CR = Crédito, TD = Tipo Documento.';

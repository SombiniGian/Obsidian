# Tabela TB_HOSPEDAGEM_FIN

**Módulo:** Hospedagem / Financeiro
Tabela financeira de uma hospedagem. Armazena os lançamentos de pagamento da hospedagem (espécie, cartão, TEF, etc.) com valores, datas, bandeiras, credenciadoras, parcelas e integrações com movimentações de caixa/conta.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `HOSF_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `HOSF_HOSPEDAGEM` | INTEGER | Não | FK para TB_HOSPEDAGEM. Parte da chave primária composta. |
| `HOSF_SEQUENCIA` | INTEGER | Não | Sequencial do lançamento financeiro dentro da hospedagem. Parte da chave primária composta. |
| `HOSF_ESPECIE_MOEDA` | INTEGER | Sim | FK para TB_ESPECIE_MOEDA. Espécie/forma de pagamento utilizada. |
| `HOSF_VALOR` | NUMERIC(15,2) | Sim | Valor pago/recebido no lançamento. |
| `HOSF_TROCO` | NUMERIC(15,2) | Sim | Valor do troco devolvido, quando aplicável. |
| `HOSF_VALOR_VENDA` | NUMERIC(15,2) | Sim | Valor de venda do lançamento (pode diferir do valor recebido em promoções). |
| `HOSF_DT_EMISSAO` | DATE | Sim | Data de emissão do lançamento. |
| `HOSF_DT_VECTO` | DATE | Sim | Data de vencimento do lançamento, quando aplicável. |
| `HOSF_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que efetuou o lançamento. |
| `HOSF_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de gravação do registro. |
| `HOSF_MOVIMENTAR` | VARCHAR(10) | Sim | Indicador/observação sobre a movimentação do lançamento. |
| `HOSF_CAIXA` | INTEGER | Sim | FK para o caixa onde o lançamento foi registrado. |
| `HOSF_INTEGRACAO` | INTEGER | Sim | Código/status de integração com sistemas externos (TEF, adm. cartão, etc.). |
| `HOSF_CNPJ_CREDENCIADORA` | VARCHAR(14) | Sim | CNPJ da credenciadora/operadora de cartão. |
| `HOSF_BANDEIRA` | VARCHAR(2) | Sim | Código da bandeira do cartão (Visa, Master, etc.). |
| `HOSF_CREDENCIADORA` | VARCHAR(100) | Sim | Nome/descrição da credenciadora. |
| `HOSF_DOCUMENTO` | VARCHAR(20) | Sim | Número do documento/NSU/comprovante do lançamento. |
| `HOSF_PARCELA` | VARCHAR(3) | Sim | Identificador da parcela atual (ex.: 01/03). |
| `HOSF_NR_PARCELAS` | INTEGER | Sim | Número total de parcelas da venda. |
| `HOSF_TEF` | VARCHAR(1) | Sim | Indica se o lançamento foi realizado via TEF (S/N). |
| `HOSF_ID_MOVIMENTO` | INTEGER | Sim | FK para TB_MOVIMENTO_CONTA gerado a partir deste lançamento. |
| `HOSF_ADM_CARTAO` | INTEGER | Sim | FK para TB_PESSOA (PES_ADM_CARTAO=S). Administradora de cartão. |
| `HOSF_TIPO` | VARCHAR(2) | Sim | Tipo do lançamento financeiro. |
| `HOSF_SEM_BX_ADM` | VARCHAR(1) | Sim | Indica se o lançamento NÃO deve ser baixado pela administradora (S/N). |
| `HOSF_CONTA` | INTEGER | Sim | FK para TB_CONTA. Conta contábil/financeira do lançamento. |
| `HOSF_CODIGO_AUT` | VARCHAR(200) | Sim | Código de autorização retornado pelo TEF/credenciadora. |

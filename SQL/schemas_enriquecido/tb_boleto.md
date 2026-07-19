# Tabela TB_BOLETO

**Módulo:** Financeiro / Cobrança
Tabela principal de boletos emitidos/recebidos. Armazena dados do título (documento, vencimento, valor, juros, multa, desconto, protesto), dados do sacado, mensagens, controle de remessa/baixa e dados PIX (copia-cola, linha digitável). Cada boleto pertence a uma empresa e pode estar vinculado a um recebimento.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BOL_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `BOL_ID` | INTEGER | Não | Identificador único do boleto. Parte da chave primária composta. |
| `BOL_REMESSA` | INTEGER | Sim | FK para TB_BOLETO_REMESSA (remessa de envio ao banco). |
| `BOL_REMESSA_CANC` | INTEGER | Sim | FK para remessa de cancelamento. |
| `BOL_BOLETO_CONF` | INTEGER | Sim | FK para TB_BOLETO (boleto de confirmação/recorrência). |
| `BOL_SELECIONADO` | VARCHAR(1) | Sim | Marcador para seleção em processos (S/N). |
| `BOL_DOCUMENTO` | VARCHAR(20) | Sim | Número do documento/título. |
| `BOL_DT_DOCUMENTO` | DATE | Sim | Data do documento. |
| `BOL_DT_VENCIMENTO` | DATE | Sim | Data de vencimento do boleto. |
| `BOL_DT_LIMITE_PAGTO` | DATE | Sim | Data limite para pagamento com desconto. |
| `BOL_DT_BAIXA` | DATE | Sim | Data de baixa/pagamento do boleto. |
| `BOL_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro no sistema. |
| `BOL_DT_ANTECIPACAO` | DATE | Sim | Data de antecipação do recebimento. |
| `BOL_DT_MORA_JUROS` | DATE | Sim | Data de início da cobrança de juros. |
| `BOL_DT_DESCONTO` | DATE | Sim | Data limite para concessão de desconto. |
| `BOL_DT_ABATIMENTO` | DATE | Sim | Data limite para abatimento. |
| `BOL_DT_PROTESTO` | DATE | Sim | Data de protesto do boleto. |
| `BOL_DT_DESCONTO_2` | DATE | Sim | Data limite para segundo desconto. |
| `BOL_DT_DESCONTO_3` | DATE | Sim | Data limite para terceiro desconto. |
| `BOL_DT_MULTA` | DATE | Sim | Data de início da multa. |
| `BOL_DT_RET_DESC` | DATE | Sim | Data de retorno do desconto. |
| `BOL_ESPECIE_DOC` | VARCHAR(4) | Sim | Espécie do documento (ex.: DM=Duplicata Mercantil). |
| `BOL_NOSSO_NUMERO` | VARCHAR(100) | Sim | Nosso número atribuído pelo banco. |
| `BOL_NOSSO_NUMERO_CORRESPONDENTE` | VARCHAR(300) | Sim | Nosso número do banco correspondente. |
| `BOL_VALOR_DOCUMENTO` | NUMERIC(15,2) | Sim | Valor original do documento. |
| `BOL_VALOR_ABATIMENTO` | NUMERIC(15,2) | Sim | Valor de abatimento concedido. |
| `BOL_VALOR_MORA_JUROS` | NUMERIC(15,2) | Sim | Valor de juros de mora. |
| `BOL_VALOR_DESCONTO` | NUMERIC(15,2) | Sim | Valor de desconto. |
| `BOL_VALOR_DESCONTO_2` | NUMERIC(15,2) | Sim | Valor do segundo desconto. |
| `BOL_VALOR_DESCONTO_3` | NUMERIC(15,2) | Sim | Valor do terceiro desconto. |
| `BOL_VALOR_MULTA` | NUMERIC(15,2) | Sim | Valor da multa. |
| `BOL_VALOR_DESPESAS` | NUMERIC(15,2) | Sim | Valor de despesas (ex.: protesto, cobrança). |
| `BOL_PERCENTUAL_MULTA` | NUMERIC(17,4) | Sim | Percentual da multa. |
| `BOL_JUROS` | NUMERIC(17,4) | Sim | Percentual de juros. |
| `BOL_MULTA` | NUMERIC(17,4) | Sim | Percentual de multa. |
| `BOL_CODIGO_MORA` | VARCHAR(1) | Sim | Código do tipo de mora (1=Valor diário, 2=Taxa mensal, 3=Isento). |
| `BOL_CODIGO_MULTA` | VARCHAR(1) | Sim | Código do tipo de multa. |
| `BOL_TIPO_PROTESTO` | VARCHAR(1) | Sim | Tipo de protesto (1=Dias corridos, 2=Dias úteis, 3=Não protestar). |
| `BOL_MENSAGEM` | VARCHAR(2000) | Sim | Mensagens/instruções impressas no boleto. |
| `BOL_RECEBIMENTO` | INTEGER | Sim | FK para TB_RECEBIMENTO (código do recebimento relacionado ao boleto). |
| `BOL_ORIGEM` | VARCHAR(30) | Sim | Sigla do módulo/rotina de origem (ex.: RECEBIMENTO, VENDA). |
| `BOL_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem. |
| `BOL_STATUS` | VARCHAR(1) | Sim | Status do boleto (A=Aberto, B=Baixado, C=Cancelado). |
| `BOL_PARCELA` | INTEGER | Sim | Número da parcela. |
| `BOL_NR_PARCELAS` | INTEGER | Sim | Quantidade total de parcelas. |
| `BOL_CARTEIRA` | VARCHAR(10) | Sim | Carteira de cobrança (ex.: 109, 157). |
| `BOL_DESTACAR_DEDUCOES` | VARCHAR(1) | Sim | Destacar deduções no boleto (S/N). |
| `BOL_CONTA` | INTEGER | Sim | FK para TB_CONTA.CNT_ID de destino do recebimento. |
| `BOL_ESPECIE_MOEDA` | INTEGER | Sim | FK para TB_ESPECIE_MOEDA.ESP_ID. |
| `BOL_EMAIL_ENVIADO` | VARCHAR(1) | Sim | Indica se o e-mail do boleto foi enviado (S/N). |
| `BOL_EMAIL` | VARCHAR(100) | Sim | E-mail do sacado para envio do boleto. |
| `BOL_LINHA_DIGITAVEL` | VARCHAR(100) | Sim | Linha digitável do boleto (código de barras). |
| `BOL_PIX_COPIA_COLA` | VARCHAR(500) | Sim | Código PIX copia-e-cola associado ao boleto. |
| `BOL_MOTIVO_CANCELAMENTO` | INTEGER | Sim | FK para TB_DEVOLUCAO_MOTIVO (motivo do cancelamento). |

COMMENT ON COLUMN TB_BOLETO.BOL_RECEBIMENTO IS 'Código do recebimento relacionado à Boleta';
COMMENT ON COLUMN TB_BOLETO.BOL_STATUS IS 'A - ABERTO
B - BAIXADO
C - CANCELADO';
COMMENT ON COLUMN TB_BOLETO.BOL_SELECIONADO IS 'Campo para testar quais boletos foram selecionados. S - SIM, N - NÃO';

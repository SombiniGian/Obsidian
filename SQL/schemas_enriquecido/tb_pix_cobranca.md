# Tabela TB_PIX_COBRANCA

**Módulo:** Financeiro / PIX
Tabela de cobranças PIX geradas para clientes. Armazena dados do PSP (Provedor de Serviço de Pagamento), TXID, E2E, QR Code, valores (original, juros, multa, desconto), dados do pagador, datas de vencimento, pagamento e devolução, controle de envio por e-mail/WhatsApp e dados de retorno da API (status cobrança/devolução, motivo, natureza). É a tabela de integração com APIs PIX (Pagar.me, Mercado Pago, etc).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PIX_ID` | INTEGER | Não | Identificador único da cobrança PIX. |
| `PIX_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `PIX_TXID` | VARCHAR(255) | Sim | TXID da cobrança PIX (identificador único da transação no PSP). |
| `PIX_E2E` | VARCHAR(255) | Sim | Identificador E2E (end-to-end) do pagamento PIX. |
| `PIX_QRCODE` | BLOB SUB_TYPE TEXT | Sim | QR Code PIX em formato texto/BR Code. |
| `PIX_PSP` | INTEGER | Sim | Identificador do PSP (Provedor de Serviço de Pagamento). |
| `PIX_NOME_PAGADOR` | VARCHAR(60) | Sim | Nome do pagador. |
| `PIX_CNPJ_CPF` | VARCHAR(14) | Sim | CNPJ/CPF do pagador. |
| `PIX_VALOR` | NUMERIC(15,2) | Sim | Valor original da cobrança PIX. |
| `PIX_VALOR_DOC` | NUMERIC(15,2) | Sim | Valor do documento/título vinculado. |
| `PIX_VALOR_MULTA` | NUMERIC(15,2) | Sim | Valor de multa. |
| `PIX_VALOR_JUROS` | NUMERIC(15,2) | Sim | Valor de juros. |
| `PIX_VALOR_TAXA` | NUMERIC(15,6) | Sim | Taxa cobrada pelo PSP. |
| `PIX_VALOR_DESCONTO` | NUMERIC(15,6) | Sim | Valor de desconto aplicado. |
| `PIX_TIPO_MULTA` | VARCHAR(1) | Sim | Tipo de multa (P=Percentual, V=Valor). |
| `PIX_MULTA` | NUMERIC(15,6) | Sim | Percentual/valor base da multa. |
| `PIX_TIPO_JUROS` | VARCHAR(1) | Sim | Tipo de juros (P=Percentual, V=Valor). |
| `PIX_JUROS` | NUMERIC(15,6) | Sim | Percentual/valor base dos juros. |
| `PIX_TIPO_DESCONTO` | VARCHAR(1) | Sim | Tipo de desconto (P=Percentual, V=Valor). |
| `PIX_DESCONTO` | NUMERIC(15,6) | Sim | Percentual/valor base do desconto. |
| `PIX_ERRO` | VARCHAR(1) | Sim | Indica se houve erro na integração (S/N). |
| `PIX_STATUS` | VARCHAR(1) | Sim | Status da cobrança PIX (A=Ativa, P=Paga, C=Cancelada, E=Expirada). |
| `PIX_STATUS_COBRANCA` | VARCHAR(100) | Sim | Status retornado pela API do PSP (ex.: ATIVA, CONCLUIDA). |
| `PIX_STATUS_DEVOLUCAO` | VARCHAR(100) | Sim | Status de devolução retornado pelo PSP. |
| `PIX_DEV_NATUREZA` | VARCHAR(20) | Sim | Natureza da devolução (ORIGINAL, RETIRADA). |
| `PIX_DEV_DESCRICAO` | VARCHAR(100) | Sim | Descrição da devolução. |
| `PIX_DEV_MOTIVO` | VARCHAR(100) | Sim | Motivo da devolução (ex.: A01=Saldo Insuficiente). |
| `PIX_DEV_RTRID` | VARCHAR(255) | Sim | ID de retorno (RTRID) da devolução. |
| `PIX_DEV_ID` | VARCHAR(255) | Sim | ID da devolução. |
| `PIX_QTDE_CONSULTA` | INTEGER | Sim | Quantidade de consultas realizadas na API do PSP. |
| `PIX_ORIGEM` | VARCHAR(20) | Sim | Sigla do módulo/rotina de origem (ex.: BOLETO, RECEBIMENTO). |
| `PIX_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem. |
| `PIX_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento da cobrança PIX. |
| `PIX_DT_PAGAMENTO` | TIMESTAMP | Sim | Data e hora do pagamento PIX. |
| `PIX_DT_DEVOLUCAO` | TIMESTAMP | Sim | Data e hora da devolução PIX. |
| `PIX_DT_VENCIMENTO` | DATE | Sim | Data de vencimento da cobrança PIX. |
| `PIX_DIAS_VALIDADE` | INTEGER | Sim | Dias de validade da cobrança após criação. |
| `PIX_USUARIO` | INTEGER | Sim | Identificador do usuário que gerou a cobrança. |
| `PIX_USUARIO_DEV` | INTEGER | Sim | Identificador do usuário que registrou a devolução. |
| `PIX_AMBIENTE` | INTEGER | Sim | Ambiente (1=Homologação, 2=Produção). |
| `PIX_TIPO` | VARCHAR(20) | Sim | Tipo da cobrança (IMEDIATO, VENCIMENTO). |
| `PIX_SOLICITACAO` | VARCHAR(100) | Sim | Tipo de solicitação/Permissão (ex.: cob, cobv). |
| `PIX_LOC_ID` | VARCHAR(255) | Sim | ID de localização do PIX (LOC.ID do PSP). |
| `PIX_PESSOA` | INTEGER | Sim | FK para TB_PESSOA.PES_ID do pagador. Use JOIN por PES_ID. |
| `PIX_EMAIL` | VARCHAR(255) | Sim | E-mail do pagador. |
| `PIX_ENDERECO` | VARCHAR(255) | Sim | Endereço do pagador. |
| `PIX_CIDADE` | VARCHAR(100) | Sim | Cidade do pagador. |
| `PIX_UF` | VARCHAR(2) | Sim | UF do pagador. |
| `PIX_DOCUMENTO` | VARCHAR(20) | Sim | Número do documento/título. |
| `PIX_EMAIL_ENVIADO` | VARCHAR(1) | Sim | Indica se o e-mail foi enviado (S/N). |
| `PIX_EMAIL_ENVIO` | VARCHAR(255) | Sim | E-mail utilizado para envio. |
| `PIX_WHATS_ENVIADO` | VARCHAR(1) | Sim | Indica se o WhatsApp foi enviado (S/N). |
| `PIX_WHATS_ENVIO` | VARCHAR(50) | Sim | Número do WhatsApp utilizado para envio. |
| `PIX_MENSAGEM` | VARCHAR(2000) | Sim | Mensagem adicional enviada ao pagador. |
| `PIX_GUID` | VARCHAR(50) | Sim | GUID para integração. |

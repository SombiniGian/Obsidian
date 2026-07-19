# Tabela TB_ORDEM_SERVICO_FIN

**Módulo:** Ordem de Serviço / Financeiro
Lançamentos financeiros (parcelas/formas de pagamento) de uma ordem de serviço (TB_ORDEM_SERVICO). Integra com o financeiro (TB_MOVIMENTO_CONTA / TB_FECHAMENTO_CAIXA), administradoras de cartão (CNPJ, bandeira, TEF, PIX, credenciadoras digitais como Stone e Pagar.me) e controle de caixa/fechamento.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `OSF_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `OSF_ORDEM_SERVICO` | INTEGER | Não | FK para TB_ORDEM_SERVICO. Parte da chave primária composta. |
| `OSF_SEQUENCIA` | INTEGER | Não | Sequencial do lançamento financeiro dentro da OS. Parte da chave primária composta. |
| `OSF_ESPECIE_MOEDA` | INTEGER | Sim | FK para TB_ESPECIE_MOEDA.ESP_ID — espécie de pagamento. |
| `OSF_VALOR` | NUMERIC(15,2) | Sim | Valor recebido nesta forma de pagamento. |
| `OSF_TROCO` | NUMERIC(15,2) | Sim | Valor do troco (quando houver). |
| `OSF_VALOR_VENDA` | NUMERIC(15,2) | Sim | Valor de venda desta forma (com taxas). |
| `OSF_DT_EMISSAO` | DATE | Sim | Data de emissão do título/parcela. |
| `OSF_DT_VECTO` | DATE | Sim | Data de vencimento do título/parcela. |
| `OSF_USUARIO` | INTEGER | Sim | FK para TB_USUARIO — usuário que lançou. |
| `OSF_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento. |
| `OSF_MOVIMENTAR` | VARCHAR(10) | Sim | Tipo de movimentação financeira gerada (CX/CB/CH/CC/CR/TD). |
| `OSF_CAIXA` | INTEGER | Sim | FK para TB_CONTA.CNT_ID — caixa relacionado. |
| `OSF_INTEGRACAO` | INTEGER | Sim | Identificador da integração (Stone, Pagar.me etc.). |
| `OSF_CNPJ_CREDENCIADORA` | VARCHAR(14) | Sim | CNPJ da credenciadora/adquirente (somente números). |
| `OSF_BANDEIRA` | VARCHAR(2) | Sim | Bandeira do cartão (Visa, Master, Elo, Hiper etc.). |
| `OSF_CREDENCIADORA` | VARCHAR(100) | Sim | Nome da credenciadora. |
| `OSF_DOCUMENTO` | VARCHAR(20) | Sim | Número do documento/título gerado. |
| `OSF_PARCELA` | VARCHAR(3) | Sim | Identificador da parcela (ex.: 01/03). |
| `OSF_NR_PARCELAS` | INTEGER | Sim | Número total de parcelas. |
| `OSF_TEF` | VARCHAR(1) | Sim | Indica se foi paga via TEF (S/N). |
| `OSF_ID_MOVIMENTO` | INTEGER | Sim | FK para TB_MOVIMENTO_CONTA.MOV_ID — movimento gerado. |
| `OSF_ADM_CARTAO` | INTEGER | Sim | FK para TB_PESSOA.PES_ID — administradora de cartão. |
| `OSF_TIPO` | VARCHAR(2) | Sim | Tipo do título (DP=Duplicata, CR=Crédito, JR=Juros etc.). |
| `OSF_SEM_BX_ADM` | VARCHAR(1) | Sim | Indica se não passa pela baixa administrativa do cartão (S/N). |
| `OSF_CONTA` | INTEGER | Sim | FK para TB_CONTA.CNT_ID — conta destino do movimento. |
| `OSF_PAGADOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID — pagador/cliente. |
| `OSF_FECHAMENTO` | INTEGER | Sim | Identificador do fechamento de caixa. |
| `OSF_CODIGO_PSP` | VARCHAR(50) | Sim | Código do PSP (PIX). |
| `OSF_ID_CARTEIRA_DIGITAL` | VARCHAR(50) | Sim | Identificador da carteira digital. |
| `OSF_NOME_CARTEIRA_DIGITAL` | VARCHAR(100) | Sim | Nome da carteira digital (PicPay, Mercado Pago etc.). |
| `OSF_TEF_NSU` | VARCHAR(100) | Sim | NSU da transação TEF. |
| `OSF_PIX` | INTEGER | Sim | Identificador do PIX gerado. |
| `OSF_ID_PAGARME` | VARCHAR(100) | Sim | ID da transação na Pagar.me. |
| `OSF_NR_CARTAO` | VARCHAR(20) | Sim | Número do cartão (mascarado). |
| `OSF_STONE_CODE` | VARCHAR(100) | Sim | Código da transação na Stone. |
| `OSF_CODIGO_AUT` | VARCHAR(200) | Sim | Código de autorização (cartão/TEF). |

COMMENT ON COLUMN TB_ORDEM_SERVICO_FIN.OSF_ORDEM_SERVICO IS 'FK para TB_ORDEM_SERVICO — use JOIN por OSF_ORDEM_SERVICO.';
COMMENT ON COLUMN TB_ORDEM_SERVICO_FIN.OSF_MOVIMENTAR IS 'CX = Caixa, CB = Conta Bancária, CH = Cheque, CC = Cartão Crédito, CR = Crédito, TD = Tipo Documento.';

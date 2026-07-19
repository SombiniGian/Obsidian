# Tabela TB_BORDERO_COBRANCA

**Módulo:** Financeiro
Borderô de cobrança gerado para consolidar cobranças periódicas (mensalidades, adesões e outros valores), permitindo controle por mês/ano de competência, vencimentos de parcelas e valor total a cobrar.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BDC_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `BDC_ID` | INTEGER | Não | Identificador único do borderô de cobrança. Parte da chave primária composta. |
| `BDC_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do borderô no sistema. |
| `BDC_DT_EMISSAO` | DATE | Sim | Data de emissão do borderô. |
| `BDC_USUARIO` | INTEGER | Sim | Identificador do usuário responsável pelo lançamento do borderô. |
| `BDC_STATUS` | VARCHAR(2) | Não | Status do borderô de cobrança. |
| `BDC_VALOR` | NUMERIC(15,2) | Sim | Valor total do borderô de cobrança. |
| `BDC_MES` | INTEGER | Sim | Mês de competência do borderô. |
| `BDC_ANO` | INTEGER | Sim | Ano de competência do borderô. |
| `BDC_VCTO_PRI_PARCELA` | DATE | Sim | Data de vencimento da primeira parcela. |
| `BDC_VCTO_SEG_PARCELA` | DATE | Sim | Data de vencimento da segunda parcela. |
| `BDC_VALOR_ADESAO` | NUMERIC(15,2) | Sim | Valor de adesão cobrado no borderô. |
| `BDC_VALOR_MENSALIDADE` | NUMERIC(15,2) | Sim | Valor de mensalidade cobrado no borderô. |
| `BDC_VALOR_OUTROS` | NUMERIC(15,2) | Sim | Outros valores cobrados no borderô. |
| `BDC_DESCRICAO` | VARCHAR(100) | Sim | Descrição livre do borderô de cobrança. |
| `BDC_TIPO` | VARCHAR(1) | Sim | Tipo do borderô de cobrança. |
| `BDC_MODALIDADE` | INTEGER | Sim | Identificador da modalidade de cobrança aplicada ao borderô. |

COMMENT ON COLUMN TB_BORDERO_COBRANCA.BDC_STATUS IS 'BDR_STATUS
------------
''A'' -> Ativo
''C'' -> Cancelado';
# Tabela TB_NOTA_FISCAL_REF

**Módulo:** Fiscal
Documentos fiscais referenciados por uma nota fiscal. Armazena chaves de acesso e dados de identificação de NF-e, CT-e, notas convencionais, produtor rural e cupons fiscais.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `NFR_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `NFR_NOTA_FISCAL` | INTEGER | Não | Identificador da nota fiscal que contém a referência (TB_NOTA_FISCAL.NF_ID). Parte da chave primária composta. |
| `NFR_SEQUENCIA` | INTEGER | Não | Sequencial do documento referenciado. Parte da chave primária composta. |
| `NFR_NOTA_FISCAL_REF` | INTEGER | Sim | Identificador da nota fiscal referenciada no cadastro interno. |
| `NFR_TIPO` | VARCHAR(3) | Sim | Tipo do documento: NFE = Nota Fiscal Eletrônica, CTE = Conhecimento de Transporte Eletrônico, NF = Nota Fiscal 1/A1, NFP = Nota Fiscal de Produtor Rural, ECF = Cupom Fiscal, NFC = NFC-e. |
| `NFR_CHAVE_ACESSO` | VARCHAR(44) | Sim | Chave de acesso do documento fiscal referenciado. |
| `NFR_UF` | VARCHAR(2) | Sim | Unidade federativa do documento referenciado. |
| `NFR_AAMM` | VARCHAR(10) | Sim | Ano e mês de emissão do documento referenciado. |
| `NFR_CNPJ_CPF` | VARCHAR(14) | Sim | CPF ou CNPJ do emitente do documento referenciado. |
| `NFR_IE` | VARCHAR(18) | Sim | Inscrição Estadual do emitente do documento referenciado. |
| `NFR_MODELO` | VARCHAR(2) | Sim | Modelo do documento fiscal referenciado. |
| `NFR_SERIE` | INTEGER | Sim | Série do documento referenciado. |
| `NFR_NUMERO` | INTEGER | Sim | Número do documento referenciado. |
| `NFR_ECF_MODELO` | VARCHAR(2) | Sim | Modelo do cupom fiscal: 2D, 2C, 2B ou N. |
| `NFR_ECF_NUMERO` | VARCHAR(10) | Sim | Número do equipamento ou documento ECF. |
| `NFR_COO` | VARCHAR(10) | Sim | Contador de Ordem de Operação do cupom fiscal. |

COMMENT ON COLUMN TB_NOTA_FISCAL_REF.NFR_TIPO IS 'NFE - Nota Fiscal Eletronica
CTE - Conhecimento Transporte Eletronico
NF - Nota Fiscal 1/A1
NFP - Nota Fiscal Produtor Rural
ECF - Cupom Fiscal
NFC - Nota Fiscal Consumidor Final - NFC-e';
COMMENT ON COLUMN TB_NOTA_FISCAL_REF.NFR_ECF_MODELO IS '2D - CUPOM FISCAL EMITIDO POR ECF
2C - CUPOM FISCAL PDV
2B - CUPOM FISCAL EMITIDO POR MAQUINA REGISTRADORA (NAO ECF)
N - NENHUM';

# Tabela TB_CARTAO_CREDITO_PLANILHA

**Módulo:** Financeiro / Cartão
Mapeamento das colunas de uma planilha de importação de vendas de cartão de crédito. Indica em qual coluna da planilha estão os dados de NSU, valor, taxa, bandeira, parcela, datas etc., permitindo automatizar a importação e conciliação.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CCP_ID` | INTEGER | Não | Identificador único do mapeamento. |
| `CCP_TAB` | INTEGER | Sim | Identificador/aba da planilha. |
| `CCP_LINHA_TITULO` | INTEGER | Sim | Linha da planilha onde está o cabeçalho. |
| `CCP_STATUS_BAIXA` | VARCHAR(200) | Sim | Coluna/regra para identificar o status de baixa. |
| `CCP_COL_STATUS` | VARCHAR(50) | Sim | Coluna referente ao status. |
| `CCP_COL_NSU` | VARCHAR(50) | Sim | Coluna do NSU. |
| `CCP_COL_VALOR_TOTAL` | VARCHAR(50) | Sim | Coluna do valor total. |
| `CCP_COL_VALOR_LIQUIDO` | VARCHAR(50) | Sim | Coluna do valor líquido. |
| `CCP_COL_TAXA` | VARCHAR(50) | Sim | Coluna da taxa (%). |
| `CCP_COL_VALOR_TAXA` | VARCHAR(50) | Sim | Coluna do valor da taxa. |
| `CCP_COL_AGENCIA` | VARCHAR(50) | Sim | Coluna da agência. |
| `CCP_COL_CONTA` | VARCHAR(50) | Sim | Coluna da conta. |
| `CCP_COL_BANCO` | VARCHAR(50) | Sim | Coluna do banco. |
| `CCP_COL_ESTABELECIMENTO` | VARCHAR(50) | Sim | Coluna do estabelecimento. |
| `CCP_COL_DT_VENDA` | VARCHAR(50) | Sim | Coluna da data de venda. |
| `CCP_COL_DT_PAGTO` | VARCHAR(50) | Sim | Coluna da data de pagamento. |
| `CCP_COL_BANDEIRA` | VARCHAR(50) | Sim | Coluna da bandeira. |
| `CCP_COL_FORMAPAGTO` | VARCHAR(50) | Sim | Coluna da forma de pagamento. |
| `CCP_COL_PARCELA` | VARCHAR(50) | Sim | Coluna da parcela. |
| `CCP_COL_QTDE_PARCELAS` | VARCHAR(50) | Sim | Coluna da quantidade de parcelas. |
| `CCP_CAMPO_ID` | VARCHAR(30) | Sim | Coluna de identificação única do registro. |

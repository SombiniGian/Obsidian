# Tabela TB_BORDERO_DEPOSITO_CHEQUE

**Módulo:** Financeiro
Tabela de relacionamento entre um borderô de depósito e os cheques recebidos que foram depositados nesse borderô. Cada linha associa um cheque recebido (TB_CHEQUE_RECEBIDO) ao borderô de depósito correspondente, registrando também o valor descontado pelo banco para o cheque.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BDDC_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `BDDC_BORDERO_DEPOSITO` | INTEGER | Não | Identificador do borderô de depósito (TB_BORDERO_DEPOSITO.BDD_ID). Parte da chave primária composta. |
| `BDDC_SEQUENCIAL` | INTEGER | Não | Sequencial do cheque dentro do borderô de depósito. Parte da chave primária composta. |
| `BDDC_CHEQUE_RECEBIDO` | INTEGER | Sim | Identificador do cheque recebido (TB_CHEQUE_RECEBIDO.CHR_ID) depositado no borderô. |
| `BDDC_VALOR_DESCONTADO` | NUMERIC(15,2) | Sim | Valor descontado pelo banco para o cheque neste borderô de depósito. |
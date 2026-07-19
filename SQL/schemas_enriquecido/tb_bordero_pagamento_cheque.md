# Tabela TB_BORDERO_PAGAMENTO_CHEQUE

**Módulo:** Financeiro / Contas a Pagar
Tabela de relacionamento entre um borderô de pagamento e os cheques recebidos que foram passados/utilizados nesse borderô. Cada linha associa um cheque recebido (TB_CHEQUE_RECEBIDO) ao borderô de pagamento correspondente.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BPIC_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `BPIC_BORDERO_PAGAMENTO` | INTEGER | Não | Identificador do borderô de pagamento (TB_BORDERO_PAGAMENTO.BDP_ID). Parte da chave primária composta. |
| `BPIC_SEQUENCIAL` | INTEGER | Não | Sequencial do cheque dentro do borderô de pagamento. Parte da chave primária composta. |
| `BPIC_CHEQUE_RECEBIDO` | INTEGER | Sim | Identificador do cheque recebido (TB_CHEQUE_RECEBIDO.CHR_ID) associado ao borderô. |
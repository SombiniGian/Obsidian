# Tabela TB_BORDERO_DEPOSITO

**Módulo:** Financeiro
Gera um borderô para depósito de cheques e valores em conta, consolidando totais de cheques, dinheiro, descontos aplicados pelo banco e valor efetivamente depositado, vinculando-se a uma conta bancária, plano de contas e data de depósito.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BDD_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `BDD_ID` | INTEGER | Não | Identificador único do borderô de depósito. Parte da chave primária composta. |
| `BDD_CONTA` | INTEGER | Sim | Identificador da conta (TB_CONTA.CNT_ID) de destino do depósito. |
| `BDD_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do borderô no sistema. |
| `BDD_DT_EMISSAO` | DATE | Sim | Data de emissão do borderô. |
| `BDD_QUANTIDADE_CHEQUE` | INTEGER | Sim | Quantidade de cheques incluídos no borderô de depósito. |
| `BDD_VALOR_CHEQUE` | NUMERIC(15,2) | Sim | Valor total dos cheques incluídos no borderô. |
| `BDD_USUARIO` | INTEGER | Sim | Identificador do usuário responsável pelo lançamento do borderô. |
| `BDD_STATUS` | VARCHAR(1) | Sim | Status do borderô de depósito. |
| `BDD_DESCONTO` | NUMERIC(15,2) | Sim | Percentual descontado pelo banco sobre o borderô de depósito. |
| `BDD_VALOR_DESCONTO` | NUMERIC(15,2) | Sim | Valor total descontado pelo banco no borderô. |
| `BDD_VALOR_DINHEIRO` | NUMERIC(15,2) | Sim | Valor em dinheiro incluído no borderô de depósito. |
| `BDD_VALOR_DEPOSITO` | NUMERIC(15,2) | Sim | Valor efetivamente depositado (após descontos). |
| `BDD_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total do borderô de depósito. |
| `BDD_PLANO_CONTAS` | INTEGER | Sim | Identificador do plano de contas (TB_PLANO_CONTA) associado ao borderô. |
| `BDD_TAXA_MENSAL` | NUMERIC(15,2) | Sim | Taxa mensal aplicada ao borderô de depósito. |
| `BDD_DT_DEPOSITO` | DATE | Sim | Data em que o depósito foi realizado. |
| `BDD_CONTA_DESCONTO` | INTEGER | Sim | Identificador da conta (TB_CONTA.CNT_ID) para lançamento do desconto bancário. |

COMMENT ON COLUMN TB_BORDERO_DEPOSITO.BDD_STATUS IS 'BDD_STATUS:
''A'' -> ABERTO
''P'' -> DEPOSITADO
''C'' -> CANCELADO
''D'' -> DESCONTADO';
COMMENT ON COLUMN TB_BORDERO_DEPOSITO.BDD_DESCONTO IS '% descontado pelo banco';
COMMENT ON COLUMN TB_BORDERO_DEPOSITO.BDD_VALOR_DESCONTO IS 'Valor descontado pelo banco';
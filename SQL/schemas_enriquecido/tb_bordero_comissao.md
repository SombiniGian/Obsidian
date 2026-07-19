# Tabela TB_BORDERO_COMISSAO

**Módulo:** Financeiro / Comissões
Borderô de comissão apurado por período para vendedores/comissionados, considerando vendas, devoluções, recebimentos, saldo flex e ordens de serviço.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BDC_EMPRESA` | INTEGER | Não | Identificador da empresa. |
| `BDC_ID` | INTEGER | Não | Identificador único do borderô de comissão. |
| `BDC_PESSOA` | INTEGER | Sim | FK para TB_PESSOA (vendedor/comissionado). |
| `BDC_STATUS` | VARCHAR(1) | Sim | Status do borderô (A=Aberto, F=Fechado, C=Cancelado). |
| `BDC_DT_INICIAL` | DATE | Sim | Data inicial do período de apuração. |
| `BDC_DT_FINAL` | DATE | Sim | Data final do período de apuração. |
| `BDC_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora do lançamento. |
| `BDC_DT_EMISSAO` | DATE | Sim | Data de emissão do borderô. |
| `BDC_TOTAL_VENDAS` | NUMERIC(15,2) | Sim | Soma das vendas no período. |
| `BDC_TOTAL_DEVOLUCAO` | NUMERIC(15,2) | Sim | Soma das devoluções no período. |
| `BDC_BC_COMISSAO` | NUMERIC(15,2) | Sim | Base de cálculo da comissão. |
| `BDC_TOTAL_COMISSAO` | NUMERIC(15,2) | Sim | Valor total da comissão apurada. |
| `BDC_COMISSAO` | NUMERIC(15,2) | Sim | Percentual de comissão aplicado. |
| `BDC_VALOR_COMISSAO` | NUMERIC(15,2) | Sim | Valor final da comissão. |
| `BDC_SALDO_FLEX_COMISSAO` | NUMERIC(15,2) | Sim | Valor do saldo flex incluído na comissão. |
| `BDC_PERC_SALDO_FLEX` | NUMERIC(15,2) | Sim | Percentual do saldo flex aplicado sobre a comissão. |
| `BDC_SALDO_FLEX` | NUMERIC(15,2) | Sim | Valor total de saldo flex no período. |
| `BDC_DESCONTO` | NUMERIC(15,2) | Sim | Percentual de desconto aplicado. |
| `BDC_VALOR_DESCONTO` | NUMERIC(15,2) | Sim | Valor de desconto aplicado. |
| `BDC_ACRESCIMO` | NUMERIC(15,2) | Sim | Percentual de acréscimo aplicado. |
| `BDC_VALOR_ACRESCIMO` | NUMERIC(15,2) | Sim | Valor de acréscimo aplicado. |
| `BDC_VALOR_META` | NUMERIC(15,2) | Sim | Valor da meta de vendas do vendedor. |
| `BDC_DESCRICAO` | VARCHAR(100) | Sim | Descrição/observação do borderô. |
| `BDC_COMISSAO_VENDAS` | NUMERIC(15,2) | Sim | Comissão sobre vendas. |
| `BDC_COMISSAO_DEV` | NUMERIC(15,2) | Sim | Comissão sobre devoluções. |
| `BDC_SALDO_FLEX_DEV` | NUMERIC(15,2) | Sim | Saldo flex sobre devoluções. |
| `BDC_SALDO_FLEX_VENDAS` | NUMERIC(15,2) | Sim | Saldo flex sobre vendas. |
| `BDC_DESP_FRETE` | NUMERIC(15,2) | Sim | Despesas de frete consideradas. |
| `BDC_PAGAMENTO` | INTEGER | Sim | FK para TB_PAGAMENTO gerado. |
| `BDC_TOTAL_RECEBIMENTO` | NUMERIC(15,2) | Sim | Soma dos recebimentos no período. |
| `BDC_COMISSAO_RECEBIMENTO` | NUMERIC(15,2) | Sim | Comissão sobre recebimentos. |
| `BDC_COMISSAO_CHEQUE_DEV` | NUMERIC(15,2) | Sim | Comissão sobre cheques devolvidos. |
| `BDC_VENDAS` | VARCHAR(1) | Sim | Considera vendas na apuração (S/N). |
| `BDC_DEVOLUCAO` | VARCHAR(1) | Sim | Considera devoluções na apuração (S/N). |
| `BDC_RECEBIMENTOS` | VARCHAR(1) | Sim | Considera recebimentos na apuração (S/N). |
| `BDC_TIPO_REC` | VARCHAR(1) | Sim | Tipo de recebimento considerado. |
| `BDC_CHEQUES_DEV` | VARCHAR(1) | Sim | Considera cheques devolvidos na apuração (S/N). |
| `BDC_TOTAL_CHEQUES_DEV` | NUMERIC(15,2) | Sim | Total de cheques devolvidos no período. |
| `COM_OS` | VARCHAR(1) | Sim | Considera ordens de serviço na apuração (S/N). |
| `BDC_TOTAL_OS` | NUMERIC(15,2) | Sim | Soma das OS no período. |
| `BDC_COMISSAO_OS` | NUMERIC(15,2) | Sim | Comissão sobre ordens de serviço. |
| `BDC_OS` | VARCHAR(1) | Sim | Flag para apuração de comissão de OS. |

COMMENT ON COLUMN TB_BORDERO_COMISSAO.BDC_SALDO_FLEX_COMISSAO IS 'Valor do saldo flex que vai incluir à comissão';
COMMENT ON COLUMN TB_BORDERO_COMISSAO.BDC_PERC_SALDO_FLEX IS 'Percentual do saldo flex irá somar na comissão do vendedor';

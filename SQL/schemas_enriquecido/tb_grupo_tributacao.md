# Tabela TB_GRUPO_TRIBUTACAO

**Módulo:** Fiscal
Grupo de tributação que agrupa CSTs e alíquotas de PIS, COFINS e IPI para entradas e saídas. Utilizado nos produtos e naturezas de operação para cálculo automático de impostos.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TRB_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `TRB_ID` | INTEGER | Não | Identificador único do grupo de tributação. Parte da chave primária composta. |
| `TRB_DESCRICAO` | VARCHAR(100) | Sim | Descrição do grupo. |
| `TRB_NCM` | VARCHAR(10) | Sim | NCM padrão do grupo (referência). |
| `TRB_PIS_CST_SAI` | VARCHAR(2) | Sim | CST do PIS na saída. |
| `TRB_PIS_ALIQ_SAI` | NUMERIC(15,2) | Sim | Alíquota do PIS na saída. |
| `TRB_PIS_NAT` | VARCHAR(3) | Sim | Natureza da receita do PIS. |
| `TRB_PIS_CST_ENT` | VARCHAR(2) | Sim | CST do PIS na entrada. |
| `TRB_PIS_ALIQ_ENT` | NUMERIC(15,2) | Sim | Alíquota do PIS na entrada. |
| `TRB_COFINS_CST_SAI` | VARCHAR(2) | Sim | CST do COFINS na saída. |
| `TRB_COFINS_ALIQ_SAI` | NUMERIC(15,2) | Sim | Alíquota do COFINS na saída. |
| `TRB_COFINS_NAT` | VARCHAR(3) | Sim | Natureza da receita do COFINS. |
| `TRB_COFINS_CST_ENT` | VARCHAR(2) | Sim | CST do COFINS na entrada. |
| `TRB_COFINS_ALIQ_ENT` | NUMERIC(15,2) | Sim | Alíquota do COFINS na entrada. |
| `TRB_IPI_CST_ENT` | VARCHAR(2) | Sim | CST do IPI na entrada. |
| `TRB_IPI_ALIQ_ENT` | NUMERIC(15,2) | Sim | Alíquota do IPI na entrada. |
| `TRB_IPI_CST_SAI` | VARCHAR(2) | Sim | CST do IPI na saída. |
| `TRB_IPI_ALIQ_SAI` | NUMERIC(15,2) | Sim | Alíquota do IPI na saída. |
| `TRB_IPI_ENQ` | VARCHAR(3) | Sim | Código de enquadramento do IPI. |
| `TRB_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. Default: current_timestamp. |
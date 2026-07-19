# Tabela TB_CENTRO_CUSTO

**Módulo:** Financeiro
Cadastro de centros de custo utilizados para classificação contábil e rateio em lançamentos financeiros, movimentos e documentos fiscais.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CEN_ID` | INTEGER | Não | Identificador único do centro de custo. |
| `CEN_EMPRESA` | INTEGER | Sim | Identificador da empresa à qual o centro de custo pertence. |
| `CEN_DESCRICAO` | VARCHAR(100) | Sim | Descrição do centro de custo. |
| `CEN_STATUS` | VARCHAR(1) | Sim | Status do centro de custo (A=Ativo, I=Inativo). |
| `CEN_PORCENTAGEM_RATEAR` | NUMERIC(15,2) | Sim | Porcentagem de rateio padrão do centro de custo (Default 0). |

COMMENT ON COLUMN TB_CENTRO_CUSTO.CEN_STATUS IS 'A - Ativo
I - Inativo';
COMMENT ON COLUMN TB_CENTRO_CUSTO.CEN_PORCENTAGEM_RATEAR IS 'Porcentagem usada como sugestão no rateio de lançamentos entre centros de custo';

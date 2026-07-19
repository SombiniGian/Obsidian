# Tabela TB_FORMULA

**Módulo:** Produção / Restaurante
Cadastro de fórmulas (receitas) com descrição e expressão de cálculo. Utilizada em produtos produzidos, manipulação de ingredientes e composição.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `FRM_ID` | INTEGER | Não | Identificador único da fórmula. |
| `FRM_TITULO` | VARCHAR(50) | Sim | Título da fórmula. |
| `FRM_DESCRICAO` | BLOB SUB_TYPE TEXT | Sim | Descrição detalhada da fórmula em formato texto. |
| `FRM_FORMULA` | BLOB SUB_TYPE TEXT | Sim | Expressão da fórmula em formato texto. |
| `FRM_STATUS` | VARCHAR(1) | Sim | Status da fórmula (A=Ativo, I=Inativo). |

COMMENT ON COLUMN TB_FORMULA.FRM_STATUS IS 'A - ATIVO
I - INATIVO';
# Tabela TB_PERDA

**Módulo:** Estoque
Registro de perdas de produtos (quebras, vencimentos, avarias, furtos). Pode movimentar ou não o estoque dependendo do tipo e impactar o custo médio.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRD_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PRD_ID` | INTEGER | Não | Identificador único da perda. Parte da chave primária composta. |
| `PRD_PRODUTO` | INTEGER | Sim | FK para TB_PRODUTO. |
| `PRD_DT_EMISSAO` | DATE | Sim | Data de emissão da perda. |
| `PRD_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento. |
| `PRD_TIPO` | VARCHAR(1) | Sim | Tipo da perda (Q=Quebra, V=Vencimento, A=Avaria, F=Furto, O=Outros). |
| `PRD_STATUS` | VARCHAR(1) | Sim | Status (A=Ativa, C=Cancelada). |
| `PRD_QUANTIDADE` | DECIMAL(15,4) | Sim | Quantidade perdida. |
| `PRD_USUARIO` | INTEGER | Sim | FK para TB_USUARIO. |
| `PRD_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações em formato binário. NUNCA selecione em queries SELECT. |
| `PRD_VALOR_UNITARIO` | NUMERIC(15,4) | Sim | Valor unitário do produto. |
| `PRD_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total da perda. |

COMMENT ON COLUMN TB_PERDA.PRD_TIPO IS 'Q - QUEBRA
V - VENCIMENTO
A - AVARIA
F - FURTO
O - OUTROS';
COMMENT ON COLUMN TB_PERDA.PRD_STATUS IS 'A - ATIVA
C - CANCELADA';
COMMENT ON COLUMN TB_PERDA.PRD_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
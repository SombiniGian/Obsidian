# Tabela TB_TRANSF_ESTOQUE

**Módulo:** Estoque
Transferência de mercadorias entre locais de estoque (e/ou empresas). Pode gerar nota fiscal e movimentar estoque com base no tipo de preço utilizado.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TRFE_ID` | INTEGER | Não | Identificador único da transferência. |
| `TRFE_STATUS` | VARCHAR(1) | Sim | Status (A=Aberta, F=Fechada, C=Cancelada, P=Processada). |
| `TRFE_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento. |
| `TRFE_DT_EMISSAO` | DATE | Sim | Data de emissão. |
| `TRFE_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que lançou. |
| `TRFE_EMP_ORIGEM` | INTEGER | Sim | Identificador da empresa de origem. |
| `TRFE_EMP_DESTINO` | INTEGER | Sim | Identificador da empresa de destino. |
| `TRFE_LOCAL_ORIGEM` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE de origem. |
| `TRFE_LOCAL_DESTINO` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE de destino. |
| `TRFE_TIPO_PRECO` | VARCHAR(1) | Sim | Tipo do preço utilizado (V=Venda, C=Custo, M=Médio). |
| `TRFE_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total da transferência. |
| `TRFE_OBSERVACAO` | VARCHAR(1000) | Sim | Observações da transferência. |
| `TRFE_NOTA_FISCAL` | INTEGER | Sim | FK para TB_NOTA_FISCAL vinculada. |
| `TRFE_TABELA_PRECO` | INTEGER | Sim | FK para TB_TABELA_PRECO utilizada. |
| `TRFE_TIPO_TABELA_PRECO` | VARCHAR(1) | Sim | Tipo de aplicação da tabela de preço (A=Acréscimo, D=Desconto). |
| `TRFE_TABELA_DESC_ACRES` | NUMERIC(15,2) | Sim | Percentual/valor de desconto/acréscimo aplicado pela tabela. |

COMMENT ON COLUMN TB_TRANSF_ESTOQUE.TRFE_TIPO_PRECO IS 'V - VENDA
C - CUSTO
M - MEDIO';
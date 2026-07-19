# Tabela TB_MOV_PRODUTO

**Módulo:** Estoque / Financeiro
Cabeçalho das movimentações de produtos, usado para registrar ajustes de entrada, saída ou diferença e seu destinatário, com os valores consolidados e a situação do lançamento.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `MVP_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `MVP_ID` | INTEGER | Não | Identificador único da movimentação de produto. Parte da chave primária composta. |
| `MVP_DT_EMISSAO` | DATE | Sim | Data de emissão da movimentação. |
| `MVP_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento da movimentação. |
| `MVP_USUARIO` | INTEGER | Sim | Identificador do usuário responsável pelo lançamento. |
| `MVP_TIPO` | VARCHAR(2) | Sim | Tipo da movimentação de produto. |
| `MVP_VALOR_ENTRADA` | NUMERIC(15,2) | Sim | Valor total dos produtos de entrada. |
| `MVP_VALOR_SAIDA` | NUMERIC(15,2) | Sim | Valor total dos produtos de saída. |
| `MVP_VALOR_DIFERENCA` | NUMERIC(15,2) | Sim | Diferença entre os valores de entrada e saída. |
| `MVP_OBSERVACAO` | VARCHAR(2000) | Sim | Observações da movimentação. |
| `MVP_STATUS` | VARCHAR(1) | Sim | Status da movimentação: A = Ativo, C = Cancelado. |
| `MVP_DESTINATARIO` | VARCHAR(1) | Sim | Tipo do destinatário: C = Cliente, F = Fornecedor, O = Comissionado. |
| `MVP_DEST_ID` | INTEGER | Sim | Identificador do destinatário. |
| `MVP_DEST_NOME` | VARCHAR(100) | Sim | Nome do destinatário, mantido para identificação do lançamento. |

COMMENT ON COLUMN TB_MOV_PRODUTO.MVP_STATUS IS 'A - ATIVO
C - CANCELADO';
COMMENT ON COLUMN TB_MOV_PRODUTO.MVP_DESTINATARIO IS 'C - CLIENTE
F - FORNECEDOR
O - COMISSIONADO';

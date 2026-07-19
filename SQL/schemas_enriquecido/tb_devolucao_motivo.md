# Tabela TB_DEVOLUCAO_MOTIVO

**Módulo:** Cadastros / Devoluções
Cadastro de motivos de devolução utilizados em devoluções de venda, pedidos, perdas, inventário, cargas e boletos. Define se o motivo se aplica a cada contexto (venda, inventário, perda, carga, desconto, boleto) e o plano de contas associado.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `DEVM_ID` | INTEGER | Não | Identificador único do motivo de devolução. Chave primária. |
| `DEVM_EMPRESA` | INTEGER | Sim | Identificador da empresa à qual o motivo pertence. |
| `DEVM_DESCRICAO` | VARCHAR(100) | Sim | Descrição do motivo de devolução. |
| `DEVM_PLANO_CONTA` | INTEGER | Sim | FK para TB_PLANO_CONTA — plano de contas associado ao motivo. |
| `DEVM_STATUS` | VARCHAR(1) | Sim | Status do motivo (A=Ativo, I=Inativo). |
| `DEVM_DEVOLUCAO` | VARCHAR(1) | Sim | Indica se o motivo aplica-se a devoluções (S/N). |
| `DEVM_VENDA` | VARCHAR(1) | Sim | Indica se o motivo aplica-se a vendas (S/N). |
| `DEVM_INVENTARIO` | VARCHAR(1) | Sim | Indica se o motivo aplica-se a inventário (S/N). |
| `DEVM_PERDA` | VARCHAR(1) | Sim | Indica se o motivo aplica-se a perdas (S/N). |
| `DEVM_CARGA` | VARCHAR(1) | Sim | Indica se o motivo aplica-se a cargas (S/N). |
| `DEVM_DESCONTO` | VARCHAR(1) | Sim | Indica se o motivo aplica-se a descontos (S/N). |
| `DEVM_BOLETO` | VARCHAR(1) | Sim | Indica se o motivo aplica-se a boletos (S/N). |

COMMENT ON COLUMN TB_DEVOLUCAO_MOTIVO.DEVM_STATUS IS 'A - Ativo / I - Inativo';
COMMENT ON COLUMN TB_DEVOLUCAO_MOTIVO.DEVM_DEVOLUCAO IS 'Para filtrar motivos válidos para devoluções utilize WHERE DEVM_DEVOLUCAO = ''S''.';

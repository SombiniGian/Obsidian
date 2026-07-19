# Tabela TB_INVENTARIO

**Módulo:** Estoque
Cabeçalho do inventário de estoque: registra a contagem física dos produtos em um determinado local/período, com percentual de estoque/preço a aplicar, valor de diferença e geração de acerto.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `INV_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `INV_ID` | INTEGER | Não | Identificador único do inventário. Parte da chave primária composta. |
| `INV_DT_INVENTARIO` | DATE | Sim | Data de referência do inventário. |
| `INV_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do inventário no sistema. |
| `INV_USUARIO` | INTEGER | Sim | FK para TB_USUARIO — usuário que lançou o inventário. |
| `INV_QUAL_ESTOQUE` | VARCHAR(1) | Sim | Qual estoque será considerado (L = Loja, D = Depósito). |
| `INV_PERC_ESTOQUE` | NUMERIC(15,4) | Sim | Percentual aplicado ao estoque. |
| `INV_QUAL_PRECO` | VARCHAR(1) | Sim | Qual preço será considerado (C = Custo, V = Venda). |
| `INV_PERC_PRECO` | NUMERIC(15,4) | Sim | Percentual aplicado ao preço. |
| `INV_VALOR` | NUMERIC(15,2) | Sim | Valor total de diferença apurado no inventário. |
| `INV_GERAR_ACERTO` | VARCHAR(1) | Sim | Indica se o inventário deve gerar acerto de estoque (S/N). |
| `INV_STATUS` | VARCHAR(1) | Sim | Status do inventário (A = Ativo, C = Cancelado). |
| `INV_ACAO` | VARCHAR(1) | Sim | Ação aplicada (A = Aumentar estoque, D = Diminuir estoque). |
| `INV_MOTIVO` | INTEGER | Sim | FK para TB_DEVOLUCAO_MOTIVO — motivo da diferença. |
| `INV_LOCAL_ESTOQUE` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE.LOC_ID. |

COMMENT ON COLUMN TB_INVENTARIO.INV_QUAL_ESTOQUE IS 'L - LOJA
D - DEPOSITO';
COMMENT ON COLUMN TB_INVENTARIO.INV_QUAL_PRECO IS 'C - CUSTO
V - VENDA';
COMMENT ON COLUMN TB_INVENTARIO.INV_GERAR_ACERTO IS 'S - SIM
N - NAO';
COMMENT ON COLUMN TB_INVENTARIO.INV_STATUS IS 'A - ATIVO
C - CANCELADO';
COMMENT ON COLUMN TB_INVENTARIO.INV_ACAO IS 'A - AUMENTAR
D - DIMINUIR';

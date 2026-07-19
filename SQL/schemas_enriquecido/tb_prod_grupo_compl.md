# Tabela TB_PROD_GRUPO_COMPL

**Módulo:** Restaurante / PDV
Associação de grupos de complemento (TB_GRUPO_COMPLEMENTO) a um produto (TB_PRODUTO). Permite controlar quais grupos de adicionais podem ser selecionados para cada produto, com integração ao iFood.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PGC_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID — produto associado ao grupo de complemento. Parte da chave primária composta. |
| `PGC_GRUPO` | INTEGER | Não | FK para TB_GRUPO_COMPLEMENTO — grupo de complemento vinculado. Parte da chave primária composta. |
| `PGC_ID_IFOOD` | VARCHAR(100) | Sim | ID do grupo na integração com iFood. |
| `PGC_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração do registro. |

COMMENT ON COLUMN TB_PROD_GRUPO_COMPL.PGC_PRODUTO IS 'FK para TB_PRODUTO.PRD_ID — use JOIN com TB_PRODUTO para obter descrição do produto.';
COMMENT ON COLUMN TB_PROD_GRUPO_COMPL.PGC_GRUPO IS 'FK para TB_GRUPO_COMPLEMENTO — use JOIN com TB_GRUPO_COMPLEMENTO para obter descrição do grupo.';

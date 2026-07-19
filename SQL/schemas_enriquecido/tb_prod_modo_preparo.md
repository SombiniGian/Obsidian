# Tabela TB_PROD_MODO_PREPARO

**Módulo:** Restaurante / PDV
Vínculo entre um produto (TB_PRODUTO) e um modo de preparo (TB_MODO_PREPARADO). Define quais modos de preparo estão disponíveis para o item, com controle de timestamp de alteração.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRMP_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PRMP_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID — produto associado ao modo de preparo. Parte da chave primária composta. |
| `PRMP_MODO_PREPARO` | INTEGER | Não | FK para TB_MODO_PREPARADO — modo de preparo vinculado. Parte da chave primária composta. |
| `PRMP_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração do registro. |

COMMENT ON COLUMN TB_PROD_MODO_PREPARO.PRMP_PRODUTO IS 'FK para TB_PRODUTO.PRD_ID — use JOIN com TB_PRODUTO para obter descrição do produto.';
COMMENT ON COLUMN TB_PROD_MODO_PREPARO.PRMP_MODO_PREPARO IS 'FK para TB_MODO_PREPARADO — use JOIN com TB_MODO_PREPARADO para obter descrição do modo de preparo.';

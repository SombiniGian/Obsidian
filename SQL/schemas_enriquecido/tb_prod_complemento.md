# Tabela TB_PROD_COMPLEMENTO

**Módulo:** Restaurante / PDV
Associação de complementos (TB_COMPLEMENTO) a um produto (TB_PRODUTO), permitindo definir quais adicionais/retiradas estão disponíveis para cada item. Opcionalmente vinculado a um grupo de complemento.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PCO_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID — produto ao qual o complemento está vinculado. Parte da chave primária composta. |
| `PCO_COMPLEMENTO` | INTEGER | Não | FK para TB_COMPLEMENTO.COM_ID — complemento vinculado. Parte da chave primária composta. |
| `PCO_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PCO_GRUPO` | INTEGER | Sim | FK para o grupo de complemento (TB_GRUPO_COMPLEMENTO) ao qual a associação pertence. |

COMMENT ON COLUMN TB_PROD_COMPLEMENTO.PCO_PRODUTO IS 'FK para TB_PRODUTO.PRD_ID — use JOIN com TB_PRODUTO para obter descrição do produto.';
COMMENT ON COLUMN TB_PROD_COMPLEMENTO.PCO_COMPLEMENTO IS 'FK para TB_COMPLEMENTO.COM_ID — use JOIN com TB_COMPLEMENTO para obter descrição, tipo e valor do complemento.';

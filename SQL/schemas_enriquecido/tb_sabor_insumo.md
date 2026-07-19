# Tabela TB_SABOR_INSUMO

**Módulo:** Produção / Sabor
Tabela que associa insumos (produtos) a um sabor, indicando a quantidade do insumo utilizada na composição do sabor.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `SBIN_ID` | INTEGER | Não | Identificador único do registro de insumo do sabor. |
| `SBIN_SABOR` | INTEGER | Sim | FK para TB_SABOR. Sabor ao qual o insumo pertence. |
| `SBIN_INSUMO` | INTEGER | Sim | FK para TB_PRODUTO. Produto/insumo que compõe o sabor. |
| `SBIN_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade do insumo utilizada no sabor. |

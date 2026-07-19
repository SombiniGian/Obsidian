# Tabela TB_PRODUTO_COMB_ORIGEM

**Módulo:** Fiscal / Combustíveis
Origem da mercadoria por UF para produtos do tipo combustível (vinculados a TB_PRODUTO). Permite informar a codificação de origem (0–8) e o percentual de origem por estado, atendendo às exigências fiscais de ICMS para combustível na NF-e.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PCBO_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID — produto combustível. Parte da chave primária composta. |
| `PCBO_COD_UF` | INTEGER | Não | FK para TB_ESTADO — código da UF de destino da operação. Parte da chave primária composta. |
| `PCBO_ORIGEM` | INTEGER | Sim | Código de origem da mercadoria (0 a 8) conforme tabela fiscal. |
| `PCBO_PERC_ORIGEM` | NUMERIC(15,6) | Sim | Percentual de origem da mercadoria para a UF informada. |

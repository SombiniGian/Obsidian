# Tabela TB_PROD_VARIACAO_ATRIBUTO

**Módulo:** Cadastros / Estoque
Relaciona uma variação de produto aos tipos e valores de atributos que a caracterizam, como cor, tamanho ou modelo.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PVA_ID` | INTEGER | Não | Identificador único do relacionamento. |
| `PVA_PRODUTO` | INTEGER | Não | Identificador do produto (TB_PRODUTO.PRD_ID). |
| `PVA_VARIACAO` | INTEGER | Não | Identificador da variação do produto (TB_PRODUTO_VARIACAO.PRV_ID). |
| `PVA_TIPO_ATRIBUTO` | INTEGER | Sim | Identificador do tipo de atributo associado à variação. |
| `PVA_ATRIBUTO` | INTEGER | Sim | Identificador do valor de atributo associado à variação. |

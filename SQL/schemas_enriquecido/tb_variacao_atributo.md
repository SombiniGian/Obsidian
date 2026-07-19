# Tabela TB_VARIACAO_ATRIBUTO

**Módulo:** Cadastros / Variações
Tabela de relacionamento que define a ordem e a composição das variações de produto, vinculando cada variação a um tipo de atributo.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `VAR_ID` | INTEGER | Não | Identificador único da variação de atributo. |
| `VAR_TIPO_VARIACAO` | INTEGER | Sim | Identificador do tipo de variação. |
| `VAR_TIPO_ATRIBUTO` | INTEGER | Sim | FK para TB_TIPO_ATRIBUTO.TAT_ID. |
| `VAR_ORDEM_DESCRICAO` | INTEGER | Sim | Ordem em que o atributo aparece na descrição da variação. |

# Tabela TB_COMPLEMENTO_COMP

**Módulo:** Cardápio / Complementos
Tabela que associa produtos (componentes) a um complemento, definindo a quantidade e a unidade utilizada em cada composição.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `COMP_COMPLEMENTO` | INTEGER | Não | FK para TB_COMPLEMENTO. Identificador do complemento. Parte da chave primária composta. |
| `COMP_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO. Produto/componente do complemento. Parte da chave primária composta. |
| `COMP_EMPRESA` | INTEGER | Sim | Identificador da empresa à qual a composição pertence. |
| `COMP_QUANTIDADE` | NUMERIC(15,4) | Sim | Quantidade do produto utilizada no complemento. |
| `COMP_UNIDADE` | VARCHAR(6) | Sim | Unidade de medida da quantidade. |

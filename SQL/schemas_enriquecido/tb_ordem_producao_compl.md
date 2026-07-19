# Tabela TB_ORDEM_PRODUCAO_COMPL

**Módulo:** Produção
Tabela de complementos vinculados a uma ordem de produção, indicando o produto do complemento, a quantidade e o tipo (insumo/produção).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `OPC_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `OPC_ORDEM_PRODUCAO` | INTEGER | Não | FK para TB_ORDEM_PRODUCAO. Identificador da ordem. Parte da chave primária composta. |
| `OPC_COMPLEMENTO` | INTEGER | Não | FK para TB_COMPLEMENTO. Complemento vinculado. Parte da chave primária composta. |
| `OPC_PRODUTO` | INTEGER | Sim | FK para TB_PRODUTO. Produto/componente do complemento. |
| `OPC_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade do complemento na ordem. |
| `OPC_TIPO` | VARCHAR(1) | Sim | Tipo do complemento (I=Insumo, P=Produto acabado). |
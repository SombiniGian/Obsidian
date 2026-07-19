# Tabela TB_CONFERENCIA_ITEM

**Módulo:** Estoque / Conferência
Tabela de itens da conferência de estoque, registrando a quantidade conferida por produto, com origem (pedido, nota, inventário etc.), unidade, variação e pessoa responsável.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CONI_CONFERENCIA` | INTEGER | Não | FK para TB_CONFERENCIA. Identificador da conferência. Parte da chave primária composta. |
| `CONI_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO. Produto conferido. Parte da chave primária composta. |
| `CONI_SEQUENCIA` | INTEGER | Não | Sequencial do item dentro da conferência. Parte da chave primária composta. |
| `CONI_QUANTIDADE` | NUMERIC(15,4) | Sim | Quantidade conferida do produto. |
| `CONI_UNIDADE` | VARCHAR(6) | Sim | Unidade de medida da quantidade conferida. |
| `CONI_QTDE_ORIGEM` | NUMERIC(15,4) | Sim | Quantidade de origem esperada para conferência. |
| `CONI_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do item. |
| `CONI_COD_DIGITADO` | VARCHAR(20) | Sim | Código do produto digitado na conferência (código de barras ou similar). |
| `CONI_VARIACAO` | INTEGER | Sim | FK para TB_PRODUTO_VARIACAO. Variação do produto conferido. |
| `CONI_ORIGEM` | VARCHAR(30) | Sim | Tabela/documento de origem (PEDIDO, NOTA, INVENTARIO etc.). |
| `CONI_ORIGEM_ID` | INTEGER | Sim | Identificador do registro de origem. |
| `CONI_ORIGEM_ID_SEQ` | INTEGER | Sim | Sequência do item de origem. |
| `CONI_PESSOA` | INTEGER | Sim | FK para TB_PESSOA relacionada à conferência. |
# Tabela TB_TRANSF_ESTOQUE_ITEM

**Módulo:** Estoque / Transferências
Tabela de itens das transferências de estoque entre locais. Registra produtos, quantidades, conversões de unidade, variações, tabela de preço aplicada e observações por item.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TRFI_TRANSF_ESTOQUE` | INTEGER | Não | FK para TB_TRANSF_ESTOQUE. Identificador da transferência. Parte da chave primária composta. |
| `TRFI_SEQUENCIA` | INTEGER | Não | Sequencial do item dentro da transferência. Parte da chave primária composta. |
| `TRFI_PRODUTO` | INTEGER | Sim | FK para TB_PRODUTO. Produto transferido. |
| `TRFI_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do item transferido. |
| `TRFI_UNIDADE` | VARCHAR(6) | Sim | Unidade de medida do item. |
| `TRFI_VALOR_UNITARIO` | NUMERIC(15,6) | Sim | Valor unitário do item. |
| `TRFI_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade transferida na unidade do item. |
| `TRFI_FATOR_CONVERSAO` | VARCHAR(1) | Sim | Fator de conversão entre unidade do item e unidade de estoque (M/D). |
| `TRFI_QTDE_CONVERSAO` | NUMERIC(15,4) | Sim | Fator numérico de conversão de unidade. |
| `TRFI_QTDE_ESTOQUE` | NUMERIC(15,6) | Sim | Quantidade equivalente na unidade de estoque. |
| `TRFI_OBSERVACAO` | VARCHAR(1000) | Sim | Observações do item. |
| `TRFI_VARIACAO` | INTEGER | Sim | FK para TB_PRODUTO_VARIACAO. Variação do produto transferido. |
| `TRFI_TABELA_PRECO` | INTEGER | Sim | FK para TB_TABELA_PRECO aplicada ao item. |
| `TRFI_TIPO_TABELA_PRECO` | VARCHAR(1) | Sim | Tipo da tabela de preço (A=Acrescimo, D=Desconto). |
| `TRFI_TABELA_PRECO_DESC_ACRES` | NUMERIC(15,2) | Sim | Percentual/valor de desconto ou acréscimo aplicado pela tabela de preço. |

# Tabela TB_OUTRAS_MOV_ITEM

**Módulo:** Estoque / Movimentações
Tabela de itens das "outras movimentações" de estoque. Registra produto, quantidade, conversões de unidade, estoque atual, tipo de produto e variação por item.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `OMPI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `OMPI_OUTRAS_MOV` | INTEGER | Não | FK para TB_OUTRAS_MOV. Identificador da movimentação. Parte da chave primária composta. |
| `OMPI_SEQUENCIA` | INTEGER | Não | Sequencial do item dentro da movimentação. Parte da chave primária composta. |
| `OMPI_PRODUTO` | INTEGER | Sim | FK para TB_PRODUTO movimentado. |
| `OMPI_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do item. |
| `OMPI_TIPO_MOV` | VARCHAR(1) | Sim | Tipo de movimento do item (E=Entrada, S=Saída). |
| `OMPI_OBSERVACAO` | VARCHAR(2000) | Sim | Observações do item. |
| `OMPI_DT_EMISSAO` | DATE | Sim | Data de emissão do item. |
| `OMPI_UNIDADE` | VARCHAR(6) | Sim | Unidade de medida do item. |
| `OMPI_VALOR_UNITARIO` | NUMERIC(15,6) | Sim | Valor unitário do item. |
| `OMPI_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade movimentada na unidade do item. |
| `OMPI_FATOR_CONVERSAO` | VARCHAR(1) | Sim | Fator de conversão entre unidade do item e unidade de estoque (M/D). |
| `OMPI_QTDE_CONVERSAO` | NUMERIC(15,4) | Sim | Fator numérico de conversão. |
| `OMPI_QTDE_ESTOQUE` | NUMERIC(15,6) | Sim | Quantidade equivalente na unidade de estoque. |
| `OMPI_ESTOQUE_ATUAL` | NUMERIC(15,6) | Sim | Estoque atual do produto no momento da movimentação. |
| `OMPI_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo do produto (P=Produto, S=Serviço, etc.). |
| `OMPI_VARIACAO` | INTEGER | Sim | FK para TB_PRODUTO_VARIACAO. Variação do produto movimentado. |
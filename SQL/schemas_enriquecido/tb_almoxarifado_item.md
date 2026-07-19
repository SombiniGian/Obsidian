# Tabela TB_ALMOXARIFADO_ITEM

**Módulo:** Estoque / Movimentações
Itens solicitados em uma requisição de almoxarifado (vinculados a TB_ALMOXARIFADO). Armazena produto, unidade, quantidade solicitada, valor unitário, variação e tabela de preço aplicada. A diferença para TB_ALMOXARIFADO_ATENDIDO é que esta tabela representa o pedido original, enquanto a atendida registra o que foi efetivamente separado/entregue.

## Campos

| Coluna                        | Tipo          | Nulo | Descrição                                                                                     |
| ----------------------------- | ------------- | ---- | --------------------------------------------------------------------------------------------- |
| `ALMI_ALMOXARIFADO`           | INTEGER       | Não  | FK para TB_ALMOXARIFADO.ALM_ID — movimento de almoxarifado. Parte da chave primária composta. |
| `ALMI_SEQUENCIA`              | INTEGER       | Não  | Sequencial do item dentro do movimento. Parte da chave primária composta.                     |
| `ALMI_PRODUTO`                | INTEGER       | Sim  | FK para TB_PRODUTO.PRD_ID — produto solicitado.                                               |
| `ALMI_VALOR_TOTAL`            | NUMERIC(15,4) | Sim  | Valor total do item (quantidade × valor unitário).                                            |
| `ALMI_UNIDADE`                | VARCHAR(6)    | Sim  | Unidade de medida do produto solicitado (ex.: UN, KG).                                        |
| `ALMI_VALOR_UNITARIO`         | NUMERIC(15,6) | Sim  | Valor unitário do produto no item.                                                            |
| `ALMI_QUANTIDADE`             | NUMERIC(15,6) | Sim  | Quantidade solicitada do produto.                                                             |
| `ALMI_FATOR_CONVERSAO`        | VARCHAR(1)    | Sim  | Operação aplicada no fator de conversão (M/D).                                                |
| `ALMI_QTDE_CONVERSAO`         | NUMERIC(15,4) | Sim  | Fator numérico de conversão aplicado à quantidade.                                            |
| `ALMI_FATOR_VOLUME`           | VARCHAR(1)    | Sim  | Operação aplicada ao fator de volume (M/D).                                                   |
| `ALMI_VOLUME`                 | INTEGER       | Sim  | Quantidade de volumes equivalentes do item.                                                   |
| `ALMI_QTDE_ESTOQUE`           | NUMERIC(15,6) | Sim  | Quantidade em estoque no momento da requisição.                                               |
| `ALMI_OBSERVACAO`             | VARCHAR(1000) | Sim  | Observações do item solicitado.                                                               |
| `ALMI_VARIACAO`               | INTEGER       | Sim  | FK para TB_PRODUTO_VARIACAO — variação do produto.                                            |
| `ALMI_TABELA_PRECO`           | INTEGER       | Sim  | FK para TB_TABELA_PRECO aplicada ao item.                                                     |
| `ALMI_TIPO_TABELA_PRECO`      | VARCHAR(1)    | Sim  | Tipo da tabela de preço aplicada (A=Acrescimo, D=Desconto).                                   |
| `ALMI_TABELA_PRECO_DESC_ACRE` | NUMERIC(15,2) | Sim  | Percentual/valor de desconto ou acréscimo aplicado pela tabela de preço.                      |
| `ALMI_STATUS_VALOR`           | VARCHAR(1)    | Sim  | Status de processamento do valor do item.                                                     |
| `ALMI_TIPO_PRODUTO`           | VARCHAR(1)    | Sim  | Tipo do produto solicitado (ex.: P=Produto, S=Serviço).                                       |

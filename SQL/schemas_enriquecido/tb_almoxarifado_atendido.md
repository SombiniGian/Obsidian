# Tabela TB_ALMOXARIFADO_ATENDIDO

**Módulo:** Estoque / Movimentações
Itens efetivamente atendidos de uma requisição de almoxarifado (vinculados a TB_ALMOXARIFADO). Registra produto, unidade, quantidade atendida, valor, estoque no momento, variação, tabela de preço aplicada e dados da empresa/local atendente.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `ALMA_ALMOXARIFADO` | INTEGER | Não | FK para TB_ALMOXARIFADO.ALM_ID — movimento de almoxarifado atendido. Parte da chave primária composta. |
| `ALMA_SEQUENCIA` | INTEGER | Não | Sequencial do item dentro do atendimento. Parte da chave primária composta. |
| `ALMA_PRODUTO` | INTEGER | Sim | FK para TB_PRODUTO.PRD_ID — produto atendido. |
| `ALMA_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do item atendido (quantidade × valor unitário). |
| `ALMA_UNIDADE` | VARCHAR(6) | Sim | Unidade de medida do produto atendido (ex.: UN, KG). |
| `ALMA_VALOR_UNITARIO` | NUMERIC(15,6) | Sim | Valor unitário do produto no atendimento. |
| `ALMA_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade atendida do produto. |
| `ALMA_FATOR_CONVERSAO` | VARCHAR(1) | Sim | Operação aplicada no fator de conversão (M/D). |
| `ALMA_QTDE_CONVERSAO` | NUMERIC(15,4) | Sim | Fator numérico de conversão aplicado à quantidade. |
| `ALMA_FATOR_VOLUME` | VARCHAR(1) | Sim | Operação aplicada ao fator de volume (M/D). |
| `ALMA_VOLUME` | INTEGER | Sim | Quantidade de volumes equivalentes do item atendido. |
| `ALMA_QTDE_ESTOQUE` | NUMERIC(15,6) | Sim | Quantidade em estoque no momento do atendimento. |
| `ALMA_OBSERVACAO` | VARCHAR(1000) | Sim | Observações do item atendido. |
| `ALMA_VARIACAO` | INTEGER | Sim | FK para TB_PRODUTO_VARIACAO — variação do produto atendida. |
| `ALMA_TABELA_PRECO` | INTEGER | Sim | FK para TB_TABELA_PRECO aplicada ao item. |
| `ALMA_TIPO_TABELA_PRECO` | VARCHAR(1) | Sim | Tipo da tabela de preço aplicada (A=Acrescimo, D=Desconto). |
| `ALMA_TABELA_PRECO_DESC_ACRE` | NUMERIC(15,2) | Sim | Percentual/valor de desconto ou acréscimo aplicado pela tabela de preço. |
| `ALMA_EMPRESA_ATENDENTE` | INTEGER | Sim | Identificador da empresa que está atendendo a requisição. |
| `ALMA_LOCAL_ESTOQUE_ATENDENTE` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE.LOC_ID — local de estoque que está atendendo a requisição. |
| `ALMA_STATUS_VALOR` | VARCHAR(1) | Sim | Status de processamento do valor do item atendido. |
| `ALMA_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo do produto atendido (ex.: P=Produto, S=Serviço). |
| `ALMA_VOLUME_ITEM` | INTEGER | Sim | Volume unitário do item (caixa/embalagem). |
| `ALMA_DT_EMISSAO` | DATE | Sim | Data de emissão do atendimento. |
| `ALMA_USUARIO` | INTEGER | Sim | Identificador do usuário que registrou o atendimento. |

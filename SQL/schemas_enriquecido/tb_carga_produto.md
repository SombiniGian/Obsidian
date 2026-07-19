# Tabela TB_CARGA_PRODUTO

**Módulo:** Logística / Cargas
Itens de produtos que compõem uma carga (romaneio), permitindo controlar quantidade, metragem, pesos, volumes, valores e fatores de conversão por produto.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CARGP_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `CARGP_CARGA` | INTEGER | Não | Identificador da carga (TB_CARGA.CARG_ID). Parte da chave primária composta. |
| `CARGP_SEQUENCIA` | INTEGER | Não | Sequencial do item dentro da carga. Parte da chave primária composta. |
| `CARGP_PRODUTO` | INTEGER | Sim | Identificador do produto (TB_PRODUTO.PRD_ID) carregado. |
| `CARGP_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade do produto na carga. |
| `CARGP_METRAGEM` | NUMERIC(15,4) | Sim | Metragem ocupada pelo produto na carga. |
| `CARGP_PESO_BRUTO` | NUMERIC(15,4) | Sim | Peso bruto do item na carga. |
| `CARGP_PESO_LIQUIDO` | NUMERIC(15,4) | Sim | Peso líquido do item na carga. |
| `CARGP_VOLUMES` | INTEGER | Sim | Quantidade de volumes do item na carga. |
| `CARGP_UNIDADE` | VARCHAR(3) | Sim | Unidade de medida utilizada no item da carga. |
| `CARGP_VALOR_UNITARIO` | NUMERIC(15,4) | Sim | Valor unitário do produto no item da carga. |
| `CARGP_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do item (quantidade x valor unitário). |
| `CARGP_FATOR_VOLUME` | VARCHAR(1) | Sim | Operação aplicada ao fator de volume (M = Multiplicar, D = Dividir). |
| `CARGP_VOLUME` | INTEGER | Sim | Volume (capacidade) considerado no cálculo do item. |
| `CARGP_FATOR_CONVERSAO` | VARCHAR(1) | Sim | Operação aplicada ao fator de conversão (M = Multiplicar, D = Dividir). |
| `CARGP_QTDE_CONVERSAO` | NUMERIC(15,4) | Sim | Quantidade convertida aplicada ao item conforme o fator de conversão. |
| `CARGP_QTDE_ESTOQUE` | NUMERIC(15,6) | Sim | Quantidade em estoque do produto no momento do lançamento da carga. |
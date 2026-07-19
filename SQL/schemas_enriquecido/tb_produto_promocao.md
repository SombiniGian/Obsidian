# Tabela TB_PRODUTO_PROMOCAO

**Módulo:** Comercial / Vendas
Faixas de promoção por quantidade de um produto: define o valor promocional (ou percentual) aplicado quando a quantidade vendida está dentro de uma faixa (quantidade inicial até quantidade final). É a tabela base das promoções do tipo "leve X por Y".

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRDM_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PRDM_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID — produto em promoção. Parte da chave primária composta. |
| `PRDM_SEQUENCIA` | SMALLINT | Não | Sequencial da faixa de promoção. Parte da chave primária composta. |
| `PRDM_QTDE_INI` | NUMERIC(15,4) | Sim | Quantidade inicial da faixa da promoção. |
| `PRDM_QTDE_FIM` | NUMERIC(15,4) | Sim | Quantidade final da faixa da promoção. |
| `PRDM_VALOR_PROM` | NUMERIC(15,4) | Sim | Valor promocional (ou percentual, conforme PRDM_TIPO_VALOR) aplicado na faixa. |
| `PRDM_TIPO_VALOR` | VARCHAR(1) | Sim | Tipo do valor promocional (P = Percentual, V = Valor). |

COMMENT ON COLUMN TB_PRODUTO_PROMOCAO.PRDM_PRODUTO IS 'FK para TB_PRODUTO.PRD_ID — use JOIN com TB_PRODUTO para obter descrição do produto.';
COMMENT ON COLUMN TB_PRODUTO_PROMOCAO.PRDM_TIPO_VALOR IS 'P - PERCENTUAL
V - VALOR';

# Tabela TB_PROMOCAO_ENCARTE_QTDE

**Módulo:** Comercial / Vendas
Faixas de quantidade com preço promocional por produto dentro de uma promoção de encarte. Define, para cada produto participante, o valor promocional aplicado quando a quantidade vendida está dentro de uma faixa (quantidade inicial até quantidade final).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PREQ_PROMOCAO_ENCARTE` | INTEGER | Não | FK para TB_PROMOCAO_ENCARTE — encarte da promoção. Parte da chave primária composta. |
| `PREQ_PROMOCAO` | INTEGER | Não | FK para a promoção (TB_PRODUTO_PROMOCAO) à qual a faixa pertence. Parte da chave primária composta. |
| `PREQ_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID — produto participante da promoção. Parte da chave primária composta. |
| `PREQ_SEQUENCIA` | SMALLINT | Não | Sequencial da faixa dentro do produto/encarte. Parte da chave primária composta. |
| `PREQ_QTDE_INI` | NUMERIC(15,4) | Sim | Quantidade inicial da faixa promocional. |
| `PREQ_QTDE_FIM` | NUMERIC(15,4) | Sim | Quantidade final da faixa promocional. |
| `PREQ_VALOR_PROM` | NUMERIC(15,4) | Sim | Valor promocional (ou percentual, conforme PREQ_TIPO_VALOR) aplicado na faixa. |
| `PREQ_TIPO_VALOR` | VARCHAR(1) | Sim | Tipo do valor promocional (P = Percentual, V = Valor). |

COMMENT ON COLUMN TB_PROMOCAO_ENCARTE_QTDE.PREQ_PRODUTO IS 'FK para TB_PRODUTO.PRD_ID — use JOIN com TB_PRODUTO para obter descrição do produto.';
COMMENT ON COLUMN TB_PROMOCAO_ENCARTE_QTDE.PREQ_TIPO_VALOR IS 'P - PERCENTUAL
V - VALOR';

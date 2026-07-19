# Tabela TB_PRODUTO_COMPOSICAO

**Módulo:** Produção / Estoque
Composição (ficha técnica) de um produto acabado/semi-acabado: define a matéria-prima, quantidade, fator de rendimento, sabor, unidade e tipo de produto utilizado na produção. É a base para a geração de ordens de produção e apontamentos de consumo.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRDC_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PRDC_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID — produto acabado/principal. Parte da chave primária composta. |
| `PRDC_MATERIA_PRIMA` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID — matéria-prima consumida. Parte da chave primária composta. |
| `PRDC_DT_INICIO` | DATE | Sim | Data de início da validade da composição. |
| `PRDC_UNIDADE` | VARCHAR(6) | Sim | Unidade de medida da matéria-prima na composição. |
| `PRDC_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo do produto componente na composição. |
| `PRDC_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade da matéria-prima consumida por unidade produzida. |
| `PRDC_FATOR_RENDIMENTO` | NUMERIC(15,6) | Sim | Fator de rendimento aplicado à quantidade (perdas/ganhos de processo). |
| `PRDC_SABOR` | INTEGER | Sim | FK para TB_SABOR — sabor associado à matéria-prima. |
| `PRDC_ID` | INTEGER | Não | Identificador único da composição. Parte da chave primária composta. |
| `PRDC_TIPO_VALOR` | VARCHAR(1) | Sim | Tipo do valor (P=Percentual, V=Valor). |
| `PRDC_VALOR_SERVICO` | NUMERIC(15,2) | Sim | Valor de mão-de-obra/serviço aplicado à composição. |
| `PRDC_TIPO_TP` | VARCHAR(1) | Sim | Tipo do tipo de produto. |
| `PRDC_TP` | INTEGER | Sim | Identificador do tipo de produto. |
| `PRDC_NAO_PRODUZIR_LOTE` | VARCHAR(1) | Sim | Indica se a matéria-prima não deve produzir lote (S/N). |

COMMENT ON COLUMN TB_PRODUTO_COMPOSICAO.PRDC_PRODUTO IS 'FK para TB_PRODUTO.PRD_ID — identifica o produto acabado/principal. Use JOIN com TB_PRODUTO para obter descrição.';
COMMENT ON COLUMN TB_PRODUTO_COMPOSICAO.PRDC_MATERIA_PRIMA IS 'FK para TB_PRODUTO.PRD_ID — identifica a matéria-prima consumida. Use JOIN com TB_PRODUTO para obter descrição da matéria-prima.';

# Tabela TB_PRODUTO_UNIDADE

**Módulo:** Estoque / Cadastros
Unidades de medida alternativas para um mesmo produto (vinculado a TB_PRODUTO). Permite registrar fator de conversão entre unidades, preços de venda/compra por unidade, código de barras, peso, volume, metragem cúbica e flags de utilização para venda/compra.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRDU_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PRDU_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID — produto ao qual a unidade pertence. Parte da chave primária composta. |
| `PRDU_SEQUENCIA` | INTEGER | Não | Sequencial da unidade dentro do produto. Parte da chave primária composta. |
| `PRDU_UNIDADE` | VARCHAR(6) | Sim | Unidade de medida da alternativa (ex.: UN, CX, KG, M). |
| `PRDU_FATOR_CONVERSAO` | VARCHAR(1) | Sim | Operação aplicada no fator: M = Multiplicar, D = Dividir. |
| `PRDU_QUANTIDADE` | NUMERIC(15,4) | Sim | Fator numérico de conversão entre a unidade alternativa e a unidade padrão do produto. |
| `PRDU_PRECO_VENDA` | NUMERIC(15,6) | Sim | Preço de venda do produto nesta unidade. |
| `PRDU_COD_BARRAS` | VARCHAR(20) | Sim | Código de barras (EAN) do produto nesta unidade. |
| `PRDU_UTILIZAR_VENDA` | VARCHAR(1) | Sim | Indica se a unidade pode ser usada em vendas (S/N). |
| `PRDU_UTILIZAR_COMPRA` | VARCHAR(1) | Sim | Indica se a unidade pode ser usada em compras (S/N). |
| `PRDU_PRECO_COMPRA` | NUMERIC(15,6) | Sim | Preço de compra do produto nesta unidade. |
| `PRDU_LUCRO` | NUMERIC(15,2) | Sim | Percentual de lucro aplicado nesta unidade. |
| `PRDU_FATOR_VOLUME` | VARCHAR(1) | Sim | Indica se o fator de volume deve multiplicar ou dividir (M/D). |
| `PRDU_VOLUME` | INTEGER | Sim | Quantidade de volumes correspondente a uma unidade. |
| `PRDU_PESO_BRUTO` | NUMERIC(15,3) | Sim | Peso bruto do produto nesta unidade. |
| `PRDU_PESO_LIQUIDO` | NUMERIC(15,3) | Sim | Peso líquido do produto nesta unidade. |
| `PRDU_METRAGEM_CUBICA` | NUMERIC(15,4) | Sim | Metragem cúbica (m³) ocupada pelo produto nesta unidade. |
| `PRDU_PRECO_CUSTO` | NUMERIC(15,6) | Sim | Preço de custo do produto nesta unidade. |
| `PRDU_REFERENCIA` | VARCHAR(100) | Sim | Referência/descrição auxiliar da unidade (ex.: "Caixa com 12 un"). |
| `PRDU_PRECO_MINIMO` | NUMERIC(15,6) | Sim | Preço mínimo permitido para venda nesta unidade. |

COMMENT ON COLUMN TB_PRODUTO_UNIDADE.PRDU_FATOR_CONVERSAO IS 'M - Multiplicar
D - Dividir';

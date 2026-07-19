# Tabela TB_PRODUTO_MOVIMENTO_NF

**Módulo:** Fiscal / Estoque
Movimentações de estoque originadas por documentos fiscais. Registra entradas e saídas de produtos vinculadas à nota fiscal, com custos e valores de ICMS-ST e FCP-ST.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PMNF_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PMNF_PRODUTO` | INTEGER | Não | Identificador do produto (TB_PRODUTO.PRD_ID). Parte da chave primária composta. |
| `PMNF_SEQUENCIA` | INTEGER | Não | Sequencial da movimentação do produto. Parte da chave primária composta. |
| `PMNF_TIPO` | VARCHAR(3) | Sim | Tipo da movimentação de estoque, como entrada, saída ou acerto. |
| `PMNF_DT_MOVIMENTO` | DATE | Sim | Data do movimento de estoque. |
| `PMNF_QUANTIDADE` | NUMERIC(15,4) | Sim | Quantidade movimentada. |
| `PMNF_ORIGEM_NUMERO` | INTEGER | Sim | Número do documento que originou o movimento. |
| `PMNF_ORIGEM_MOVIMENTO` | VARCHAR(10) | Sim | Tipo ou módulo de origem do movimento. |
| `PMNF_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora do lançamento do movimento. |
| `PMNF_USUARIO` | INTEGER | Sim | Identificador do usuário responsável pelo lançamento. |
| `PMNF_HISTORICO` | VARCHAR(100) | Sim | Histórico ou descrição do movimento. |
| `PMNF_PROD_COR` | INTEGER | Sim | Identificador da cor ou grade do produto. |
| `PMNF_ORIGEM_ITEM` | INTEGER | Sim | Sequencial do item no documento de origem. |
| `PMNF_CUSTO_UN` | NUMERIC(15,4) | Sim | Custo unitário do produto no movimento. |
| `PMNF_CUSTO` | NUMERIC(15,4) | Sim | Custo total do produto movimentado. |
| `PMNF_ST_BC` | NUMERIC(15,2) | Sim | Base de cálculo do ICMS-ST associada ao movimento. |
| `PMNF_ST_VALOR` | NUMERIC(15,2) | Sim | Valor do ICMS-ST associado ao movimento. |
| `PMNF_ICMS_VALOR` | NUMERIC(15,2) | Sim | Valor do ICMS do movimento. |
| `PMNF_FCP_ST_BC` | NUMERIC(15,2) | Sim | Base de cálculo do FCP-ST. |
| `PMNF_FCP_ST_VALOR` | NUMERIC(15,2) | Sim | Valor do FCP-ST. |
| `PMNF_FCP_ST_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do FCP-ST. |
| `PMNF_LOCAL` | INTEGER | Sim | Identificador do local de estoque do movimento. |
| `PMNF_ID` | INTEGER | Não | Identificador do movimento fiscal. |
| `PMNF_VARIACAO` | INTEGER | Sim | Identificador da variação do produto (TB_PRODUTO_VARIACAO.PRV_ID). |

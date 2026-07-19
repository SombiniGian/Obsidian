# Tabela TB_ORDEM_PRODUCAO

**Módulo:** Produção / Estoque
Ordens de produção para transformar insumos em produtos, controlar origem, colaborador, situação, lote, quantidade, custos e vínculos com pedidos ou notas fiscais.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `OP_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `OP_ID` | INTEGER | Não | Identificador único da ordem de produção. Parte da chave primária composta. |
| `OP_PRODUTO` | INTEGER | Sim | Produto a ser produzido (TB_PRODUTO.PRD_ID). |
| `OP_DT_EMISSAO` | DATE | Sim | Data de emissão da ordem de produção. |
| `OP_STATUS` | VARCHAR(1) | Sim | Status da ordem: A = Aberto, E = Em produção, P = Produzido. |
| `OP_ORIGEM` | VARCHAR(20) | Sim | Módulo ou documento que originou a ordem. |
| `OP_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem. |
| `OP_USUARIO` | INTEGER | Sim | Identificador do usuário responsável pelo lançamento. |
| `OP_COLABORADOR` | INTEGER | Sim | Identificador do colaborador responsável pela produção. |
| `OP_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento da ordem. |
| `OP_DT_PRODUCAO` | DATE | Sim | Data prevista ou realizada da produção. |
| `OP_UNIDADE` | VARCHAR(3) | Sim | Unidade de medida da produção. |
| `OP_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo do produto a ser produzido. |
| `OP_OBSERVACAO` | VARCHAR(2000) | Sim | Observações da ordem de produção. |
| `OP_NR_CONTROLE` | VARCHAR(20) | Sim | Número de controle da ordem. |
| `OP_DESCRICAO` | VARCHAR(100) | Sim | Descrição da ordem ou do produto produzido. |
| `OP_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total da produção. |
| `OP_SEQ_ORIGEM` | INTEGER | Sim | Sequencial do item do documento de origem. |
| `OP_LOTE_PRODUCAO` | INTEGER | Sim | Identificador do lote de produção. |
| `OP_DT_INICIO` | DATE | Sim | Data de início da produção. |
| `OP_TIPO_PRECO` | VARCHAR(1) | Sim | Tipo de preço utilizado no cálculo da ordem. |
| `OP_CLASSIFICACAO` | INTEGER | Sim | Classificação da ordem de produção. |
| `OP_SITUACAO` | INTEGER | Sim | Situação operacional da ordem. |
| `OP_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção em processos de produção (S/N). |
| `OP_TIPO` | VARCHAR(1) | Sim | Tipo da ordem de produção. |
| `OP_LOCAL_ESTOQUE` | INTEGER | Sim | Local de estoque da produção (TB_LOCAL_ESTOQUE.LOC_ID). |
| `OP_NOTA_FISCAL` | INTEGER | Sim | Nota fiscal relacionada à ordem. |
| `OP_NOTA_FISCAL_PROD_ACABADO` | INTEGER | Sim | Nota fiscal do produto acabado. |
| `OP_COD_SABORES` | VARCHAR(100) | Sim | Códigos dos sabores associados à produção, quando aplicável. |
| `OP_VALOR_INSUMO` | NUMERIC(15,2) | Sim | Valor dos insumos utilizados. |
| `OP_VALOR_SERVICO` | NUMERIC(15,2) | Sim | Valor do serviço de produção. |
| `OP_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade a ser produzida. |
| `OP_QUANTIDADE_ORIGINAL` | NUMERIC(15,6) | Sim | Quantidade original solicitada para produção. |
| `OP_ID_PAI` | INTEGER | Sim | Identificador da ordem de produção pai. |
| `OP_PROD_PARCIAL` | VARCHAR(1) | Sim | Indica se a produção é parcial (S/N). |
| `OP_VARIACAO` | INTEGER | Sim | Identificador da variação do produto (TB_PRODUTO_VARIACAO.PRV_ID). |

COMMENT ON COLUMN TB_ORDEM_PRODUCAO.OP_STATUS IS 'A - ABERTO
E - EM PRODUCAO
P - PRODUZIDO';

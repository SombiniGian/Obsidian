# Tabela TB_ORDEM_PRODUCAO_ITEM

**Módulo:** Produção / Estoque
Itens (componentes/insumos) que compõem uma ordem de produção (TB_ORDEM_PRODUCAO). Registra o produto, unidade, quantidades, fator de rendimento, sabor, complemento, valor unitário e total para apurar o custo e os insumos consumidos na produção.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `OPI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `OPI_ORDEM_PRODUCAO` | INTEGER | Não | FK para TB_ORDEM_PRODUCAO.OP_ID. Parte da chave primária composta. |
| `OPI_SEQUENCIA` | INTEGER | Não | Sequencial do item dentro da ordem de produção. Parte da chave primária composta. |
| `OPI_DT_EMISSAO` | DATE | Sim | Data de emissão do item. |
| `OPI_COLABORADOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID — colaborador responsável pelo item. |
| `OPI_VALOR_UNITARIO` | NUMERIC(15,4) | Sim | Valor unitário do insumo/produto. |
| `OPI_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do item (quantidade × valor unitário). |
| `OPI_PRODUTO` | INTEGER | Sim | FK para TB_PRODUTO.PRD_ID — produto/insumo do item. |
| `OPI_UNIDADE` | VARCHAR(3) | Sim | Unidade de medida do item (UN, KG, LT etc.). |
| `OPI_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo do produto (P=Produto, S=Serviço, I=Insumo etc.). |
| `OPI_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade consumida/necessária do produto. |
| `OPI_FATOR_RENDIMENTO` | NUMERIC(15,6) | Sim | Fator de rendimento do insumo no processo produtivo. |
| `OPI_SABOR` | INTEGER | Sim | FK para TB_SABOR — sabor associado ao item, quando aplicável. |
| `OPI_COMPLEMENTO` | INTEGER | Sim | FK para TB_COMPLEMENTO — complemento associado ao item. |
| `OPI_TIPO_VALOR` | VARCHAR(1) | Sim | Tipo do valor aplicado (V=Valor, P=Percentual). |
| `OPI_VALOR_TIPO` | NUMERIC(15,2) | Sim | Valor conforme o tipo (valor absoluto ou percentual). |

COMMENT ON COLUMN TB_ORDEM_PRODUCAO_ITEM.OPI_ORDEM_PRODUCAO IS 'FK para TB_ORDEM_PRODUCAO.OP_ID — use JOIN por OPI_ORDEM_PRODUCAO.';
COMMENT ON COLUMN TB_ORDEM_PRODUCAO_ITEM.OPI_PRODUTO IS 'FK para TB_PRODUTO.PRD_ID — use JOIN por PRD_ID para obter descrição do produto.';

# Tabela TB_PRODUTO_MOVIMENTO

**Módulo:** Estoque
Tabela central de movimentações de estoque por produto. Registra entradas, saídas e acertos de estoque com origem em pedidos de venda, compras, acertos de inventário ou cadastros de produto. É a fonte primária para consultas de histórico de estoque, kardex e relatórios de movimentação.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRDM_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PRDM_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRO_ID. Parte da chave primária composta. |
| `PRDM_SEQUENCIA` | INTEGER | Não | Sequência do movimento dentro do produto/empresa. Parte da chave primária composta. |
| `PRDM_PROD_COR` | INTEGER | Sim | FK para TB_PRODUTO_VARIACAO — cor/variante do produto. |
| `PRDM_TIPO` | VARCHAR(3) | Sim | Tipo do movimento: ENT=Entrada, SAI=Saída, ACE=Acerto. |
| `PRDM_DT_MOVIMENTO` | DATE | Sim | Data do movimento de estoque. |
| `PRDM_QUANTIDADE` | NUMERIC(15,4) | Sim | Quantidade movimentada (positiva para entrada, negativa para saída). |
| `PRDM_ORIGEM_NUMERO` | INTEGER | Sim | Número/ID do documento de origem do movimento. |
| `PRDM_ORIGEM_ITEM` | INTEGER | Sim | Sequência do item de origem (quando aplicável). |
| `PRDM_ORIGEM_MOVIMENTO` | VARCHAR(10) | Sim | Tipo do documento de origem: PEDIDO, COMPRA, ACERTO, CADASTRO. |
| `PRDM_DT_LANCAMENTO` | TIMESTAMP | Sim | Data/hora de lançamento do movimento. |
| `PRDM_USUARIO` | INTEGER | Sim | Identificador do usuário que lançou o movimento. |
| `PRDM_HISTORICO` | VARCHAR(100) | Sim | Histórico/descrição do movimento. |
| `PRDM_GRADE` | INTEGER | Sim | Identificador da grade do produto (quando aplicável). |
| `PRDM_CUSTO_UN` | NUMERIC(15,4) | Sim | Custo unitário do produto no momento do movimento. |
| `PRDM_CUSTO` | NUMERIC(15,4) | Sim | Custo total do movimento (CUSTO_UN × QUANTIDADE). |
| `PRDM_PESSOA` | INTEGER | Sim | FK para TB_PESSOA.PES_ID — pessoa vinculada (cliente/fornecedor). |
| `PRDM_LOCAL` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE.LOC_ID — local de estoque. |
| `PRDM_ID` | INTEGER | Não | Identificador único do movimento. |
| `PRDM_VARIACAO` | INTEGER | Sim | FK para TB_PRODUTO_VARIACAO.PRV_ID — variação do produto. |
| `PRDM_EMPRESA_ORIGEM` | INTEGER | Não | Identificador da empresa de origem (para movimentações entre empresas). |

COMMENT ON COLUMN TB_PRODUTO_MOVIMENTO.PRDM_TIPO IS 'ENT - ENTRADA NO ESTOQUE
SAI - SAIDA DO ESTOQUE
ACE - ACERTO DE ESTOQUE';
COMMENT ON COLUMN TB_PRODUTO_MOVIMENTO.PRDM_ORIGEM_NUMERO IS 'PRDM_ORIGEM_NUMERO
-----------------
NR DO PEDIDO QUE GEROU O MOVIMENTO
NR DA COMPRA QUE GEROU O MOVIMENTO
NR DO ACERTO QUE GEROU O MOVIMENTO
NR DO ID DO PRODUTO CADASTRADO';
COMMENT ON COLUMN TB_PRODUTO_MOVIMENTO.PRDM_ORIGEM_MOVIMENTO IS 'PEDIDO - Origem é um pedido
COMPRA - Origem é uma compra
ACERTO - Origem é um acerto
CADASTRO - Origem é um cadastro de produto';
COMMENT ON COLUMN TB_PRODUTO_MOVIMENTO.PRDM_QUANTIDADE IS 'Para movimentos de saída o valor é armazenado positivo. Use o tipo (PRDM_TIPO) para inferir o sinal ao calcular saldo. Para movimentos de acerto (ACE) pode representar diferença positiva ou negativa conforme configurado.';

# Tabela TB_DEVOLUCAO_ITEM

**Módulo:** Vendas / Devoluções
Itens de uma devolução de mercadoria, com produto, unidade, quantidade, valor, comissão, imposto e informações de origem (sequencial e grade).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `DEVI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `DEVI_DEVOLUCAO` | INTEGER | Não | Identificador da devolução (TB_DEVOLUCAO.DEV_ID). Parte da chave primária composta. |
| `DEVI_SEQUENCIA` | INTEGER | Não | Sequencial do item dentro da devolução. Parte da chave primária composta. |
| `DEVI_PRODUTO` | INTEGER | Sim | Identificador do produto devolvido (TB_PRODUTO.PRD_ID). |
| `DEVI_UN_VENDA` | VARCHAR(3) | Sim | Unidade de venda do produto na devolução. |
| `DEVI_VALOR_UNITARIO` | NUMERIC(15,4) | Sim | Valor unitário do produto no item da devolução. |
| `DEVI_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade devolvida do produto. |
| `DEVI_GRADE` | INTEGER | Sim | Identificador da grade do produto utilizada na devolução. |
| `DEVI_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do item (quantidade x valor unitário). |
| `DEVI_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção em listagens/processos (S/N). |
| `DEVI_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo do produto no item da devolução. |
| `DEVI_SEQUENCIAL_ORIGEM` | INTEGER | Sim | Sequencial do item no documento de origem da devolução. |
| `DEVI_COMISSAO` | NUMERIC(15,4) | Sim | Percentual/valor de comissão aplicada ao item. |
| `DEVI_VALOR_COMISSAO` | NUMERIC(15,4) | Sim | Valor de comissão calculado para o item. |
| `DEVI_VALOR_IMPOSTO` | NUMERIC(15,4) | Sim | Valor de imposto do item devolvido. |
| `DEVI_QTDE_ESTOQUE` | NUMERIC(15,6) | Sim | Quantidade em estoque do produto no momento da devolução. |
| `DEVI_FATOR_CONVERSAO` | VARCHAR(1) | Sim | Indica se há fator de conversão de unidade (S/N). |
| `DEVI_QTDE_CONVERSAO` | NUMERIC(15,4) | Sim | Quantidade convertida aplicada ao item conforme o fator de conversão. |
| `DEVI_UNITARIO_FLEX` | NUMERIC(15,4) | Sim | Valor unitário flexível utilizado na devolução. |
| `DEVI_SALDO_FLEX` | NUMERIC(15,4) | Sim | Saldo flexível do item após a devolução. |
| `DEVI_VARIACAO` | INTEGER | Sim | Identificador da variação do produto (TB_PRODUTO_VARIACAO.PRV_ID). |

COMMENT ON COLUMN TB_DEVOLUCAO_ITEM.DEVI_SEQUENCIAL_ORIGEM IS 'Armazena o sequencial do documento de origem.';
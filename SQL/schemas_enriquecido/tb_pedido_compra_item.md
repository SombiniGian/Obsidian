# Tabela TB_PEDIDO_COMPRA_ITEM

**Módulo:** Compras / Estoque
Itens do pedido de compra (TB_PEDIDO_COMPRA). Permite controlar a quantidade pedida vs recebida, valores unitários, impostos (IPI, ST), conversão de unidades, saldos de estoque e custo atual.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PDCI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PDCI_PEDIDO_COMPRA` | INTEGER | Não | FK para TB_PEDIDO_COMPRA.PDC_ID. Parte da chave primária composta. |
| `PDCI_SEQUENCIA` | INTEGER | Não | Sequencial do item no pedido. Parte da chave primária composta. |
| `PDCI_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID do produto comprado. |
| `PDCI_DESCRICAO` | VARCHAR(100) | Sim | Descrição do item (pode diferir da descrição do produto). |
| `PDCI_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade pedida. |
| `PDCI_VALOR_UNITARIO` | NUMERIC(15,10) | Sim | Valor unitário de compra (preço do item). |
| `PDCI_VALOR_PEDIDO` | NUMERIC(15,4) | Sim | Valor total do item (qtde × valor unitário − descontos). |
| `PDCI_UNIDADE` | VARCHAR(6) | Sim | Unidade de medida do item (UN, KG, CX etc.). |
| `PDCI_VALOR_UN_RECEBIDO` | NUMERIC(15,10) | Sim | Valor unitário efetivamente recebido. |
| `PDCI_VALOR_RECEBIDO` | NUMERIC(15,4) | Sim | Valor total recebido do item (qtde recebida × unitário recebido). |
| `PDCI_QTDE_RECEBIDA` | NUMERIC(15,6) | Sim | Quantidade já recebida do item. |
| `PDCI_STATUS` | VARCHAR(1) | Sim | Status do item (A = Aberto, P = Parcialmente Recebido, R = Recebido). |
| `PDCI_REFERENCIA` | VARCHAR(20) | Sim | Referência/SKU do produto no item. |
| `PDCI_QTDE_ESTOQUE` | NUMERIC(15,6) | Sim | Quantidade que movimentará no estoque. |
| `PDCI_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo do produto (N=Normal, S=Serviço, etc.). |
| `PDCI_CAIXA_MASTER` | NUMERIC(15,2) | Sim | Quantidade de caixas master (embalagem). |
| `PDCI_VALOR_IPI` | NUMERIC(15,2) | Sim | Valor de IPI do item. |
| `PDCI_VALOR_ST` | NUMERIC(15,2) | Sim | Valor de ICMS-ST do item. |
| `PDCI_FATOR_CONVERSAO` | VARCHAR(1) | Sim | Fator de conversão de unidade (M = Multiplica, D = Divide). |
| `PDCI_QTDE_CONVERSAO` | NUMERIC(15,4) | Sim | Quantidade de conversão entre unidades. |
| `PDCI_OBSERVACAO` | VARCHAR(2000) | Sim | Observações do item. |
| `PDCI_VOLUME` | INTEGER | Sim | Volume (etiqueta de expedição). |
| `PDCI_FATOR_VOLUME` | VARCHAR(1) | Sim | Fator de cálculo do volume. |
| `PDCI_VOLUME_ITEM` | INTEGER | Sim | Volume unitário do item. |
| `PDCI_PESO_LIQUIDO` | NUMERIC(15,4) | Sim | Peso líquido (kg). |
| `PDCI_PESO_BRUTO` | NUMERIC(15,4) | Sim | Peso bruto (kg). |
| `PDCI_METRAGEM` | NUMERIC(15,4) | Sim | Metragem cúbica (m³). |
| `PDCI_ULTIMO_CUSTO` | NUMERIC(15,4) | Sim | Último custo do produto antes deste pedido. |
| `PDCI_CUSTO_ATUAL` | NUMERIC(15,4) | Sim | Custo atual do produto após este pedido. |
| `PDCI_ESTOQUE` | NUMERIC(15,6) | Sim | Estoque atual do produto no momento da compra. |
| `PDCI_MINIMO` | NUMERIC(15,6) | Sim | Estoque mínimo configurado do produto. |
| `PDCI_DESCONTO` | NUMERIC(15,2) | Sim | Percentual de desconto aplicado ao item. |
| `PDCI_VARIACAO` | INTEGER | Sim | FK para TB_PRODUTO_VARIACAO.PRV_ID. |

COMMENT ON COLUMN TB_PEDIDO_COMPRA_ITEM.PDCI_PRODUTO IS 'FK para TB_PRODUTO.PRD_ID — use JOIN com TB_PRODUTO por PRD_ID para obter descrição do produto.';
COMMENT ON COLUMN TB_PEDIDO_COMPRA_ITEM.PDCI_VALOR_UNITARIO IS 'Preço de compra unitário do item.';
COMMENT ON COLUMN TB_PEDIDO_COMPRA_ITEM.PDCI_STATUS IS 'A - ABERTO
P - PARCIALMENTE RECEBIDO
R - RECEBIDO';
COMMENT ON COLUMN TB_PEDIDO_COMPRA_ITEM.PDCI_QTDE_ESTOQUE IS 'Quantidade que irá movimentar no estoque.';

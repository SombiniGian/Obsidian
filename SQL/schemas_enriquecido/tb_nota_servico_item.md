# Tabela TB_NOTA_SERVICO_ITEM

**Módulo:** Fiscal / Serviços
Itens da Nota Fiscal de Serviço, com produto ou serviço prestado, quantidades, valores, descrição e cálculo de ISS e deduções.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `NSI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `NSI_NOTA_SERVICO` | INTEGER | Não | Identificador da nota de serviço (TB_NOTA_SERVICO.NS_ID). Parte da chave primária composta. |
| `NSI_SEQUENCIA` | INTEGER | Não | Sequencial do item na nota de serviço. Parte da chave primária composta. |
| `NSI_PRODUTO` | INTEGER | Sim | Identificador do produto ou serviço (TB_PRODUTO.PRD_ID). |
| `NSI_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade do serviço ou produto. |
| `NSI_VALOR_UNITARIO` | NUMERIC(15,10) | Sim | Valor unitário do serviço ou produto. |
| `NSI_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do item. |
| `NSI_NCM` | VARCHAR(10) | Sim | Código NCM do produto, quando aplicável. |
| `NSI_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo do produto ou serviço. |
| `NSI_DESCRICAO` | VARCHAR(100) | Sim | Descrição do serviço ou produto no item. |
| `NSI_SUB_TOTAL` | NUMERIC(15,4) | Sim | Subtotal do item antes dos descontos. |
| `NSI_VALOR_DESCONTO` | NUMERIC(15,4) | Sim | Valor de desconto aplicado ao item. |
| `NSI_BC_VALOR` | NUMERIC(15,2) | Sim | Base de cálculo do ISS do item. |
| `NSI_ALIQ_ISS` | NUMERIC(15,4) | Sim | Alíquota do ISS aplicada ao item. |
| `NSI_VALOR_ISS` | NUMERIC(15,2) | Sim | Valor do ISS do item. |
| `NSI_ALIQ_DEDUCAO` | NUMERIC(15,4) | Sim | Alíquota de dedução aplicada ao item. |
| `NSI_VALOR_DEDUCAO` | NUMERIC(15,2) | Sim | Valor de dedução do item. |

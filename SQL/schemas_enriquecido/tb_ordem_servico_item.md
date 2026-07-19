# Tabela TB_ORDEM_SERVICO_ITEM

**Módulo:** Ordem de Serviço
Itens (produtos/serviços) da ordem de serviço. Contém quantidades, valores, descontos, comissões, técnicos, vendedores e dados de estoque/faturamento.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `OSI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `OSI_ORDEM_SERVICO` | INTEGER | Não | FK para TB_ORDEM_SERVICO. Parte da chave primária composta. |
| `OSI_SEQUENCIA` | INTEGER | Não | Sequência do item na OS. Parte da chave primária composta. |
| `OSI_PRODUTO` | INTEGER | Sim | FK para TB_PRODUTO. |
| `OSI_DESCRICAO` | VARCHAR(100) | Sim | Descrição do item. |
| `OSI_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade do item. |
| `OSI_UNIDADE` | VARCHAR(6) | Sim | Unidade de medida. |
| `OSI_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo (P=Produto, S=Serviço). |
| `OSI_OBSERVACAO` | BLOB SUB_TYPE TEXT | Sim | Observações em formato texto. |
| `OSI_COMISSAO_PERC` | NUMERIC(15,2) | Sim | Percentual de comissão do técnico. |
| `OSI_TECNICO` | INTEGER | Sim | FK para TB_PESSOA (técnico responsável). |
| `OSI_CALCULA_COMISSAO` | VARCHAR(1) | Sim | Calcula comissão (S/N). |
| `OSI_VENDEDOR` | INTEGER | Sim | FK para TB_PESSOA (vendedor). |
| `OSI_COMISSAO_VEND` | NUMERIC(15,2) | Sim | Percentual de comissão do vendedor. |
| `OSI_VALOR_UNITARIO` | NUMERIC(15,6) | Sim | Valor unitário. |
| `OSI_VALOR_DESCONTO` | NUMERIC(15,4) | Sim | Valor de desconto. |
| `OSI_VALOR_ACRESCIMO` | NUMERIC(15,4) | Sim | Valor de acréscimo. |
| `OSI_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do item. |
| `OSI_VALOR_SUB_TOTAL` | NUMERIC(15,4) | Sim | Subtotal do item. |
| `OSI_COMISSAO_VALOR` | NUMERIC(15,4) | Sim | Valor da comissão do técnico. |
| `OSI_COMISSAO_VALOR_VEND` | NUMERIC(15,4) | Sim | Valor da comissão do vendedor. |
| `OSI_APLICA_DESCONTO` | VARCHAR(1) | Sim | Aplica desconto (S/N). |
| `OSI_TIPO_ACRESCIMO` | VARCHAR(1) | Sim | Tipo de acréscimo (V=Valor, P=Percentual). |
| `OSI_TIPO_DESCONTO` | VARCHAR(1) | Sim | Tipo de desconto (V=Valor, P=Percentual). |
| `OSI_ACRESCIMO` | NUMERIC(15,4) | Sim | Valor/percentual de acréscimo. |
| `OSI_DESCONTO` | NUMERIC(15,4) | Sim | Valor/percentual de desconto. |
| `OSI_FATOR_CONVERSAO` | VARCHAR(1) | Sim | Fator de conversão de unidade (M=Multiplica, D=Divide). |
| `OSI_QTDE_CONVERSAO` | NUMERIC(15,4) | Sim | Quantidade de conversão. |
| `OSI_QTDE_ESTOQUE` | NUMERIC(15,6) | Sim | Quantidade em estoque no momento. |
| `OSI_PESO_BRUTO` | NUMERIC(15,3) | Sim | Peso bruto do item. |
| `OSI_PESO_LIQUIDO` | NUMERIC(15,3) | Sim | Peso líquido do item. |
| `OSI_METRAGEM` | NUMERIC(15,4) | Sim | Metragem do item. |
| `OSI_FATOR_VOLUME` | VARCHAR(1) | Sim | Fator de cálculo de volume (M=Multiplica, D=Divide). |
| `OSI_VOLUME` | INTEGER | Sim | Volume padrão da embalagem. |
| `OSI_VOLUME_ITEM` | INTEGER | Sim | Quantidade de volumes do item. |
| `OSI_STATUS_VALOR` | VARCHAR(1) | Sim | Status do valor (N=Normal, C=Cortesia, P=Preço promocional). |
| `OSI_DESC_RATEADO` | NUMERIC(15,4) | Sim | Desconto rateado do cabeçalho. |
| `OSI_ACRESC_RATEADO` | NUMERIC(15,4) | Sim | Acréscimo rateado do cabeçalho. |
| `OSI_PRODUTO_NF` | INTEGER | Sim | Produto a ser faturado. |
| `OSI_UN_NF` | VARCHAR(6) | Sim | Unidade de medida na NF. |
| `OSI_ITEM_PAI` | INTEGER | Sim | Sequência do item pai (para itens relacionados). |
| `OSI_TIPO_MARCADOR` | VARCHAR(1) | Sim | Tipo do marcador (cópia/impressão). |
| `OSI_MARCADOR_INICIAL` | VARCHAR(50) | Sim | Marcador inicial. |
| `OSI_MARCADOR_FINAL` | VARCHAR(50) | Sim | Marcador final. |
| `OSI_MARCADOR_CODIGO` | VARCHAR(50) | Sim | Código do marcador. |
| `OSI_COD_PED_COMPRA` | VARCHAR(20) | Sim | Código do pedido de compra vinculado. |
| `OSI_SEQ_PED_COMPRA` | INTEGER | Sim | Sequência no pedido de compra. |
| `OSI_VALOR_IPI` | NUMERIC(15,2) | Sim | Valor de IPI. |
| `OSI_VALOR_ST` | NUMERIC(15,2) | Sim | Valor de ICMS ST. |
| `OSI_VALOR_ICMS_DESON` | NUMERIC(15,2) | Sim | Valor de ICMS desonerado. |
| `OSI_LOCAL_ESTOQUE` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE. |
| `OSI_VALOR_CUSTO_UNITARIO` | NUMERIC(15,6) | Sim | Valor de custo unitário. |
| `OSI_ALIQ_DEDUCAO` | NUMERIC(15,4) | Sim | Alíquota de dedução. |
| `OSI_VALOR_DEDUCAO` | NUMERIC(15,2) | Sim | Valor de dedução. |

COMMENT ON COLUMN TB_ORDEM_SERVICO_ITEM.OSI_TIPO_PRODUTO IS 'P - PRODUTO
S - SERVICO';
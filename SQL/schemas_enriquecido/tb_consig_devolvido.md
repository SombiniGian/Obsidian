# Tabela TB_CONSIG_DEVOLVIDO

**Módulo:** Vendas / Consignado
Tabela de itens devolvidos de uma consignação. Registra o produto devolvido, quantidades, valores, comissão, variação e observações por item.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CNSD_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `CNSD_CONSIGNADO` | INTEGER | Não | FK para TB_CONSIGNADO. Consignação de origem. Parte da chave primária composta. |
| `CNSD_SEQUENCIA` | INTEGER | Não | Sequencial do item devolvido. Parte da chave primária composta. |
| `CNSD_DT_LANCAMENTO` | INTEGER | Sim | Data/hora de lançamento do item. |
| `CNSD_DT_EMISSAO` | DATE | Sim | Data de emissão da devolução. |
| `CNSD_PRODUTO` | INTEGER | Sim | FK para TB_PRODUTO devolvido. |
| `CNSD_UNIDADE` | VARCHAR(6) | Sim | Unidade de medida do item. |
| `CNSD_VALOR_UNITARIO` | NUMERIC(15,6) | Sim | Valor unitário do item. |
| `CNSD_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do item devolvido. |
| `CNSD_SUB_TOTAL` | NUMERIC(15,4) | Sim | Subtotal do item (sem descontos). |
| `CNSD_QTDE_ESTOQUE` | NUMERIC(15,6) | Sim | Quantidade equivalente na unidade de estoque. |
| `CNSD_FATOR_CONVERSAO` | VARCHAR(1) | Sim | Fator de conversão entre unidade do item e unidade de estoque (M/D). |
| `CNSD_QTDE_CONVERSAO` | NUMERIC(15,4) | Sim | Fator numérico de conversão. |
| `CNSD_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que registrou a devolução. |
| `CNSD_VOLUME` | INTEGER | Sim | Volume do item. |
| `CNSD_VOLUME_ITEM` | INTEGER | Sim | Sequência do item dentro do volume. |
| `CNSD_FATOR_VOLUME` | VARCHAR(1) | Sim | Fator de conversão de volume (M/D). |
| `CNSD_OBSERVACAO` | VARCHAR(2000) | Sim | Observações do item devolvido. |
| `CNSD_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo do produto (P=Produto, S=Serviço, etc.). |
| `CNSD_COMISSAO` | NUMERIC(15,2) | Sim | Percentual/valor da comissão. |
| `CNSD_VALOR_COMISSAO` | NUMERIC(15,2) | Sim | Valor da comissão calculada. |
| `CNSD_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade devolvida. |
| `CNSD_STATUS_VALOR` | VARCHAR(1) | Sim | Status do valor do item (D=Devolvido, V=Vendido, P=Parcial). |
| `CNSD_ORIGEM_CODIGO` | VARCHAR(20) | Sim | Código de origem do produto. |
| `CNSD_VARIACAO` | INTEGER | Sim | FK para TB_PRODUTO_VARIACAO. Variação do produto devolvido. |
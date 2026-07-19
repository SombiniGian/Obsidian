# Tabela TB_CONSIGNADO

**Módulo:** Vendas / Consignado
Tabela de cabeçalho de vendas consignadas. Controla remessas enviadas ao cliente para posterior fechamento com devolução/venda, registrando totais, comissões, percentuais vendidos, fechamento e integração com nota fiscal.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CNS_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `CNS_ID` | INTEGER | Não | Identificador único da consignação. Parte da chave primária composta. |
| `CNS_DT_EMISSAO` | DATE | Sim | Data de emissão da consignação. |
| `CNS_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que emitiu a consignação. |
| `CNS_CLIENTE` | INTEGER | Sim | FK para TB_PESSOA (PES_CLIENTE=S). Cliente destinatário da consignação. |
| `CNS_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro. |
| `CNS_DT_FECHAMENTO` | DATE | Sim | Data de fechamento da consignação. |
| `CNS_TABELA_PRECO` | INTEGER | Sim | FK para TB_TABELA_PRECO aplicada. |
| `CNS_STATUS` | VARCHAR(1) | Sim | Status da consignação (A=Aberta, F=Fechada, C=Cancelada). |
| `CNS_VOLUMES` | INTEGER | Sim | Quantidade de volumes enviados. |
| `CNS_QTDE_ITENS` | INTEGER | Sim | Quantidade de itens enviados. |
| `CNS_PEDIDO_VENDA` | INTEGER | Sim | FK para TB_PEDIDO_VENDA que originou a consignação. |
| `CNS_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total da consignação. |
| `CNS_VALOR_DEVOLVIDO` | NUMERIC(15,2) | Sim | Valor total devolvido. |
| `CNS_VALOR_VENDIDO` | NUMERIC(15,2) | Sim | Valor total vendido. |
| `CNS_COMISSAO_BC` | NUMERIC(15,2) | Sim | Base de cálculo da comissão. |
| `CNS_COMISSAO_ALIQ` | NUMERIC(15,2) | Sim | Alíquota da comissão. |
| `CNS_COMISSAO_TIPO` | VARCHAR(1) | Sim | Tipo de cálculo da comissão (P=Percentual, V=Valor). |
| `CNS_TIPO_TABELA_PRECO` | VARCHAR(1) | Sim | Tipo da tabela de preço (A=Acrescimo, D=Desconto). |
| `CNS_TABELA_DESC_ACRES` | NUMERIC(15,2) | Sim | Percentual/valor de desconto ou acréscimo aplicado. |
| `CNS_PRECO_VENDA_CUSTO` | VARCHAR(1) | Sim | Indica se o preço usado é de venda ou custo (V/C). |
| `CNS_COMISSAO_DESC` | NUMERIC(15,2) | Sim | Desconto aplicado na comissão. |
| `CNS_COMISSAO_VALOR` | NUMERIC(15,2) | Sim | Valor da comissão calculada. |
| `CNS_PAGAMENTO` | INTEGER | Sim | FK para TB_PAGAMENTO. Forma de pagamento do fechamento. |
| `CNS_VALOR_FEC` | NUMERIC(15,2) | Sim | Valor total no fechamento da consignação. |
| `CNS_DEVOLVIDO_FEC` | NUMERIC(15,2) | Sim | Valor devolvido no fechamento. |
| `CNS_PERC_VENDIDO` | NUMERIC(15,2) | Sim | Percentual vendido sobre o total. |
| `CNS_PERC_VEND_FEC` | NUMERIC(15,2) | Sim | Percentual vendido registrado no fechamento. |
| `CNS_DIAS` | INTEGER | Sim | Prazo (em dias) previsto para fechamento da consignação. |
| `CNS_DT_PREVISTA` | DATE | Sim | Data prevista para devolução/fechamento. |
| `CNS_LUCRO_LIQUIDO` | NUMERIC(15,2) | Sim | Lucro líquido apurado no fechamento. |
| `CNS_VENDEDOR` | INTEGER | Sim | FK para TB_PESSOA (PES_VENDEDOR=S). Vendedor responsável. |
| `CNS_NOTA_FISCAL` | INTEGER | Sim | FK para TB_NOTA_FISCAL emitida no fechamento. |
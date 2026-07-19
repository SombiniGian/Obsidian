# Tabela TB_PEDIDO_VENDA_ITEM

**Módulo:** Vendas
Itens do pedido de venda: produtos, quantidades, preços unitários, descontos, acréscimos, fretes, comissão, impostos, controle de estoque, preparo e vínculo com a tabela de preço.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PEVI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PEVI_PEDIDO_VENDA` | INTEGER | Não | Identificador do pedido de venda (TB_PEDIDO_VENDA.PEV_ID). Parte da chave primária composta. |
| `PEVI_SEQUENCIA` | INTEGER | Não | Sequencial do item dentro do pedido. Parte da chave primária composta. |
| `PEVI_PRODUTO` | INTEGER | Sim | Identificador do produto (TB_PRODUTO.PRD_ID). |
| `PEVI_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade vendida do item. |
| `PEVI_UN_VENDA` | VARCHAR(6) | Sim | Unidade de venda (UN, PCT, KG, LT etc.). |
| `PEVI_VALOR_UNITARIO` | NUMERIC(15,6) | Sim | Valor unitário de venda do item. |
| `PEVI_VALOR_DESCONTO` | NUMERIC(15,4) | Sim | Valor de desconto aplicado ao item (em moeda). |
| `PEVI_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total do item (quantidade × unitário − descontos + acréscimos). |
| `PEVI_VALOR_ACRESCIMO` | NUMERIC(15,4) | Sim | Valor de acréscimo aplicado ao item (em moeda). |
| `PEVI_VALOR_FRETE` | NUMERIC(15,4) | Sim | Valor de frete rateado para o item. |
| `PEVI_QTDE_ESTOQUE` | NUMERIC(15,6) | Sim | Quantidade baixada do estoque neste item. |
| `PEVI_GRADE` | INTEGER | Sim | Identificador da grade (variação) do produto. |
| `PEVI_SUB_TOTAL` | NUMERIC(15,4) | Sim | Subtotal do item antes de descontos e acréscimos (quantidade × unitário). |
| `PEVI_VALOR_COMISSAO` | NUMERIC(15,4) | Sim | Valor de comissão calculado para o item. |
| `PEVI_DESCRICAO` | VARCHAR(100) | Sim | Descrição do produto no item (denormalizada). |
| `PEVI_DESCONTO` | NUMERIC(15,4) | Sim | Porcentagem de desconto aplicada ao item. |
| `PEVI_ACRESCIMO` | NUMERIC(15,4) | Sim | Porcentagem de acréscimo aplicada ao item. |
| `PEVI_COMISSAO` | NUMERIC(15,2) | Sim | Porcentagem de comissão do item. |
| `PEVI_FRETE` | NUMERIC(15,2) | Sim | Porcentagem de frete aplicada ao item. |
| `PEVI_FATOR_CONVERSAO` | VARCHAR(1) | Sim | Fator de conversão entre unidade de compra e venda. |
| `PEVI_QTDE_CONVERSAO` | NUMERIC(15,4) | Sim | Quantidade convertida entre unidades. |
| `PEVI_TIPO_PRODUTO` | VARCHAR(1) | Sim | Tipo do produto (N=Normal, V=Veículo, S=Serviço, G=Grade, U=Uso Consumo, M=Materia Prima, E=Embalagem, R=Produto em Processo, B=Balanca, P=Produto Acabado). |
| `PEVI_QUANTIDADE_NF` | NUMERIC | Sim | Quantidade do item após faturamento (NF). |
| `PEVI_VALOR_UNITARIO_NF` | NUMERIC(15,6) | Sim | Valor unitário do item na NF. |
| `PEVI_VALOR_TOTAL_NF` | NUMERIC(15,4) | Sim | Valor total do item na NF. |
| `PEVI_IMPOSTOS_NF` | NUMERIC(15,4) | Sim | Valor de impostos destacado na NF para o item. |
| `PEVI_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção do item (auxílio em processos de importação para NF). |
| `PEVI_DESC_RATEADO` | NUMERIC(15,4) | Sim | Desconto rateado da capa do pedido para o item. |
| `PEVI_ACRESC_RATEADO` | NUMERIC(15,4) | Sim | Acréscimo rateado da capa do pedido para o item. |
| `PEVI_TIPO_DESCONTO` | VARCHAR(1) | Sim | Tipo do desconto aplicado (V = Valor, P = Percentual). |
| `PEVI_TIPO_ACRESCIMO` | VARCHAR(1) | Sim | Tipo do acréscimo aplicado (V = Valor, P = Percentual). |
| `PEVI_METRAGEM` | NUMERIC(15,4) | Sim | Metragem cúbica do item. |
| `PEVI_PESO_BRUTO` | NUMERIC(15,3) | Sim | Peso bruto do item. |
| `PEVI_PESO_LIQUIDO` | NUMERIC(15,3) | Sim | Peso líquido do item. |
| `PEVI_TABELA_PRECO` | INTEGER | Sim | Identificador da tabela de preço aplicada ao item. |
| `PEVI_TIPO_TABELA_PRECO` | VARCHAR(1) | Sim | Tipo de operação da tabela de preço: D = Desconto, A = Acréscimo. |
| `PEVI_TABELA_PRECO_DESC_ACRE` | NUMERIC(15,2) | Sim | Percentual de desconto/acréscimo da tabela de preço aplicada. |
| `PEVI_QUANTIDADE_ENTREGUE` | NUMERIC(15,6) | Sim | Quantidade efetivamente entregue do item. |
| `PEVI_APLICA_DESCONTO` | VARCHAR(1) | Sim | Indica se o item permite desconto (S/N). |
| `PEVI_OBSERVACAO` | VARCHAR(2000) | Sim | Observações do item. |
| `PEVI_DESP_ACESSORIA` | DECIMAL(15,4) | Sim | Despesa acessória da capa rateada para o item, sem somar no valor do item. |
| `PEVI_UNITARIO_FLEX` | NUMERIC(15,4) | Sim | Valor unitário que o produto deveria ser vendido considerando descontos/acréscimos de forma de pagamento e tabela de preço (usado para calcular Saldo Flex). |
| `PEVI_TOTAL_FLEX` | NUMERIC(15,4) | Sim | Valor total que o produto deveria ser vendido considerando descontos/acréscimos (usado para calcular Saldo Flex). |
| `PEVI_SALDO_FLEX` | NUMERIC(15,4) | Sim | Saldo Flex — diferença entre o valor que deveria ter sido vendido e o que realmente foi vendido. |
| `PEVI_STATUS_VALOR` | VARCHAR(1) | Sim | Origem do valor aplicado: N = Valor Normal, T = Tabela Preço, Q = Promoção por Qtde, D = Promoção por Data, C = Custo. |
| `PEVI_COD_DIGITADO` | VARCHAR(20) | Sim | Código digitado para localizar o produto. |
| `PEVI_ORIGEM_CODIGO` | VARCHAR(20) | Sim | Origem do código digitado (balança, manual, importado). |
| `PEVI_VOLUME_ITEM` | INTEGER | Sim | Quantidade de volumes do item. |
| `PEVI_VOLUME` | INTEGER | Sim | Volume (número) do item na expedição. |
| `PEVI_FATOR_VOLUME` | VARCHAR(1) | Sim | Fator de multiplicação de volume. |
| `PEVI_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do item. |
| `PEVI_INFORMAR_TOTAL` | VARCHAR(1) | Sim | Indica se o usuário informa o valor total (venda por total) (S/N). |
| `PEVI_COMISSAO_SUPERVISOR` | NUMERIC(15,2) | Sim | Percentual de comissão do supervisor sobre o item. |
| `PEVI_VALOR_COMISSAO_SUPERVISOR` | NUMERIC(15,4) | Sim | Valor calculado da comissão do supervisor. |
| `PEVI_PEDIDO_CLIENTE` | VARCHAR(20) | Sim | Número do pedido do cliente (referência externa). |
| `PEVI_PEDIDO_VENDEDOR` | VARCHAR(20) | Sim | Número do pedido interno do vendedor. |
| `PEVI_PEDIDO_ORIGEM` | INTEGER | Sim | Identificador do pedido de origem (quando o item foi copiado/remessado). |
| `PEVI_VALOR_DESCARTE` | NUMERIC(15,4) | Sim | Valor de descarte do item (perda). |
| `PEVI_VENDEDOR` | INTEGER | Sim | Identificador do vendedor do item (TB_PESSOA.PES_ID). |
| `PEVI_STATUS_PREPARO` | VARCHAR(1) | Sim | Status de preparo do item: N = Não Controla, A = Aguardando, P = Pronto, E = Entregue. |
| `PEVI_IMPRESSO` | VARCHAR(1) | Sim | Indica se o item já foi impresso em cozinha/produção (S/N). |
| `PEVI_MODO_PREPARO` | INTEGER | Sim | Identificador do modo de preparo do item. |
| `PEVI_VALOR_COMPL_ADD` | NUMERIC(15,4) | Sim | Valor de complementos a adicionar no item. |
| `PEVI_VALOR_COMPL_RET` | NUMERIC(15,4) | Sim | Valor de complementos a retirar no item. |
| `PEVI_KIT` | INTEGER | Sim | Identificador do kit associado (TB_PEDIDO_VENDA_ITEM_KIT). |
| `PEVI_RECENTE` | VARCHAR(1) | Sim | Indica se o item foi adicionado recentemente (S = Sim, N = Não). |
| `PEVI_VALOR_TX_SERVICO` | NUMERIC(15,4) | Sim | Valor da taxa de serviço aplicada ao item. |
| `PEVI_PRODUTO_NF` | INTEGER | Sim | Produto utilizado para emissão na NF (caso seja diferente do produto original). |
| `PEVI_UN_NF` | VARCHAR(6) | Sim | Unidade de venda utilizada na NF. |
| `PEVI_SEQ_PED_COMPRA` | INTEGER | Sim | Sequencial do pedido de compra que originou o item. |
| `PEVI_COD_PED_COMPRA` | VARCHAR(20) | Sim | Código do pedido de compra de origem. |
| `PEVI_DESC_PED_COMPRA` | VARCHAR(100) | Sim | Descrição do item no pedido de compra de origem. |
| `PEVI_QTDE_PED_COMPRA` | NUMERIC(15,6) | Sim | Quantidade do item no pedido de compra de origem. |
| `PEVI_UN_PED_COMPRA` | VARCHAR(6) | Sim | Unidade do item no pedido de compra de origem. |
| `PEVI_ENTREGUE` | VARCHAR(1) | Sim | Indica se o item foi entregue (S/N). |
| `PEVI_TURNO` | INTEGER | Sim | Identificador do turno de produção/expedição. |
| `PEVI_PEDIDO_CLIENTE_ITEM` | INTEGER | Sim | Sequencial do item no pedido do cliente. |
| `PEVI_SISTEMA` | VARCHAR(1) | Sim | Indica se o item é de uso do sistema (S/N). |
| `PEVI_STATUS_FLEX` | VARCHAR(1) | Sim | Status do cálculo Flex do item. |
| `PEVI_VALOR_IPI` | NUMERIC(15,2) | Sim | Valor de IPI do item. |
| `PEVI_VALOR_ST` | NUMERIC(15,2) | Sim | Valor de substituição tributária do item. |
| `PEVI_VALOR_VOLUME` | NUMERIC(15,6) | Sim | Valor unitário do volume. |
| `PEVI_VOLUME_MANUAL` | VARCHAR(1) | Sim | Volume informado manualmente (S/N). |
| `PEVI_VALOR_COVER` | NUMERIC(15,2) | Sim | Valor de cover por pessoa no item. |
| `PEVI_VALOR_ICMS_DESON` | NUMERIC(15,2) | Sim | Valor de ICMS desonerado do item. |
| `PEVI_FOTO_CLIENTE` | INTEGER | Sim | Identificador da foto do cliente associada ao item. |
| `PEVI_ALTURA` | NUMERIC(15,6) | Sim | Altura do item (dimensões). |
| `PEVI_COMPRIMENTO` | NUMERIC(15,6) | Sim | Comprimento do item (dimensões). |
| `PEVI_LARGURA` | NUMERIC(15,6) | Sim | Largura do item (dimensões). |
| `PEVI_IMPRESSO_STONE` | VARCHAR(1) | Sim | Indica se o item foi impresso na impressora Stone (S/N). |
| `PEVI_VALOR_CUSTO_UNITARIO` | NUMERIC(15,6) | Sim | Valor de custo unitário do item no momento da venda. |
| `PEVI_DESCRICAO_SABORES` | VARCHAR(100) | Sim | Descrição dos sabores escolhidos (pizza etc.). |
| `PEVI_COD_SABORES` | VARCHAR(100) | Sim | Códigos dos sabores escolhidos. |
| `PEVI_TIPO_CASHBACK` | VARCHAR(1) | Sim | Tipo do cashback aplicado ao item. |
| `PEVI_VALOR_CASHBACK` | NUMERIC(15,2) | Sim | Valor unitário de cashback do item. |
| `PEVI_TOTAL_CASHBACK` | NUMERIC(15,2) | Sim | Valor total de cashback do item. |
| `PEVI_MENSAGEM_BLOQUEIO` | BLOB SUB_TYPE TEXT | Sim | Mensagem de bloqueio do item em formato texto. NUNCA selecione em queries SELECT. |
| `PEVI_DEVOLUCAO_VASILHAME` | INTEGER | Sim | Identificador do vasilhame devolvido para este item. |
| `PEVI_SEQ_DESMEMBRADO` | INTEGER | Sim | Sequencial do item quando o pedido foi desmembrado. |
| `PEVI_AREA_CAIXA` | NUMERIC(15,6) | Sim | Área da caixa do item (logística). |
| `PEVI_QTDE_CAIXA` | NUMERIC(15,6) | Sim | Quantidade de caixas do item. |
| `PEVI_VALOR_DESC_PROMO` | NUMERIC(15,2) | Sim | Valor de desconto de promoção aplicado ao item. |
| `PEVI_VENDA_PROMOCAO` | INTEGER | Sim | Identificador da venda em promoção. |
| `PEVI_PROMOCAO` | INTEGER | Sim | Identificador da promoção aplicada. |
| `PEVI_QTDE_PROMOCAO` | NUMERIC(15,6) | Sim | Quantidade exigida pela promoção. |
| `PEVI_PROMOCAO_BENEF` | INTEGER | Sim | Identificador do benefício da promoção. |
| `PEVI_PROMOCAO_COND` | INTEGER | Sim | Identificador da condição da promoção. |
| `PEVI_APLICAR_TX_SERVICO` | VARCHAR(1) | Sim | Indica se aplica taxa de serviço ao item (S/N). |
| `PEVI_VEIC_TIPO_OPER` | VARCHAR(1) | Sim | Tipo de operação do veículo (quando o item é veículo). |
| `PEVI_VARIACAO` | INTEGER | Sim | Identificador da variação do produto (atributos/cor/tamanho). |
| `PEVI_LOCAL_ESTOQUE` | INTEGER | Sim | Identificador do local de estoque onde o item foi baixado. |

COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_DESCONTO IS 'PORCENTAGEM DE DESCONTO';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_ACRESCIMO IS 'PORCENTAM DE ACRESCIMO';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_COMISSAO IS 'PORCENTAGEM DE COMISSÃO';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_FRETE IS 'PORCENTAGEM DE FRETE';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_SELECIONADO IS 'Campo para auxiliar na seleção de itens a serem importados para NF';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_TIPO_TABELA_PRECO IS 'D - DESCONTO
A - ACRESCIMO';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_DESP_ACESSORIA IS 'Despesa acessória da capa rateada sem somar no valor do item.';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_UNITARIO_FLEX IS 'Valor unitario que produto deveria ser vendido considerando
Descontos/Acrescimos de forma de pagamento e tabela de preço.
(Campo utilizado para calcular Saldo Flex = Diferença de preço imposta pelo vendedor)';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_TOTAL_FLEX IS 'Valor Total que produto deveria ser vendido considerando
Descontos/Acrescimos de forma de pagamento e tabela de preço.
(Campo utilizado para calcular Saldo Flex = Diferença de preço imposta pelo vendedor)';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_SALDO_FLEX IS 'Saldo Flex (Valor de Diferença que valor deveria ter sido vendido e que realmente foi vendido)';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_STATUS_VALOR IS 'N - VALOR NORMAL
T - TABELA PREÇO
Q - PROMOCAO POR QTDE
D - PROMOCAO POR DATA
C - CUSTO';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_STATUS_PREPARO IS 'N - NÃO CONTROLA
    A - AGUARDANDO
    P - PRONTO
    E - ENTREGUE';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_RECENTE IS 'Controlar se foi adicionado recentemente
   S - SIM
   N - Não';
COMMENT ON COLUMN TB_PEDIDO_VENDA_ITEM.PEVI_MENSAGEM_BLOQUEIO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
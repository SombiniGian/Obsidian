# Tabela TB_PROD_SUB_GRUPO

**Módulo:** Estoque / Cadastros
Cadastro de subgrupos de produtos, hierarquicamente abaixo de TB_PROD_GRUPO. Permite aplicar promoções por período/quantidade e controlar exibição no touch do PDV.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PSGR_EMPRESA` | INTEGER | Não | Identificador da empresa. |
| `PSGR_ID` | INTEGER | Não | Identificador único do subgrupo. |
| `PSGR_DESCRICAO` | VARCHAR(100) | Sim | Descrição do subgrupo (ex.: Pizzas Doces, Refrigerantes Lata). |
| `PSGR_GRUPO` | INTEGER | Sim | FK para TB_PROD_GRUPO.PGRU_ID — grupo ao qual o subgrupo pertence. |
| `PSGR_PRECO_VENDA` | NUMERIC(15,4) | Sim | Preço de venda padrão dos produtos do subgrupo. |
| `PSGR_DT_INI_PROM` | DATE | Sim | Data de início da promoção do subgrupo. |
| `PSGR_DT_FIM_PROM` | DATE | Sim | Data de fim da promoção do subgrupo. |
| `PSGR_VALOR_PROM` | NUMERIC(15,4) | Sim | Valor promocional aplicado aos produtos do subgrupo no período informado. |
| `PSGR_USAR_LIGACAO` | VARCHAR(1) | Sim | Indica se produtos do subgrupo devem usar ligação de preço (S/N). |
| `PSGR_IMAGEM` | BLOB SUB_TYPE BINARY | Sim | Imagem do subgrupo em formato binário. NUNCA selecione em queries SELECT. |
| `PSGR_ORDEM_TOUCH` | VARCHAR(1) | Sim | Ordem de exibição do subgrupo no touch. |
| `PSGR_EXIBIR_TOUCH` | VARCHAR(1) | Sim | Indica se o subgrupo é exibido no touch do PDV (S/N). |
| `PSGR_TIPO_VALOR_PROM` | VARCHAR(1) | Sim | Tipo do valor promocional (V = Valor, P = Percentual). |
| `PSGR_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. |
| `PSGR_ULTIMO_ENVIO_ECOMMERCE` | TIMESTAMP | Sim | Timestamp do último envio do subgrupo para o e-commerce. |

COMMENT ON COLUMN TB_PROD_SUB_GRUPO.PSGR_IMAGEM IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

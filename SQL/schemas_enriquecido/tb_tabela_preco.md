# Tabela TB_TABELA_PRECO

**Módulo:** Comercial / Vendas
Cadastro das tabelas de preço utilizadas para definição de preços diferenciados por cliente, tipo de venda, formulário de pedido ou canal (NFC-e, balcão, etc.). Permite configurar se é de desconto ou acréscimo, percentual/valor e regras de promoções.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TBP_ID` | INTEGER | Não | Identificador único da tabela de preço. |
| `TBP_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `TBP_STATUS` | VARCHAR(1) | Sim | Status da tabela de preço (A = Ativo, I = Inativo). |
| `TBP_DESCRICAO` | VARCHAR(100) | Sim | Descrição da tabela de preço (ex.: Atacado, Varejo, Balcão). |
| `TBP_TIPO` | VARCHAR(1) | Sim | Tipo da tabela: D = Desconto, A = Acréscimo. |
| `TBP_DESCONTO_ACRESCIMO` | NUMERIC(15,2) | Sim | Percentual/valor padrão de desconto ou acréscimo aplicado pela tabela. |
| `TBP_EXCLUSIVIDADE` | VARCHAR(1) | Sim | Indica se a tabela é exclusiva (não acumula com outras promoções) (S/N). |
| `TBP_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. Default: current_timestamp. |
| `TBP_NAO_APLICAR_PROMOCAO` | VARCHAR(1) | Sim | Indica se as promoções automáticas não devem ser aplicadas quando esta tabela estiver em uso (S/N). |
| `TBP_ULTIMO_ENVIO_ECOMMERCE` | TIMESTAMP | Sim | Timestamp do último envio da tabela para o e-commerce. |
| `TBP_ECOMMERCE` | VARCHAR(1) | Sim | Indica se a tabela de preço é exportada para o e-commerce (S/N). |

COMMENT ON COLUMN TB_TABELA_PRECO.TBP_TIPO IS 'D - DESCONTO
A - ACRESCIMO';

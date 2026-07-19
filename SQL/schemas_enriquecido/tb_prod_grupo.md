# Tabela TB_PROD_GRUPO

**Módulo:** Estoque / Cadastros
Cadastro de grupos de produtos. Os grupos organizam o cardápio/catálogo e são utilizados em touch (PDV de restaurante), iFood, Tray e e-commerce. Cada grupo pode ter uma imagem, ordem de exibição e IDs de integrações externas.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PGRU_EMPRESA` | INTEGER | Não | Identificador da empresa. |
| `PGRU_ID` | INTEGER | Não | Identificador único do grupo. |
| `PGRU_DESCRICAO` | VARCHAR(100) | Sim | Descrição do grupo (ex.: Pizzas Salgadas, Bebidas, Sobremesas). |
| `PGRU_EXIBIR_TOUCH` | VARCHAR(1) | Sim | Indica se o grupo deve ser exibido no touch do PDV de restaurante (S/N). |
| `PGRU_ORDEM_TOUCH` | INTEGER | Sim | Ordem de exibição do grupo no touch. |
| `PGRU_IMAGEM` | BLOB SUB_TYPE BINARY | Sim | Imagem do grupo em formato binário. NUNCA selecione em queries SELECT. |
| `PGRU_IFOOD` | VARCHAR(1) | Sim | Indica se o grupo é exportado para o iFood (S/N). |
| `PGRU_ID_IFOOD` | VARCHAR(100) | Sim | ID do grupo na integração com iFood. |
| `PGRU_TRAY` | BIGINT | Sim | ID do grupo na integração com Tray. |
| `PGRU_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. |
| `PGRU_ID_MELI` | VARCHAR(50) | Sim | ID do grupo na integração com Mercado Livre. |
| `PGRU_ECOMMERCE` | VARCHAR(1) | Sim | Indica se o grupo é exportado para o e-commerce (S/N). |
| `PGRU_ULTIMO_ENVIO_ECOMMERCE` | TIMESTAMP | Sim | Timestamp do último envio do grupo para o e-commerce. |

COMMENT ON COLUMN TB_PROD_GRUPO.PGRU_IMAGEM IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

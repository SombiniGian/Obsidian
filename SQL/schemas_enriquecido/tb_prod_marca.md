# Tabela TB_PROD_MARCA

**Módulo:** Estoque / Cadastros
Cadastro de marcas associadas aos produtos. Permite filtrar produtos por marca em consultas, relatórios e integrações com e-commerce.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PMAR_EMPRESA` | INTEGER | Não | Identificador da empresa. |
| `PMAR_ID` | INTEGER | Não | Identificador único da marca. |
| `PMAR_DESCRICAO` | VARCHAR(100) | Sim | Descrição da marca (ex.: Coca-Cola, Nike, Nestlé). |
| `PMAR_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. |
| `PMAR_IMAGEM` | BLOB SUB_TYPE BINARY | Sim | Imagem/logo da marca em formato binário. NUNCA selecione em queries SELECT. |
| `PMAR_ULTIMO_ENVIO_ECOMMERCE` | TIMESTAMP | Sim | Timestamp do último envio da marca para o e-commerce. |

COMMENT ON COLUMN TB_PROD_MARCA.PMAR_IMAGEM IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

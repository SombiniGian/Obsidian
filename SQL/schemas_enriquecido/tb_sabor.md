# Tabela TB_SABOR

**Módulo:** Restaurante / PDV
Cadastro de sabores (pizzas, sorvetes, açaí, etc.) utilizados em produtos que permitem escolha de sabor pelo cliente. Cada sabor pode ter uma imagem e ID de integração com plataformas de delivery (iFood). Os insumos do sabor (composição) ficam em TB_SABOR_INSUMO.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `SAB_ID` | INTEGER | Não | Identificador único do sabor. |
| `SAB_STATUS` | VARCHAR(1) | Sim | Status do sabor (A=Ativo, I=Inativo). |
| `SAB_ID_IFOOD` | VARCHAR(100) | Sim | ID do sabor na integração com iFood. |
| `SAB_DESCRICAO` | VARCHAR(100) | Sim | Descrição do sabor (ex.: Calabresa, Margherita). |
| `SAB_IMAGEM` | BLOB SUB_TYPE BINARY | Sim | Imagem do sabor em formato binário. NUNCA selecione em queries SELECT. |
| `SAB_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. |
| `SAB_OBSERVACAO` | VARCHAR(500) | Sim | Observações do sabor. |

COMMENT ON COLUMN TB_SABOR.SAB_IMAGEM IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

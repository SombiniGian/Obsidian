# Tabela TB_COMPLEMENTO

**Módulo:** Restaurante / PDV
Cadastro de adicionais/retiradas para produtos do tipo pizza ou itens personalizáveis no módulo de restaurante. Cada complemento pode ter acréscimo ou redução de valor e opcionalmente estar vinculado a um insumo (matéria-prima) para controle de estoque.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `COM_ID` | INTEGER | Não | Identificador único do complemento. |
| `COM_EMPRESA` | INTEGER | Não | Identificador da empresa. |
| `COM_DESCRICAO` | VARCHAR(100) | Sim | Descrição do complemento (ex.: Borda recheada, Sem cebola). |
| `COM_STATUS` | VARCHAR(1) | Sim | Status do complemento (A = Ativo, I = Inativo). |
| `COM_VALOR` | NUMERIC(15,4) | Sim | Valor adicional cobrado quando o complemento for selecionado. |
| `COM_TIPO` | VARCHAR(1) | Sim | Tipo do complemento (A = Adicionar, R = Retirar). |
| `COM_IMAGEM` | BLOB SUB_TYPE BINARY | Sim | Imagem ilustrativa do complemento em formato binário. NUNCA selecione em queries SELECT. |
| `COM_ID_IFOOD` | VARCHAR(100) | Sim | ID do complemento na integração com iFood. |
| `COM_INSUMO` | INTEGER | Sim | FK para TB_PRODUTO.PRD_ID — insumo/matéria-prima consumido quando o complemento é selecionado. |
| `COM_QTDE_INSUMO` | NUMERIC(15,6) | Sim | Quantidade do insumo consumida por unidade vendida do complemento. |
| `COM_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração do registro. |

COMMENT ON COLUMN TB_COMPLEMENTO.COM_STATUS IS 'A - ATIVO
I - INATIVO';
COMMENT ON COLUMN TB_COMPLEMENTO.COM_TIPO IS 'A - ADICIONAR
R - RETIRAR';
COMMENT ON COLUMN TB_COMPLEMENTO.COM_IMAGEM IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

# Tabela TB_REGIAO

**Módulo:** Cadastros
Regiões de entrega/venda com regras de tipo de frete e valor de frete associado. Define automatizações para o cálculo de frete por bairro.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `REG_ID` | INTEGER | Não | Identificador único da região. |
| `REG_DESCRICAO` | VARCHAR(100) | Não | Descrição/nome da região. |
| `REG_TIPO_FRETE` | VARCHAR(1) | Sim | Tipo de frete aplicado (CIF/FOB/Terceiros/Sem). |
| `REG_VALOR_FRETE` | NUMERIC(15,2) | Sim | Valor do frete da região. |
| `REG_BAIRROS` | BLOB SUB_TYPE TEXT | Sim | Lista de bairros pertencentes à região (texto longo). NUNCA selecione em queries SELECT. |
| `REG_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. |

COMMENT ON COLUMN TB_REGIAO.REG_BAIRROS IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização';

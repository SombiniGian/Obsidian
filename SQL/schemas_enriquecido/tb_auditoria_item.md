# Tabela TB_AUDITORIA_ITEM

**Módulo:** Auditoria
Detalhe (campo a campo) das alterações registradas em um lançamento de auditoria, armazenando o campo alterado e seus valores antigo e novo.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `AUDI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `AUDI_TABELA` | VARCHAR(50) | Não | Nome da tabela auditada. Parte da chave primária composta. |
| `AUDI_ID_REGISTRO` | VARCHAR(20) | Não | Identificador do registro que foi auditado. Parte da chave primária composta. |
| `AUDI_AUDITORIA` | INTEGER | Não | Sequencial do lançamento de auditoria (TB_AUDITORIA.AUD_SEQUENCIA). Parte da chave primária composta. |
| `AUDI_CAMPO` | VARCHAR(50) | Não | Nome do campo alterado na tabela auditada. Parte da chave primária composta. |
| `AUDI_CAMPO_DESC` | VARCHAR(80) | Sim | Descrição do campo para exibição ao usuário. |
| `AUDI_VALOR_ANTIGO` | VARCHAR(200) | Sim | Valor anterior do campo antes da alteração. |
| `AUDI_VALOR_NOVO` | VARCHAR(200) | Sim | Novo valor do campo após a alteração. |

COMMENT ON COLUMN TB_AUDITORIA_ITEM.AUDI_ID_REGISTRO IS 'ID do Registro que foi Auditado';
COMMENT ON COLUMN TB_AUDITORIA_ITEM.AUDI_AUDITORIA IS 'Chave do campo AUD_SEQUENCIA tabela TB_AUDITORIA';
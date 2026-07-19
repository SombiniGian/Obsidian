# Tabela TB_AUDITORIA

**Módulo:** Auditoria
Cabeçalho da auditoria de registros do sistema, registrando tabela, identificação do registro, ação executada (inclusão/alteração/exclusão/cancelamento), data, usuário e versão.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `AUD_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `AUD_TABELA` | VARCHAR(50) | Não | Nome da tabela auditada (nome no banco de dados). Parte da chave primária composta. |
| `AUD_ID_REGISTRO` | VARCHAR(20) | Não | Identificador do registro que foi auditado. Parte da chave primária composta. |
| `AUD_SEQUENCIA` | INTEGER | Não | Sequencial do lançamento de auditoria. Parte da chave primária composta. |
| `AUD_TABELA_DESC` | VARCHAR(50) | Sim | Nome da tabela como aparece para o usuário. |
| `AUD_ACAO` | VARCHAR(1) | Sim | Ação executada sobre o registro (I=Inclusão, A=Alteração, E=Exclusão, C=Cancelamento). |
| `AUD_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora do lançamento da auditoria. |
| `AUD_DT_ACAO` | DATE | Sim | Data em que a ação foi executada sobre o registro. |
| `AUD_USUARIO` | INTEGER | Sim | Identificador do usuário que executou a ação (TB_USUARIO.USU_ID). |
| `AUD_DESC_REGISTRO` | VARCHAR(200) | Sim | Descrição do registro auditado para identificação no log. |
| `AUD_VENDEDOR` | INTEGER | Sim | Identificador do vendedor relacionado ao registro auditado (TB_PESSOA.PES_ID). |
| `AUD_VERSAO` | VARCHAR(10) | Sim | Versão do sistema/aplicação no momento da auditoria. |
| `AUD_VERSAO_SERVIDOR` | VARCHAR(10) | Sim | Versão do servidor no momento da auditoria. |

COMMENT ON COLUMN TB_AUDITORIA.AUD_TABELA IS 'Nome da Tabela Auditada (Nome no BD)';
COMMENT ON COLUMN TB_AUDITORIA.AUD_ID_REGISTRO IS 'ID do Registro que foi Auditado';
COMMENT ON COLUMN TB_AUDITORIA.AUD_TABELA_DESC IS 'Nome da Tabela (Como vai aparecer pro Usuário)';
COMMENT ON COLUMN TB_AUDITORIA.AUD_ACAO IS 'ACAO
I - INCLUSÃO
A - ALTERAÇÃO
E - EXCLUSÃO
C - CANCELAMENTO';
# Tabela TB_ORDEM_SERVICO_FOTOS

**Módulo:** Ordem de Serviço
Tabela de fotos anexadas às ordens de serviço. Armazena imagens relacionadas ao atendimento técnico (antes/depois, evidências, etc.) em formato binário.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `OSF_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `OSF_ORDEM_SERVICO` | INTEGER | Não | FK para TB_ORDEM_SERVICO. Identificador da OS. Parte da chave primária composta. |
| `OSF_SEQUENCIA` | INTEGER | Não | Sequencial da foto dentro da OS. Parte da chave primária composta. |
| `OSF_DESCRICAO` | VARCHAR(100) | Sim | Descrição/legenda da foto. |
| `OSF_FOTO` | BLOB SUB_TYPE BINARY | Sim | Conteúdo binário da imagem. |

COMMENT ON COLUMN TB_ORDEM_SERVICO_FOTOS.OSF_FOTO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização';

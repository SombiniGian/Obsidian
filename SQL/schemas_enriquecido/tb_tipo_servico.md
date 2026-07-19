# Tabela TB_TIPO_SERVICO

**Módulo:** Ordens de Serviço
Cadastro de tipos de serviço utilizados em ordens de serviço. Cada tipo representa uma categoria de serviço que pode ser associada à OS para classificação, filtros e relatórios.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TPS_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `TPS_ID` | INTEGER | Não | Identificador único do tipo de serviço. Parte da chave primária composta. |
| `TPS_DESCRICAO` | VARCHAR(100) | Sim | Descrição do tipo de serviço. |

# Tabela TB_CLASSIFICACAO

**Módulo:** Cadastros
Cadastro genérico de classificações utilizado em diversos módulos (pedido de venda, ordem de produção, ordem de serviço etc.).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CLA_ID` | INTEGER | Não | Identificador único da classificação. |
| `CLA_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `CLA_DESCRICAO` | VARCHAR(100) | Sim | Descrição da classificação. |
| `CAMPO_24` | VARCHAR(100) | Sim | Campo auxiliar/legado. |

# Tabela TB_SETOR

**Módulo:** Cadastros
Cadastro de setores utilizados para classificação/organização dentro da empresa (ex.: produção, vendas, administrativo). Setores podem ser referenciados por outros cadastros e movimentações para fins de rateio, controle e relatórios.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `SET_ID` | INTEGER | Não | Identificador único do setor. |
| `SET_EMPRESA` | INTEGER | Não | Identificador da empresa à qual o setor pertence. |
| `SET_DESCRICAO` | VARCHAR(100) | Sim | Descrição do setor. |

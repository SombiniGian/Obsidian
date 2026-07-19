# Tabela TB_CLIENTE_GRUPO

**Módulo:** Cadastros / Cliente
Grupos de clientes utilizados para classificação, regras de preço, comissionamento e relatórios. Permite agrupar clientes com características em comum.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CLIG_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `CLIG_ID` | INTEGER | Não | Identificador único do grupo de cliente. Parte da chave primária composta. |
| `CLIG_DESCRICAO` | VARCHAR(100) | Sim | Descrição do grupo (ex.: Atacado, Varejo, VIP). |
# Tabela TB_GRUPO_COMPLEMENTO

**Módulo:** Cardápio / Complementos
Cadastro de grupos de complementos (ex.: "Bordas", "Sabores", "Adicionais"). Define quantidade mínima e máxima permitida, ordem de exibição, tipo de seleção e integração com iFood.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `GRC_ID` | INTEGER | Não | Identificador único do grupo de complemento. |
| `GRC_DESCRICAO` | VARCHAR(100) | Sim | Descrição do grupo de complemento. |
| `GRC_MIN` | INTEGER | Sim | Quantidade mínima de itens que o cliente deve selecionar (Default 0). |
| `GRC_MAX` | INTEGER | Sim | Quantidade máxima de itens permitidos na seleção. |
| `GRC_ORDEM` | INTEGER | Sim | Ordem de exibição do grupo no cardápio. |
| `GRC_TIPO` | VARCHAR(1) | Sim | Tipo de seleção (O=Obrigatório, F=Facultativo). |
| `GRC_ID_IFOOD` | VARCHAR(100) | Sim | ID do grupo na integração com iFood. |
| `GRC_TIPO_PIZZA_IFOOD` | VARCHAR(1) | Sim | Indica se o grupo é específico de pizzas no iFood (S/N). |
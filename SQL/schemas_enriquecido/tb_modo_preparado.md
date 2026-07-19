# Tabela TB_MODO_PREPARADO

**Módulo:** Cardápio / Produção
Cadastro de modos de preparo de produtos (ex.: Bem passado, Ao ponto, Mal passado). Permite integração com iFood, atribuindo um ID externo.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `MDP_ID` | INTEGER | Não | Identificador único do modo de preparado. |
| `MDP_EMPRESA` | INTEGER | Não | Identificador da empresa à qual o modo de preparo pertence. |
| `MDP_DESCRICAO` | VARCHAR(100) | Sim | Descrição do modo de preparo. |
| `MDP_STATUS` | VARCHAR(1) | Sim | Status do modo de preparo (A=Ativo, I=Inativo). |
| `MDP_ID_IFOOD` | VARCHAR(100) | Sim | ID do modo de preparo na integração com iFood. |
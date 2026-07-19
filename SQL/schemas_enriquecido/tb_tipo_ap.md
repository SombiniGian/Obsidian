# Tabela TB_TIPO_AP

**Módulo:** Hotelaria
Cadastro de tipos de apartamento utilizados para classificar acomodações no módulo de hospedagem.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TAP_ID` | INTEGER | Não | Identificador único do tipo de apartamento. |
| `TAP_EMPRESA` | INTEGER | Não | Identificador da empresa. |
| `TAP_DESCRICAO` | VARCHAR(100) | Sim | Descrição do tipo de apartamento (ex.: Standard, Luxo, Suíte). |
| `TAP_ABREV` | VARCHAR(20) | Sim | Abreviação exibida em listagens. |

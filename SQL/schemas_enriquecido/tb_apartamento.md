# Tabela TB_APARTAMENTO

**Módulo:** Hospedagem
Cadastro de apartamentos/unidades de hospedagem (hotel, pousada, flat). Define capacidade, tipo, valores, regras de multa e status.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `AP_ID` | INTEGER | Não | Identificador único do apartamento. |
| `AP_EMPRESA` | INTEGER | Não | Identificador da empresa. |
| `AP_NUMERO` | VARCHAR(10) | Sim | Número do apartamento. |
| `AP_DESCRICAO` | VARCHAR(100) | Sim | Descrição do apartamento. |
| `AP_TIPO_AP` | INTEGER | Sim | FK para TB_TIPO_AP (tipo de apartamento). |
| `AP_RAMAL` | VARCHAR(10) | Sim | Ramal telefônico do apartamento. |
| `AP_DETALHES` | BLOB SUB_TYPE BINARY | Sim | Detalhes adicionais em formato binário. NUNCA selecione em queries SELECT. |
| `AP_STATUS` | VARCHAR(1) | Sim | Status do apartamento (L=Livre, O=Ocupado, M=Manutenção, R=Reservado). |
| `AP_HOSPEDAGEM_TIPO` | INTEGER | Sim | FK para TB_HOSPEDAGEM_TIPO (tipo de hospedagem aceita). |
| `AP_VALOR` | NUMERIC(15,2) | Sim | Valor da diária do apartamento. |
| `AP_TIPO_MULTA` | VARCHAR(1) | Sim | Tipo de multa por atraso (V=Valor, P=Percentual). |
| `AP_VALOR_MULTA` | NUMERIC(15,2) | Sim | Valor da multa por atraso. |
| `AP_PERIODO_MULTA` | INTEGER | Sim | Período (em horas) tolerado antes de aplicar a multa. |

COMMENT ON COLUMN TB_APARTAMENTO.AP_STATUS IS 'L - LIVRE
O - OCUPADO
M - MANUTENCAO
R - RESERVADO';
COMMENT ON COLUMN TB_APARTAMENTO.AP_DETALHES IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
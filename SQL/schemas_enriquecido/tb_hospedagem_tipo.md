# Tabela TB_HOSPEDAGEM_TIPO

**Módulo:** Hotelaria
Cadastro dos tipos de hospedagem (diária, mensal, pacote etc.) com seus horários, periodicidade e regras.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `HTIP_ID` | INTEGER | Não | Identificador único do tipo de hospedagem. |
| `HTIP_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `HTIP_STATUS` | VARCHAR(1) | Sim | Status do tipo (A=Ativo, I=Inativo). |
| `HTIP_DESCRICAO` | VARCHAR(50) | Sim | Descrição do tipo de hospedagem. |
| `HTIP_TIPO_PERIODO` | VARCHAR(1) | Sim | Tipo do período (D=Diária, H=Hora, M=Mensal etc.). |
| `HTIP_HR_INICIO` | TIME | Sim | Hora inicial padrão da hospedagem. |
| `HTIP_HR_FINAL` | TIME | Sim | Hora final padrão da hospedagem. |
| `HTIP_DETALHES` | BLOB SUB_TYPE BINARY | Sim | Detalhes adicionais em binário. NUNCA selecione em queries SELECT. |
| `HTIP_PERIODO` | INTEGER | Sim | Duração padrão do período. |

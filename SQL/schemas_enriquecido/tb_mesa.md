# Tabela TB_MESA

**Módulo:** Restaurante / PDV
Cadastro de mesas utilizadas em comandas e pedidos de venda no módulo de restaurante. Permite controlar número de pessoas e status da mesa.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `MSA_ID` | INTEGER | Não | Identificador único da mesa. |
| `MSA_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `MSA_CODIGO` | VARCHAR(10) | Sim | Código da mesa (ex.: 01, 02, A1). |
| `MSA_DESCRICAO` | VARCHAR(100) | Sim | Descrição da mesa (ex.: Mesa 01 - Salão). |
| `MSA_NR_PESSOAS` | INTEGER | Sim | Capacidade de pessoas da mesa. |
| `MSA_STATUS` | VARCHAR(1) | Sim | Status da mesa (L=Livre, O=Ocupada, R=Reservada). |

COMMENT ON COLUMN TB_MESA.MSA_STATUS IS 'L - Livre
O - Ocupada
R - Reservada';

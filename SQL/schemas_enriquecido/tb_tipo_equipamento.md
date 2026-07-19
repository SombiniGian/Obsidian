# Tabela TB_TIPO_EQUIPAMENTO

**Módulo:** Ordem de Serviço / Cadastros
Cadastro de tipos de equipamentos (ex.: Ar-condicionado, Refrigerador, Máquina de lavar). Permite configurar 20 campos genéricos para características específicas do tipo e flags de associação a cliente/marca.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TEQ_ID` | INTEGER | Não | Identificador único do tipo de equipamento. |
| `TEQ_EMPRESA` | INTEGER | Sim | Identificador da empresa à qual o tipo pertence. |
| `TEQ_DESCRICAO` | VARCHAR(50) | Sim | Descrição do tipo de equipamento. |
| `TEQ_STATUS` | VARCHAR(1) | Sim | Status do tipo de equipamento (A=Ativo, I=Inativo). |
| `TEQ_CAMPO_1` | VARCHAR(50) | Sim | Campo genérico 1 (uso conforme customização do cliente). |
| `TEQ_CAMPO_2` | VARCHAR(50) | Sim | Campo genérico 2 (uso conforme customização do cliente). |
| `TEQ_CAMPO_3` | VARCHAR(50) | Sim | Campo genérico 3 (uso conforme customização do cliente). |
| `TEQ_CAMPO_4` | VARCHAR(50) | Sim | Campo genérico 4 (uso conforme customização do cliente). |
| `TEQ_CAMPO_5` | VARCHAR(50) | Sim | Campo genérico 5 (uso conforme customização do cliente). |
| `TEQ_CLIENTE` | VARCHAR(1) | Sim | Indica se equipamentos deste tipo são vinculados a cliente (S/N). |
| `TEQ_MARCA` | VARCHAR(1) | Sim | Indica se equipamentos deste tipo são vinculados a marca (S/N). |
| `TEQ_PRINCIPAL` | VARCHAR(1) | Sim | Indica se é o tipo principal (S/N). |
| `TEQ_CAMPO_6` | VARCHAR(50) | Sim | Campo genérico 6 (uso conforme customização do cliente). |
| `TEQ_CAMPO_7` | VARCHAR(50) | Sim | Campo genérico 7 (uso conforme customização do cliente). |
| `TEQ_CAMPO_8` | VARCHAR(50) | Sim | Campo genérico 8 (uso conforme customização do cliente). |
| `TEQ_CAMPO_9` | VARCHAR(50) | Sim | Campo genérico 9 (uso conforme customização do cliente). |
| `TEQ_CAMPO_10` | VARCHAR(50) | Sim | Campo genérico 10 (uso conforme customização do cliente). |
| `TEQ_CAMPO_11` | VARCHAR(50) | Sim | Campo genérico 11 (uso conforme customização do cliente). |
| `TEQ_CAMPO_12` | VARCHAR(50) | Sim | Campo genérico 12 (uso conforme customização do cliente). |
| `TEQ_CAMPO_13` | VARCHAR(50) | Sim | Campo genérico 13 (uso conforme customização do cliente). |
| `TEQ_CAMPO_14` | VARCHAR(50) | Sim | Campo genérico 14 (uso conforme customização do cliente). |
| `TEQ_CAMPO_15` | VARCHAR(50) | Sim | Campo genérico 15 (uso conforme customização do cliente). |
| `TEQ_CAMPO_16` | VARCHAR(50) | Sim | Campo genérico 16 (uso conforme customização do cliente). |
| `TEQ_CAMPO_17` | VARCHAR(50) | Sim | Campo genérico 17 (uso conforme customização do cliente). |
| `TEQ_CAMPO_18` | VARCHAR(50) | Sim | Campo genérico 18 (uso conforme customização do cliente). |
| `TEQ_CAMPO_19` | VARCHAR(50) | Sim | Campo genérico 19 (uso conforme customização do cliente). |
| `TEQ_CAMPO_20` | VARCHAR(50) | Sim | Campo genérico 20 (uso conforme customização do cliente). |

COMMENT ON COLUMN TB_TIPO_EQUIPAMENTO.TEQ_CLIENTE IS 'Associar equipamento a cliente';
COMMENT ON COLUMN TB_TIPO_EQUIPAMENTO.TEQ_MARCA IS 'Associar Equipamento a marca';
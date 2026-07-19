# Tabela TB_CFOP

**Módulo:** Fiscal
Tabela de CFOP (Código Fiscal de Operações e Prestações) utilizada na emissão de NF-e/NFC-e, definindo o tipo de operação (entrada/saída), grupo, descrição e regras de ICMS (código de crédito e zerar base).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CFOP_CODIGO` | VARCHAR(4) | Não | Código CFOP de 4 dígitos (chave primária). Ex.: 5101, 6101, 1101, 5403. |
| `CFOP_DESCRICAO` | VARCHAR(500) | Sim | Descrição do CFOP. |
| `CFOP_ENTRADA_SAIDA` | VARCHAR(1) | Sim | Indica se o CFOP é de Entrada (E) ou Saída (S). |
| `CFOP_GRUPO` | INTEGER | Sim | Identificador do grupo de CFOP. |
| `CFOP_COD_CREDITO` | VARCHAR(2) | Sim | Código de crédito de ICMS associado ao CFOP. |
| `CFOP_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. Default: current_timestamp. |
| `CFOP_ZERAR_ICMS` | VARCHAR(1) | Sim | Indica se o CFOP zera o valor de ICMS (S/N). |

COMMENT ON COLUMN TB_CFOP.CFOP_CODIGO IS 'Chave primária. Use SEMPRE JOIN por CFOP_CODIGO. O primeiro dígito indica a operação (1/2=Entrada, 5/6=Saída, 3/7=Prestação).';
COMMENT ON COLUMN TB_CFOP.CFOP_ENTRADA_SAIDA IS 'E - ENTRADA
S - SAIDA';
COMMENT ON COLUMN TB_CFOP.CFOP_ZERAR_ICMS IS 'S - SIM
N - NAO';

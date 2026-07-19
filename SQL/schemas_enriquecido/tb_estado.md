# Tabela TB_ESTADO

**Módulo:** Cadastros
Cadastro de unidades federativas (estados/UF) utilizado em endereços, NF-e e regras tributárias interestaduais (ICMS, FCP, ICMS DIFAL, IBS).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `EST_ID` | INTEGER | Não | Identificador único do estado. |
| `EST_NOME` | VARCHAR(50) | Sim | Nome do estado. |
| `EST_PAIS` | INTEGER | Sim | FK para TB_PAIS (país do estado). |
| `EST_SIGLA` | VARCHAR(2) | Sim | Sigla/UF (ex.: MG, SP, RJ). |
| `EST_REGIAO` | VARCHAR(20) | Sim | Região geográfica (Sudeste, Nordeste, etc.). |
| `EST_ICMS_ALIQ` | NUMERIC(15,2) | Sim | Alíquota interestadual de ICMS. |
| `EST_ICMS_ALIQ_CONS_FINAL` | NUMERIC(15,2) | Sim | Alíquota de ICMS para consumidor final. |
| `EST_FCP_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do Fundo de Combate à Pobreza (FCP). |
| `EST_IMP_ALIQ` | NUMERIC(15,2) | Sim | Alíquota do IMP (Imposto sobre Movimentação de Produtos). |
| `EST_TIPO_DIFAL` | VARCHAR(1) | Sim | Tipo de cálculo do DIFAL. |
| `EST_COD_OR_ST` | VARCHAR(3) | Sim | Código de operação/receita ST. |
| `EST_COD_RECEITA_ST` | VARCHAR(10) | Sim | Código da receita ST. |
| `EST_DIA_VENCTO_ST` | INTEGER | Sim | Dia de vencimento do recolhimento de ST. |
| `EST_COD_OR_DIFAL` | VARCHAR(3) | Sim | Código de operação/receita DIFAL. |
| `EST_COD_RECEITA_DIFAL` | VARCHAR(10) | Sim | Código da receita DIFAL. |
| `EST_DIA_VENCTO_DIFAL` | INTEGER | Sim | Dia de vencimento do recolhimento DIFAL. |
| `EST_IBS` | NUMERIC(15,2) | Sim | Alíquota de IBS do estado (reforma tributária). |
| `EST_GOV_REDUTOR` | NUMERIC(15,2) | Sim | Redutor governamental aplicado ao IBS estadual. |

COMMENT ON COLUMN TB_ESTADO.EST_ICMS_ALIQ IS 'Alíquota de ICMS INTERESTADUAL';
COMMENT ON COLUMN TB_ESTADO.EST_SIGLA IS 'Use SEMPRE a sigla (EST_SIGLA) ao referenciar UF em queries — é o padrão ISO de 2 letras';

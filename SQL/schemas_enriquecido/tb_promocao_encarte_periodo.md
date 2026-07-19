# Tabela TB_PROMOCAO_ENCARTE_PERIODO

**Módulo:** Comercial / Vendas
Períodos (dia da semana e horário) em que uma promoção de encarte é válida. Cada registro associa uma promoção a um encarte e a uma janela de tempo (hora inicial, hora final e dia da semana) em que os preços promocionais se aplicam.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PREP_PROMOCAO` | INTEGER | Não | FK para a promoção (TB_PRODUTO_PROMOCAO) à qual o período pertence. Parte da chave primária composta. |
| `PREP_PROMOCAO_ENCARTE` | INTEGER | Não | FK para TB_PROMOCAO_ENCARTE — encarte da promoção. Parte da chave primária composta. |
| `PREP_SEQUENCIA` | SMALLINT | Não | Sequencial do período dentro do encarte. Parte da chave primária composta. |
| `PREP_ID` | SMALLINT | Não | Identificador único do período. Parte da chave primária composta. |
| `PREP_HR_INICIAL` | TIME | Sim | Horário inicial de aplicação da promoção. |
| `PREP_HR_FINAL` | TIME | Sim | Horário final de aplicação da promoção. |
| `PREP_DIA_SEMANA` | INTEGER | Sim | Dia da semana em que a promoção é válida (0=Domingo, 1=Segunda, ..., 6=Sábado). |

COMMENT ON COLUMN TB_PROMOCAO_ENCARTE_PERIODO.PREP_DIA_SEMANA IS '0 - DOMINGO
1 - SEGUNDA
2 - TERCA
3 - QUARTA
4 - QUINTA
5 - SEXTA
6 - SABADO';

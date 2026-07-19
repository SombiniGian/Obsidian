# Tabela TB_BOLETO_REMESSA

**Módulo:** Financeiro / Cobrança
Remessas de boletos enviadas ao banco, registrando data de emissão/lançamento, usuário responsável, status, arquivo gerado e número da remessa. Permite ainda vincular boletos de confirmação.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `BLTR_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `BLTR_ID` | INTEGER | Não | Identificador único da remessa de boletos. Parte da chave primária composta. |
| `BLTR_DT_EMISSAO` | DATE | Sim | Data de emissão da remessa. |
| `BLTR_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento da remessa no sistema. |
| `BLTR_USUARIO` | INTEGER | Sim | Identificador do usuário que gerou a remessa (TB_USUARIO.USU_ID). |
| `BLTR_STATUS` | VARCHAR(1) | Sim | Status da remessa de boletos. |
| `BLTR_ARQUIVO` | VARCHAR(200) | Sim | Caminho/nome do arquivo de remessa gerado. |
| `BLTR_BOLETO_CONF` | INTEGER | Sim | Identificador do boleto de confirmação/recorrência vinculado (TB_BOLETO.BOL_ID). |
| `BLTR_NR_REMESSA` | INTEGER | Sim | Número sequencial da remessa. |
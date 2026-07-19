# Tabela TB_AJUSTE_FISCAL

**Módulo:** Fiscal
Cadastro de ajustes fiscais utilizados na apuração (SPED Fiscal), permitindo informar código do ajuste, descrição complementar, observação, código OR e código de apuração.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `AJF_ID` | INTEGER | Não | Identificador único do ajuste fiscal. |
| `AJF_COD_AJUSTE` | VARCHAR(20) | Sim | Código do ajuste fiscal conforme tabela do SPED. |
| `AJF_DESC_COMPL_AJ` | VARCHAR(200) | Sim | Descrição complementar do ajuste. |
| `AJF_OBSERVACAO` | VARCHAR(1000) | Sim | Observações adicionais. |
| `AJF_COD_OR` | VARCHAR(3) | Sim | Código OR (origem) do ajuste. |
| `AJF_COD_AJ_APUR` | VARCHAR(10) | Sim | Código de ajuste da apuração. |
| `AJF_TIPO` | VARCHAR(4) | Sim | Tipo do ajuste (débitos/créditos/outros). |
| `AJF_SOMAR_REG` | VARCHAR(4) | Sim | Indica em qual registro deve somar. |
| `AJF_SOMAR_CAMPO` | INTEGER | Sim | Número do campo a ser somado no registro. |
| `AJF_STATUS` | VARCHAR(1) | Sim | Status do ajuste (A=Ativo, I=Inativo). |

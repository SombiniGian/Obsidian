# Tabela TB_CEST

**Módulo:** Fiscal
Tabela de domínio do CEST (Código Especificador da Substituição Tributária). Vincula NCM ao CEST e sua descrição conforme tabela oficial do CONFAZ.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CEST_CODIGO` | VARCHAR(7) | Não | Código CEST (7 dígitos). Parte da chave primária composta. |
| `CEST_NCM` | VARCHAR(8) | Não | NCM (8 dígitos) vinculado ao CEST. Parte da chave primária composta. |
| `CEST_DESCRICAO` | VARCHAR(512) | Sim | Descrição do CEST conforme tabela oficial. |

COMMENT ON COLUMN TB_CEST.CEST_CODIGO IS 'Código CEST oficial publicado pelo CONFAZ. Use sempre JOIN por CEST_CODIGO + CEST_NCM.';
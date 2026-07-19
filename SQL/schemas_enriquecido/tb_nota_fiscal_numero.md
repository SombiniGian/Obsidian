# Tabela TB_NOTA_FISCAL_NUMERO

**Módulo:** Fiscal
Controle da numeração de documentos fiscais por empresa, modelo e série, com vínculo opcional à nota fiscal emitida.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `NFN_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave de controle. |
| `NFN_NOTA_FISCAL` | INTEGER | Sim | Identificador da nota fiscal relacionada (TB_NOTA_FISCAL.NF_ID). |
| `NFN_MODELO` | VARCHAR(2) | Não | Modelo do documento fiscal. |
| `NFN_SERIE` | INTEGER | Não | Série do documento fiscal. |
| `NFN_NUMERO` | INTEGER | Não | Número do documento fiscal. |
| `NFN_AMBIENTE` | INTEGER | Sim | Ambiente fiscal utilizado na emissão, como homologação ou produção. |

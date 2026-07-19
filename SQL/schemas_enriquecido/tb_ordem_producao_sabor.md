# Tabela TB_ORDEM_PRODUCAO_SABOR

**Módulo:** Produção
Tabela de sabores vinculados a uma ordem de produção. Permite registrar a quantidade em unidade de produção e em unidade do sabor.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `OPS_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `OPS_ORDEM_PRODUCAO` | INTEGER | Não | FK para TB_ORDEM_PRODUCAO. Identificador da ordem. Parte da chave primária composta. |
| `OPS_SABOR` | INTEGER | Não | FK para TB_SABOR. Sabor vinculado à ordem. Parte da chave primária composta. |
| `OPS_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade do sabor na unidade de produção. |
| `OPS_QTDE_UN` | NUMERIC(15,6) | Sim | Quantidade do sabor convertida em unidade de venda. |
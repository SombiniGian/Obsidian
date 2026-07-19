# Tabela TB_PROD_SUB_GRUPO_PROMOCAO

**Módulo:** Estoque / Promoções
Faixas promocionais por quantidade aplicadas a um subgrupo de produtos (vinculado a TB_PROD_SUB_GRUPO). Permite definir preço promocional dentro de uma faixa de quantidade (QTDE_INI a QTDE_FIM) e o tipo de valor (valor fixo ou percentual).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PSGC_SUB_GRUPO` | INTEGER | Não | FK para TB_PROD_SUB_GRUPO.PSGR_ID — subgrupo ao qual a promoção se aplica. Parte da chave primária composta. |
| `PSGC_SEQUENCIA` | INTEGER | Não | Sequencial da faixa promocional dentro do subgrupo. Parte da chave primária composta. |
| `PSGC_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `PSGC_QTDE_INI` | NUMERIC(15,4) | Sim | Quantidade inicial da faixa (inclusiva) em que a promoção é válida. |
| `PSGC_QTDE_FIM` | NUMERIC(15,4) | Sim | Quantidade final da faixa (inclusiva) em que a promoção é válida. |
| `PSGC_VALOR_PROM` | NUMERIC(15,4) | Sim | Valor promocional aplicado dentro da faixa (valor ou percentual conforme PSGC_TIPO_VALOR). |
| `PSGC_TIPO_VALOR` | VARCHAR(1) | Sim | Tipo do valor promocional: V = Valor, P = Percentual. |

# Tabela TB_HOSP_PRODUTO

**Módulo:** Hospedagem
Tabela de produtos consumidos/adicionados durante uma hospedagem (frigobar, restaurante, lavanderia, etc.). Registra quantidade, valores, unidade, data/hora do consumo e observações.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `HPRD_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `HPRD_HOSPEDAGEM` | INTEGER | Não | FK para TB_HOSPEDAGEM. Identificador da hospedagem. Parte da chave primária composta. |
| `HPRD_SEQUENCIA` | INTEGER | Não | Sequencial do produto dentro da hospedagem. Parte da chave primária composta. |
| `HPRD_PRODUTO` | INTEGER | Sim | FK para TB_PRODUTO. Produto consumido/lançado. |
| `HPRD_QUANTIDADE` | NUMERIC(15,6) | Sim | Quantidade consumida. |
| `HPRD_VALOR_UNITARIO` | NUMERIC(15,4) | Sim | Valor unitário do produto. |
| `HPRD_SUB_TOTAL` | NUMERIC(15,4) | Sim | Subtotal (quantidade x valor unitário). |
| `HPRD_VALOR_TOTAL` | NUMERIC(15,4) | Sim | Valor total aplicado ao produto (com descontos/acréscimos). |
| `HPRD_UNIDADE` | VARCHAR(3) | Sim | Unidade de medida do produto. |
| `HPRD_DATA` | DATE | Sim | Data em que o consumo foi lançado. |
| `HPRD_HORA` | TIME | Sim | Hora em que o consumo foi lançado. |
| `HPRD_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de gravação do registro. |
| `HPRD_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que lançou o produto. |
| `HPRD_OBSERVACAO` | VARCHAR(1000) | Sim | Observações sobre o consumo. |
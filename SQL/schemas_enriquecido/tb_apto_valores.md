# Tabela TB_APTO_VALORES

**Módulo:** Hotelaria
Tabela de valores por tipo de hospedagem para cada apartamento. Define o preço cobrado e as regras de multa de cada combinação apartamento/tipo de hospedagem.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `APV_APARTAMENTO` | INTEGER | Não | FK para TB_APARTAMENTO.AP_ID. Parte da chave primária composta. |
| `APV_SEQUENCIA` | INTEGER | Não | Sequencial do registro. Parte da chave primária composta. |
| `APV_HOSPEDAGEM_TIPO` | INTEGER | Sim | FK para TB_HOSPEDAGEM_TIPO.HTIP_ID. |
| `APV_VALOR` | NUMERIC(15,2) | Sim | Valor da diária/período. |
| `APV_VALOR_MULTA` | NUMERIC(15,2) | Sim | Valor da multa em caso de descumprimento. |
| `APV_TIPO_MULTA` | VARCHAR(1) | Sim | Tipo da multa (V=Valor, P=Percentual). |
| `APV_PERIODO_MULTA` | INTEGER | Sim | Periodicidade da multa (em horas/períodos). |

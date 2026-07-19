# Tabela TB_CARGA_COLETA

**Módulo:** Logística / Coleta
Cadastro de cargas de coleta (coleta de mercadorias junto a fornecedores) com controle de quilometragem, valores previstos/gastos e status.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CARC_EMPRESA` | INTEGER | Não | Identificador da empresa. |
| `CARC_ID` | INTEGER | Não | Identificador único da carga de coleta. |
| `CARC_DT_EMISSAO` | DATE | Sim | Data de emissão da carga de coleta. |
| `CARC_DT_FATURAMENTO` | TIMESTAMP | Sim | Data e hora do faturamento. |
| `CARC_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro. |
| `CARC_DT_SAIDA` | DATE | Sim | Data de saída da carga. |
| `CARC_HORA_SAIDA` | TIME | Sim | Hora de saída. |
| `CARC_QTDE_PEDIDOS` | INTEGER | Sim | Quantidade de pedidos de coleta. |
| `CARC_USUARIO` | INTEGER | Sim | Usuário que lançou a carga. |
| `CARC_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total da carga. |
| `CARC_VOLUMES` | INTEGER | Sim | Quantidade de volumes. |
| `CARC_TRANSPORTADOR` | INTEGER | Sim | FK para TB_TRANSPORTADOR. |
| `CARC_METRAGEM` | NUMERIC(15,2) | Sim | Metragem cúbica total. |
| `CARC_PESO_BRUTO` | NUMERIC(15,2) | Sim | Peso bruto total. |
| `CARC_PESO_LIQUIDO` | NUMERIC(15,2) | Sim | Peso líquido total. |
| `CARC_PLACA` | VARCHAR(8) | Sim | Placa do veículo. |
| `CARC_UF` | VARCHAR(2) | Sim | UF da placa. |
| `CARC_STATUS` | VARCHAR(1) | Sim | Status da carga (A=Aberto, F=Faturado, C=Cancelado). |
| `CARC_OBSERVACAO` | VARCHAR(2000) | Sim | Observações gerais. |
| `CARC_VEICULO` | INTEGER | Sim | FK para TB_VEICULO. |
| `CARC_KM_SAIDA` | NUMERIC(15,2) | Sim | Quilometragem na saída. |
| `CARC_KM_CHEGADA` | NUMERIC(15,2) | Sim | Quilometragem na chegada. |
| `CARC_DT_CHEGADA` | DATE | Sim | Data de chegada. |
| `CARC_VALOR_PREV` | NUMERIC(15,2) | Sim | Valor previsto para a coleta. |
| `CARC_VALOR_GASTO` | NUMERIC(15,2) | Sim | Valor efetivamente gasto. |
| `CARC_LITROS_GASTO` | NUMERIC(15,2) | Sim | Litros de combustível gastos. |
| `CARC_KM_LITRO` | NUMERIC(15,2) | Sim | Consumo (km/litro). |
| `CARC_OBS_CHEGADA` | VARCHAR(2000) | Sim | Observações da chegada. |
| `CARC_KM_GASTO` | NUMERIC(15,2) | Sim | Quilometragem rodada. |
| `CARC_DESCRICAO` | VARCHAR(100) | Sim | Descrição da carga. |
| `CARC_TIPO` | VARCHAR(10) | Sim | Tipo da carga. |
| `CARC_VALOR_RECEBIDO` | NUMERIC(15,2) | Sim | Valor recebido no acerto. |

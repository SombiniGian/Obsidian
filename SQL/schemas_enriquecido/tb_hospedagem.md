# Tabela TB_HOSPEDAGEM

**Módulo:** Hotelaria
Tabela de hospedagem (reservas e estadias) de hóspedes em apartamentos. Armazena dados de check-in/check-out, cliente, apartamento, tipo de hospedagem, períodos, diárias, descontos/acréscimos, multa, taxas e valores totais. É a principal fonte de dados para relatórios de ocupação, faturamento de diárias e fechamentos de hospedagem.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `HOS_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `HOS_ID` | INTEGER | Não | Identificador único da hospedagem. Parte da chave primária composta. |
| `HOS_STATUS` | VARCHAR(1) | Sim | Status da hospedagem (A=Andamento, F=Finalizada, C=Cancelada). |
| `HOS_DT_INICIO` | DATE | Sim | Data de início da hospedagem (check-in). |
| `HOS_HR_INICIO` | TIME | Sim | Hora de início da hospedagem (check-in). |
| `HOS_DT_TERMINO` | DATE | Sim | Data de término previsto/realizado da hospedagem. |
| `HOS_HR_TERMINO` | TIME | Sim | Hora de término da hospedagem (check-out). |
| `HOS_DT_CHEGADA` | DATE | Sim | Data prevista de chegada. |
| `HOS_HR_CHEGADA` | TIME | Sim | Hora prevista de chegada. |
| `HOS_DT_SAIDA` | DATE | Sim | Data prevista de saída. |
| `HOS_HR_SAIDA` | TIME | Sim | Hora prevista de saída. |
| `HOS_CLIENTE` | INTEGER | Sim | FK para TB_PESSOA.PES_ID do cliente/hóspede. Use JOIN por PES_ID. |
| `HOS_APARTAMENTO` | INTEGER | Sim | FK para TB_APARTAMENTO.AP_ID ocupado. |
| `HOS_TIPO_APARTAMENTO` | INTEGER | Sim | FK para TB_TIPO_AP.TAP_ID. |
| `HOS_TIPO_HOSPEDAGEM` | INTEGER | Sim | FK para TB_HOSPEDAGEM_TIPO.HTIP_ID. |
| `HOS_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento da hospedagem no sistema. |
| `HOS_USUARIO` | INTEGER | Sim | Identificador do usuário que lançou a hospedagem. |
| `HOS_PESSOA_RESERVOU` | VARCHAR(100) | Sim | Nome da pessoa que fez a reserva. |
| `HOS_TELEFONE_RESERVOU` | VARCHAR(20) | Sim | Telefone da pessoa que fez a reserva. |
| `HOS_VALOR_PERIODO` | NUMERIC(15,2) | Sim | Valor do período (diária/período). |
| `HOS_TIPO_PERIODO` | VARCHAR(1) | Sim | Tipo de período (D=Diária, H=Hora, P=Pernoite). |
| `HOS_INTERVALO` | INTEGER | Sim | Intervalo entre períodos em minutos/horas. |
| `HOS_PERIODO` | NUMERIC(15,2) | Sim | Duração de cada período. |
| `HOS_QTDE_PERIODOS` | INTEGER | Sim | Quantidade de períodos consumidos. |
| `HOS_DESCONTO` | NUMERIC(15,2) | Sim | Valor de desconto aplicado. |
| `HOS_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações da hospedagem. NUNCA selecione em queries SELECT. |
| `HOS_QTDE_HOSPEDE` | INTEGER | Sim | Quantidade de hóspedes na hospedagem. |
| `HOS_CASAL` | VARCHAR(1) | Sim | Indica se é hospedagem casal (S/N). |
| `HOS_TOTAL_HOSPEDAGEM` | NUMERIC(15,2) | Sim | Valor total das diárias. |
| `HOS_TOTAL_PRODUTOS` | NUMERIC(15,2) | Sim | Valor total de produtos consumidos. |
| `HOS_SUB_TOTAL` | NUMERIC(15,2) | Sim | Subtotal (diárias + produtos). |
| `HOS_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total final da hospedagem. |
| `HOS_VALOR_RECEBER` | NUMERIC(15,2) | Sim | Valor a receber. |
| `HOS_VALOR_RECEBIDO` | NUMERIC(15,2) | Sim | Valor já recebido. |
| `HOS_VALOR_DINHEIRO` | NUMERIC(15,2) | Sim | Valor recebido em dinheiro. |
| `HOS_VALOR_ACRESCIMO` | NUMERIC(15,2) | Sim | Valor de acréscimo aplicado. |
| `HOS_VALOR_DESCONTO` | NUMERIC(15,2) | Sim | Valor de desconto aplicado. |
| `HOS_TIPO_ACRESCIMO` | VARCHAR(1) | Sim | Tipo do acréscimo (P=Percentual, V=Valor). |
| `HOS_TIPO_DESCONTO` | VARCHAR(1) | Sim | Tipo do desconto (P=Percentual, V=Valor). |
| `HOS_ACRESCIMO` | NUMERIC(15,2) | Sim | Percentual/valor de acréscimo. |
| `HOS_VALOR_DIFERENCA` | NUMERIC(15,2) | Sim | Valor de diferença (troco). |
| `HOS_CAIXA` | INTEGER | Sim | FK para TB_FECHAMENTO_CAIXA. |
| `HOS_DIAS` | INTEGER | Sim | Quantidade de dias da hospedagem. |
| `HOS_VALOR_LIGACAO` | NUMERIC(15,2) | Sim | Valor de ligações telefônicas consumidas. |
| `HOS_PLACA` | VARCHAR(10) | Sim | Placa do veículo do hóspede (estacionamento). |
| `HOS_PLANO_CONTAS` | INTEGER | Sim | FK para TB_PLANO_CONTA. |
| `HOS_FECHAMENTO` | INTEGER | Sim | Identificador do fechamento (caixa/financeiro). |
| `HOS_TIPO_TROCO` | VARCHAR(1) | Sim | Tipo de troco (D=Devolver, C=Creditar). |
| `HOS_DESCRICAO_FECHAMENTO` | VARCHAR(2000) | Sim | Descrição detalhada do fechamento. |
| `HOS_TIPO_MULTA` | VARCHAR(1) | Sim | Tipo de multa por atraso (P=Percentual, V=Valor). |
| `HOS_VALOR_MULTA` | NUMERIC(15,2) | Sim | Valor de multa. |
| `HOS_MULTA` | NUMERIC(15,2) | Sim | Percentual/valor base da multa. |
| `HOS_INTERVALO_MULTA` | INTEGER | Sim | Intervalo de aplicação da multa. |
| `HOS_QTDE_PERIODO_MULTA` | INTEGER | Sim | Quantidade de períodos para cálculo da multa. |
| `HOS_PERIODO_MULTA` | NUMERIC(15,2) | Sim | Valor do período de multa. |
| `HOS_TIPO_CANCELAMENTO` | VARCHAR(1) | Sim | Tipo de cancelamento (ex.: N=Não compareceu). |
| `HOS_NOTA_SERVICO` | INTEGER | Sim | FK para TB_NOTA_SERVICO emitida. |
| `HOS_TIPO_TAXA_SERVICO` | VARCHAR(1) | Sim | Tipo da taxa de serviço (P=Percentual, V=Valor). |
| `HOS_TAXA_SERVICO` | NUMERIC(15,1) | Sim | Percentual/valor da taxa de serviço. |
| `HOS_VALOR_TAXA_SERVICO` | NUMERIC(15,1) | Sim | Valor calculado da taxa de serviço. |
| `HOS_VALOR_ESTIMADO` | NUMERIC(15,2) | Sim | Valor estimado total da hospedagem. |
| `HOS_QTDE_PERIODOS_ESTIMADO` | INTEGER | Sim | Quantidade estimada de períodos. |

COMMENT ON COLUMN TB_HOSPEDAGEM.HOS_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

# Tabela TB_HOSP_HOSPEDE

**Módulo:** Hospedagem
Tabela de hóspedes vinculados a uma hospedagem. Permite registrar titular(es) e acompanhantes com dados de chegada, saída, placa de veículo e observações.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `HHOS_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `HHOS_HOSPEDAGEM` | INTEGER | Não | FK para TB_HOSPEDAGEM. Identificador da hospedagem. Parte da chave primária composta. |
| `HHOS_SEQUENCIA` | INTEGER | Não | Sequencial do hóspede dentro da hospedagem. Parte da chave primária composta. |
| `HHOS_DATA_CHEGADA` | DATE | Sim | Data de chegada do hóspede. |
| `HHOS_HORA_CHEGADA` | TIME | Sim | Hora de chegada do hóspede. |
| `HHOS_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro. |
| `HHOS_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que registrou o hóspede. |
| `HHOS_CLIENTE` | INTEGER | Sim | FK para TB_PESSOA (PES_CLIENTE=S). Hóspede/cliente. |
| `HHOS_DATA_SAIDA` | DATE | Sim | Data de saída do hóspede. |
| `HHOS_HORA_SAIDA` | TIME | Sim | Hora de saída do hóspede. |
| `HHOS_OBSERVACAO` | VARCHAR(1000) | Sim | Observações sobre o hóspede. |
| `HHOS_PLACA` | VARCHAR(10) | Sim | Placa do veículo do hóspede. |
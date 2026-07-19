# Tabela TB_MANUTENCAO_VEICULO

**Módulo:** Frota / Veículos
Cadastro de manutenções realizadas em veículos. Registra data da manutenção, próxima prevista, valor gasto, quilometragem, fornecedor e status.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `MAN_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `MAN_ID` | INTEGER | Não | Identificador único da manutenção. Parte da chave primária composta. |
| `MAN_VEICULO` | INTEGER | Sim | FK para TB_VEICULO. Veículo que recebeu a manutenção. |
| `MAN_DT_MANUTENCAO` | DATE | Sim | Data em que a manutenção foi realizada. |
| `MAN_DT_PROXIMA` | DATE | Sim | Data prevista para a próxima manutenção. |
| `MAN_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de gravação do registro. |
| `MAN_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que registrou a manutenção. |
| `MAN_DESCRICAO` | VARCHAR(100) | Sim | Descrição resumida da manutenção. |
| `MAN_OBSERVACAO` | VARCHAR(2000) | Sim | Observações detalhadas da manutenção. |
| `MAN_VALOR` | NUMERIC(15,2) | Sim | Valor gasto na manutenção. |
| `MAN_KM_VEICULO` | NUMERIC(15,2) | Sim | Quilometragem do veículo no momento da manutenção. |
| `MAN_FORNECEDOR` | INTEGER | Sim | FK para TB_PESSOA (PES_FORNECEDOR=S). Fornecedor/oficina que executou o serviço. |
| `MAN_STATUS` | VARCHAR(1) | Sim | Status da manutenção (A=Agendada, R=Realizada, C=Cancelada). |
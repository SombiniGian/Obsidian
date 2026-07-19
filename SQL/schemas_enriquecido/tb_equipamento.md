# Tabela TB_EQUIPAMENTO

**Módulo:** Ordem de Serviço
Cadastro de equipamentos dos clientes utilizados em ordens de serviço. Permite armazenar até 20 campos de descrição livres além de tipo, marca e vínculo com o cliente.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `EQP_ID` | INTEGER | Não | Identificador único do equipamento. |
| `EQP_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `EQP_TIPO` | INTEGER | Sim | FK para TB_TIPO_EQUIPAMENTO. |
| `EQP_MARCA` | INTEGER | Sim | FK para TB_PROD_MARCA. |
| `EQP_CLIENTE` | INTEGER | Sim | FK para TB_PESSOA (cliente proprietário). |
| `EQP_DESC_1` | VARCHAR(100) | Sim | Campo descrição 1 (ex.: Modelo). |
| `EQP_DESC_2` | VARCHAR(100) | Sim | Campo descrição 2 (ex.: Número de série). |
| `EQP_DESC_3` | VARCHAR(100) | Sim | Campo descrição 3. |
| `EQP_DESC_4` | VARCHAR(100) | Sim | Campo descrição 4. |
| `EQP_DESC_5` | VARCHAR(100) | Sim | Campo descrição 5. |
| `EQP_DESC_6` | VARCHAR(100) | Sim | Campo descrição 6. |
| `EQP_DESC_7` | VARCHAR(100) | Sim | Campo descrição 7. |
| `EQP_DESC_8` | VARCHAR(100) | Sim | Campo descrição 8. |
| `EQP_DESC_9` | VARCHAR(100) | Sim | Campo descrição 9. |
| `EQP_DESC_10` | VARCHAR(100) | Sim | Campo descrição 10. |
| `EQP_DESC_11` | VARCHAR(100) | Sim | Campo descrição 11. |
| `EQP_DESC_12` | VARCHAR(100) | Sim | Campo descrição 12. |
| `EQP_DESC_13` | VARCHAR(100) | Sim | Campo descrição 13. |
| `EQP_DESC_14` | VARCHAR(100) | Sim | Campo descrição 14. |
| `EQP_DESC_15` | VARCHAR(100) | Sim | Campo descrição 15. |
| `EQP_DESC_16` | VARCHAR(100) | Sim | Campo descrição 16. |
| `EQP_DESC_17` | VARCHAR(100) | Sim | Campo descrição 17. |
| `EQP_DESC_18` | VARCHAR(100) | Sim | Campo descrição 18. |
| `EQP_DESC_19` | VARCHAR(100) | Sim | Campo descrição 19. |
| `EQP_DESC_20` | VARCHAR(100) | Sim | Campo descrição 20. |
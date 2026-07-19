# Tabela TB_PEDIDO_IFOOD

**Módulo:** Integração / iFood
Tabela de integração com pedidos da plataforma iFood. Armazena os dados recebidos da API do iFood e faz a vinculação com o pedido de venda interno.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PFD_ID` | VARCHAR(100) | Não | Identificador único do pedido no iFood. |
| `PFD_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `PFD_CODE` | VARCHAR(50) | Sim | Código de confirmação do iFood. |
| `PFD_CORRELATIORID` | VARCHAR(100) | Não | ID de correlação da API. |
| `PFD_CREATEDAT` | TIMESTAMP | Sim | Data/hora de criação do pedido no iFood. |
| `PFD_METADATA` | BLOB SUB_TYPE BINARY | Sim | Metadados completos do pedido em formato binário (JSON). NUNCA selecione em queries SELECT. |
| `PFD_PEDIDO` | INTEGER | Sim | FK para TB_PEDIDO_VENDA vinculado. |
| `PFD_STATUS` | VARCHAR(100) | Sim | Status atual do pedido no iFood (PLC, CONFIRMED, PREPARING, READY, DISPATCHED, DELIVERED, CANCELLED). |
| `PFD_ORDER_TIMING` | VARCHAR(20) | Sim | Momento do pedido (IMMEDIATE, SCHEDULED). |
| `PFD_ORDER_TYPE` | VARCHAR(20) | Sim | Tipo do pedido (DELIVERY, TAKEOUT, INDOOR). |
| `PFD_QTDE_PEDIDOS` | INTEGER | Sim | Quantidade de pedidos/itens. |
| `PFD_DESC_IFOOD` | NUMERIC(15,2) | Sim | Desconto concedido pelo iFood. |
| `PFD_DESC_LOJA` | NUMERIC(15,2) | Sim | Desconto concedido pela loja. |
| `PFD_INICIO_AGEND` | TIMESTAMP | Sim | Início do agendamento (para pedidos agendados). |
| `PFD_FIM_AGEND` | TIMESTAMP | Sim | Fim do agendamento. |
| `PFD_DISPLAY_ID` | VARCHAR(20) | Sim | ID de exibição do pedido. |
| `PFD_VALOR_PAGO` | NUMERIC(15,2) | Sim | Valor pago pelo cliente. |
| `PFD_VALOR_PENDENTE` | NUMERIC(15,2) | Sim | Valor pendente de pagamento. |
| `PFD_TIPO_ENTREGA` | VARCHAR(20) | Sim | Tipo de entrega (DELIVERY, TAKEOUT). |
| `PFD_RESPONSAVEL_ENTREGA` | VARCHAR(20) | Sim | Responsável pela entrega (MERCHANT, LOGISTIC_OPERATOR). |
| `PFD_OBS_ENTREGA` | VARCHAR(255) | Sim | Observação para a entrega. |
| `PFD_MODO_RETIRADA` | VARCHAR(20) | Sim | Modo de retirada (TO_GO, EAT_IN). |
| `PFD_NOME_CLIENTE` | VARCHAR(100) | Sim | Nome do cliente. |
| `PFD_TELEFONE` | VARCHAR(20) | Sim | Telefone do cliente. |
| `PFD_CPF` | VARCHAR(14) | Sim | CPF do cliente. |
| `PFD_ENDERECO` | VARCHAR(255) | Sim | Endereço de entrega. |
| `PFD_BAIRRO` | VARCHAR(100) | Sim | Bairro. |
| `PFD_COMPLEMENTO` | VARCHAR(100) | Sim | Complemento do endereço. |
| `PFD_REFERENCIA` | VARCHAR(100) | Sim | Ponto de referência. |
| `PFD_CEP` | VARCHAR(10) | Sim | CEP. |
| `PFD_CIDADE` | VARCHAR(100) | Sim | Cidade. |
| `PFD_ESTADO` | VARCHAR(2) | Sim | Estado (UF). |
| `PFD_PAIS` | VARCHAR(2) | Sim | País (BR). |
| `PFD_LATITUDE` | NUMERIC(15,2) | Sim | Latitude da entrega. |
| `PFD_LONGITUDE` | NUMERIC(15,2) | Sim | Longitude da entrega. |
| `PFD_DT_HR_ENTREGA` | TIMESTAMP | Sim | Data/hora prevista para entrega. |
| `PFD_NOME_RESTAURANTE` | VARCHAR(100) | Sim | Nome do restaurante no iFood. |

COMMENT ON COLUMN TB_PEDIDO_IFOOD.PFD_METADATA IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — armazena o JSON completo do pedido';
COMMENT ON COLUMN TB_PEDIDO_IFOOD.PFD_PEDIDO IS 'FK para TB_PEDIDO_VENDA — utilize JOIN para obter os dados do pedido interno';
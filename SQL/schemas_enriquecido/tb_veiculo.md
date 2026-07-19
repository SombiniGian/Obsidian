# Tabela TB_VEICULO

**Módulo:** Cadastros / Frota
Cadastro de veículos próprios ou terceirizados utilizados para transporte de mercadorias. Armazena dados de identificação (placa, chassi, RENAVAM, RNTRC), características (marca, modelo, cor, ano fabricação/modelo, tipo, carroceria), pesos (bruto, carga, tara), metragem cúbica, consumo (km/litro) e observações. Usado em NF-e (campo veículo), manifesto de transporte e controle de frota.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `VEI_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `VEI_ID` | INTEGER | Não | Identificador único do veículo. Parte da chave primária composta. |
| `VEI_DESCRICAO` | VARCHAR(100) | Sim | Descrição/identificação do veículo (ex.: Caminhão 1 - Entregas). |
| `VEI_MARCA` | VARCHAR(50) | Sim | Marca do veículo (ex.: Mercedes-Benz, Volkswagen). |
| `VEI_MODELO` | VARCHAR(50) | Sim | Modelo do veículo (ex.: Accelo 815, Delivery 9.170). |
| `VEI_CHASSI` | VARCHAR(20) | Sim | Número do chassi. |
| `VEI_COR` | VARCHAR(20) | Sim | Cor do veículo. |
| `VEI_PLACA` | VARCHAR(8) | Sim | Placa do veículo (formato Mercosul ou antigo). |
| `VEI_PLACA_UF` | VARCHAR(2) | Sim | UF da placa. |
| `VEI_ANO_FAB` | INTEGER | Sim | Ano de fabricação. |
| `VEI_ANO_MODELO` | INTEGER | Sim | Ano do modelo. |
| `VEI_RENAVAM` | VARCHAR(20) | Sim | Número do RENAVAM. |
| `VEI_RNTRC` | VARCHAR(20) | Sim | RNTRC (Registro Nacional de Transportadores Rodoviários de Cargas). |
| `VEI_PESO_BRUTO` | NUMERIC(15,2) | Sim | Peso bruto total (PBT) em kg. |
| `VEI_PESO_CARGA` | NUMERIC(15,2) | Sim | Capacidade de carga útil em kg. |
| `VEI_TARA` | NUMERIC(15,2) | Sim | Tara (peso do veículo sem carga) em kg. |
| `VEI_METRAGEM_CUBICA` | NUMERIC(15,2) | Sim | Metragem cúbica do compartimento de carga (m³). |
| `VEI_TIPO` | VARCHAR(1) | Sim | Tipo do veículo (P=Próprio, T=Terceiro). |
| `VEI_STATUS` | VARCHAR(1) | Sim | Status do veículo (A=Ativo, I=Inativo). |
| `VEI_OBSERVACAO` | VARCHAR(2000) | Sim | Observações do veículo. |
| `VEI_KM_LITRO` | NUMERIC(15,2) | Sim | Consumo médio (km/litro). |
| `VEI_TIPO_VEICULO` | INTEGER | Sim | Tipo do veículo (1=Truck, 2=Toco, 3=Cavalo Mecânico, 4=Van, 5=Utilitário, 6=Outros). |
| `VEI_TIPO_CARROCERIA` | INTEGER | Sim | Tipo de carroceria (1=Aberta, 2=Fechada, 3=Graneleira, 4=Porta Container, 5=Sider). |

COMMENT ON COLUMN TB_VEICULO.VEI_TIPO IS 'P - PROPRIO
T - TERCEIRO';
COMMENT ON COLUMN TB_VEICULO.VEI_TIPO_VEICULO IS '1 - TRUCK
2 - TOCO
3 - CAVALO MECANICO
4 - VAN
5 - UTILITARIO
6 - OUTROS';
COMMENT ON COLUMN TB_VEICULO.VEI_TIPO_CARROCERIA IS '1 - ABERTA
2 - FECHADA
3 - GRANELEIRA
4 - PORTA CONTAINER
5 - SIDER';

# Tabela TB_CARGA

**Módulo:** Logística / Transporte
Cadastro da carga de mercadorias para entrega/coleta. Agrupa pedidos de venda em uma carga com transportador, veículo, rotas e informações de acerto/confronto.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CARG_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `CARG_ID` | INTEGER | Não | Identificador único da carga. Parte da chave primária composta. |
| `CARG_DT_EMISSAO` | DATE | Sim | Data de emissão da carga. |
| `CARG_DT_FATURAMENTO` | TIMESTAMP | Sim | Data e hora do faturamento. |
| `CARG_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro. |
| `CARG_DT_SAIDA` | DATE | Sim | Data de saída da carga. |
| `CARG_HORA_SAIDA` | TIME | Sim | Hora de saída da carga. |
| `CARG_DT_CHEGADA` | DATE | Sim | Data de chegada da carga. |
| `CARG_QTDE_PEDIDOS` | INTEGER | Sim | Quantidade de pedidos vinculados à carga. |
| `CARG_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que lançou a carga. |
| `CARG_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total da carga. |
| `CARG_VALOR_PREV` | NUMERIC(15,2) | Sim | Valor previsto da carga. |
| `CARG_VALOR_GASTO` | NUMERIC(15,2) | Sim | Valor gasto com a viagem. |
| `CARG_VOLUMES` | INTEGER | Sim | Quantidade de volumes transportados. |
| `CARG_TRANSPORTADOR` | INTEGER | Sim | FK para TB_PESSOA (transportador). |
| `CARG_METRAGEM` | NUMERIC(15,2) | Sim | Metragem cúbica da carga. |
| `CARG_PESO_BRUTO` | NUMERIC(15,2) | Sim | Peso bruto da carga. |
| `CARG_PESO_LIQUIDO` | NUMERIC(15,2) | Sim | Peso líquido da carga. |
| `CARG_PLACA` | VARCHAR(8) | Sim | Placa do veículo. |
| `CARG_UF` | VARCHAR(2) | Sim | UF da placa do veículo. |
| `CARG_TIPO_FRETE` | INTEGER | Sim | Tipo do frete (0=CIF, 1=FOB, 2=Terceiros, 3=Próprio remetente, 4=Próprio destinatário). |
| `CARG_AJUDANTE` | VARCHAR(50) | Sim | Nome do ajudante da carga. |
| `CARG_STATUS` | VARCHAR(1) | Sim | Status da carga (A=Aberta, F=Fechada, C=Cancelada, T=Em trânsito, E=Entregue). |
| `CARG_OBSERVACAO` | VARCHAR(2000) | Sim | Observações gerais. |
| `CARG_VEICULO` | INTEGER | Sim | FK para TB_VEICULO. |
| `CARG_KM_SAIDA` | NUMERIC(15,2) | Sim | Quilometragem na saída. |
| `CARG_KM_CHEGADA` | NUMERIC(15,2) | Sim | Quilometragem na chegada. |
| `CARG_KM_GASTO` | NUMERIC(15,2) | Sim | Quilometragem gasta no trecho. |
| `CARG_KM_LITRO` | NUMERIC(15,2) | Sim | Consumo (Km/litro). |
| `CARG_LITROS_GASTO` | NUMERIC(15,2) | Sim | Litros de combustível gastos. |
| `CARG_REC_DINHEIRO` | NUMERIC(15,2) | Sim | Valor recebido em dinheiro na carga. |
| `CARG_REC_CHEQUE` | NUMERIC(15,2) | Sim | Valor recebido em cheque na carga. |
| `CARG_REC_CARTAO` | NUMERIC(15,2) | Sim | Valor recebido em cartão na carga. |
| `CARG_INFORMACOES_ACERTO` | VARCHAR(2000) | Sim | Informações do acerto/confronto. |
| `CARG_DESCRICAO` | VARCHAR(100) | Sim | Descrição da carga. |
| `CARG_TIPO` | VARCHAR(10) | Sim | Tipo da carga (E=Entrega, C=Coleta, T=Transferência). |
| `CARG_RNTRC` | VARCHAR(20) | Sim | RNTRC do transportador. |
| `CARG_LOTE_PRODUCAO` | INTEGER | Sim | FK para TB_LOTE_PRODUCAO. |
| `ID` | INTEGER | Sim | Identificador legado. |
| `ID_ANT` | INTEGER | Sim | Identificador anterior (migração). |
| `CARG_NF_REMESSA` | INTEGER | Sim | FK para TB_NOTA_FISCAL de remessa. |
| `CARG_NF_RETORNO` | INTEGER | Sim | FK para TB_NOTA_FISCAL de retorno. |
| `CARG_EMP_NF` | INTEGER | Sim | Empresa emissora das NF vinculadas. |

COMMENT ON COLUMN TB_CARGA.CARG_TIPO_FRETE IS '0=CIF; 1=FOB; 2=Terceiros; 3=Próprio por conta do remetente; 4=Próprio por conta do destinatário';
COMMENT ON COLUMN TB_CARGA.CARG_TIPO IS 'E - ENTREGA
C - COLETA
T - TRANSFERENCIA';
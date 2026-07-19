# Tabela TB_MANIFESTO_ELETRONICO

**Módulo:** Fiscal / Transporte
Manifesto Eletrônico de Documentos Fiscais (MDF-e). Documento fiscal emitido para vincular múltiplos NF-e, CT-e e CT em uma operação de transporte interestadual.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `MAN_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `MAN_ID` | INTEGER | Não | Identificador único do MDF-e. Parte da chave primária composta. |
| `MAN_STATUS` | VARCHAR(1) | Sim | Status do manifesto (A=Aberto, F=Fechado, C=Cancelado, T=Em trânsito). |
| `MAN_SERIE` | VARCHAR(10) | Sim | Série do MDF-e. |
| `MAN_NUMERO` | INTEGER | Sim | Número do MDF-e. |
| `MAN_MODELO` | INTEGER | Sim | Modelo do documento (58=MDF-e). |
| `MAN_DT_EMISSAO` | DATE | Sim | Data de emissão do manifesto. |
| `MAN_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento. |
| `MAN_DATA_SAIDA` | DATE | Sim | Data de saída da viagem. |
| `MAN_HORA_SAIDA` | TIME | Sim | Hora de saída da viagem. |
| `MAN_PESO_BRUTO` | NUMERIC(15,4) | Sim | Peso bruto total da carga. |
| `MAN_VALOR_CARGA` | NUMERIC(15,2) | Sim | Valor total da carga transportada. |
| `MAN_TIPO_EMITENTE` | INTEGER | Sim | Tipo do emitente (1=Transportador, 2=Carga própria). |
| `MAN_MODALIDADE` | INTEGER | Sim | Modalidade de transporte (1=Rodoviário, 2=Aéreo, 3=Aquaviário, 4=Ferroviário, 5=Dutoviário). |
| `MAN_QTDE_NFE` | INTEGER | Sim | Quantidade de NF-e vinculadas. |
| `MAN_QTDE_NF` | INTEGER | Sim | Quantidade de NF (modelo 1/2) vinculadas. |
| `MAN_QTDE_CTE` | INTEGER | Sim | Quantidade de CT-e vinculados. |
| `MAN_QTDE_CT` | INTEGER | Sim | Quantidade de CT vinculados. |
| `MAN_UNIDADE` | VARCHAR(8) | Sim | Unidade de medida do peso. |
| `MAN_UF_INICIO` | VARCHAR(2) | Sim | UF de início da viagem. |
| `MAN_UF_TERMINO` | VARCHAR(2) | Sim | UF de término da viagem. |
| `MAN_FINALIDADE` | INTEGER | Sim | Finalidade do manifesto (1=Normal, 2=Substituição). |
| `MAN_RNTRC` | VARCHAR(20) | Sim | RNTRC do transportador. |
| `MAN_CIOT` | VARCHAR(12) | Sim | Código CIOT. |
| `MAN_CIDADE_ENCERRAMENTO` | INTEGER | Sim | FK para TB_CIDADE de encerramento. |
| `MAN_VEICULO` | INTEGER | Sim | FK para TB_VEICULO. |
| `MAN_PLACA` | VARCHAR(8) | Sim | Placa do veículo. |
| `MAN_PLACA_UF` | VARCHAR(2) | Sim | UF da placa. |
| `MAN_RENAVAM` | VARCHAR(20) | Sim | RENAVAM do veículo. |
| `MAN_TARA` | NUMERIC(15,2) | Sim | Tara do veículo. |
| `MAN_CAPACIDADE_KG` | INTEGER | Sim | Capacidade em Kg. |
| `MAN_CAPACIDADE_M3` | INTEGER | Sim | Capacidade em M3. |
| `MAN_TIPO_VEICULO` | INTEGER | Sim | Tipo do veículo (tração). |
| `MAN_TIPO_CARROCERIA` | INTEGER | Sim | Tipo de carroceria. |
| `MAN_PROPRIETARIO` | VARCHAR(1) | Sim | Indica se é veículo próprio. |
| `MAN_PROP_CNPJ_CPF` | VARCHAR(14) | Sim | CNPJ/CPF do proprietário. |
| `MAN_PROP_RNTRC` | VARCHAR(8) | Sim | RNTRC do proprietário. |
| `MAN_PROP_NOME` | VARCHAR(60) | Sim | Nome do proprietário. |
| `MAN_PROP_IE` | VARCHAR(14) | Sim | IE do proprietário. |
| `MAN_PROP_UF` | VARCHAR(2) | Sim | UF do proprietário. |
| `MAN_PROP_TIPO` | INTEGER | Sim | Tipo do proprietário. |
| `MAN_SEGURADORA` | INTEGER | Sim | FK para TB_PESSOA (seguradora). |
| `MAN_SEG_NOME` | VARCHAR(100) | Sim | Nome da seguradora. |
| `MAN_SEG_CNPJ` | VARCHAR(14) | Sim | CNPJ da seguradora. |
| `MAN_SEG_APOLICE` | VARCHAR(20) | Sim | Número da apólice. |
| `MAN_SEG_AVERBACAO` | VARCHAR(10) | Sim | Número da averbação. |
| `MAN_SEG_RESP` | INTEGER | Sim | Tipo de responsabilidade do seguro. |
| `MAN_SEG_RESP_CNPJ_CPF` | VARCHAR(14) | Sim | CNPJ/CPF do responsável pelo seguro. |
| `MAN_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações em formato binário. NUNCA selecione em queries SELECT. |
| `MAN_INFORMAR_MANUAL` | VARCHAR(1) | Sim | Informa dados manualmente (S/N). |
| `MAN_PROD_PREDOMINANTE` | VARCHAR(120) | Sim | Produto predominante da carga. |
| `MAN_TIPO_CARGA` | INTEGER | Sim | Tipo da carga (1=Granel sólido, 2=Granel líquido, 3=Contêiner, 4=Carga geral etc.). |
| `MAN_TIPO_TRANSPOTADOR` | INTEGER | Sim | Tipo do transportador. |
| `MAN_PROD_EAN` | VARCHAR(14) | Sim | EAN/GTIN do produto predominante. |
| `MAN_PROD_NCM` | VARCHAR(8) | Sim | NCM do produto predominante. |
| `MAN_CEP_CARREGA` | VARCHAR(10) | Sim | CEP do local de carregamento. |
| `MAN_CEP_DESCARREGA` | VARCHAR(10) | Sim | CEP do local de descarregamento. |
| `MAN_LONG_CARREGA` | NUMERIC(10,6) | Sim | Longitude do local de carregamento. |
| `MAN_LATITUDE_CARREGA` | NUMERIC(10,6) | Sim | Latitude do local de carregamento. |
| `MAN_LONG_DESCARREGA` | NUMERIC(10,6) | Sim | Longitude do local de descarregamento. |
| `MAN_LATITUDE_DESCARREGA` | NUMERIC(10,6) | Sim | Latitude do local de descarregamento. |
| `MAN_CATEG_VEIC` | VARCHAR(2) | Sim | Categoria do veículo (02=Caminhão, 03=Cavalo mecânico etc.). |

COMMENT ON COLUMN TB_MANIFESTO_ELETRONICO.MAN_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
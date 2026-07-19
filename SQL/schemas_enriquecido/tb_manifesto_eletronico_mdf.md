# Tabela TB_MANIFESTO_ELETRONICO_MDF

**Módulo:** Fiscal / Manifesto Eletrônico
Tabela de controle do Manifesto Eletrônico de Documentos Fiscais (MDF-e). Armazena status, chave de acesso, protocolos, recibos, retornos da SEFAZ, caminhos dos XMLs/PDFs gerados e dados de cancelamento e encerramento.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `MEM_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `MEM_MANIFESTO` | INTEGER | Não | FK para TB_MANIFESTO_ELETRONICO. Identificador do manifesto. Parte da chave primária composta. |
| `MEM_STATUS` | VARCHAR(1) | Sim | Status do MDF-e (1=Digitado, 2=Transmitido, 3=Autorizado, 4=Cancelado, 5=Encerrado). |
| `MEM_CHAVE_ACESSO` | VARCHAR(44) | Sim | Chave de acesso do MDF-e (44 dígitos). |
| `MEM_PROTOCOLO_AUT` | VARCHAR(50) | Sim | Protocolo de autorização de uso retornado pela SEFAZ. |
| `MEM_RECIBO` | VARCHAR(50) | Sim | Número do recibo de entrega do MDF-e. |
| `MEM_DATA_HORA_TRANS` | TIMESTAMP | Sim | Data e hora da transmissão do MDF-e. |
| `MEM_COD_RETORNO` | INTEGER | Sim | Código de retorno da SEFAZ. |
| `MEM_MSG_RETORNO` | VARCHAR(200) | Sim | Mensagem de retorno da SEFAZ. |
| `MEM_CAMINHO_PDF` | VARCHAR(200) | Sim | Caminho/URL do arquivo PDF do MDF-e. |
| `MEM_CAMINHO_XML` | VARCHAR(200) | Sim | Caminho/URL do XML autorizado do MDF-e. |
| `MEM_CAMINHO_XML_CANC` | VARCHAR(200) | Sim | Caminho/URL do XML de cancelamento. |
| `MEM_CAMINHO_XML_AUT` | VARCHAR(200) | Sim | Caminho/URL do XML de autorização. |
| `MEM_DATA_HORA_CANC` | TIMESTAMP | Sim | Data e hora do cancelamento do MDF-e. |
| `MEM_PROTOCOLO_CANC` | VARCHAR(50) | Sim | Protocolo de cancelamento retornado pela SEFAZ. |
| `MEM_MOTIVO_CANCELAMENTO` | VARCHAR(255) | Sim | Motivo do cancelamento do MDF-e. |
| `MEM_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que transmitiu o MDF-e. |
| `MEM_USUARIO_CANCEL` | INTEGER | Sim | FK para TB_USUARIO que cancelou o MDF-e. |
| `MEM_AMBIENTE` | INTEGER | Sim | Ambiente de emissão (1=Produção, 2=Homologação). |
| `MEM_FORMA_EMISSAO` | INTEGER | Sim | Forma de emissão do MDF-e (1=Normal, 2=Contingência). |
| `MEM_CAMINHO_XML_ENC` | VARCHAR(200) | Sim | Caminho/URL do XML de encerramento. |
| `MEM_DATA_HORA_ENC` | TIMESTAMP | Sim | Data e hora do encerramento do MDF-e. |
| `MEM_PROTOCOLO_ENC` | VARCHAR(50) | Sim | Protocolo de encerramento retornado pela SEFAZ. |
| `MEM_XML` | BLOB SUB_TYPE BINARY SEGMENT SIZE 100 | Sim | Conteúdo binário do XML do MDF-e. |
| `MEM_XML_ENCERRAMENTO` | BLOB SUB_TYPE BINARY | Sim | Conteúdo binário do XML de encerramento. |
| `MEM_XML_CANC` | BLOB SUB_TYPE BINARY | Sim | Conteúdo binário do XML de cancelamento. |

COMMENT ON COLUMN TB_MANIFESTO_ELETRONICO_MDF.MEM_XML IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização';
COMMENT ON COLUMN TB_MANIFESTO_ELETRONICO_MDF.MEM_XML_ENCERRAMENTO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_MANIFESTO_ELETRONICO_MDF.MEM_XML_CANC IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

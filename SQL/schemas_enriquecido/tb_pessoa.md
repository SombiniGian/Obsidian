# Tabela TB_PESSOA

**Módulo:** Cadastros
Tabela principal de cadastro de pessoas (Clientes, Fornecedores, Vendedores, Colaboradores, Transportadores, Técnicos).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PES_ID` | INTEGER | Não | Identificador único do cadastro. |
| `PES_TIPO_PESSOA` | VARCHAR(1) | Sim | Tipo de pessoa (F=Física, J=Jurídica). |
| `PES_RSOCIAL_NOME` | VARCHAR(100) | Sim | Nome completo ou Razão Social. |
| `PES_FANTASIA_APELIDO` | VARCHAR(100) | Sim | Nome fantasia (PJ) ou apelido (PF). |
| `PES_CNPJ_CPF` | VARCHAR(14) | Sim | Número do CPF ou CNPJ (somente números). |
| `PES_IE_RG` | VARCHAR(18) | Sim | Inscrição Estadual (PJ) ou RG (PF). |
| `PES_ENDERECO` | VARCHAR(100) | Sim | Logradouro do endereço. |
| `PES_COMPLEMENTO` | VARCHAR(20) | Sim | Complemento do endereço. |
| `PES_NUMERO` | VARCHAR(10) | Sim | Número do endereço. |
| `PES_BAIRRO` | VARCHAR(50) | Sim | Bairro do endereço. |
| `PES_CIDADE` | INTEGER | Sim | FK para TB_CIDADE.CID_ID. |
| `PES_CEP` | VARCHAR(10) | Sim | CEP do endereço. |
| `PES_TELEFONE` | VARCHAR(20) | Sim | Telefone fixo. |
| `PES_FAX` | VARCHAR(20) | Sim | Número de fax. |
| `PES_CELULAR` | VARCHAR(20) | Sim | Telefone celular. |
| `PES_EMAIL` | VARCHAR(1000) | Sim | Endereço(s) de e-mail. |
| `PES_CONTATO` | VARCHAR(50) | Sim | Nome do contato principal. |
| `PES_OBSERVACAO` | VARCHAR(2000) | Sim | Observações gerais do cadastro. |
| `PES_DT_CADASTRO` | DATE | Sim | Data de cadastro do registro. |
| `PES_DT_NASCIMENTO` | DATE | Sim | Data de nascimento (PF) ou fundação (PJ). |
| `PES_STATUS` | VARCHAR(1) | Sim | Status do cadastro (A=Ativo, I=Inativo). |
| `PES_CLIENTE` | VARCHAR(1) | Sim | Indica se a pessoa é cliente (S/N). |
| `PES_FORNECEDOR` | VARCHAR(1) | Sim | Indica se a pessoa é fornecedora (S/N). |
| `PES_VENDEDOR` | VARCHAR(1) | Sim | Indica se a pessoa é vendedora (S/N). |
| `PES_COLABORADOR` | VARCHAR(1) | Sim | Indica se a pessoa é colaboradora (S/N). |
| `PES_TRANSPORTADOR` | VARCHAR(1) | Sim | Indica se a pessoa é transportadora (S/N). |
| `PES_TECNICO` | VARCHAR(1) | Sim | Indica se a pessoa é técnica (S/N). |
| `PES_COMPRADOR` | VARCHAR(1) | Sim | Indica se a pessoa é compradora (S/N). |
| `PES_INTERMEDIADOR` | VARCHAR(1) | Sim | Indica se a pessoa é intermediadora (S/N). |
| `PES_ADM_CARTAO` | VARCHAR(1) | Sim | Indica se a pessoa é administradora de cartão (S/N). |
| `PES_CONTRIBUINTE` | VARCHAR(1) | Sim | Indica se a pessoa é contribuinte ICMS (S/N). |
| `PES_EXTERIOR` | VARCHAR(1) | Sim | Indica se a pessoa é do exterior (S/N). |
| `PES_DEPENDENTE` | VARCHAR(1) | Sim | Indica se o cadastro é dependente de outro (S/N). |
| `PES_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção em listagens (S/N). |
| `PES_SEXO` | VARCHAR(1) | Sim | Sexo (M/F). |
| `PES_RACA` | VARCHAR(20) | Sim | Raça/Etnia declarada (AMARELA/BRANCA/INDIGENA/PARDA/PRETA/NAOINFORMAR). |
| `PES_DEFICIENCIA` | VARCHAR(20) | Sim | Indica se a pessoa possui deficiência (SIM/NAO/NAOINFORMAR). |
| `PES_PROFISSAO` | VARCHAR(50) | Sim | Profissão declarada. |
| `PES_REFERENCIA` | VARCHAR(100) | Sim | Referência comercial/pessoal. |
| `PES_CODIGO_INTERNO` | VARCHAR(10) | Sim | Código interno do cadastro. |
| `PES_CODIGO_ACESSO` | VARCHAR(30) | Sim | Código de acesso (controle de acesso/portaria). |
| `PES_DOC_EXTERIOR` | VARCHAR(20) | Sim | Documento para pessoas do exterior. |
| `PES_INSC_MUNICIPAL` | VARCHAR(20) | Sim | Inscrição Municipal. |
| `PES_INSC_SUFRAMA` | VARCHAR(10) | Sim | Inscrição SUFRAMA. |
| `PES_MOTIVO` | VARCHAR(100) | Sim | Motivo do cancelamento do cadastro. |
| `PES_DATA_CANCELAMENTO` | DATE | Sim | Data de cancelamento do cadastro. |
| `PES_DATA_INICIO` | DATE | Sim | Data de início do acesso/contrato. |
| `PES_HORA_INICIO` | TIME | Sim | Hora de início do acesso/contrato. |
| `PES_DATA_FIM` | DATE | Sim | Data de fim do acesso/contrato. |
| `PES_HORA_FIM` | TIME | Sim | Hora de fim do acesso/contrato. |
| `PES_STATUS_ACESSO` | VARCHAR(1) | Sim | Status de controle de acesso (A/I). |
| `PES_QUANTIDADE_ACESSO` | INTEGER | Sim | Quantidade de acessos realizados. |
| `PES_CONTA_RECEBER` | INTEGER | Sim | FK para conta contábil de recebimentos. |
| `PES_CONTA_PAGAR` | INTEGER | Sim | FK para conta contábil de pagamentos. |
| `PES_CONTA_CHEQUES_REC` | INTEGER | Sim | FK para conta contábil de cheques recebidos. |
| `PES_CONTA_CREDITO_REC` | INTEGER | Sim | FK para conta contábil de crédito a receber. |
| `PES_CONTA_CREDITO_PAG` | INTEGER | Sim | FK para conta contábil de crédito a pagar. |
| `PES_CONTA_DESPESAS` | INTEGER | Sim | FK para conta contábil de despesas. |
| `PES_CONTA_RECEITAS` | INTEGER | Sim | FK para conta contábil de receitas. |
| `PES_END` | INTEGER | Sim | FK para endereço alternativo (TB_ENDERECO). |
| `PES_GUID` | VARCHAR(50) | Sim | GUID para integração. |
| `PES_ATT_SERVIDOR` | VARCHAR(1) | Sim | Atualizado via servidor de integração (S/N). |
| `PES_ID_IFOOD` | VARCHAR(100) | Sim | ID do cadastro na integração com iFood. |
| `PES_ID_MELI` | VARCHAR(100) | Sim | ID do cadastro na integração com Mercado Livre. |
| `PES_ID_SERVIDOR` | INTEGER | Sim | FK para TB_SERVIDOR (servidor de origem). |
| `PES_ID_LOCAL` | INTEGER | Sim | FK para TB_LOCAL (local/loja de origem). |
| `PES_ESTACAO_PDV` | INTEGER | Sim | Estação PDV associada ao cadastro. |
| `PES_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. Default: current_timestamp. |
| `PES_FOTO` | BLOB SUB_TYPE BINARY | Sim | Foto de perfil em formato binário. |
| `PES_DIGITAL1` | BLOB SUB_TYPE BINARY | Sim | Biometria - digital 1. |
| `PES_DIGITAL2` | BLOB SUB_TYPE BINARY | Sim | Biometria - digital 2. |
| `PES_DIGITAL3` | BLOB SUB_TYPE BINARY | Sim | Biometria - digital 3. |

COMMENT ON COLUMN TB_PESSOA.PES_ID IS 'Chave primária. É referenciada por TB_PEDIDO_VENDA.PEV_VENDEDOR, TB_PEDIDO_VENDA.PEV_CLIENTE, TB_PEDIDO_VENDA.PEV_TRANSPORTADOR, TB_PEDIDO_VENDA.PEV_COMPRADOR, TB_RECEBIMENTO.REC_VENDEDOR etc. Use SEMPRE JOIN por PES_ID, nunca por PES_NOME/PES_CODIGO/PES_CNPJ_CPF.';
COMMENT ON COLUMN TB_PESSOA.PES_CLIENTE IS 'Para filtrar clientes utilize WHERE PES_CLIENTE = ''S''';
COMMENT ON COLUMN TB_PESSOA.PES_FORNECEDOR IS 'Para filtrar fornecedores utilize WHERE PES_FORNECEDOR = ''S''';
COMMENT ON COLUMN TB_PESSOA.PES_VENDEDOR IS 'Para filtrar vendedores utilize WHERE PES_VENDEDOR = ''S''';
COMMENT ON COLUMN TB_PESSOA.PES_COLABORADOR IS 'Para filtrar colaboradores utilize WHERE PES_COLABORADOR = ''S''';
COMMENT ON COLUMN TB_PESSOA.PES_STATUS IS 'Para filtrar apenas cadastros ativos utilize WHERE PES_STATUS = ''A''';
COMMENT ON COLUMN TB_PESSOA.PES_CNPJ_CPF IS 'Armazena CPF (11 dígitos) ou CNPJ (14 dígitos) somente números, sem máscara';
COMMENT ON COLUMN TB_PESSOA.PES_FOTO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização';
COMMENT ON COLUMN TB_PESSOA.PES_DIGITAL1 IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_PESSOA.PES_DIGITAL2 IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_PESSOA.PES_DIGITAL3 IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_PESSOA.PES_CIDADE IS 'FK para TB_CIDADE.CID_ID — use JOIN com TB_CIDADE para obter nome da cidade';


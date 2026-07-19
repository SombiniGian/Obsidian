# Tabela TB_CHEQUE_RECEBIDO

**Módulo:** Financeiro
Tabela de cheques recebidos pela empresa (de clientes). Armazena dados do cheque, titular, banco, agência, conta, CMC7, tipo (próprio/terceiro), situação (recebido, depositado, passado, devolvido, inadimplente), contas de origem/destino, valores de comissão e vínculo com borderôs de depósito/pagamento/comissão.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CHR_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `CHR_ID` | INTEGER | Não | Identificador único do cheque recebido. Parte da chave primária composta. |
| `CHR_CLIENTE` | INTEGER | Sim | FK para TB_PESSOA.PES_ID do cliente emitente. Use JOIN por PES_ID. |
| `CHR_STATUS` | VARCHAR(2) | Sim | Status do cheque (AB=Aberto, BX=Baixado, CN=Cancelado). |
| `CHR_SITUACAO` | VARCHAR(2) | Sim | Situação do cheque (CR=Recebido, CD=Depositado, CP=Passado, C1/C2=Devolvido, CI=Inadimplente, CC=Cancelado). |
| `CHR_NUMERO_CHEQUE` | VARCHAR(15) | Sim | Número do cheque. |
| `CHR_BANCO` | VARCHAR(10) | Sim | Código do banco. |
| `CHR_NUMERO_AGENCIA` | VARCHAR(10) | Sim | Número da agência. |
| `CHR_NUMERO_CONTA` | VARCHAR(14) | Sim | Número da conta. |
| `CHR_TITULAR` | VARCHAR(30) | Sim | Nome do titular do cheque. |
| `CHR_VALOR_CHEQUE` | NUMERIC(15,2) | Sim | Valor do cheque. |
| `CHR_DT_EMISSAO` | DATE | Sim | Data de emissão do cheque. |
| `CHR_DT_VENCIMENTO` | DATE | Sim | Data de vencimento/compensação do cheque. |
| `CHR_VENCIMENTO_ORIGINAL` | DATE | Sim | Data de vencimento original (antes de devoluções/prorrogações). |
| `CHR_DT_DEPOSITO` | DATE | Sim | Data do depósito do cheque. |
| `CHR_DT_DEVOLUCAO` | DATE | Sim | Data de devolução do cheque. |
| `CHR_USUARIO` | INTEGER | Sim | Identificador do usuário que lançou o cheque. |
| `CHR_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro no sistema. |
| `CHR_TIPO_CHEQUE` | VARCHAR(1) | Sim | Tipo do cheque (P=Próprio, T=Terceiro). |
| `CHR_ORIGEM` | VARCHAR(30) | Sim | Sigla do módulo/rotina de origem (ex.: RECEBIMENTO). |
| `CHR_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem. |
| `CHR_BORDERO_DEPOSITO` | INTEGER | Sim | FK para TB_BORDERO_DEPOSITO (borderô em que o cheque foi depositado). |
| `CHR_BORDERO_PAGAMENTO` | INTEGER | Sim | FK para TB_BORDERO_PAGAMENTO (borderô em que o cheque foi passado). |
| `CHR_BORDERO_COMISSAO` | INTEGER | Sim | FK para TB_BORDERO_COMISSAO. |
| `CHR_SELECIONADO` | VARCHAR(1) | Sim | Marcador para seleção em processos (S/N). |
| `CHR_OBSERVACAO` | BLOB SUB_TYPE BINARY SEGMENT SIZE 1000 | Sim | Observações em formato binário. NUNCA selecione em queries SELECT. |
| `CHR_CMC7` | VARCHAR(34) | Sim | Código CMC7 do cheque (triagem magnética). |
| `CHR_CAIXA` | INTEGER | Sim | FK para TB_FECHAMENTO_CAIXA. |
| `CHR_FECHAMENTO` | INTEGER | Sim | Identificador do fechamento de caixa. |
| `CHR_PESSOA` | INTEGER | Sim | FK para TB_PESSOA.PES_ID. Use JOIN por PES_ID. |
| `CHR_DESTINATARIO` | INTEGER | Sim | FK para TB_PESSOA.PES_ID destinatário (para quem o cheque foi passado). |
| `CHR_ESPECIE_MOEDA` | INTEGER | Sim | FK para TB_ESPECIE_MOEDA.ESP_ID (para fechar caixa). |
| `CHR_CONTA_ORIGEM` | INTEGER | Sim | FK para TB_CONTA.CNT_ID de origem. |
| `CHR_CONTA_DESTINO` | INTEGER | Sim | FK para TB_CONTA.CNT_ID de destino. |
| `CHR_CONTA_DEPOSITO` | INTEGER | Sim | FK para TB_CONTA.CNT_ID de depósito. |
| `CHR_CONTA_BANC_DEPOSITO` | INTEGER | Sim | FK para TB_CONTA.CNT_ID bancária de depósito. |
| `CHR_ESP_MOEDA_INAD` | INTEGER | Sim | FK para TB_ESPECIE_MOEDA.ESP_ID (espécie de moeda para geração de recebimento em caso de inadimplência). |
| `CHR_COMISSAO` | NUMERIC(15,2) | Sim | Percentual de comissão. |
| `CHR_VALOR_COMISSAO` | NUMERIC(15,2) | Sim | Valor da comissão. |
| `CHR_VENDEDOR` | INTEGER | Sim | FK para TB_VENDEDOR (vendedor responsável). |
| `CHR_GUID` | VARCHAR(50) | Sim | GUID para integração. |

COMMENT ON COLUMN TB_CHEQUE_RECEBIDO.CHR_STATUS IS 'AB -> ABERTO
BX -> BAIXADO
CN -> CANCELADO';
COMMENT ON COLUMN TB_CHEQUE_RECEBIDO.CHR_SITUACAO IS 'CR -> CHEQUES RECEBIDOS
CD -> CHEQUES DEPOSITADOS
CP -> CHEQUES PASSADO
C1 -> CHEQUES 1 DEVOLUÇÃO
C2 -> CHEQUES 2 DEVOLUÇÃO
CI -> INADIMPLÊNCIA
CC -> CANCELADO';
COMMENT ON COLUMN TB_CHEQUE_RECEBIDO.CHR_TIPO_CHEQUE IS '''P'' -> PRÓPRIO
''T'' -> TERCEIRO';
COMMENT ON COLUMN TB_CHEQUE_RECEBIDO.CHR_BORDERO_DEPOSITO IS 'GUARDA ID DO BORDERÔ DE DEPÓSITO EM QUE O CHEQUE FOI DEPOSITADO';
COMMENT ON COLUMN TB_CHEQUE_RECEBIDO.CHR_BORDERO_PAGAMENTO IS 'GUARDA ID DO BORDERO DE PAGAMENTO EM QUE O CHEQUE FOI PASSADO';
COMMENT ON COLUMN TB_CHEQUE_RECEBIDO.CHR_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

# Tabela TB_CHEQUE_EMITIDO

**Módulo:** Financeiro
Tabela de cheques emitidos pela empresa (pagamentos). Armazena dados do cheque (número, valor, emissão, vencimento, compensação, conta de origem/destino), dados do nominal, CMC7 e vínculo com borderô de pagamento. Permite rastrear o ciclo de vida do cheque: emitido, compensado ou cancelado.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CHE_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `CHE_ID` | INTEGER | Não | Identificador único do cheque emitido. Parte da chave primária composta. |
| `CHE_STATUS` | VARCHAR(2) | Sim | Status do cheque (AB=Aberto, CP=Compensado, CN=Cancelado). |
| `CHE_SITUACAO` | VARCHAR(2) | Sim | Situação do cheque (EM=Emitido, CN=Cancelado). |
| `CHE_NUMERO_CHEQUE` | VARCHAR(15) | Sim | Número do cheque. |
| `CHE_VALOR_CHEQUE` | NUMERIC(15,2) | Sim | Valor do cheque. |
| `CHE_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do cheque no sistema. |
| `CHE_DT_EMISSAO` | DATE | Sim | Data de emissão do cheque. |
| `CHE_DT_VENCIMENTO` | DATE | Sim | Data de vencimento/compensação do cheque. |
| `CHE_DT_COMPESACAO` | DATE | Sim | Data efetiva de compensação. |
| `CHE_OBSERVACAO` | BLOB SUB_TYPE BINARY SEGMENT SIZE 1000 | Sim | Observações em formato binário. NUNCA selecione em queries SELECT. |
| `CHE_NOMINAL` | VARCHAR(80) | Sim | Nome de quem é o cheque (nominal). |
| `CHE_IMPRESSO` | VARCHAR(1) | Sim | Indica se o cheque já foi impresso (S/N). |
| `CHE_ORIGEM` | VARCHAR(30) | Sim | Sigla do módulo/rotina de origem (ex.: PAGAMENTO). |
| `CHE_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem. |
| `CHE_BORDERO_PAGAMENTO` | INTEGER | Sim | FK para TB_BORDERO_PAGAMENTO que originou o cheque. |
| `CHE_USUARIO` | INTEGER | Sim | Identificador do usuário que emitiu o cheque. |
| `CHE_CMC7` | VARCHAR(34) | Sim | Código CMC7 do cheque (triagem magnética). |
| `CHE_CONTA` | INTEGER | Sim | FK para TB_CONTA.CNT_ID de origem/destino. |
| `CHE_PESSOA` | INTEGER | Sim | FK para TB_PESSOA.PES_ID do emitente/beneficiado. Use JOIN por PES_ID. |
| `CHE_CONTA_ORIGEM` | INTEGER | Sim | FK para TB_CONTA.CNT_ID de origem. |
| `CHE_CONTA_DESTINO` | INTEGER | Sim | FK para TB_CONTA.CNT_ID de destino. |
| `CHE_CONTA_COMPENSACAO` | INTEGER | Sim | FK para TB_CONTA.CNT_ID de compensação. |

COMMENT ON COLUMN TB_CHEQUE_EMITIDO.CHE_STATUS IS 'AB -> ABERTO
CP -> COMPENSADO
CN -> CANCELADO';
COMMENT ON COLUMN TB_CHEQUE_EMITIDO.CHE_SITUACAO IS 'EM -> EMITIDOS
CN -> CANCELADO';
COMMENT ON COLUMN TB_CHEQUE_EMITIDO.CHE_IMPRESSO IS '''S'' -> SIM
''N'' -> NÃO';
COMMENT ON COLUMN TB_CHEQUE_EMITIDO.CHE_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

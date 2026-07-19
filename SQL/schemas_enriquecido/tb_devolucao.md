# Tabela TB_DEVOLUCAO

**Módulo:** Vendas / Devoluções
Tabela principal de devoluções de mercadorias oriundas de pedidos de venda. Permite registrar devoluções parciais ou totais, geração de crédito para o cliente, comissão do vendedor, integração com carga/romaneio e envio de cancelamento para o XRM.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `DEV_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `DEV_ID` | INTEGER | Sim | Identificador único da devolução. Parte da chave primária composta. |
| `DEV_DT_EMISSAO` | DATE | Sim | Data de emissão da devolução. |
| `DEV_CLIENTE` | INTEGER | Sim | FK para TB_PESSOA.PES_ID — cliente da devolução. |
| `DEV_VENDEDOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID — vendedor da devolução. |
| `DEV_TOTAL_DEVOLUCAO` | NUMERIC(15,2) | Sim | Valor total da devolução. |
| `DEV_USUARIO` | INTEGER | Sim | Identificador do usuário que lançou a devolução. |
| `DEV_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações da devolução em binário. NUNCA selecione em queries SELECT. |
| `DEV_PEDIDO` | INTEGER | Sim | FK para TB_PEDIDO_VENDA.PEV_ID — pedido de venda de origem. |
| `DEV_STATUS` | VARCHAR(1) | Sim | Status da devolução (A=Ativo, C=Cancelado). |
| `DEV_GERAR_CREDITO` | VARCHAR(1) | Sim | Indica se a devolução gera crédito para o cliente (S/N). |
| `DEV_VALOR_COMISSAO` | NUMERIC(15,2) | Sim | Valor de comissão estornado/gerado na devolução. |
| `DEV_MOTIVO` | INTEGER | Sim | FK para TB_DEVOLUCAO_MOTIVO — motivo da devolução. |
| `DEV_PLANO_CONTAS` | INTEGER | Sim | FK para plano de contas (vem do motivo da devolução). |
| `DEV_CONTA_CREDITO` | INTEGER | Sim | Conta de crédito do cliente. |
| `DEV_CONTA_CUSTO` | INTEGER | Sim | Conta de custo debitada quando a mercadoria saiu (a creditar quando voltar). |
| `DEV_CARGA` | INTEGER | Sim | FK para TB_CARGA — carga/romaneio vinculado. |
| `DEV_TIPO_TROCO` | VARCHAR(1) | Sim | Tipo de troco na devolução. |
| `DEV_CAIXA` | INTEGER | Sim | FK para TB_CONTA.CNT_ID — caixa onde foi processada. |
| `DEV_FECHAMENTO` | INTEGER | Sim | FK para TB_FECHAMENTO_CAIXA — fechamento de caixa. |
| `DEV_SALDO_FLEX` | NUMERIC(15,2) | Sim | Saldo flexível da devolução. |
| `DEV_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção em listagens (S/N). |
| `DEV_COMISSAO` | NUMERIC(15,2) | Sim | Percentual/valor de comissão aplicada. |
| `DEV_BORDERO_COMISSAO` | INTEGER | Sim | FK para TB_BORDERO_COMISSAO — borderô de comissão vinculado. |
| `DEV_LOCAL_ESTOQUE` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE.LOC_ID — local onde a mercadoria retornou. |
| `DEV_NOTA_FISCAL` | INTEGER | Sim | FK para TB_NOTA_FISCAL — NF de devolução gerada. |
| `DEV_DEVOLUCAO_FUTURA` | INTEGER | Sim | FK para TB_DEVOLUCAO — devolução futura quando gerada em separado. |
| `DEV_GUID` | VARCHAR(50) | Sim | GUID para integração. |
| `DEV_ID_SERVIDOR` | INTEGER | Sim | FK para TB_SERVIDOR — servidor de origem da integração. |
| `DEV_ID_LOCAL` | INTEGER | Sim | FK para TB_LOCAL — local/loja de origem. |
| `DEV_DT_ENVIO_DEVOLUCAO_XRM` | TIMESTAMP | Sim | Data/hora de envio da devolução para o XRM. |
| `DEV_DT_ENVIO_CANCELAMENTO_XRM` | TIMESTAMP | Sim | Data/hora de envio do cancelamento para o XRM. |

COMMENT ON COLUMN TB_DEVOLUCAO.DEV_STATUS IS 'A - ATIVO
C - CANCELADO';
COMMENT ON COLUMN TB_DEVOLUCAO.DEV_GERAR_CREDITO IS 'S - SIM
N - NAO';
COMMENT ON COLUMN TB_DEVOLUCAO.DEV_PLANO_CONTAS IS 'Conta que vem do motivo da devolução';
COMMENT ON COLUMN TB_DEVOLUCAO.DEV_CONTA_CREDITO IS 'Conta de crédito do cliente';
COMMENT ON COLUMN TB_DEVOLUCAO.DEV_CONTA_CUSTO IS 'Conta de custo debitada no momento em que a mercadoria saiu. Deve ser creditada quando a mercadoria voltar.';
COMMENT ON COLUMN TB_DEVOLUCAO.DEV_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

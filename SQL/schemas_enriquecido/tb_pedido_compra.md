# Tabela TB_PEDIDO_COMPRA

**Módulo:** Compras
Pedidos de compra de mercadorias/produtos a fornecedores. Pode ser gerado a partir de uma cotação e gerar nota fiscal de entrada e financeiro a pagar.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PDC_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PDC_ID` | INTEGER | Não | Identificador único do pedido de compra. Parte da chave primária composta. |
| `PDC_STATUS` | VARCHAR(1) | Sim | Status: A=Aberto, E=Enviado, P=Parcialmente Recebido, R=Recebido, C=Cancelado. |
| `PDC_NATUREZA_OPERACAO` | INTEGER | Sim | FK para TB_NATUREZA_OPERACAO.NOP_ID. |
| `PDC_DT_EMISSAO` | DATE | Sim | Data de emissão do pedido. |
| `PDC_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro. |
| `PDC_FORNECEDOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (fornecedor). |
| `PDC_USUARIO` | INTEGER | Sim | Identificador do usuário que lançou o pedido. |
| `PDC_VALOR_PEDIDO` | NUMERIC(15,2) | Sim | Valor total do pedido. |
| `PDC_VALOR_RECEBIDO` | NUMERIC(15,2) | Sim | Valor já recebido/baixado do pedido. |
| `PDC_DT_ENVIO` | DATE | Sim | Data em que o pedido foi enviado ao destinatário. |
| `PDC_DT_RECEBIMENTO` | DATE | Sim | Última data de recebimento do pedido. |
| `PDC_ENVIADO_EMAIL` | VARCHAR(1) | Sim | Indica se o pedido foi enviado por e-mail (S/N). |
| `PDC_TIPO_FRETE` | VARCHAR(3) | Sim | Tipo de frete do pedido. |
| `PDC_RESPONSAVEL_PEDIDO` | VARCHAR(50) | Sim | Nome do responsável pelo pedido. |
| `PDC_OBSERVACAO` | VARCHAR(2000) | Sim | Observações do pedido. |
| `PDC_DT_ENTREGA` | DATE | Sim | Data prevista de entrega. |
| `PDC_VALOR_DESCONTO` | NUMERIC(15,2) | Sim | Valor total de desconto. |
| `PDC_VALOR_FRETE` | NUMERIC(15,2) | Sim | Valor do frete. |
| `PDC_VALOR_DESPESAS` | NUMERIC(15,2) | Sim | Valor de despesas acessórias. |
| `PDC_VALOR_IPI` | NUMERIC(15,2) | Sim | Valor do IPI. |
| `PDC_NOTA_FISCAL` | INTEGER | Sim | FK para TB_NOTA_FISCAL.NF_ID — NF que originou/recebeu o pedido. |
| `PDC_NUMERO_NOTA` | INTEGER | Sim | Número da NF vinculada. |
| `PDC_PEDIDO_FORN` | VARCHAR(20) | Sim | Número do pedido no fornecedor. |
| `PDC_GERA_FINANCEIRO` | VARCHAR(1) | Sim | Indica se gera financeiro (contas a pagar) (S/N). |
| `PDC_CUSTO_ADICIONAL` | NUMERIC(15,2) | Sim | Custo adicional lançado. |
| `PDC_CUSTO_TOTAL` | NUMERIC(15,2) | Sim | Custo total do pedido. |
| `PDC_CONTA_DEBITO` | INTEGER | Sim | Conta contábil de débito. |
| `PDC_CONTA_CREDITO` | INTEGER | Sim | Conta contábil de crédito. |
| `PDC_CARGA` | INTEGER | Sim | FK para carga vinculada. |
| `PDC_CARGA_ORDEM` | INTEGER | Sim | Ordem dentro da carga. |
| `PDC_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção (S/N). |
| `PDC_PESO_BRUTO` | NUMERIC(15,2) | Sim | Peso bruto total (kg). |
| `PDC_PESO_LIQUIDO` | NUMERIC(15,2) | Sim | Peso líquido total (kg). |
| `PDC_METRAGEM_CUBICA` | NUMERIC(15,2) | Sim | Metragem cúbica total. |
| `PDC_VOLUME` | INTEGER | Sim | Quantidade de volumes. |
| `PDC_ATUALIZAR_CUSTO` | VARCHAR(1) | Sim | Indica se atualiza custo dos produtos ao receber (S/N). |
| `PDC_TIPO_PRECO` | VARCHAR(1) | Sim | Tipo de preço usado. |
| `PDC_LOTE_PRODUCAO` | INTEGER | Sim | FK para lote de produção. |
| `PDC_DESMEMBRAR` | VARCHAR(1) | Sim | Indica se desmembra o pedido em recebimentos parciais (S/N). |
| `PDC_CAMINHO_JSON` | VARCHAR(255) | Sim | Caminho do JSON de integração. |
| `PDC_LOCAL_ESTOQUE` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE.LOC_ID de destino. |
| `PDC_COTACAO` | INTEGER | Sim | FK para a cotação que originou o pedido. |
| `PDC_MOVIMENTA_ESTOQUE` | VARCHAR(1) | Sim | Indica se movimenta estoque ao receber (S/N). |
| `PDC_ORIGEM` | VARCHAR(20) | Sim | Sigla da rotina de origem. |
| `PDC_VENDEDOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (vendedor/comprador). |
| `PDC_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem. |

COMMENT ON COLUMN TB_PEDIDO_COMPRA.PDC_STATUS IS 'A - ABERTO
E - ENVIADO
P - PARCIALMENTE RECEBIDO
R - RECEBIDO
C - CANCELADO';
COMMENT ON COLUMN TB_PEDIDO_COMPRA.PDC_DT_ENVIO IS 'Data que pedido foi enviado ao destinatário';
COMMENT ON COLUMN TB_PEDIDO_COMPRA.PDC_DT_RECEBIMENTO IS 'Última data de recebimento';
COMMENT ON COLUMN TB_PEDIDO_COMPRA.PDC_ENVIADO_EMAIL IS 'S - Sim
N - Não';
COMMENT ON COLUMN TB_PEDIDO_COMPRA.PDC_FORNECEDOR IS 'FK para TB_PESSOA.PES_ID — use JOIN com TB_PESSOA por PES_ID (e filtre PES_FORNECEDOR = ''S'' se quiser somente fornecedores)';

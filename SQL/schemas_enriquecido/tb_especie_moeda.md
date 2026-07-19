# Tabela TB_ESPECIE_MOEDA

**Módulo:** Financeiro
Espécies de pagamento, muito chamado pelos usuários como Tipo de Pagamento, Tipo de Documento, muito utilizado para fazer joins com tabelas financeiras, normalmente a nomenclatura em outras tabelas é: _especie_moeda (dinheiro, cartão, cheque, PIX, boleto, etc.). Define uso por módulo (recebimentos, pagamentos, PDV, pedidos), parcelamento, comportamento no caixa, integração com administradora de cartão e configurações específicas (acréscimo/desconto, TEF, PSP, iFood).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `ESP_ID` | INTEGER | Não | Identificador único da espécie de moeda. |
| `ESP_SIGLA` | VARCHAR(3) | Sim | Sigla da espécie de moeda (ex.: DIN, CAR, PIX, CHQ). |
| `ESP_DESCRICAO` | VARCHAR(50) | Sim | Descrição da espécie de moeda. |
| `ESP_STATUS` | VARCHAR(1) | Sim | Status da espécie (A = Ativo, I = Inativo). |
| `ESP_MOVIMENTAR` | VARCHAR(2) | Sim | Tipo de movimentação financeira gerada: TD = Tipo Documento, CX = Movimentar Conta Caixa, CB = Movimentar Conta Bancária, CH = Lançar Cheque Recebido, CE = Lançar Cheque Emitido, CC = Lançar Parcelas Cartão Crédito, CR = Crédito. |
| `ESP_LOCAL_UTILIZAR` | VARCHAR(2) | Sim | Local onde a espécie pode ser utilizada: RC = Recebimentos, PG = Pagamentos, TD = Todos. |
| `ESP_USAR_REC` | VARCHAR(1) | Sim | Indica se a espécie é usada em recebimentos (S/N). |
| `ESP_USAR_PAG` | VARCHAR(1) | Sim | Indica se a espécie é usada em pagamentos (S/N). |
| `ESP_USAR_PDV` | VARCHAR(1) | Sim | Indica se a espécie é usada no PDV (S/N). |
| `ESP_USAR_PEDIDO` | VARCHAR(1) | Sim | Indica se a espécie é usada em pedidos (S/N). |
| `ESP_FORMA_PAG_NF` | INTEGER | Sim | Código da forma de pagamento na NF-e: 01=Dinheiro; 02=Cheque; 03=Cartão de Crédito; 04=Cartão de Débito; 05=Crédito Loja; 10=Vale Alimentação; 11=Vale Refeição; 12=Vale Presente; 13=Vale Combustível; 14=Duplicata Mercantil; 15=Boleto Bancário; 90=Sem pagamento; 99=Outros. |
| `ESP_TECLA_PDV` | VARCHAR(10) | Sim | Tecla de atalho da espécie no PDV. |
| `ESP_SEQUENCIA` | INTEGER | Sim | Sequência de exibição da espécie. |
| `ESP_PLANO_CONTAS` | INTEGER | Sim | Identificador do plano de contas contábil associado. |
| `ESP_ACEITAR_TROCO` | VARCHAR(1) | Sim | Indica se aceita troco (S/N). |
| `ESP_UTILIZAR_TROCO` | VARCHAR(1) | Sim | Indica se utiliza troco (S/N). |
| `ESP_ADM_CARTAO` | INTEGER | Sim | Identificador da administradora de cartão (TB_PESSOA.PES_ID). |
| `ESP_PARCELAR` | VARCHAR(1) | Sim | Indica se a espécie permite parcelamento (S/N). |
| `ESP_DIAS` | INTEGER | Sim | Intervalo de dias entre parcelas. |
| `ESP_NR_PARCELAS` | INTEGER | Sim | Número máximo de parcelas. |
| `ESP_SEM_BX_ADM` | VARCHAR(1) | Sim | Indica se a espécie não passa pela baixa administrativa do cartão (S/N). |
| `ESP_AJUSTE` | NUMERIC(15,2) | Sim | Valor de ajuste manual padrão da espécie. |
| `ESP_CONTA` | INTEGER | Sim | Identificador da conta (TB_CONTA.CNT_ID) padrão para a espécie. |
| `ESP_USAR_LOJA` | VARCHAR(1) | Sim | Indica se a espécie pode ser usada em outras lojas (S/N). |
| `ESP_TEF` | VARCHAR(1) | Sim | Indica se a espécie trabalha com TEF (S/N). |
| `ESP_DIA_VENCIMENTO` | INTEGER | Sim | Dia de vencimento padrão para títulos desta espécie. |
| `ESP_DOC_CARTAO` | VARCHAR(1) | Sim | Indica se gera documento de cartão (S/N). |
| `ESP_TABELA_PRECO` | INTEGER | Sim | Identificador da tabela de preço padrão vinculada. |
| `ESP_TIPO_IFOOD` | BLOB SUB_TYPE TEXT | Sim | Tipo do pagamento no iFood em formato texto. NUNCA selecione em queries SELECT. |
| `ESP_METODO_IFOOD` | BLOB SUB_TYPE TEXT | Sim | Método de pagamento no iFood em formato texto. NUNCA selecione em queries SELECT. |
| `ESP_IND_PAG` | INTEGER | Sim | Indicador de pagamento da NF-e (1=À vista, 2=A prazo, etc.). |
| `ESP_PIX_PSP` | VARCHAR(1) | Sim | Indica se o PIX é via PSP (S/N). |
| `ESP_VALOR_MINIMO` | NUMERIC(15,2) | Sim | Valor mínimo permitido para a espécie. |
| `ESP_VALOR_MAXIMO` | NUMERIC(15,2) | Sim | Valor máximo permitido para a espécie. |
| `ESP_PSP` | INTEGER | Sim | Identificador do PSP (provedor de pagamento). |
| `ESP_PAG_ELETRONICO` | VARCHAR(1) | Sim | Indica se é pagamento eletrônico (S/N). |
| `ESP_INTEGRACAO_APP` | VARCHAR(20) | Sim | Código da espécie na integração com o app. |
| `ESP_USAR_AUTO_ATENDIMENTO` | VARCHAR(1) | Sim | Indica se a espécie está disponível no auto-atendimento (S/N). |
| `ESP_DEBITO_PRE_DATADO` | VARCHAR(1) | Sim | Indica se aceita débito pré-datado (S/N). |
| `ESP_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `ESP_SECRET_KEY` | VARCHAR(100) | Sim | Chave secreta da integração (Stone/Pagar.me). |
| `ESP_SERIAL_STONE` | VARCHAR(50) | Sim | Serial do terminal Stone. |
| `ESP_PROD_PAG_ELETRONICO` | INTEGER | Sim | Identificador do produto de pagamento eletrônico (vinculado em TB_PRODUTO). |
| `ESP_LIMPAR_PROMOCAO` | VARCHAR(1) | Sim | Indica se a espécie limpa promoções aplicadas (S/N). |
| `ESP_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. |
| `ESP_MOSTRAR_FECH_CEGAS` | VARCHAR(1) | Sim | Indica se mostra a espécie no fechamento cego (S/N). |
| `ESP_ACRES_DESC` | VARCHAR(1) | Sim | Indica se a espécie aplica acréscimo/desconto (S/N). |
| `ESP_TIPO_ACRES_DESC` | VARCHAR(1) | Sim | Tipo do acréscimo/desconto (V = Valor, P = Percentual). |
| `ESP_VALOR_ACRES_DESC` | NUMERIC(15,2) | Sim | Valor/percentual de acréscimo/desconto. |
| `ESP_ALTERAR_ACRES_DESC` | VARCHAR(1) | Sim | Permite alterar acréscimo/desconto no lançamento (S/N). |
| `ESP_TIPO_DESPESA` | VARCHAR(1) | Sim | Tipo da despesa associada à espécie. |
| `ESP_VALOR_DESPESA` | NUMERIC(15,2) | Sim | Valor da despesa. |
| `ESP_ARQUIVO_IMPRESSAO` | VARCHAR(20) | Sim | Arquivo de impressão do comprovante. |
| `ESP_IMPRESSORA` | INTEGER | Sim | Identificador da impressora de comprovantes. |
| `ESP_PREVIEW` | VARCHAR(1) | Sim | Indica se mostra preview do comprovante (S/N). |
| `ESP_DIALOG` | VARCHAR(1) | Sim | Indica se exibe caixa de diálogo específica (S/N). |
| `ESP_USU_NAO_FINALIZA` | VARCHAR(1) | Sim | Indica se usuários sem permissão não podem finalizar com esta espécie (S/N). |

COMMENT ON COLUMN TB_ESPECIE_MOEDA.ESP_MOVIMENTAR IS 'TD - Tipo Documento
CX - Movimentar Conta Caixa
CB - Movimentar Conta Bancária
CH - Lançar Cheque Recebido
CE - Lançar Cheque Emitido
CC - Lançar Parcelas Cartão Crédito
CR - Crédito';
COMMENT ON COLUMN TB_ESPECIE_MOEDA.ESP_LOCAL_UTILIZAR IS 'RC - Recebimentos
PG - Pagamentos
TD - Todos';
COMMENT ON COLUMN TB_ESPECIE_MOEDA.ESP_FORMA_PAG_NF IS '01=Dinheiro
    02=Cheque
    03=Cartão de Crédito
    04=Cartão de Débito
    05=Crédito Loja
    10=Vale Alimentação
    11=Vale Refeição
    12=Vale Presente
    13=Vale Combustível
    14=Duplicata Mercantil
    15=Boleto Bancário
    90= Sem pagamento
    99=Outros';
COMMENT ON COLUMN TB_ESPECIE_MOEDA.ESP_TIPO_IFOOD IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_ESPECIE_MOEDA.ESP_METODO_IFOOD IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
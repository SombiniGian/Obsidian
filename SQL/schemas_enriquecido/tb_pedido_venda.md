# Tabela TB_PEDIDO_VENDA

**Módulo:** Vendas
Cabeçalho do pedido de venda (PDV): dados do cliente, vendedor, valores totais, frete, descontos, acréscimos, comissão, status, entrega, faturamento, delivery e integrações (iFood, Tray, Stone). Os itens vivem em TB_PEDIDO_VENDA_ITEM e as formas de pagamento em TB_PEDIDO_VENDA_FIN.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PEV_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PEV_ID` | INTEGER | Não | Identificador único do pedido de venda. Parte da chave primária composta. |
| `PEV_DT_EMISSAO` | DATE | Sim | Data de emissão do pedido. |
| `PEV_CLIENTE` | INTEGER | Sim | Identificador do cliente (TB_PESSOA.PES_ID). |
| `PEV_VENDEDOR` | INTEGER | Sim | Identificador do vendedor (TB_PESSOA.PES_ID). |
| `PEV_OBSERVACAO` | VARCHAR(2000) | Sim | Observações gerais do pedido. |
| `PEV_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do pedido no sistema. |
| `PEV_USUARIO` | INTEGER | Sim | Identificador do usuário que lançou o pedido. |
| `PEV_SUB_TOTAL` | NUMERIC(15,2) | Sim | Subtotal do pedido (soma dos itens antes de descontos e acréscimos). |
| `PEV_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total final do pedido. |
| `PEV_VALOR_DESCONTO` | NUMERIC(15,2) | Sim | Valor total de desconto aplicado ao pedido. |
| `PEV_VALOR_ACRESCIMO` | NUMERIC(15,2) | Sim | Valor total de acréscimo aplicado ao pedido. |
| `PEV_STATUS` | VARCHAR(1) | Não | Status do pedido: A = Aberto, F = Faturado, C = Cancelado. |
| `PEV_FORMA_PAGAMENTO` | INTEGER | Sim | Identificador da forma de pagamento padrão (TB_ESPECIE_MOEDA.ESP_ID). |
| `PEV_QTDE_ITENS` | INTEGER | Sim | Quantidade de itens do pedido. |
| `PEV_VALOR_COMISSAO` | NUMERIC(15,2) | Sim | Valor total de comissão do pedido. |
| `PEV_COD_PED_CLIENTE` | VARCHAR(20) | Sim | Código do pedido informado pelo cliente. |
| `PEV_COD_PED_VENDEDOR` | VARCHAR(20) | Sim | Código do pedido informado pelo vendedor. |
| `PEV_DT_FATURAMENTO` | DATE | Sim | Data de faturamento do pedido. |
| `PEV_DT_ENTREGA` | DATE | Sim | Data prevista/realizada de entrega. |
| `PEV_AJUSTE` | NUMERIC(15,2) | Sim | Valor de ajuste manual no pedido. |
| `PEV_COMISSAO` | NUMERIC(15,2) | Sim | Comissão (%) do vendedor. |
| `PEV_TIPO_FRETE` | INTEGER | Sim | Tipo de frete: 0 = CIF, 1 = FOB, 2 = Terceiros, 9 = Sem Frete. |
| `PEV_TRANSPORTADOR` | INTEGER | Sim | Identificador do transportador (TB_PESSOA.PES_ID). |
| `PEV_VEICULO` | INTEGER | Sim | Identificador do veículo utilizado na entrega. |
| `PEV_MENSAGEM_ALERTA` | BLOB SUB_TYPE BINARY | Sim | Mensagens de alerta do pedido em formato binário. NUNCA selecione em queries SELECT. |
| `PEV_LIMITE_CREDITO` | NUMERIC(15,2) | Sim | Limite de crédito do cliente no momento do pedido. |
| `PEV_LIMITE_DISPONIVEL` | NUMERIC(15,2) | Sim | Limite de crédito disponível no momento do pedido. |
| `PEV_LIMITE_UTILIZADO` | NUMERIC(15,2) | Sim | Limite de crédito já utilizado. |
| `PEV_DT_SAIDA` | DATE | Sim | Data de saída dos itens do estoque. |
| `PEV_VOLUME` | INTEGER | Sim | Quantidade de volumes do pedido. |
| `PEV_TOTAL_NOTA` | NUMERIC(15,2) | Sim | Valor total da(s) nota(s) fiscal(is) emitida(s) para o pedido. |
| `PEV_NOTA_FISCAL` | INTEGER | Sim | Identificador da nota fiscal principal do pedido. |
| `PEV_RECEPCAO_PEDIDO` | INTEGER | Sim | Identificador da recepção do pedido (expedição). |
| `PEV_VALOR_RECEBER_AVISTA` | NUMERIC(15,2) | Sim | Valor a receber à vista. |
| `PEV_VALOR_RECEBER_APRAZO` | NUMERIC(15,2) | Sim | Valor a receber a prazo. |
| `PEV_VALOR_RECEBIDO_CHEQUE` | NUMERIC(15,2) | Sim | Valor recebido em cheque. |
| `PEV_VALOR_TOTAL_RECEBIDO` | NUMERIC(15,2) | Sim | Valor total recebido do pedido. |
| `PEV_NATUREZA_OPERACAO` | INTEGER | Sim | Identificador da natureza de operação (CFOP). |
| `PEV_VALOR_IMPOSTO` | NUMERIC(15,2) | Sim | Valor total de impostos do pedido. |
| `PEV_TABELA_PRECO` | INTEGER | Sim | Identificador da tabela de preço aplicada ao pedido. |
| `PEV_PESO_LIQUIDO` | NUMERIC(15,3) | Sim | Peso líquido total do pedido. |
| `PEV_PESO_BRUTO` | NUMERIC(15,3) | Sim | Peso bruto total do pedido. |
| `PEV_METRAGEM_CUBICA` | NUMERIC(15,4) | Sim | Metragem cúbica total do pedido. |
| `PEV_ACRESC_DESC_NF` | VARCHAR(1) | Sim | Como enviar acréscimo/desconto para NF: N = Não envia; R = Envia apenas o que foi rateado; T = Envia total. |
| `PEV_TIPO_DESCONTO` | VARCHAR(1) | Sim | Tipo de desconto aplicado: V = Valor, P = Porcentagem, T = Total do Pedido. |
| `PEV_DESCONTO` | NUMERIC(15,2) | Sim | Valor/percentual de desconto aplicado. |
| `PEV_VALOR_DESC_RAT` | NUMERIC(15,2) | Sim | Valor de desconto já rateado para os itens. |
| `PEV_CONFERENTE` | INTEGER | Sim | Identificador do conferente do pedido. |
| `PEV_EMBALADOR` | INTEGER | Sim | Identificador do embalador. |
| `PEV_PEDIDO_TABLET` | INTEGER | Sim | Identificador do pedido originado em tablet/PDA. |
| `PEV_CARGA` | INTEGER | Sim | Identificador da carga de expedição. |
| `PEV_PLACA` | VARCHAR(8) | Sim | Placa do veículo de entrega. |
| `PEV_PLACA_UF` | VARCHAR(2) | Sim | UF da placa do veículo. |
| `PEV_DESTACAR_TRANSP` | VARCHAR(1) | Sim | Indica se destaca transportadora na impressão (S/N). |
| `PEV_CARGA_ORDEM` | INTEGER | Sim | Ordem do pedido dentro da carga. |
| `PEV_SELECIONADO` | VARCHAR(1) | Sim | Marcador de seleção do pedido (S/N). |
| `PEV_SEL_IMPRESSAO` | VARCHAR(1) | Sim | Marcador para selecionar pedido a ser separado para impressão. |
| `PEV_CAIXA` | INTEGER | Sim | Identificador do caixa (TB_CONTA.CNT_ID) no qual o pedido foi registrado. |
| `PEV_ORDEM_SERVICO` | INTEGER | Sim | Identificador da ordem de serviço relacionada. |
| `PEV_USUARIO_LIBERACAO` | INTEGER | Sim | Identificador do usuário que liberou o pedido (após senha de liberação). |
| `PEV_DT_LIBERACAO` | TIMESTAMP | Sim | Data e hora da liberação do pedido. |
| `PEV_SENHA_LIBERACAO` | INTEGER | Sim | Identificador da senha de liberação utilizada (TB_SENHA_LIBERACAO). |
| `PEV_DT_CANCELAMENTO` | DATE | Sim | Data de cancelamento do pedido. |
| `PEV_DESP_ACESSORIA` | NUMERIC(15,2) | Sim | Valor de despesa acessória do pedido. |
| `PEV_TIPO_ACRESCIMO` | VARCHAR(1) | Sim | Tipo do acréscimo: V = Valor, P = Percentual. |
| `PEV_ACRESCIMO` | NUMERIC(15,2) | Sim | Valor/percentual de acréscimo aplicado. |
| `PEV_VALOR_CUSTO_MEDIO` | NUMERIC(15,2) | Sim | Valor de custo médio do pedido. |
| `PEV_SALDO_FLEX` | NUMERIC(15,2) | Sim | Saldo Flex — diferença entre o valor que deveria ter sido vendido e o que realmente foi vendido (imposto pelo vendedor). |
| `PEV_RNTRC` | VARCHAR(20) | Sim | RNTRC do transportador. |
| `PEV_PRECO_VENDA_CUSTO` | VARCHAR(1) | Sim | Indica se o preço de venda veio do custo do produto (S/N). |
| `PEV_TIPO_FORMA_PAGTO` | VARCHAR(1) | Sim | Tipo da forma de pagamento (A = À vista, P = A prazo). |
| `PEV_FORMA_PAGTO_DESC_ACRES` | NUMERIC(15,2) | Sim | Percentual de desconto/acréscimo da forma de pagamento. |
| `PEV_VALOR_TOTAL_RECEBER` | NUMERIC(15,2) | Sim | Valor total a receber do pedido. |
| `PEV_VALOR_TOTAL_PARCELADO` | NUMERIC(15,2) | Sim | Valor total parcelado. |
| `PEV_VALOR_DIFERENCA` | NUMERIC(15,2) | Sim | Diferença entre valor total e valor recebido. |
| `PEV_TIPO_TABELA_PRECO` | VARCHAR(1) | Sim | Tipo da tabela de preço: D = Desconto, A = Acréscimo. |
| `PEV_TABELA_DESC_ACRES` | NUMERIC(15,2) | Sim | Percentual de desconto/acréscimo da tabela de preço. |
| `PEV_GERA_FINANCEIRO` | VARCHAR(1) | Sim | Indica se o pedido gera financeiro (S/N). |
| `PEV_TIPO_TELA` | VARCHAR(1) | Sim | Tipo da tela em que o pedido foi gerado (Mesa, Comanda, Delivery, Balcão). |
| `PEV_PLANO_CONTAS` | INTEGER | Sim | Identificador do plano de contas do pedido. |
| `PEV_CLASSIFICACAO` | INTEGER | Sim | Identificador da classificação do pedido. |
| `PEV_ALTERAR_VOLUME` | VARCHAR(1) | Sim | Permite alterar volume após o pedido (S/N). |
| `PEV_TRIBUTA_IPI` | VARCHAR(1) | Sim | Pedido tributa IPI (S/N). |
| `PEV_TRIBUTA_ICMS` | VARCHAR(1) | Sim | Pedido tributa ICMS (S/N). |
| `PEV_OBS_NOTA` | BLOB SUB_TYPE BINARY | Sim | Observações da nota fiscal em formato binário. NUNCA selecione em queries SELECT. |
| `PEV_REDESPACHO` | INTEGER | Sim | Identificador do transportador de redespacho. |
| `PEV_TIPO_FRETE_RED` | INTEGER | Sim | Tipo de frete do redespacho (0=CIF, 1=FOB, 2=Terceiros, 9=Sem Frete). |
| `PEV_ENDERECO_ENTREGA` | INTEGER | Sim | Identificador do endereço de entrega (TB_ENDERECO.END_ID). |
| `PEV_NR_PARCELAS` | INTEGER | Sim | Número de parcelas do pedido. |
| `PEV_IND_PRESENCA` | INTEGER | Sim | Indicador de presença da NF-e: 0=Não se aplica; 1=Operação presencial; 2=Não presencial, Internet; 3=Não presencial, Teleatendimento; 4=NFC-e em operação com entrega a domicílio; 5=Operação presencial fora do estabelecimento; 9=Não presencial, outros. |
| `PEV_EMAIL_NF` | VARCHAR(1000) | Sim | E-mail(s) para envio da NF-e. |
| `PEV_MOV_ESTOQUE` | VARCHAR(1) | Sim | Indica se o pedido movimenta estoque (S/N). |
| `PEV_SUPERVISOR` | INTEGER | Sim | Identificador do supervisor do vendedor. |
| `PEV_COMISSAO_SUPERVISOR` | NUMERIC(15,2) | Sim | Percentual de comissão do supervisor. |
| `PEV_VALOR_COMISSAO_SUPERVISOR` | NUMERIC(15,2) | Sim | Valor calculado da comissão do supervisor. |
| `PEV_PEDIDOS_CLIENTE` | VARCHAR(200) | Sim | Lista consolidada de pedidos do cliente. |
| `PEV_PEDIDOS_VENDEDOR` | VARCHAR(200) | Sim | Lista consolidada de pedidos do vendedor. |
| `PEV_PEDIDO_UNIFICADO` | INTEGER | Sim | Identificador do pedido unificado (quando vários pedidos foram unificados). |
| `PEV_TIPO_TROCO` | VARCHAR(1) | Sim | Destino do troco: T = Lançou Troco, C = Lançou Crédito, D = Descartou. |
| `PEV_SUBST_NF` | VARCHAR(1) | Sim | Indica se o pedido substituirá NF (S/N). |
| `PEV_FECHAMENTO` | INTEGER | Sim | Identificador do fechamento de caixa. |
| `PEV_LOTE_PRODUCAO` | INTEGER | Sim | Identificador do lote de produção. |
| `PEV_GERAR_OP` | VARCHAR(1) | Sim | Indica se gera ordem de produção (S/N). |
| `PEV_VALOR_DESCARTE` | NUMERIC(15,2) | Sim | Valor de descarte do pedido. |
| `PEV_NOME` | VARCHAR(100) | Sim | Nome do cliente não registrado (quando aplicável). |
| `PEV_CPF_CNPJ` | VARCHAR(14) | Sim | CPF/CNPJ do cliente não registrado (somente números). |
| `PEV_CLIENTE_NAO_REG` | VARCHAR(1) | Sim | Indica se o cliente não está registrado (S = Sim). |
| `PEV_MESA` | INTEGER | Sim | Identificador da mesa (TB_MESA.MSA_ID) quando o pedido é de mesa. |
| `PEV_COMANDA` | VARCHAR(30) | Sim | Número da comanda. |
| `PEV_DT_HR_ATEDIMENTO` | TIMESTAMP | Sim | Data e hora de início do atendimento. |
| `PEV_DELIVERY` | VARCHAR(1) | Sim | Indica se o pedido é delivery (S = Sim, N = Não). |
| `PEV_STATUS_DELIVERY` | VARCHAR(1) | Sim | Status do delivery: A = Aberto, P = Pronto para entrega, E = Entregando, F = Entrega Finalizada, C = Cancelado. |
| `PEV_TIPO_ENTREGA` | VARCHAR(1) | Sim | Tipo da entrega: E = Entregar, B = Cliente Buscar. |
| `PEV_DT_HR_PRONTO` | TIMESTAMP | Sim | Data e hora em que o pedido ficou pronto. |
| `PEV_DT_HR_ENTREGA` | TIMESTAMP | Sim | Data e hora de saída para entrega. |
| `PEV_DT_HR_ENTREGUE` | TIMESTAMP | Sim | Data e hora em que o pedido foi entregue ao cliente. |
| `PEV_DT_HR_FINALIZADO` | TIMESTAMP | Sim | Data e hora de finalização do pedido. |
| `PEV_AGUARDANDO` | VARCHAR(1) | Sim | Indica que o cliente está aguardando e o produto está pronto (S/N). |
| `PEV_VENDEDOR_ATIVO` | INTEGER | Sim | Identificador do vendedor ativo (sessão) no momento do pedido. |
| `PEV_VALOR_COMPL_ADD` | NUMERIC(15,2) | Sim | Valor de complementos adicionados no pedido. |
| `PEV_VALOR_COMPL_RET` | NUMERIC(15,2) | Sim | Valor de complementos retirados no pedido. |
| `PEV_COMPRADOR` | INTEGER | Sim | Identificador do comprador (TB_PESSOA.PES_ID). |
| `PEV_MOTIVO_CANCELAMENTO` | INTEGER | Sim | Identificador do motivo de cancelamento. |
| `PEV_DESCRICAO_CANCELAMENTO` | VARCHAR(100) | Sim | Descrição do motivo de cancelamento. |
| `PEV_VENDER_CREDITO` | VARCHAR(1) | Sim | Indica se o pedido vende crédito do cliente (S/N). |
| `PEV_VALOR_TX_SERV` | NUMERIC(15,2) | Sim | Valor da taxa de serviço do pedido. |
| `PEV_TIPO_VALOR_SERV` | VARCHAR(1) | Sim | Tipo do valor da taxa de serviço (V = Valor, P = Percentual). |
| `PEV_TOTAL_TX_SERV` | NUMERIC(15,2) | Sim | Total da taxa de serviço cobrada. |
| `PEV_DESPESAS_FRETE` | NUMERIC(15,2) | Sim | Despesas adicionais de frete. |
| `PEV_VALOR_DESP_FRETE` | NUMERIC(15,2) | Sim | Valor total das despesas de frete. |
| `PEV_BORDERO_COMISSAO` | INTEGER | Sim | Identificador do borderô de comissão. |
| `PEV_CAMINHO_JSON` | VARCHAR(255) | Sim | Caminho do JSON gerado para integrações. |
| `PEV_FORMA_PAGTO_APP` | INTEGER | Sim | Identificador da forma de pagamento no app (delivery). |
| `PEV_TROCO_APP` | NUMERIC(15,2) | Sim | Valor do troco informado no app. |
| `PEV_TIPO_PAGTO_APP` | VARCHAR(2) | Sim | Tipo de pagamento no app (DP, CR, JR etc.). |
| `PEV_ENDERECO_APP` | VARCHAR(2000) | Sim | Endereço de entrega informado no app. |
| `PEV_CONSIGNADO` | INTEGER | Sim | Identificador do pedido consignado de origem. |
| `PEV_TIPO_CANCELAMENTO` | VARCHAR(1) | Sim | Tipo de cancelamento do pedido. |
| `PEV_NUMERACAO` | VARCHAR(60) | Sim | Numeração dos volumes. |
| `PEV_ESPECIE` | VARCHAR(60) | Sim | Espécie dos volumes. |
| `PEV_MARCA` | VARCHAR(60) | Sim | Marca dos volumes. |
| `PEV_LOCAL_ESTOQUE` | INTEGER | Sim | Local de estoque de onde o pedido foi baixado. |
| `PEV_HOSPEDAGEM` | INTEGER | Sim | Identificador da hospedagem (quando venda para hotel). |
| `PEV_QTDE_PESSOAS` | INTEGER | Sim | Quantidade de pessoas (venda para hotel/restaurante). |
| `PEV_VALOR_PESSOA` | NUMERIC(15,2) | Sim | Valor por pessoa. |
| `PEV_DURACAO_PEDIDO` | INTEGER | Sim | Duração do pedido em minutos. |
| `PEV_TURNO` | INTEGER | Sim | Identificador do turno. |
| `PEV_VALOR_MAXIMO` | NUMERIC(15,2) | Sim | Valor máximo permitido no pedido. |
| `PEV_MAX_ITENS` | INTEGER | Sim | Quantidade máxima de itens no pedido. |
| `PEV_TIPO_BLOQUEIO` | VARCHAR(1) | Sim | Tipo de bloqueio aplicado ao pedido. |
| `PEV_BALCAO` | VARCHAR(1) | Sim | Indica se é venda de balcão (S/N). |
| `PEV_ABERTO` | VARCHAR(1) | Sim | Indica se o pedido está em aberto (S/N). |
| `PEV_IFOOD` | VARCHAR(1) | Sim | Indica se o pedido veio do iFood (S/N). |
| `PEV_EMP_TRANSF` | INTEGER | Sim | Empresa de origem da transferência entre lojas. |
| `PEV_ID_EMP_TRANSF` | INTEGER | Sim | Identificador do pedido na empresa de origem. |
| `PEV_ALTERAR_TABELA` | VARCHAR(1) | Sim | Permite alterar tabela de preço no pedido (S/N). |
| `PEV_VALOR_IPI` | NUMERIC(15,2) | Sim | Valor de IPI do pedido. |
| `PEV_VALOR_ST` | NUMERIC(15,2) | Sim | Valor de substituição tributária do pedido. |
| `PEV_TIPO_COVER` | VARCHAR(1) | Sim | Tipo do cover (couvert). |
| `PEV_VALOR_COVER` | NUMERIC(15,2) | Sim | Valor do cover por pessoa. |
| `PEV_TOTAL_COVER` | NUMERIC(15,2) | Sim | Total de cover do pedido. |
| `PEV_INGRESSO` | INTEGER | Sim | Identificador do ingresso (venda de ingressos). |
| `PEV_CALCULAR_IMPOSTO` | VARCHAR(1) | Sim | Indica se calcula imposto no pedido (S/N). |
| `PEV_VALOR_PEDIDO` | NUMERIC(15,2) | Sim | Valor do pedido (cálculo geral). |
| `PEV_PEDIDO_ENTREGA` | INTEGER | Sim | Identificador do pedido de entrega (delivery). |
| `PEV_STATUS_ENTREGA` | VARCHAR(1) | Sim | Status da entrega do delivery. |
| `PEV_DT_BASE_FIN` | DATE | Sim | Data base financeira do pedido. |
| `PEV_ENTREGA_FUTURA` | VARCHAR(1) | Sim | Indica se é entrega futura (S/N). |
| `PEV_HR_ENTREGA` | TIME | Sim | Horário previsto de entrega. |
| `PEV_TABELA_NF` | INTEGER | Sim | Identificador da tabela de preço aplicada na NF. |
| `PEV_INGRESSO_COMANDA` | VARCHAR(1) | Sim | Indica se a comanda é de ingresso (S/N). |
| `PEV_LATITUDE` | NUMERIC(10,8) | Sim | Latitude do endereço de entrega. |
| `PEV_LONGITUDE` | NUMERIC(10,8) | Sim | Longitude do endereço de entrega. |
| `PEV_LOCALIZACAO` | VARCHAR(500) | Sim | Localização textual (delivery). |
| `PEV_ICMS_DESON_TOTAL` | VARCHAR(1) | Sim | Indica se aplica desoneração total de ICMS no pedido (S/N). |
| `PEV_VALOR_ICMS_DESON` | NUMERIC(15,2) | Sim | Valor de ICMS desonerado. |
| `PEV_FOTO_CLIENTE` | INTEGER | Sim | Identificador da foto do cliente. |
| `PEV_TIPO_PAGTO_CAIXA` | INTEGER | Sim | Tipo de pagamento definido no caixa. |
| `PEV_PEDIDO_VINCULADO` | INTEGER | Sim | Identificador do pedido vinculado (mesa, por exemplo). |
| `PEV_GUID` | VARCHAR(50) | Sim | GUID para integração. |
| `PEV_DT_VENCIMENTO_ORCAMENTO` | DATE | Sim | Data de vencimento do orçamento. |
| `PEV_DESC_COND` | NUMERIC(15,2) | Sim | Desconto da condição de pagamento. |
| `PEV_LIMITE_DESC_COND` | NUMERIC(15,2) | Sim | Limite do desconto da condição. |
| `PEV_BASE_DESC_COND` | NUMERIC(15,2) | Sim | Base de cálculo do desconto da condição. |
| `PEV_TIPO_DESC_COND` | VARCHAR(1) | Sim | Tipo do desconto da condição. |
| `PEV_VALOR_DESC_COND` | NUMERIC(15,2) | Sim | Valor final do desconto da condição. |
| `PEV_MOTIVO_DESCONTO` | INTEGER | Sim | Identificador do motivo do desconto. |
| `PEV_MOTIVO_DESCONTO_DESCRICAO` | VARCHAR(100) | Sim | Descrição do motivo do desconto. |
| `PEV_NUMERO_DAV` | INTEGER | Sim | Número do DAV (Documento Auxiliar de Venda). |
| `PEV_DAV` | VARCHAR(1) | Sim | Indica se é um DAV (S/N). |
| `PEV_NUMERO_RE` | INTEGER | Sim | Número do RE (Registro de Entrada/Saída). |
| `PEV_TRAY_ID_PEDIDO` | VARCHAR(100) | Sim | ID do pedido na Tray. |
| `PEV_TRAY_PRONTO` | TIMESTAMP | Sim | Data e hora em que o pedido ficou pronto (Tray). |
| `PEV_TRAY_ENVIADO` | TIMESTAMP | Sim | Data e hora de envio do pedido (Tray). |
| `PEV_TRAY_ENTREGUE` | TIMESTAMP | Sim | Data e hora de entrega do pedido (Tray). |
| `PEV_TRAY_FINALIZADO` | TIMESTAMP | Sim | Data e hora de finalização do pedido (Tray). |
| `PEV_VALOR_RETENCAO_TRIB` | NUMERIC(15,2) | Sim | Valor de retenção tributária. |
| `PEV_IPI_INTEGRA_BC_ICMS` | VARCHAR(1) | Sim | Indica se o IPI integra a base de cálculo do ICMS (S/N). |
| `PEV_ID_SERVIDOR` | INTEGER | Sim | Identificador do servidor de origem. |
| `PEV_ID_LOCAL` | INTEGER | Sim | Identificador do local/loja de origem. |
| `PEV_ESTACAO_PDV` | INTEGER | Sim | Estação PDV de origem. |
| `PEV_TOTAL_CASHBACK` | NUMERIC(15,2) | Sim | Valor total de cashback gerado. |
| `PEV_GERA_CASHBACK` | VARCHAR(1) | Sim | Indica se gera cashback (S/N). |
| `PEV_TELEFONE` | VARCHAR(20) | Sim | Telefone do cliente (delivery). |
| `PEV_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. Default: current_timestamp. |
| `PEV_GUID_DESMEMBRADO` | VARCHAR(50) | Sim | GUID do pedido original quando houve desmembramento. |
| `PEV_TIPO_DESMEMBRAMENTO` | VARCHAR(1) | Sim | Tipo de desmembramento aplicado. |
| `PEV_GUID_CLIENTE` | VARCHAR(50) | Sim | GUID do cliente (delivery/app). |
| `PEV_ENVIO_SCANTECH` | INTEGER | Sim | Identificador do envio Scantech. |
| `PEV_ENVIO_CANC_SCANTECH` | INTEGER | Sim | Identificador do envio de cancelamento Scantech. |
| `PEV_STATUS_SCANTECH` | VARCHAR(1) | Sim | Status da integração Scantech. |
| `PEV_ERRO_SCANTECH` | BLOB SUB_TYPE TEXT | Sim | Mensagem de erro da Scantech em formato texto. NUNCA selecione em queries SELECT. |
| `PEV_DT_HR_FATURAMENTO` | TIMESTAMP | Sim | Data e hora do faturamento. |
| `PEV_VALOR_PROMOCAO` | NUMERIC(15,2) | Sim | Valor de promoção aplicado ao pedido. |
| `PEV_ORIGEM_DELIVERY` | VARCHAR(50) | Sim | Origem do pedido delivery (app, site, iFood etc.). |
| `PEV_TRAY_CANCELADO` | TIMESTAMP | Sim | Data e hora de cancelamento na Tray. |
| `PEV_TRAY_LOJA` | VARCHAR(50) | Sim | Identificador da loja na Tray. |
| `PEV_DT_ENVIO_VENDA_XRM` | TIMESTAMP | Sim | Data de envio da venda ao XRM. |
| `PEV_DT_ENVIO_CANCELAMENTO_XRM` | TIMESTAMP | Sim | Data de envio do cancelamento ao XRM. |
| `PEV_NAO_APLICAR_PROMOCAO` | VARCHAR(1) | Sim | Indica se não aplica promoção no pedido (S/N). |
| `PEV_AGRUPAR_RECEBIMENTOS` | VARCHAR(1) | Sim | Indica se agrupa recebimentos do pedido (S/N). |
| `PEV_ESPECIE_MOEDA_DESPESA` | NUMERIC(15,2) | Sim | Valor de despesa por espécie de moeda. |
| `PEV_ESPECIE_MOEDA_DESC` | NUMERIC(15,2) | Sim | Valor de desconto por espécie de moeda. |
| `PEV_ESPECIE_MOEDA_ACRE` | NUMERIC(15,2) | Sim | Valor de acréscimo por espécie de moeda. |
| `PEV_ESPECIE_MOEDA_ALT_DES_ACR` | VARCHAR(1) | Sim | Indica se a espécie de moeda altera desconto/acréscimo (S/N). |
| `PEV_GUID_FECHAMENTO` | VARCHAR(50) | Sim | GUID do fechamento de caixa. |
| `PEV_CUPOM_DESCONTO` | VARCHAR(100) | Sim | Cupom de desconto aplicado. |
| `PEV_OPCAO_FINAL` | VARCHAR(30) | Sim | Opção final selecionada no pedido. |
| `PEV_SESSAO_PHP` | VARCHAR(255) | Sim | Sessão PHP (integração web). |
| `PEV_ORIGEM_URL` | VARCHAR(255) | Sim | URL de origem do pedido (integração web). |
| `PEV_TEM_NEGOCIACAO` | VARCHAR(1) | Sim | Indica se o pedido tem negociação em aberto (S/N). |

COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_STATUS IS 'A - ABERTO
F - FATURADO
C - CANCELADO. Para consultas de faturamento ou análise financeira, use WHERE PEV_STATUS = ''F'' para trazer somente pedidos finalizados.';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_FORMA_PAGAMENTO IS 'Espécie padrão ou forma de pagamento do cabeçalho do pedido. FK para TB_ESPECIE_MOEDA.ESP_ID. Para o detalhamento por forma de pagamento, use TB_PEDIDO_VENDA_FIN.PEVF_ESPECIE_MOEDA.';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_COMISSAO IS 'Comissão (%) do vendedor';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_TIPO_FRETE IS 'NF_TIPO_FRETE
0 - CIF
1 - FOB
2 - TERCEIROS
9 - SEM FRETE';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_ACRESC_DESC_NF IS 'N - Nao envia acrescimo e desconto para nf
R - Envia apenas acrescimo e desconto que foi rateado
T - Envia total de acrescimo e desconto';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_TIPO_DESCONTO IS 'V - VALOR DE DESCONTO
P - PORCENTAGEM DE DESCONTO
T - TOTAL DO PEDIDO';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_SEL_IMPRESSAO IS 'Campo para selecionar Pedido a ser separado';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_TIPO_ACRESCIMO IS 'V - VALOR
P - PERCENTUAL';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_SALDO_FLEX IS 'Saldo Flex (Calcula valor desconto ou acréscimo que vendedor deu ao cliente
)';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_IND_PRESENCA IS '0=Não se aplica (por exemplo, Nota Fiscal complementar ou de ajuste);
    1=Operação presencial;
    2=Operação não presencial, pela Internet;
    3=Operação não presencial, Teleatendimento;
    4=NFC-e em operação com entrega a domicílio; 5=Operação presencial, fora do estabelecimento;
    9=Operação não presencial, outros.';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_TIPO_TROCO IS 'o que foi feito com troco
  T - Lançou Troco
  C - Lançou Credito
  D - Descartou';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_CLIENTE_NAO_REG IS 'Cliente Não Registrado';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_DELIVERY IS 'S - Sim
    N - Não';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_STATUS_DELIVERY IS 'A - Aberto
    P - Pronto para entrega
    E - Entregando
    F - Entrega Finalizada
    C - Cancelado';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_TIPO_ENTREGA IS 'E - Entregar
    B - Cliente Buscar';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_AGUARDANDO IS 'Cliente aguardando e produto está pronto';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_MENSAGEM_ALERTA IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_OBS_NOTA IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_PEDIDO_VENDA.PEV_ERRO_SCANTECH IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
Este módulo detalha os fluxos de faturamento de pedidos com geração automática de cobranças bancárias, a arquitetura de desacoplamento entre títulos financeiros e boletos físicos, e a flexibilidade multibanco do ERP Código UP.

### 1. Parametrização Comercial e Herança Bancária `[00:00:14]`

A automação de geração de cobranças é condicionada pelas diretrizes estruturadas no cadastro de _Formas de Pago_.

- **Mapeamento do Tipo de Documento:** Ao configurar uma forma de pagamento, o administrador define o tipo de documento como **"Boleto Bancário"** `[00:00:21]`.
    
- **Vínculo de Conta Corrente (Carteira):** Essa parametrização obriga a associação de uma conta bancária específica (ex: Sicoob, Banco do Brasil) à forma de pagamento `[00:00:41]`. Toda vez que essa condição for selecionada no Pedido de Venda, o sistema já herda a carteira de cobrança correspondente `[00:01:04]`.
    
- **Regras de Parcelamento (Gatilho de Intervalo) `[00:00:48]`:** Definição das matrizes de parcelamento padrão (ex: configuração de 2 parcelas com intervalo rígido de 30 dias), que calcula automaticamente as datas de vencimento no ato do faturamento `[00:00:55]`.
    

### 2. Fluxo de Faturamento e Emissão Automática `[00:01:13]`

A conversão de um Pedido de Venda em faturamento financeiro ocorre de forma integrada na tela de vendas.

- **Processamento do Contas a Receber:** Ao salvar o pedido, o motor financeiro gera as provisões de recebimento correspondentes às parcelas da forma de pagamento, registrando-as inicialmente como títulos em aberto (débito normal) `[00:01:29]`.
    
- **Ação de Emissão Executiva `[00:01:46]`:** O operador aciona o comando **"Emitir Boleto"** diretamente na interface do pedido `[00:01:46]`. O ERP processa os dados da conta corrente associada, injeta as taxas de juros/multas parametrizadas para aquela carteira e gera os documentos de cobrança física em lote (ex: gerando os dois boletos do Sicoob em cascata) `[00:01:46]`.
    
- **Gatilho de Transição de Status `[00:02:00]`:** A emissão bem-sucedida dos boletos dispara automaticamente a transição do status do Pedido de Venda para **"Faturado"**, concluindo a janela operacional de venda `[00:02:00]`.
    

### 3. Engenharia de Dados: Desacoplamento entre Título e Boleto `[00:02:39]`

O ERP implementa uma arquitetura de banco de dados onde a entidade **Contas a Receber (Título)** e a entidade **Boleto Bancário** são tratadas de forma independente, ligadas apenas por um relacionamento lógico `[00:03:16]`. Esse modelo resolve problemas comuns de conciliação e rigidez financeira:

- **Independência de Cancelamento de Boleto `[00:02:47]`:** Caso o cliente mude de ideia e decida pagar a cobrança em carteira usando outra modalidade (ex: dinheiro, cheque ou PIX) ou necessite de uma prorrogação de prazo, o operador pode acessar o módulo de boletos e **cancelar estritamente o boleto físico** `[00:02:55]`.
    
- **Preservação da Conta a Receber `[00:03:25]`:** O cancelamento do boleto altera o status do documento de cobrança para "Cancelado" (mantendo o histórico para auditoria) `[00:03:42]`, mas **não exclui nem liquida o título financeiro** no Contas a Receber do cliente `[00:03:50]`.
    
- **Flexibilidade de Liquidação Secundária `[00:03:50]`:** Com a conta a receber preservada e liberada do vínculo do boleto anterior, o operador pode baixá-la normalmente através de qualquer outro meio de pagamento, evitando o retrabalho de ter que reestornar recebimentos, reabrir pedidos ou recriar lançamentos contábeis manuais `[00:03:59]`.
    

### 4. Operação Multibanco Concorrente `[00:04:40]`

A arquitetura de tabelas do ERP suporta a emissão simultânea e concorrente de cobranças para múltiplas instituições financeiras a partir do mesmo ambiente operacional.

- **Isolamento de Carteiras por Documento:** O operador pode manter um pedido faturado na carteira do Sicoob `[00:01:46]` e o pedido seguinte direcionado à carteira do Banco do Brasil `[00:05:07]`. O ERP faz o roteamento dos arquivos de remessa, regras de digitação de código de barras e layouts de impressão de forma independente, baseando-se estritamente na agência/conta parametrizada na forma de pagamento selecionada `[00:05:16]`.

ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link
https://www.youtube.com/watch?v=2EDlh07da_g

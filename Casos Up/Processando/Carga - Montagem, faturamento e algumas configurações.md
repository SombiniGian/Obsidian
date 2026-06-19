Este módulo detalha o ecossistema de **Gestão e Processamento de Cargas** do ERP Código UP, cobrindo o fluxo ponta a ponta: desde o agrupamento logístico de pedidos e sequenciamento de rotas, passando pelo faturamento massivo e emissão integrada de cobranças, até o fechamento financeiro e de despesas de viagem (prestação de contas do motorista).

### 1. Engenharia de Montagem e Roteirização da Carga `[00:00:41]`

O módulo, localizado em _Movimentações > Cargas_, atua como um consolidador logístico para otimizar o fluxo de expedição de mercadorias capturadas em campo (ex: via força de vendas externa em tablets) `[00:00:29]`.

- **Estruturação do Manifesto de Saída:** O operador define metadados de controle livre para identificação do lote (ex: "Zona da Mata") e realiza a amarração estrutural do transportador parceiro e do veículo de frota específico `[00:00:52]`.
    
- **Carga por Amostragem Dinâmica (Filtros de Dataset) `[00:01:10]`:** A interface de captura limpa o banco de dados e exibe os pedidos em aberto filtrados de forma cruzada por _Região Comercial, Vendedor responsável, Cidade de destino ou Período de lançamento_ `[00:01:30]`.
    
- **Validação Cromática de Estoque Crítico:** Na grade de seleção, pedidos com linhas sinalizadas na cor **Vermelha** alertam o faturista que existem produtos internos com saldo físico zerado ou negativo no estoque `[00:02:00]`. O sistema permite ignorar o aviso para geração do lote ou realizar a exclusão pontual do pedido `[00:03:00]`.
    
- **Sequenciamento de Rota (Drag-and-Drop) `[00:02:27]`:** O operador pode ordenar visualmente a sequência exata de entrega das mercadorias. Ao mover um pedido para cima ou para baixo, o sistema reordena a prioridade logística e atualiza o mapa de descarregamento `[00:02:44]`.
    
- **Análise de Cubagem e Capacidade Logística `[00:03:28]`:** O ERP cruza automaticamente a somatória de peso e metragem cúbica dos produtos contidos nos pedidos selecionados contra a capacidade máxima cadastrada no prontuário do veículo, prevenindo sobrecarga de frota `[00:03:45]`.
    
- **Emissão de Documentos de Expedição:** Uma vez consolidada, a interface emite os relatórios de separação, agrupamento de produtos e o **Romaneio de Carga/Entrega** para o almoxarifado `[00:04:10]`.
    

### 2. Painel de Faturamento Massivo e Transmissão SEFAZ `[00:04:15]`

A esteira de faturamento de carga permite que dezenas de pedidos sejam processados em lote, mantendo travas de conferência e tratamento de exceções de rejeição.

- **Conferência Guiada (F5 - Modo Solo) `[00:04:35]`:** O sistema posiciona o cursor no primeiro pedido do lote e exibe painéis laterais de conferência. O faturista pressiona `F5` para aprovar e faturar o item corrente, avaliando observações internas e alertas de última hora (ex: clientes com histórico recente de cheques devolvidos ou restrições de crédito adicionadas pós-venda) `[00:04:44]`.
    
- **Separação Automática de Escopo Fiscal `[00:05:27]`:** O sistema identifica quais pedidos exigem a emissão de Nota Fiscal Eletrônica (NF-e) e quais operam sob outras modalidades de venda, separando-os de forma autônoma na aba de transmissão `[00:05:34]`.
    
- **Roteamento de Comunicação Síncrona:** O painel de transmissão gerencia o envio em lote dos arquivos XML para os servidores da SEFAZ, permitindo parametrizar o envio automático do DANFE e do arquivo XML para o e-mail do destinatário final `[00:05:53]`.
    
- **Resiliência a Rejeições (Tratamento de Duplicidade) `[00:06:14]`:** Se uma nota apresentar erro de comunicação (ex: _Rejeição: Duplicidade de NF-e com diferença na chave de acesso_ devido a falhas em testes anteriores) `[00:06:42]`, o sistema isola o documento com erro para correção ou cancelamento do faturamento pontual `[00:08:29]`, liberando o fluxo de impressão física e distribuição das demais notas autorizadas do lote `[00:07:10]`.
    

### 3. Emissão Integrada de Cobranças Multibanco `[00:07:20]`

Concluído o faturamento fiscal da carga, o ERP executa o processamento em lote de todas as carteiras bancárias envolvidas naquele fluxo logístico.

- **Roteamento Inteligente de Layouts:** Em um único comando, o operador dispara a geração de boletos da carga inteira `[00:07:20]`. O sistema varre os pedidos, identifica as formas de pagamento contratadas e processa as cobranças em lote, segregando as regras de layout e ordenação por banco (ex: gera e agrupa primeiro os boletos pertencentes à carteira do Banco do Brasil e, na sequência, os documentos vinculados ao Sicoob) `[00:08:00]`.
    
- **Bloqueio de Emissão por Dependência Fiscal:** O ERP impede a geração e impressão do boleto bancário caso a NF-e vinculada àquele pedido específico tenha sido rejeitada ou não esteja devidamente autorizada na SEFAZ, blindando a empresa contra emissões de cobrança sem lastro fiscal `[00:08:16]`.
    

### 4. Auditoria de Viagem e Acerto Financeiro (Prestação de Contas) `[00:10:08]`

No retorno do veículo à base de distribuição, a carga passa pelo processo de fechamento de viagem para conciliação financeira do motorista.

```
+----------------------------------------------------------------------------+
|                       MÓDULO DE ACERTO DE VIAGEM                           |
+----------------------------------------------------------------------------+
| 1. CONTROLE DE ENTRADAS DE VIAGEM                                          |
|    - Adiantamento Fornecido p/ Viagem (R$)                                 |
|    - Km de Saída vs. Km de Chegada (Cálculo de Consumo Médio)              |
|                                                                            |
| 2. LANÇAMENTO DE DESPESAS OPERACIONAIS                                     |
|    - Combustível, Pedágios, Alimentação, Manutenções de Emergência         |
|                                                                            |
| 3. CONCILIAÇÃO POR INTELIGÊNCIA DE FORMA DE PAGAMENTO                      |
|    - [Boletos]      --> Conferência de Canhotos/Comprovantes               |
|    - [Dinheiro]     --> Conferência de Espécie p/ Caixa                    |
|    - [Cheques]      --> Conferência de Títulos Físicos                     |
|                                                                            |
| 4. ENGENHARIA FINANCEIRA DE RESULTADOS                                     |
|    - [Valor Bruto da Carga] - [Despesas Globais] = Valor Líquido da Carga  |
|    - Margem de Contribuição e Cálculo de Lucro Líquido Real da Operação     |
+----------------------------------------------------------------------------+
```

- **Lançamento de Despesas do Veículo `[00:10:38]`:** Registro sistemático das variáveis de viagem, incluindo odômetro (KM de saída vs. KM de chegada) para cálculo de consumo médio de combustível `[00:10:45]`, além do lançamento de notas de despesa com pedágio, alimentação e manutenções corretivas na estrada `[00:10:53]`.
    
- **Conciliação por Agrupamento de Meios de Pagamento `[00:11:16]`:** A interface do acerto estrutura o balanço financeiro separando as obrigações do motorista com base nas formas de pagamento das notas fiscais entregues `[00:11:26]`:
    
    - _Cotas de Dinheiro:_ Exibe o montante exato em espécie que o motorista coletou nas entregas à vista e deve repassar ao caixa central `[00:11:49]`.
        
    - _Cotas de Cheque:_ Lista os títulos físicos recebidos em campo para conferência e custódia `[00:11:49]`.
        
    - _Cotas de Boleto:_ Consolida o montante de canhotos de notas assinados e comprovantes de entrega de cobrança registrados `[00:11:49]`.
        
- **Cálculo da Rentabilidade da Viagem:** O ERP deduz as despesas gerais de transporte do valor bruto das mercadorias, fornecendo em tempo real o **Valor Líquido da Carga** e a margem de **Lucro Líquido Real** gerada por aquela operação logística específica `[00:11:00]`.
- 
**Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: https://www.youtube.com/watch?v=3VVhaTVsHn4
---
id: CASO-213
link: https://www.youtube.com/watch?v=wy_xhhilA70
setor: Suporte
modulo: Faturamento / Ordem de Serviço
tags: [ordem_de_servico, garantia, nfe, gerenciamento_de_fotos, faturamento]
data_criacao: 2026-07-18
---

# Gerenciamento Avançado de Ordem de Serviço: Garantias, Fotos e NF-e de Produtos

Esta documentação detalha as atualizações e rotinas operacionais do módulo de **Ordem de Serviço (O.S.)**, cobrindo o gerenciamento de garantias corporativas e de terceiros, anexo de evidências fotográficas em lote e o fluxo de faturamento integrado para a emissão de Nota Fiscal Eletrônica (**NF-e**) de produtos aplicados na prestação de serviço.

## Sumário
- [[#Parametrização Geral do Módulo de O.S.]]
- [[#Gestão de Garantia de Terceiros e Fluxo Financeiro]]
- [[#Anexo e Captura de Fotos por Ordem de Serviço]]
- [[#Faturamento da O.S. e Emissão de NF-e de Produtos]]

---

## Parametrização Geral do Módulo de O.S.

As preferências operacionais do fluxo de trabalho das ordens de serviço devem ser configuradas previamente para automatizar as telas de atendimento e faturamento. Para configurar as regras globais, acesse **Movimentações** > **Ordem de Serviço** e clique no botão **Configurar Pedido** (ou acesse a tela de manutenção de configurações).

### Campos de Operação Padrão
* **Operação de Produtos:** Define a [[Natureza de Operação]] fiscal automática a ser aplicada sobre as peças e insumos inseridos na ordem de serviço quando ela for convertida em faturamento de venda.
* **Seleção Dinâmica de Natureza:** A opção **Selecionar Natureza de Operação na Nota Fiscal de Produtos** força o sistema a exibir um pop-up de seleção no exato momento do faturamento, dando flexibilidade ao operador caso precise alternar CFOPs com base no tipo de cliente.
* **Exibição da NF-e para Transmissão:** O parâmetro **Abrir Tela de Nota Fiscal de Produtos para Transmissão** determina se, logo após o faturamento, o sistema deve abrir a janela do módulo de NF-e para o envio manual. Caso esteja desmarcada, a transmissão do XML para a SEFAZ ocorre de forma automática e em segundo plano.

---

## Gestão de Garantia de Terceiros e Fluxo Financeiro

O sistema estende a capacidade de gerenciamento de ordens de serviço para além da garantia direta da empresa prestadora, cobrindo cenários de **Assistências Técnicas** que atendem ordens de serviço acobertadas por fabricantes ou garantidores externos (ex: Samsung, Fiat, Volkswagen).

### Mecanismo de Garantia de Terceiros
* **Garantia de Terceiros como Padrão:** Ao marcar este sinalizador nas configurações, o sistema ativa nativamente a aba **Garantia de Terceiros** na criação de novas ordens de serviço.
* **Vínculo do Garantidor:** Na aba de garantia, defina o **Cliente Garantidor** (a fabricante ou seguradora responsável pelo custo do reparo), informe o número do certificado de garantia fornecido pelo cliente e a data original da venda do bem.

### Comportamento Regido pelo Sinalizador Financeiro
O campo **Gerar Financeiro para Garantidor** altera radicalmente a destinação de cobrança dos títulos no módulo [[Financeiro]]:

> [!info] Direcionamento das Contas a Receber
> * **Sinalizador Marcado (Garantia de Fábrica):** No momento da liquidação da O.S., as contas a receber (títulos de cobrança) serão geradas e associadas ao cadastro do **Cliente Garantidor** (Fabricante), isentando o cliente final do pagamento.
> * **Sinalizador Desmarcado (Garantia Interna):** O faturamento gera os lançamentos financeiros diretamente contra o cadastro do **Cliente Proprietário** do equipamento ou veículo.

---

## Anexo e Captura de Fotos por Ordem de Serviço

Para assegurar o registro do estado físico de entrada de equipamentos e veículos e resguardar a empresa contra contestações e sinistros, o sistema conta com a aba **Fotos** na manutenção da O.S.
[Ordem de Serviço]
└── [Aba Fotos] 
├── Inserir Descrição (ex: Motor, Lataria) 
└── Origem da Imagem ──► [Carregar Arquivo Local] 
└── [Captura Direta via WebCam]

 Processo para Anexo de Imagens 1. Na visualização ou edição da O.S., navegue até a aba **Fotos**. 2. Clique no comando **Incluir (F2)**, defina um nome de identificação ou **Descrição** para o arquivo (ex: "Motor 1", "Lateral Direita") e confirme. 3. Com o registro criado, clique com o **botão direito do mouse** sobre a área de exibição cinza para exibir o menu de contexto. 4. Selecione uma das ações de entrada de imagem: - **Carregar:** Abre o explorador de arquivos do Windows para selecionar uma foto armazenada no disco local ou servidor. - **Assign from Camera (Captura Direta):** Caso haja uma câmera ou webcam homologada e conectada ao terminal, o sistema aciona o hardware de captura de vídeo para registrar a imagem em tempo real, anexando-a diretamente à O.S. sem necessidade de intermediários. 5. Clique em **Salvar (F12)**. As mídias passam a ser gravadas e atreladas permanentemente ao ID da ordem de serviço. --- ## Faturamento da O.S. e Emissão de NF-e de Produtos A conclusão das ordens de serviço do tipo "Serviço com Peças Aplicadas" exige o desmembramento fiscal e financeiro para recolhimento de impostos estaduais. ### Fluxo de Liquidação 1. Com a O.S. finalizada pelo corpo técnico, selecione o registro na grade e clique no comando **Faturar (F9)**. 2. O sistema abrirá a interface financeira para preenchimento da **Forma de Pagamento** (Dinheiro, Cartão, Boleto, etc.). 3. O ERP realiza o processamento segregado: os valores de insumos/produtos e as taxas de serviços prestados geram lançamentos analíticos e independentes no fluxo de caixa. ### Emissão da NF-e de Produtos (Modelo 55) * Após confirmar o faturamento financeiro, clique em **Opções** > **Nota Fiscal dos Produtos**. * O sistema comporá o espelho da [[NF-e]] importando os dados cadastrais do cliente e agrupando todos os produtos e óleos sintéticos utilizados como peças na O.S. com seus respectivos preços e alíquotas. 
 > [!warning] Ponto Crítico de Validação do Suporte > Ao acessar o painel de NF-e a partir da O.S., o erro *"Diretório de Arquivos de Resposta não encontrado"* será exibido caso a máquina operadora não possua os caminhos de pastas fiscais configurados no gerenciador do certificado digital. Para sanar, configure os diretórios conforme instruído nas diretrizes do módulo fiscal. * Com a nota estruturada e validada em tela, clique em **Transmitir (F5)** para assinar digitalmente e enviar o arquivo XML para a SEFAZ autorizadora.
 
 
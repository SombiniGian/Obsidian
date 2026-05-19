# ![[images/image1]]

# `Código UP Sistemas`

Manual para usuários administradores  
Edição 1   
09/12/2024

## **Sumário** {#sumário}

[Sumário	2](#sumário)

[CADASTRO DA EMPRESA	4](#cadastro-da-empresa)

[DADOS PRINCIPAIS	4](#dados-principais)

[DOCUMENTOS ELETRÔNICOS	5](#documentos-eletrônicos)

[OUTRAS	8](#outras)

[CONFIGURAÇÃO DO EMAIL	9](#configuração-do-email)

[OUTRAS INFORMAÇÕES	9](#outras-informações)

[RESOLVER PENDÊNCIAS NOTAS FISCAIS	11](#resolver-pendências-notas-fiscais)

[CONTABILIDADE	12](#contabilidade)

[CONFIGURAÇÕES DO SISTEMA	13](#configurações-do-sistema)

[CONFIGURAÇÃO DO WHATSAPP	13](#configuração-do-whatsapp)

[CADASTRO DE PRODUTOS	14](#cadastro-de-produtos)

[CONFIGURAÇÃO DE PRODUTOS	14](#configuração-de-produtos)

[INCLUIR OU ALTERAR PRODUTO	15](#incluir-ou-alterar-produto)

[DADOS PRINCIPAIS	15](#dados-principais-1)

[DADOS FISCAIS	16](#dados-fiscais)

[INSUMOS	16](#insumos)

[CONVERSÃO DE UNIDADE	16](#conversão-de-unidade)

[RELACIONADOS	16](#relacionados)

[SIMILARES	16](#similares)

[LOTES	17](#lotes)

[MOVIMENTAÇÕES INVENTÁRIO / CONTÁBIL	17](#movimentações-inventário-/-contábil)

[CUSTOS	17](#custos)

[OPÇÕES	17](#opções)

[CADASTRO DE PESSOAS	17](#cadastro-de-pessoas)

[CADASTRO DE NATUREZA DE OPERAÇÃO	20](#cadastro-de-natureza-de-operação)

[CFOP: Código Fiscal de Operações e Prestações	20](#cfop:-código-fiscal-de-operações-e-prestações)

[MENSAGEM DOCUMENTO FISCAL	20](#mensagem-documento-fiscal)

[CONFIGURAÇÕES DE VENDA	21](#configurações-de-venda)

[CONSIGNADOS	21](#consignados)

[CONVERSÃO DE UNIDADE	24](#conversão-de-unidade-1)

[SITUAÇÃO PROBLEMA CONVERSÃO MEDIDA	26](#situação-problema-conversão-medida)

[ENTRADA NFE XML MANIFESTAÇÃO DESTINATÁRIO	27](#entrada-nfe-xml-manifestação-destinatário)

[ROTINA AGENDAMENTO DE RELATÓRIO	28](#rotina-agendamento-de-relatório)

[CAMPOS PERSONALIZADOS, GRIDS E DASHBOARD	29](#campos-personalizados,-grids-e-dashboard)

[CAMPOS PERSONALIZADOS	29](#campos-personalizados)

[TELA INICIAL: DASHBOARD	32](#tela-inicial:-dashboard)

[PERSONALIZAR GRID	33](#personalizar-grid)

[ORDEM DE SERVIÇO	34](#ordem-de-serviço)

[INSTALAR VÁRIOS FIREBIRDS	35](#instalar-vários-firebirds)

[PDV OFFLINE	37](#pdv-offline)

[INSTALAÇÃO DA ESTAÇÃO OFFLINE	38](#instalação-da-estação-offline)

[XML	41](#xml)

[FECHAMENTO INDEVIDO DO SISTEMA	41](#fechamento-indevido-do-sistema)

[CONTROLE DE ID	41](#controle-de-id)

[DESCONTO	42](#desconto)

[CASHBACK	44](#cashback)

[ABRIR GAVETA AO FINALIZAR VENDA	45](#abrir-gaveta-ao-finalizar-venda)

[VÁRIOS LOCAIS DE ESTOQUE	46](#vários-locais-de-estoque)

[MOVIMENTAR ESTOQUE CONTÁBIL COM OUTRO PRODUTO	47](#movimentar-estoque-contábil-com-outro-produto)

[VÁRIOS ENDEREÇOS POR PESSOA / ESCOLHER ENDEREÇO AO EMITIR NF	48](#vários-endereços-por-pessoa-/-escolher-endereço-ao-emitir-nf)

[Mudar endereço na NF	49](#mudar-endereço-na-nf)

[EMAIL	50](#email)

[CONTROLE DE ENTREGA \- ENTREGA FUTURA	51](#controle-de-entrega---entrega-futura)

[CRÉDITO ICMS E RELAÇÃO COM SIMPLES NACIONAL	53](#crédito-icms-e-relação-com-simples-nacional)

[A integração do sistema com o IFOOD	54](#heading=h.g8c5lljc568y)

[Uma NF de vários produtos, precisa gerar uma nota para cada	58](#uma-nf-de-vários-produtos,-precisa-gerar-uma-nota-para-cada)

[Configuração de Ordem de Serviço](#configuração-de-ordem-de-serviço-opções-de-"obrigar-cadastrar-equipamento"-e-"obrigar-cadastrar-defeito")  
[Opções de "Obrigar cadastrar Equipamento" e "Obrigar Cadastrar Defeito"	58](#configuração-de-ordem-de-serviço-opções-de-"obrigar-cadastrar-equipamento"-e-"obrigar-cadastrar-defeito")

[GERAR ARQUIVOS XML E ENVIAR AO CONTADOR	59](#gerar-arquivos-xml-e-enviar-ao-contador)

[CONFIGURAR AJUSTE FISCAL	60](#configurar-ajuste-fiscal)

[DIVISÃO DE CONTA c/ TAXA COUVERT	62](#divisão-de-conta-c/-taxa-couvert)

[MOVIMENTAR/TRANSFERIR VALOR CAIXA	62](#movimentar/transferir-valor-caixa)

[DEFINIR CAIXA POR PDV/USUÁRIO OU  VENDEDOR	62](#definir-caixa-por-pdv/usuário-ou-vendedor)

[DESCONTAR DO CONTAS A PAGAR UM RECEBIMENTO](#descontar-do-contas-a-pagar-um-recebimento-descontar-do-salário-uma-compra/vale-realizado-pelo-funcionário-por-ex.)  
[Descontar do salário uma compra/vale realizado pelo funcionário por ex.	64](#descontar-do-contas-a-pagar-um-recebimento-descontar-do-salário-uma-compra/vale-realizado-pelo-funcionário-por-ex.)

[ITENS SUGERIDOS \- NOTA FISCAL	66](#itens-sugeridos---nota-fiscal)

[RELATÓRIO NO MOBILE	67](#heading=h.t096x7oqih0c)

[CONTROLE ENTREGA APK MOBILE	70](#controle-entrega-apk-mobile)

[CONFIGURAÇÃO BALANÇA	74](#configuração-balança)

[INTEGRAÇÃO  PIX PSP	76](#integração-pix-psp)

[CONFIGURAR PIX MAQUININHA	78](#configurar-pix-maquininha)

[PRODUTO DESMEMBRÁVEL	78](#produto-desmembrável)

[GERANDO LOTE DE PRODUÇÃO AO VENDER PRODUTO	83](#gerando-lote-de-produção-ao-vender-produto)

[DIFERENÇA ENTRE POS E TEF	85](#diferença-entre-pos-e-tef)

[TEF APP	86](#tef-app)

[EMITIR NF PELO APLICATIVO/MAQUININHA	87](#emitir-nf-pelo-aplicativo/maquininha)

[DESTACAR QUANTIDADE DE PESSOAS NA MESA	89](#destacar-quantidade-de-pessoas-na-mesa)

[CONCILIAÇÃO BANCÁRIA	91](#heading=h.4nn8eahrygz)

## 

## **CADASTRO DA EMPRESA** {#cadastro-da-empresa}

### **DADOS PRINCIPAIS** {#dados-principais}

Ao cadastrar ou alterar um registo de empresa é importante preencher todos os dados, o cadastro é necessário para a emissão de documentos fiscais e para o funcionamento do sistema.

![[images/image2.png]]

**EMPRESA**

* Atenção no cadastro **CRT \- Código Regime Tributário** pois irá impactar diretamente no cadastro do produto.   
  * Sendo tributação normal será **CST**(lucro real e lucro presumido),   
  * Sendo simples nacional terá o **CSOSN**: excesso de sublimite, parecido com o lucro presumido portanto também usará o CST.

  ### **DOCUMENTOS ELETRÔNICOS** {#documentos-eletrônicos}

YOUTUBE:  [Configurando os documentos eletrônicos](https://youtu.be/A0WM_7yadDU?list=PLYBb7Dry90CR9X4sCXMqh4Wgj458Ah_Gi&t=393)

Antes de iniciar a configuração, é fundamental identificar o tipo de certificado digital que está sendo utilizado. O sistema possui compatibilidade garantida com certificados do tipo A1 (arquivos .PFX ou .P12). Siga atentamente as instruções abaixo para verificação e instalação adequada.  
Para verificar se o **certificado digital está instalado** no windows pesquise pela ferramenta **certmgr.msc**

![[images/image3]]

**WEB SERVICES**

* O padrão **SSL type** utilizamos o LT\_TLSv1\_2.  
  * Colocar em **homologação** caso queira emitir uma NF sem validade(teste)  
  * **Produção** caso queira emitir NF válida.  
* Se a rede precisar configurar algum **Proxy** para conectar com o estado, temos a opção em tela  
* O parâmetro **TimeOut** determina o tempo máximo (em milissegundos) que o sistema tentará enviar uma nota fiscal à **SEFAZ** antes de interromper a tentativa e retornar uma mensagem de erro.  
  * 30.000 milissegundos é geralmente o tempo limite máximo da requisição aceito pela SEFAZ 

  **CERTIFICADO**


O certificado digital é a identidade eletrônica de uma pessoa ou empresa. Ele funciona como uma carteira de identificação virtual e permite assinar documentos à distância com o mesmo valor jurídico da assinatura feita de próprio punho no papel, mas sem precisar reconhecer firma em cartório.

* Na aba Certificado indicamos o **Caminho do Certificado** digital e colocamos a senha  
* É importante sempre trabalharmos com arquivo e indicarmos o caminho correto  
* O padrão ouro da configuração **SSLLib** é **libOpenSSL**  
  * Caso não consiga com libOpenSSL, use o **libCampcom**  
  * De ultimo caso use **libWinCrypt**  
    * Utilizando o libWinCrypt ou Capcom clique no botão (...) em Serial do Certificado, abrirá as opções do windows para escolher o certificado  
  * A utilização do WinCrypt corre o risco de parar o funcionamento após uma atualização do Windows.  
* Após configurar, clique em **Dados do Certificado** para concluir

**NF-e**

As abas seguintes seguem o mesmo padrão, as **configurações de diretório dos arquivos** devem ser definidas em cada uma das abas **caso a revenda tenha alterado a pasta de instalação padrão**.

**![[images/image4]]**

*  Na **NF-e** e na **NFC-e** utilizam o mesmo caminho dos Schemas.  
* **Arquivo de Impressão(DANFE)** definimos o schema utilizado para imprimir a NF e pode ser escolhido a forma que melhor servir ao cliente na pasta de Documentos Fiscais, em cada pasta existirá uma outra como nome Report.  
* **Logomarca** carrega a imagem da logomarca que será impressa na NF.  
* **Preview Impressão** define se quer a impressão direto na impressora ou se abre na tela  
* **Dialog  Impressão** permite definir em qual impressora deseja imprimir.  
* **Email ao Transmitir** dispara um email após transmitir a nota fiscal.  
* **Numeração** à direita para refletir a última nota fiscal emitida em seu sistema anterior. Ao escrever "1000" ali e pressionar o botão "+" no sistema, na próxima vez que emitir uma nota fiscal, ela será da série 1 e terá o número 1001\. Essa série será configurada na natureza da operação.

**NFC-e**

* **Configuração da NFC-e**: Semelhante à configuração do NF-e, com destaque para a **importância do QR Code**.  
  * **QR Code em 2.0**: Durante a instalação, a **versão 2.0 do QR Code é padrão**, mas atenção a possíveis problemas de transmissão do cupom fiscal \- verifique se a marcação está correta.  
  * Atualização do QR Code: Para versões mais antigas, ajuste manual pode ser necessário; salve a configuração no 2.0 para garantir a atualização na base de dados.  
* **CS** e **Id. CSC**: Elementos cruciais para a NFC-e, obtidos no site da Sefaz ou através da contabilidade com certificado digital.

	**SAT e MFE**

O SAT é específico para as empresas de São Paulo assim como o MFE é para o Ceará(entrou em desuso, ainda sim temos a opção de configurá-lo).

**NFS-e**

Único detalhe é se atentar  que **cada prefeitura utiliza um schema próprio** que deve ser verificado e configurado corretamente. Escolha o dentro da pasta **NFSe\>Schemas** o provedor em que a sua cidade trabalha.

#### **OUTRAS** {#outras}

YOUTUBE: [Cadastro da Empresa \- configurações](https://youtu.be/ZvmiEbYt9kY?list=PLYBb7Dry90CR9X4sCXMqh4Wgj458Ah_Gi&t=16)

* A aba "Outras" é fundamental para o funcionamento eficiente da empresa dentro do sistema.  
* Permite configurar aspectos essenciais para a operação diária e a edição de documentos fiscais.  
* Configurações para resolver pendências de Notas Fiscais.  
* Configuração de email.

Abaixo demonstraremos algumas opções de configuração:   
![[images/image5]]

##### **CONFIGURAÇÃO DO EMAIL** {#configuração-do-email}

* No topo da interface, encontra-se a configuração do e-mail.  
* Este e-mail é utilizado como padrão para o envio de todos os e-mails do sistema, exceto para boletos.  
* Para boletos, a configuração é feita na conta bancária.

##### **OUTRAS INFORMAÇÕES** {#outras-informações}

* **Gerar Tag Grupo de Repasse do ICMS:**  
  * Essa configuração é específica para alguns estados que podem apresentar dificuldades nesse processo.  
  * É importante que cada revenda, de acordo com seu conhecimento local, decida se utilizará essa configuração ou não.

* **Grupo Cartão Obrigatório:** Esta configuração está relacionada à transmissão, sendo mais relevante para alguns estados, como a Bahia, que podem ter requisitos específicos.  
    
* **Alertar, transmitir e resolver automaticamente:**  
  * Toda vez que entrar no sistema ou sair recebe um alerta e executará as opções/processos que estão ao lado direito da tela **“Resolver Pendências Notas Fiscais”**.  
  * Algumas configurações, como a transmissão automática, estão diretamente ligadas a estados específicos, como a Bahia. Caso haja algum detalhe particular relacionado a isso, deve-se considerar essa configuração.

* **Permitir Emissão de NFC para Contribuinte do ICMS:**  
  * Esta configuração permite a emissão de NFC-e para clientes marcados como contribuintes do ICMS.  
  * Porém, é importante entender que a NFC-e é destinada a consumidores finais, não a empresas.  
  * No entanto, se um cliente com CNPJ e inscrição estadual receber uma NFC-e, isso pode violar as regulamentações fiscais.  
  * Em casos em que um cliente com inspeção estadual recebe uma NFC-e, é **necessário marcar o campo como "isento" na nota fiscal**.  
  * Este procedimento indica que o destinatário não é um consumidor final, mas sim uma empresa com inscrição estadual.

* **Variações entre Estados**  
  * É crucial considerar que **as regulamentações fiscais variam de estado para estado**.  
  * Alguns estados permitem a emissão de NFC-e para contribuintes do ICMS, enquanto outros não.

* **O que acontece ao cancelar Nota Fiscal**  
  * Ao cancelar uma nota fiscal, o sistema oferece várias opções para lidar com o pedido de venda associado.  
  * As opções disponíveis incluem:  
    * **Não Faz Nada com o Pedido:** A nota fiscal é cancelada, mas o pedido de venda permanece inalterado no sistema.  
    * **Cancela o Faturamento do Pedido:** O faturamento do pedido associado à nota fiscal é cancelado, mas o pedido em si permanece ativo.  
    * **Cancela o Pedido Diretamente:** O pedido de venda é cancelado integralmente junto com a nota fiscal.  
    * **Pergunta para o Usuário:** O sistema solicita a intervenção do usuário para determinar o próximo passo em relação ao pedido de venda.  
* Em relação à **Part. ICMS**, é importante observar que ela é considerada como **100% por padrão** e não tem havido necessidade de ajuste nessa configuração há muito tempo.


##### **RESOLVER PENDÊNCIAS NOTAS FISCAIS** {#resolver-pendências-notas-fiscais}

* **Atualizar Status, Cancelar ou Inutilizar as Substituídas**   
  * A funcionalidade permite lidar com situações em que a **comunicação** com a Secretaria da Fazenda (**SeFaz**) **falha** durante a **tentativa de transmissão de uma nota fiscal**. Nesses casos, o sistema **cria uma nota fiscal em contingência offline** **e mantém a nota anterior**. Esta funcionalidade automatizada verifica se a nota anterior foi transmitida com sucesso e toma ações apropriadas com base nesse resultado.  
  * O número da nota fiscal anterior é mantido para verificar se foi transmitida com sucesso.O sistema verifica se a nota fiscal anterior foi transmitida corretamente.  
  * Se a nota anterior foi **transmitida com sucesso**, a nota offline é **cancelada e substituída**.  
  * Se **não foi transmitida**, a numeração da **nota offline é inutilizada**.

* **Transmitir as NFC e OFFLINES**  
  * Opção para transmitir todas as NFC-e offline geradas pelo sistema.  
  * Importante manter a opção marcada para que o sistema transmita automaticamente ao entrar ou sair do sistema.

* **Retransmitir as Notas Fiscais com transmissão Atrasada**  
  * Identificação de notas fiscais com data atrasada para retransmissão.  
  * Inutilização da numeração antiga para manter a sequência cronológica com base na data.  
  * **Procedimento de Inutilização de Numeração Antiga:**  
    * Se uma nota, por exemplo, com o número 1, foi transmitida às 10 horas e ocorreu um erro, e posteriormente, a nota número 2 foi transmitida às 11 horas, ao retransmitir a nota número 1, ela é transmitida como número 3 com a data correta.  
    * Isso garante a cronologia adequada da numeração em relação à data e evita duplicatas.

* **Aproveitar Número do Documento ao Retransmitir NFe**  
  A funcionalidade permite atualizar a data e hora da transmissão sem inutilizar a numeração anterior. Embora não seja a prática recomendada, atende a pedidos de algumas revendas cujos contadores exigem esse formato.  
  * Ao transmitir uma NFe, o sistema atualiza a data e a hora de transmissão.  
  * Isso ocorre sem inutilizar a numeração anterior da NFe  
  * A atualização da data e hora da transmissão pode resultar em situações em que o número 1 seja transmitido às 10h e o número 2 às 9h, o que pode causar inconsistências.  
      
* **Inutilização de numeração não encontradas**  
  A funcionalidade foi desenvolvida para garantir a integridade e continuidade da sequência numérica das NFs emitidas pelo sistema. Ela identifica  lacunas na numeração e inutiliza automaticamente as numerações não encontradas dentro de um período específico, como os últimos três dias  
    
* **O que fazer com notas não transmitidas**

  * Permite que o usuário defina o que fazer com as notas que ainda não foram enviadas ao sistema de emissão fiscal.

  * Existem três opções disponíveis para lidar com essas notas:  
    * **DEIXAR** as notas como estão, sem tomar nenhuma ação.  
    * **TRANSMITIR** as notas fiscais para o sistema de emissão fiscal.  
    * **INUTILIZAR** as notas fiscais que não foram transmitidas.  
      

  ### **CONTABILIDADE** {#contabilidade}

 Nessa aba preenchemos os dados da contabilidade. 

* Se marcarmos a opção para autorizar o contador a fazer o download de xml’s no portal nacional, o contador conseguirá baixar o xml completo no site da sefaz ou com software pronto.  
* Marcando a opção enviar como cópia NFe para a contabilidade ao enviar por email . Sempre que enviamos uma nota fiscal para o email do cliente, também mandará uma cópia para a contabilidade.  
* Temos a opção de o sistema avisar sempre no dia que precisa gerar o SINTEGRA, SPED, PIS COFINS.

![[images/image6]]

### **CONFIGURAÇÕES DO SISTEMA**  {#configurações-do-sistema}

* A opção de **não validar dados fiscais** permite registar um cliente sem a necessidade de validação, podendo apenas registrar os dados e salvar  
* A opção **Filtrar os Vendedores por Empresa ao pesquisar**, mostrará apenas os vendedores daquela empresa(um cliente com mais de uma empresa e muitos funcionários)  
* **Não carregar Dados ao Abrir Tela** é bom para o cliente que tem muitos dados(milhares) portanto só trará os dados após filtrar, agilizando o sistema que pode ficar lento ao tentar trazer milhares de dados ao iniciar.  
* **Validar Plano de Contas** se estiver marcado não permite salvar as movimentações financeiras, de venda e de compra se o plano de contas não estiver configurado corretamente.(questão contábil).


### **CONFIGURAÇÃO DO WHATSAPP** {#configuração-do-whatsapp}

Nessa tela podemos indicar o IP Servidor, a porta e o caminho para os arquivos para a integração do servidor WhatsApp utilizado na loja.  
![[images/image7]]

## 

## **CADASTRO DE PRODUTOS** {#cadastro-de-produtos}

### **CONFIGURAÇÃO DE PRODUTOS** {#configuração-de-produtos}

YOUTUBE: [Configuração de Produtos](https://youtu.be/20SR89LnkR4?list=PLYBb7Dry90CR9X4sCXMqh4Wgj458Ah_Gi&t=24)  
Na engrenagem de configuração de produtos podemos definir as opções globais para a tela de produtos.

* **Mostrar estoque por empresa:** O cliente multiempresa que vende o mesmo produto irá mostrar o estoque que cada empresa tem.  
* As opções de **Controlar o estoque contábil** ou **Controlar estoque gerencial** muda se o usuário poderá ver a quantidade de estoque de cada. Configuração apenas visual.	  
* **Validar grupo de tributação:** Essa opção não irá permitir imprimir um documento fiscal caso não haja definido o grupo de tributação  
* **Validar Dados Fiscais** permitirá salvar um produto sem NCM e CST. Caso um cliente precise somente de uma gestão gerencial, deixar desmarcado.  
* **Movimentar estoque thread:** ao deixar marcado o sistema fará transferências de estoque com mais eficiência pois utilizará mais recursos do computador(Não indicado para computadores com poucos recursos).  
* **Solicitar código de barras ao incluir**: se encontrar na base de dados federal é preenchido automaticamente o NCM, o CEST e a descrição.

  ---


* **Código Fiscal:** é através dessa configuração que geramos os códigos que vão para a nota fiscal quando emitido um documento fiscal.

* **Dados Fiscais:** Os campos dos dados já vêm preenchidos automaticamente ao incluir um produto novo por padrão.  
* Quando tem o cadastro do produto do cliente iguais, você configura da forma que melhor se adequa. Após configurar, o sistema automaticamente irá incluir esses dados ao fazer um novo cadastro.  
* As últimas 2 opções de configuração das legislações define se vai **excluir o ICMS ou IPI da base de cálculo do PIS/COFINS**

  ### 

  ### **INCLUIR OU ALTERAR PRODUTO** {#incluir-ou-alterar-produto}

YOUTUBE: [Incluir ou Alterar Produtos](https://youtu.be/20SR89LnkR4?list=PLYBb7Dry90CR9X4sCXMqh4Wgj458Ah_Gi&t=267)

#### **DADOS PRINCIPAIS** {#dados-principais-1}

**O Grupo, Subgrupo, marca, descrição e setor** são cadastros que servem para cadastrar, organizar e identificar o produto com mais eficiência.

* É possível criar uma ou mais **“tabela de preço”** por produto.  
  * Uma tabela para atacado, outra para cliente, outra para cliente especial, entre outros.  
  * É possível fazer alterações da tabela de preço diretamente da tela.

* **Observação:** É possível adicionar informações que **ajudam na filtragem** e/ou informação para **qual situação o produto se adequa**.  
  * Exemplo: Em uma auto peças é possível destacar para quais carros um produto x serve.  
  * Isso permite uma busca mais eficiente por um produto específico.

* **Vasilhame:** Funciona bem para depósitos de gás, água, cervejaria, etc.   
  * Definindo a forma de trabalho com o vasilhame:	  
    * **Não** para que o vasilhame não seja recolhido.  
    * **Recolher** para  retornar o vasilhame em outro momento do processo.  
    * **Devolvido** para recolher o vasilhame ao realizar a venda(mesmo funcionamento da distribuidora de gás, em que o vasilhame é recolhido no momento da venda).

* **Controle de lote:** Função para controle de produção.  
  * Através das configurações consigo **gerar um lote para o produto produzido**.  
  * Controlar a **validade**.  
  * Se quero **validar** **o lote** na **entrada e/ou na saída** desse produto (posso configurar nas opções à esquerda se é na entrada, saída ou ambos).  
  * Após a produção é possível deixar o produto em **quarentena**(existem indústrias que não podem comercializar o produto logo após a produção).

* **Código Fiscal**  
  É o código que vai para a nota fiscal, identifica o produto para o estado. Caso seja necessário trocar o número fiscal do produto é necessário informar ao estado para que reconheça o produto e possa abater a quantidade em estoque ao vendê-lo.

    
* **TIPOS DE PRODUTO**  
  * **Destaque especial** para essa parte da configuração, **temos um tipo de produto específico para cada utilização ou necessidade.**  
  * Ao habilitar um tipo de produto , em alguns casos ativará uma aba de configuração para esse tipo de produto específico.

Informações sobre a parte de OPÇÕES.   
Imagens ilustrativas

#### **DADOS FISCAIS** {#dados-fiscais}

Aqui informamos a **tributação do produto**.

* A empresa optante pelo **Simples Nacional** tem a maioria das informações fiscais preenchidas de forma automática.  
* Se tratando de **lucro presumido** ou **lucro real** da tributação devemos configurar de acordo com a necessidade.  
  * Sendo nessa tela um diferencial de agregação de valor para a revenda.

Em grupo tributário fazemos a tributação por estado, por tipo de cliente ou por natureza de operação. Você pode criar um grupo tributário e vincular vários produtos

#### **INSUMOS** {#insumos}

Tudo que é utilizado no processo de produção é um insumo. O Insumo pode ser um bem ou serviço utilizado para a produção ou realização de um outro bem ou serviço. Se temos uma camisa que gasta linha, tecido e botão é nesta aba que informamos, assim o sistema da baixa automaticamente dos insumos.

#### **CONVERSÃO DE UNIDADE** {#conversão-de-unidade}

Temos um tópico que aborda somente este assunto, clique [aqui para saber mais.](#conversão-de-unidade-1) 

#### **RELACIONADOS** {#relacionados}

Quando fizer importação do XML de entrada é nessa aba que será informado os vínculos do produto com o fornecedor. Se compramos de diversos fornecedores, teremos a informação do produto em relação a cada fornecedor.

#### **SIMILARES** {#similares}

Ferramenta utilizada mais por auto peças, permite amarrar o produto A com o produto B, o B com o C. Assim o sistema apresentará os produtos similares, sugerindo um produto que está atrelado um ao outro em uma falta de estoque ou pelo cliente querer levar o produto similar de preço mais em conta por exemplo.

#### **LOTES** {#lotes}

Nesta aba conseguimos acompanhar o estoque de cada lote quando tirar uma produção ou quando dou entrada em um produto por lote(10 caixas de remédio de um lote, 10 caixas de remédio de outro lote).

* Na tela principal à esquerda definimos se devemos ou não informar o lote na venda.

#### **MOVIMENTAÇÕES INVENTÁRIO / CONTÁBIL** {#movimentações-inventário-/-contábil}

Nessas duas abas conseguimos visualizar todas as movimentações de estoque.

#### **CUSTOS** {#custos}

A cada entrada da nota e cada cálculo do preço de custo vai estar relacionado nesta aba.

#### **OPÇÕES** {#opções}

* Permitir ou não alterar o **preço do produto**.  
* Permitir ou não **controlar estoque**.  
* **Informar total:** ao vender o produto aparece uma tela para que você coloque o valor total  
  Ex: Se você vende a carne a KG, você também pode calcular pelo valor total. Você coloca o valor e o sistema calcula a quantidade.  
* **Vender área/volume:** da mesma forma que o exemplo acima, ao invés de escrever o total, utilizará a altura, largura e comprimento.  
* **Enviar Loja virtual:** se ele deve ser exportado ou não para a loja virtual.  
* **Enviar IFood:** se irá importar ou não para o ifood.  
* **Sistema:** Se utilizará o sistema para emitir nota fiscal, caso desmarcado ele somente fará o pedido.  
* **Exportar mobile:** se o produto pode ser utilizado no “força de vendas” , para o celular.  
* **Favoritos:**No modo touch existe um atalho somente para produtos favoritos para facilitar encontrá-los.

## **CADASTRO DE PESSOAS** {#cadastro-de-pessoas}

YOUTUBE: [Cadastro de Pessoas](https://youtu.be/uZ1yzSYDewU?list=PLYBb7Dry90CR9X4sCXMqh4Wgj458Ah_Gi)

* Funcionalidade central do sistema, permitindo o registro de clientes, vendedores, fornecedores e outros.   
* Unificação em uma única tabela: Todos os tipos de cadastro são realizados em uma única tabela, simplificando o processo.  
* Evita duplicações: Bloqueio de cadastros com o mesmo CNPJ, garantindo a unicidade das informações.  
* Uma mesma pessoa pode possuir mais de uma ou todas as características; sendo cliente, vendedor e fornecedor ao mesmo tempo, por exemplo.

![[images/image8]]

* **Configurações Específicas:**  
  * Abas específicas: Ao marcar o tipo de pessoa, são habilitadas abas com dados específicos para cada categoria (cliente, vendedor, fornecedor).  
  * Facilidade de busca: Integração com o site da Receita Federal permite a busca de dados, como CNPJ e inscrições estaduais.  
  * Registro detalhado: Possibilidade de cadastrar múltiplos telefones e endereços para cada pessoa.

* **Destaque para o Cadastro de Clientes:**  
  * Vínculos e configurações: Possibilidade de vincular clientes a vendedores específicos, tabelas de preço e formas de pagamento.  
  * Controle de cobranças: Funcionalidade que permite gerar mensalidades e modalidades de pagamento para os clientes. Gera o boleto e quantidade de parcelas, dá a opção de desconto para o cliente que paga antecipadamente(Opções Boletos)  
  * Configurações Tributárias:  
  * **Regime tributário**: Configuração importante para tributar produtos de acordo com o regime tributário do cliente.  
    ![[images/image9]]  
  * Personalização das configurações(**Opções**):   
    ![[images/image10]]  
    * Possibilidade de configurar cálculos de impostos como IPI e ICMS de acordo com as necessidades.  
    * Exportar o Cliente para a plataforma Mobile  
    * Validar Limite de Créd. para permitir a compra por crédito até o limite Valor Concedido, após exceder é necessário liberação para continuar comprando acima do valor concedido.   
      * Esse limite é para compra com o tipo pagamento **A Prazo**  
      * O valor limite é definido em **Valor Concedido**  
        **![[images/image11]]**  
* **Destaque para o Cadastro de Vendedor:**

O tipo pessoa vendedor  faz login no app força de vendas(vendedor externo, garçom, mobile). Podemos fazer configurações específicas para esse vendedor e quando ele realizar o  login, ele será o usuário atual naquele sistema, funcionará conforme as definições e permissões utilizadas.  
Configurações principais:  
Login e senha para logar no força de vendas

**FINANCEIRO**

* Mostra todos os vínculos financeiros dessa pessoa  
  * Recebimentos  
  * Cheques Recebidos  
  * Pagamentos  
  * Cheques emitidos

**PLANO DE CONTAS**

* Classificamos quais são as contas no plano de contas que movimentará a parte contábil do sistema

	**FOTOS e AUDITORIA**

* Também incluídos na configuração de Pessoa, são abas padrões do sistema.

## **CADASTRO DE NATUREZA DE OPERAÇÃO** {#cadastro-de-natureza-de-operação}

A natureza da operação **é uma descrição mais ampla sobre o tipo de atividade comercial que a nota está amparando**. Como, por exemplo, “Venda de Produto” ou “Venda para o consumidor final”. Já o CFOP é um campo que também identifica a operação, contudo, com mais detalhes.

* Em **cadastro\>natureza de operações** 

![[images/image12]]

* Aqui configuramos a indicação de presença do comprador, se o preço é de venda ou compra, **plano de contas**, etc...

**Podemos utilizar uma natureza de operação em mais de uma empresa registrada?**

Na **Natureza de Operações**  quando não parametrizamos a **Empresa** para **Natureza Padrão de Venda** deixando-o em branco a configuração fica global, podendo ser usada por todas as empresas registradas.

#### **CFOP: Código Fiscal de Operações e Prestações** {#cfop:-código-fiscal-de-operações-e-prestações}

Trata-se de um código numérico utilizado na área fiscal e contábil no Brasil para identificar a natureza das operações de compra e venda de mercadorias, bem como a prestação de serviços de transporte e comunicação.

#### **MENSAGEM DOCUMENTO FISCAL** {#mensagem-documento-fiscal}

Essa mensagem será representada no documento fiscal

## **CONFIGURAÇÕES DE VENDA** {#configurações-de-venda}

Em construção

## **CONSIGNADOS** {#consignados}

* Em **movimentação\>consignados**  
* podemos incluir ou alterar um consignado:

![[images/image13]]

* Ao adicionar um produto, no botão **alterar** podemos mudar a quantidade ou valor do mesmo.

![[images/image14]]

* Não é possível alterar a **Tabela de Preço** após devolver itens do pedido.  
* Após salvar o consignado podemos alterá-lo quando necessário adicionando ou devolvendo itens.

![[images/image15]]

* Temos a opção de **gerar uma comissão** alterando porcentagem ou o valor, após clicar no botão aparecerá a tela de pagamento.

![[images/image16]]

* Ao clicar no botão **gerar venda** podemos gravar o consignado

![[images/image17]]

* O produto vendido pode ser encontrado na tela de vendas.

![[images/image18]]

* Para desfazer o consignado basta clicar no mesmo e no botão **cancelar\[f11\]**.  
* Caso queira deixar um registro da devolução dos produtos ao devolver todos os itens, vá na aba financeiro e salve o consignado, deixando-o em aberto para registrar o ocorrido.

## 

## **CONVERSÃO DE UNIDADE** {#conversão-de-unidade-1}

* Na aba produtos  temos como adicionar/alterar um produto e alterar sua **Unidade Principal**  
* Em seguida podemos adicionar uma **Conversão de Unidade**

![[images/image19]]

* Na aba **Conversão de Unidades** podemos adicionar/alterar uma conversão  
* A **Qtde Conversão** e o **Volume** devem ter o **mesmo valor** caso precise que o sistema mostre no pedido o preço do volume, e para que o sistema calcule corretamente o **preço unitário**  
* Deixe o **Preço de Venda** em branco para que o sistema multiplique o **Preço Venda** unitário pela **Qtde Conversão** e traga o preço de venda automaticamente.

YOUTUBE: [Como funciona a conversão](https://youtu.be/NMpL_RqdEHg?t=33)     
![[images/image20]]

* Com a conversão configurada corretamente posso realizar uma **venda**, preencho os dados principais e adiciono um  **Item de Pedido Venda** onde posso escolher a **Unidade** desejada

**![[images/image21]]**

*  Na opção abaixo podemos ver, alterar e adicionar unidades de medida.

  ### **![[images/image22]]** 

  ### **SITUAÇÃO PROBLEMA CONVERSÃO MEDIDA** {#situação-problema-conversão-medida}

O cliente compra a peça em metro e revende em rolo, agora ele deseja vender na mesma unidade em que compra.  
O programa apresenta erro ao tentar mudar a unidade de conversão de rolo para metro.

SOLUÇÃO  
Uma possível solução está na aba **Conversão de Unidade** e alterando a **Unidade de Conversão** dentro da **Manutenção de Unidades do Produto.**  
É importante verificar as permissões do usuário.

## 

## **ENTRADA NFE XML MANIFESTAÇÃO DESTINATÁRIO** {#entrada-nfe-xml-manifestação-destinatário}

A manifestação do destinatário permite ao destinatário da Nota Fiscal Eletrônica \- NF-e manifestar-se sobre a sua participação comercial descrita na NF-e, confirmando as informações prestadas pelo seu fornecedor e emissor do respectivo documento fiscal.

	**Manifestação do Destinatário**  
Essa função é obrigatória podendo gerar multa para quem não executar essa rotina, em resumo o cliente está confirmando se a NF emitida contra ele,  é dele ou não.

* Caso o fornecedor não esteja cadastrado é possível inseri-lo em nosso banco de dados através do botão mais ![[images/image23]]  
* Em **Itens Nota Fiscal** temos em cada um dos produtos a opção de:  
  * **Incluir** ![[images/image24]]  Um novo produto e na tela que abre já busca tudo que está no xml daquele produto como descrição, parte tributário, etc. Aqui você está fazendo um cadastramento manual.  
  * Na tabela de Unidade podemos alterar ou incluir uma **Conversão de Unidade** clicando no botão mais  
     ![[images/image25]]  
  * Também podemos adicionar uma **conversão de unidade** selecionando o item e apertando a tecla **F4.**  
* ![[images/image26]] **Incluir Prod. \[F3\]** irá fazer o processo anterior de forma automatizada adicionando todos os produtos ao banco de dados além de fazer o vínculo deste item com a NF

Após verificar que está tudo dentro dos conformes basta **importar.**  
Os itens estarão registrados no banco de dados local lhe permitindo tomar as decisões cabíveis através da Nota Fiscal.

## 

## **ROTINA AGENDAMENTO DE RELATÓRIO** {#rotina-agendamento-de-relatório}

* Na aba **sistema**, em ***Agendamentos Envio Relatórios”\>incluir***  
* Temos as opções de adicionar um modelo pronto de relatório no **Gerenciador de Relatórios**.  
* Existem as opções XML  
* Existe o campo específico para adicionar destinatários e-mails ou WhatsApps  
* Opção de agendar a **data** de quando enviar os relatórios

![[images/image27]]

## 

## **CAMPOS PERSONALIZADOS, GRIDS E DASHBOARD** {#campos-personalizados,-grids-e-dashboard}

### **CAMPOS PERSONALIZADOS** {#campos-personalizados}

YOUTUBE: [Campos Personalizado](https://youtu.be/o7_GxaBdExA?list=PLYBb7Dry90CR9X4sCXMqh4Wgj458Ah_Gi&t=251)  
Configurações personalizáveis que funcionam em quase todas as telas do sistema, de forma individual .  
![[images/image28]]

* Permite a **adição** de **campos de registros** extras em diversas telas, proporcionando **flexibilidade** e **adaptabilidade**.  
* Capacidade de **incluir** campos personalizados, atendendo às necessidades exclusivas dos usuários.  
* Capacidade de **alterar** campos já criados.

![[images/image29]]  
Existem diferentes **tipos**:

* **COMBOBOX**: Permite escolher uma opção.  
* **DATA**: reservado para escolher uma data, traz um calendário.  
* **INTEIRO**: Guarda números inteiros.  
* **NUMÉRICO**: guarda números decimais.

![[images/image30]]Na tela de produtos por exemplo,ao clicar em um produto agora temos disponível a aba   
**Campos Personalizados** onde podemos adicionar e personalizar a disposição dos campos que criamos.

* Podemos criar grupos para agrupar os campos.  
* Podemos criar subgrupos para organizar as informações dentro de um grupo.  
* Movemos ao arrastar com o mouse e organizamos onde fica cada grupo, subgrupo ou campo.


![[images/image31]]  
Neste exemplo criei um grupo(Grupo de Assuntos) que reúne os outros dois grupos de cabeçalhoAssunto, e com **Layout Direction** na opção tabbed os organizei em forma de abas.

* Perceba que o grupo selecionado, também ficará selecionado na tela de manutenção para facilitar saber o que estamos alterando.  
* Temos opções de alinhamento(**Alignment**) e posicionamento.  
* Caso faça uma alteração em um grupo que dentro dele há outros grupos e campos, todos eles herdam as configurações.

Os campos criados podem ser **visualizados na tabela** do cadastro utilizado. Após criar os campos personalizados, reinicie o sistema, volte no cadastro utilizado e altere o grid para ver o campo criado.

* Caso não apareça, verificar na empresa\>configurações do sistema se a opção Não Carregar Dados ao Abrir Tela está marcado, se sim, desmarque.  
  ![[images/image32]]

  ### **TELA INICIAL: DASHBOARD** {#tela-inicial:-dashboard}

Para disponibilizarmos o DashBoard na tela inicial primeiramente devemos ir na engrenagem no topo esquerdo da tela e selecionar o **usuário.** Na tela de alterar ou incluir um usuário temos a opção **Visualizar Dashboard.**  
**![[images/image33]]**

### **PERSONALIZAR GRID** {#personalizar-grid}

**PERSONALIZAR GRID EM UM PDV BALCÃO**

* Na tela de balcão, para que apareça a opção de **Configurar Grid** utilize as teclas **ALT \+ A**   
  ![[images/image34]]  
* Salve um Layout de Grade![[images/image35]]  
* Faça o processo padrão de customização de uma grid e em seguida salve no Layout de Grade criado anteriormente.

## 

## **ORDEM DE SERVIÇO** {#ordem-de-serviço}

YOUTUBE:[Ordem de Serviço \- Garantia e NFe de Produtos](https://www.youtube.com/watch?v=LtdMeLDREgc)

Todo serviço precisa de instruções para ser realizado de forma assertiva, e a ordem de serviço é o documento que formaliza essas informações, organizando os processos das empresas e garantindo que a equipe saiba exatamente o que fazer.  
Para o funcionamento da OS temos que cadastrar corretamente os Tipos Equipamentos, os Equipamentos e a Situação.

1. **Tipos Equipamentos**: Aqui configuramos quais as características dos equipamentos  
2. **Equipamentos**:   
3. **Situação**:

Em **Movimentações\>Ordem de Serviço** ao clicar na engrenagem podemos adicionar algumas configurações:

* Configuração da **Natureza da Operação**: Possibilidade de configurar a natureza da operação dos produtos para que a nota fiscal seja emitida automaticamente com a natureza selecionada.  
* **Lançamento de Garantia**: Permite lançar garantias concedidas pela empresa prestadora de serviço, como garantia de 30 dias para peças ou serviços realizados.  
* **Financeiro para Garantidor**: Geração automática  de registros financeiros para terceiros responsáveis pela garantia, como a Samsung, em caso de problemas cobertos pela garantia.  
* Funcionalidade de **inclusão de fotos**: Adição de fotos para complementar a ordem de serviço, permitindo armazenar várias imagens para documentação e descrição detalhada do serviço prestado.  
  Em **opções:**  
* Temos a opção de **obrigar a “Selecionar Natureza de Operação na Nota Fiscal de Produtos”**  
*  A opção de **“Abrir Tela de Nota Fiscal de Produtos para Transmissão**” se marcada abre um um PDF da nota que está sendo transmitida. Caso contrário imprime direto a NF sem abri-la no windows. 

**INCLUIR UMA ORDEM DE SERVIÇO**  
	**GARANTIA**

* Com o “**Serviço Garantido por Terceiro**” selecionado aparecerá a aba de “**Garantia de Terceiros**” e nela podemos escolher o Cliente Garantidor. Por exemplo, se fosse uma manutenção de um Tipo Equipamento VEÍCULO o Cliente Garantidor pode ser a Fiat ou Chevrolet.  
* A opção “**Gerar Financeiro para Garantido**r” se marcada define que o financeiro será cobrado do “Cliente Garantidor”, caso a opção estiver em branco será cobrado do cliente.

## **INSTALAR VÁRIOS FIREBIRDS** {#instalar-vários-firebirds}

Ter mais de um Firebird torna-se necessário quando temos clientes utilizando mais de uma versão do banco de dados ou para uso em laboratório.  
Caso tenha um firebird em funcionamento no computador é necessário parar o serviço em execução para prosseguir instalando outras versões. O ideal é instalar as versões ordenadamente começando da versão mais baixa a versão mais atualizada.   
	Instalando as versões do Firebird

* Ao finalizar a instalação desmarcar a opção de abrir o aplicativo, pois **só é possível instalar outras versões quando nenhum serviço do Firebird estiver em execução.**  
  ![[images/image36]]

* Instalando o firebird 4.0 apresentará uma mensagem avisando que já existe um firebird. Clique em **não** para prosseguir instalando a outra versão.![[images/image37]]

* Faça a instalação padrão do sistema UP e guarde a informação do diretório de instalação do firebird.  
* Abra a pasta de instalação do firebird e procure pelo arquivo **firebird.conf**![[images/image38]]  
  * No arquivo localize  pelo nome **RemoteServicePort** ou por **3050 (porta padrão)**  
  * Em seguida substitua por uma porta válida e livre para utilizar  
    * Retire do início da linha o caractere **\#**  
  * Procure por “DataTypeCompability” e sete para que seja compatível com 3.0: **DataTypeCompability \= 3.0**   
    * Retire do início da linha o caractere **\#**

![[images/image39]]

Agora precisamos criar e nomear serviços para cada Firebird instalado. Para isso entramos no diretório de cada firebird e executamos o cmd nela.   
Também é possível acessar o diretório direto do CMD copiando o endereço da pasta e colocando o comando **cd (Cole o caminho da pasta)**

* Exemplo comando para entrar na pasta do Firebird 3:  
  * **32 bits**:  
    **cd** C:\\Program Files (x86)\\Firebird\\Firebird\_3\_0  
  * **64 bits**:  
    **cd** C:\\Program Files\\Firebird\\Firebird\_3\_0

* Comando para criar o serviço para o firebird 3(este comando é realizado no diretório):  
  **instsvc i \-g \-name "Firebird 3.0**"

![[images/image40]]

* Comando para entrar na pasta do Firebird 4:  
  * **32 bits**  
    **cd** C:\\Program Files (x86)\\Firebird\\Firebird\_4\_0  
  * **64 bits**  
    **cd** C:\\Program Files\\Firebird\\Firebird\_4\_0


* Comando para criar o serviço para o firebird 4(este comando é realizado no diretório):  
  **instsvc i \-g \-name "Firebird 4.0"**

Com os 2 Firebird instalados prosseguimos com a instalação do sistema UP, instalamos um para cada firebird e utilizamos em suas **conf.INI** as portas que configuramos no **RemoteServicePort** do arquivo firebird.conf.  
![[images/image41]]

**PARA EXECUTAR O SISTEMA, É PRECISO ATIVAR NOVAMENTE OS SERVIÇOS DO FIREBIRD INCLUINDO OS SERVIÇOS QUE NOMEAMOS.**  
**![[images/image42]]**

## **PDV OFFLINE** {#pdv-offline}

**CONCEITO:**  
Ponto de venda (PDV) autônomo, com base de dados própria. A instalação desta estação deve ser feita como SERVIDOR.

	**OBJETIVO DA FERRAMENTA:**Possibilitar que uma estação de vendas não fique conectada ao servidor para executar as tarefas básicas. Ou seja, a máquina fará as vendas independente se o servidor (**retaguarda**) está ligado ou não.

	**REPLICAÇÃO DE DADOS:**  
A estação OFFLINE de tempo em tempo irá replicar os dados das vendas, notas fiscais e novos clientes cadastrados.

Na estação **OFFLINE** teremos uma configuração para que ao iniciar o dia, ou um novo caixa, os dados sejam atualizados.  
Essa ferramenta buscará somente os dados alterados no servidor para evitar grande volume de informações desnecessárias.

**OBS: TODO cadastro de novos produtos, naturezas, tabelas, etc. Deverá ser feito no retaguarda, e através da ferramenta de replicação de dados, atualizamos na estação offline.**

### **INSTALAÇÃO DA ESTAÇÃO OFFLINE** {#instalação-da-estação-offline}

1. Instalar e configurar o Servidor Força de Vendas, será necessário para a comunicação do servidor retaguarda com a estação.  
2. Configurar no servidor retaguarda a estação PDV:  
   1. Clique em **Cadastros\>Outras Configurações\>Estação PDV**  
      ![[images/image43]]  
   2. **Incluir\[F2\]** uma nova estação  
   3. Insira o código, a descrição da estação e a Conta caixa  
      ![[images/image44]]  
   4. Defina a rotina de atualização dos dados. Podendo automatizar a troca de informações entre o PDV OFFLINE e o RETAGUARDA. A opção de **Obrigar Atualização** e **Envio automático**.  
      ![[images/image45]]  
   5. A **Série NF** deve ser diferente entre as estações para que não haja duplicidade da NF.  
      ![[images/image46]]

      **INSTALANDO O PDV OFF**

3. Faça a instalação do sistema Up com base de dados utilizando a mesma versão de firebird utilizada pelo servidor retaguarda.  
4. Utilize uma base de Dados que esteja **totalmente zerada**, uma base com registros pode acarretar em problemas na instalação ou problemas futuros.  
5. Ao fazer login pedirá para cadastrar/atualizar os dados da empresa  
   1. Neste momento clique no botão **PDV OFFLINE** e configure o acesso ao servidor   
      ![[images/image47]]  
   2. Preencher os dados de host, porta,etc.. corretamente e clique em **habilitar PDV OFFLINE**  
   3. Escolha em qual estação relacionar o PDV OFFLINE  
   4. Ao retornar para a tela Dados da empresa, basta salvar para prosseguir  
      **![[images/image48]]**  
      

**OBSERVAÇÕES**

* Para acessar novamente as configurações do PDV OFFLINE:  
  Entre em **empresa\>configurações do sistema\>configuração offline**

* **Envio automático PDV Offline:** na estação offline, localize a aba **Sistema** e abra a **Configuração da Estação**, marque a opção Enviar Dados PDV Offline  
  ![[images/image49]]

* Para fazer carga/atualizar ou enviar Dados a qualquer momento entre em **Cadastros\>outras configurações\>atualizar dados** ou acesse a partir da tela de vendas a partir da tecla de atalho configurada para a finalidade.

**ATENÇÃO COM IP E PORTA PARA CONEXÃO**

* Se utilizamos o Servidor retaguarda e o pdv off **na mesma rede**, configuramos na estação o IP da máquina Servidor retaguarda.  
* Se utilizamos em computadores que **não estão na mesma rede,** instalamos e configuramos a ferramenta **ZeroTier** ou VPN e nas configurações do PDV off o **IP do Servidor retaguarda disponível no ZeroTier** em que está o retaguarda e a porta do Servidor Força de Vendas.  
* Se o Servidor Retaguarda está em uma **máquina na nuvem**, utilize o endereço ip do servidor em nuvem e a porta do Servidor Força de Vendas.  
* Se precisamos utilizar a **maquininha para vender externamente** e o nosso sistema funciona local é necessário ligar para a provedora de internet e solicitar um **ip fixo**, desta forma basta utilizar esse ip.

## **XML** {#xml}

É uma linguagem de marcação, os arquivos de texto delimitados são frequentemente usados para importar dados de planilha e de aplicativos de banco de dados para o Analytics.   
YOUTUBE: [O que é XML \- Quebrando mitos e lendas](https://youtu.be/9408HdOYhAA?t=269)

## **FECHAMENTO INDEVIDO DO SISTEMA** {#fechamento-indevido-do-sistema}

Utilizamos esse recurso quando o usuário fica preso, não conseguindo logar por exemplo.  
Para logar em um caixa que passou por uma interrupção(fechado forçadamente como em uma queda de energia) Devemos iniciar o sistema e clicar no raio, a senha específica utilizada é a **hora, mês e dia.**

**![[images/image50]]**

Se estiver em fechamento de um caixa e o sistema for fechado indevidamente. Basta logar com o mesmo usuário e o sistema abrirá na tela de fechamento novamente.

Alguns erros são corrigidos na tela de Registros Utilizados

## 

## **CONTROLE DE ID** {#controle-de-id}

A funcionalidade de "**Controle de ID**" ou "**Manutenção de Sequência"** é comumente utilizada para gerenciar e controlar a numeração dos identificadores únicos (IDs) atribuídos a registros em tabelas de banco de dados.  
O objetivo principal dessa funcionalidade é **garantir que os IDs atribuídos aos registros** em diferentes tabelas do banco de dados **sejam únicos e sequenciais**. Isso é fundamental para manter a integridade dos dados e evitar problemas de duplicidade ou inconsistência.

**Sempre que houver um erro de duplicidade na chave pode ser corrigido ao ir em sistema\>Controle de ID e atualizar o id da tabela que está acusando duplicidade.**   
![[images/image51]]

## 

## **DESCONTO** {#desconto}

Para aplicar desconto em uma nota fiscal ou pedido

* Em **Usuários**![[images/image52]]  
  * Aplicar um valor no “**Desconto máximo**” (somente o valor serve)  
  * Se o usuário for administrador ele poderá aplicar descontos

* No **produto** é possível **permitir** “**Aplica Desconto**”  
* Na **NF-e ou NFC-e** também é **possível aplicar desconto**  
* **Observar a “Finalidade da Nota”**  
  * Se a nota estiver em **DEVOLUÇÃO/RETORNO** somente é possível **aplicar desconto diretamente no item da NF**	  
  * No item da nota, clique em alterar e procure pela aba **Devolução** para **aplicar o desconto em uma devolução**, por exemplo.![[images/image53]]

## 

## **CASHBACK** {#cashback}

Todas as vendas com cashback precisam ter a identificação do cliente (por cadastro).  
Ao configurar o sistema para o uso de cashback o sistema irá gerar um crédito para o cliente (recebimentos) para que possa ser usado em suas futuras compras.  
Pode ser configurado de duas formas, por natureza de operação ou por produto, por porcentagem ou valor.

* **NATUREZA DE OPERAÇÃO**: Quando é por porcentagem o sistema aplica sobre o total da venda, e quando for valor vai aplicar o valor concedido;  
  ![[images/image54]]  
* **PRODUTO:** Por porcentagem vai aplicar sobre o valor total do item e por valor vai aplicar multiplicando pela quantidade de item.  
  ![[images/image55]]

**CONFIGURAÇÃO:**  
Mesmo que use por produto, é necessário que na natureza de operação esteja marcada para **gerar CASHBACK** na venda.  
Existe também a possibilidade de definir o **valor mínimo de cashback** para ser usado.  
Configuração de venda na aba PDV.

* tem que ter tipo documento **crédito** configurado para que o cliente utilize esse cashback no pagamento.

## **ABRIR GAVETA AO FINALIZAR VENDA** {#abrir-gaveta-ao-finalizar-venda}

1. É necessário compartilhar a impressora em rede, no windows procure por **configurações\>dispositivos\>impressora e scanners** e procure pela impressora utilizada.   
* Clique na impressora e em **Gerenciar**  
* Clique em **Propriedades da impressora**  
* Clique na aba **Compartilhamento**  
* Clique em **Compartilhar esta impressora**  
* Guarde o caminho “**Nome de compartilhamento**”

Para descobrir se a impressora está compartilhada, vá em uma pasta do sistema e busque pelo diretório da máquina.  
 ![[images/image56]]  
Visualize a impressora compartilhada e guarde o endereço da mesma  
**Ex.:**(\\MAQUINA\\IMPRESSORA)

2. Extrair o arquivo **gaveta.rar** dentro da pasta do sistema  
   ![[images/image57]]

 


   

3. Na pasta do sistema e procure por  **AbreGavetaConfi**  
   1. Inserir o “Serial” da impressora: Basta utilizar o **Nome de compartilhamento** da impressora  
      ![[images/image58]]  
   2. Clique em cada número para descobrir qual porta abre a gaveta (Ao clicar e a gaveta abrir, está será a porta utilizada)

4. Abra o arquivo de configuração **gaveta**![[images/image59]]  
   1. Na configuração **“COM=”** coloque o endereço em rede da impressora(visto no passo 1\)  
      **Ex.:** COM=\\MAQUINA\\IMPRESSORA  
      ![[images/image60]]  
   2. No **BOTÃO** utilize a **porta** que foi descoberta no **AbreGavetaConfi**

5. No sistema abra **Pedidos de Venda\>Engrenagem de Configuração\>Aba PDV**  
   1. procure pela Configuração Gaveta na parte inferior da tela  
      **![[images/image61]]**  
      **Obs.:**  Esta forma de configuração não é necessário marcar a porta 

## 

## **VÁRIOS LOCAIS DE ESTOQUE** {#vários-locais-de-estoque}

YOUTUBE:[Vários Locais de Estoque](https://www.youtube.com/watch?v=SbN02Qu57Zc)

Este recurso permite controlar o estoque de uma empresa em diversos locais distintos, proporcionando uma gestão mais eficiente e detalhada do inventário.

Para visualizar as informações de um produto por estoque(depósito) registrado:

* Em cadastro de produtos selecione a opção **Mostrar Estoque por Empresa![[images/image62]]**

* Para as vendas serem efetuadas no PDV e **informar corretamente o estoque** que está sendo utilizado é necessário na **Natureza de Operação** escolher o **Local Estoque.**   
* Se não tiver escolhido o Local Estoque ele utilizará o estoque **principal**.![[images/image63]]

## 

## 

## **MOVIMENTAR ESTOQUE CONTÁBIL COM OUTRO PRODUTO** {#movimentar-estoque-contábil-com-outro-produto}

Ex: Quer vender um produto x que não movimenta o estoque e no lugar movimenta o estoque de outro produto.

* Cria os dois produtos  
* Em um dos produtos vá na aba “movimentações contábil”  
* Na parte de baixo acrescente o produto que irá movimentar o estoque.  
  ![[images/image64]]

**Detalhes:**   
Ambos produtos ficam como REVENDA  
Marque ou desmarque a **opção controla estoque** de acordo com as necessidades

## 

## **VÁRIOS ENDEREÇOS POR PESSOA / ESCOLHER ENDEREÇO AO EMITIR NF** {#vários-endereços-por-pessoa-/-escolher-endereço-ao-emitir-nf}

## Cliente com 2 inscrições estaduais quer registrar mais de um endereço  para cada inscrição para ao emitir uma NF ele possa incluir o endereço apenas alternando entre eles. É comum acontecer com escolas também, em que a cidade ou estado tem apenas um CNPJ mas com diversas escolas e localizações. Veja abaixo:

*    Abra o cadastro de pessoas, vá à aba endereços e inclua os endereços  
  ![[images/image65]]  
*     Preencha corretamente os dados  
*    Nessa tela você pode incluir a Insc. Estadual de cada endereço e sua Razão Social  
*   Verifique as informações e salve todos os endereços

  ### **Mudar endereço na NF** {#mudar-endereço-na-nf}

*  Para alterar o endereço, clicamos na aba Local Entrega/Retirada  
  **![[images/image66]]**  
* Nesta aba podemos pesquisar pelos endereços já registrados, alterar endereços ou incluir um novo  
  ![[images/image67]]  
* Após inserir o endereço, será alterado as informações no “Local Entrega/Retirada” e essas informações serão “puxadas” para o “Dados do Destinatário/Remetente”  
  ![[images/image68]]

## **EMAIL** {#email}

**Configuração de email na empresa.**

* No sistema vá na aba de Empresa  
  * Selecione a aba **Documentos Eletrônicos e clique na aba outros.**  
  * Configure o Host, Porta, Email, senha e opções de envio de acordo com a provedora de email. Neste exemplo utilizaremos o Google Gmail.  
    * Para email e senha é **necessário ativar a autenticação de 2 fatores**  
    * Porta: 465  
    * Host: smtp.gmail.com  
    * Marque apenas a **opção SSL**

* No Gmail vá na **Engrenagem\>Mostrar Todas as configurações\>Encaminhamento POP/IMAP** e procure pela parte de Acesso IMAP. Você deve deixar o status **Ativar IMAP**  
    
* Crie uma senha para o aplicativo e utilize na configuração de email do cadastro da empresa no sistema.  
    
* Pode fazer o teste indo em produto\>opções\>impressão por email. Acrescenta o seu email e envia para testar.

**CONFIGURAÇÃO DE EMAIL NA MANUTENÇÃO DE CONTA(BOLETOS)**  
Esta configuração é feita no cadastro de **Contas**:  
Selecione a conta **Bancária** que **emite boleto**  
selecione a aba **Configuração Boleto** e procure pela aba **Configuração de E-mail**.  
Para enviar E-mail a partir da tela de boletos siga os passos feitos na configuração de email na empresa, podendo utilizar os mesmos parâmetros. Lembre de utilizar uma senha criada para o aplicativo\!  
![[images/image69]]

## **CONTROLE DE ENTREGA \- ENTREGA FUTURA** {#controle-de-entrega---entrega-futura}

![[images/image70]][Controle de entregas \- Entrega Futura](https://www.youtube.com/watch?v=LdNEwnR4Emg)

Ao realizar uma venda é possível  agendar a entrega de cada produto para um dia específico e acompanhar o andamento da entrega. Se por exemplo o cliente faz uma compra e precisa que parte dos itens seja entregue em uma data e outra parte em outra data.

**Configurar Natureza de Operação específica para Entrega Futura**

1. Em Dados Principais desmarque a opção **Movimenta Estoque** e marcar a opção **Gerar Financeiro**.  
2. em Opções Avançadas marcar a opção **Entrega Futura**

Ao realizar uma venda com essa Nat.Op ela **vai gerar o financeiro sem movimentar o estoque**, de acordo que as entregas forem realizadas o estoque será movimentado.

**Obs:** Se vou retirar a nota que irá representar a venda e depois retirar as notas que representarão as entregas, consulte a contabilidade se deve ou não zerar a base de cálculo. É bem provável que em uma dessas notas não destacamos os impostos.  
No exemplo utilizado na aula do youtube o imposto foi destacado no momento da venda, sendo assim, a Nat.Op. de entrega  não destaca imposto.

**Configuração de Vendas**  
Na configuração da tela de vendas procuramos pela aba **Delivery/entrega** nela temos a configuração de Entrega Futura onde configuramos a Nat.Op. de entrega que criamos e o ajuste de acordo com as necessidades.  
![[images/image71]]  
**Vendendo e Entregando**  
Após todos os parâmetros configurados corretamente, ao realizar uma venda, você altera para a Nat.Op. para a Entrega Futura.

1. Clique em opções\>Entregas ou acesse pela tecla de atalho Alt+E  
2. Nesta tela você tem o controle sobre as entregas podendo incluir, alterar, excluir ou visualizar.  
3. Vamos Incluir\[F2\] novas entregas:  
   1. Nesta tela marcamos a Nat.Op. de entrega que configuramos.  
   2. Marcamos a data de entrega  
   3. Configuramos o Ajuste Fiscal  
   4. Na aba itens nós controlamos quais e quantos itens irão nessa entrega  
      1. Se clicar em salvar  entrega ela fica em aberto  
      2. Se clicar em finalizar, concluímos a entrega  
      3. Uma entrega agendada para outro dia deve ser salva para ser finalizada na conclusão da entrega

## **CRÉDITO ICMS E RELAÇÃO COM SIMPLES NACIONAL** {#crédito-icms-e-relação-com-simples-nacional}

Decreto 67975 de 2023

Decreto é em relação ao credito ICMS que ja vem na xml. AS outras informações fiscais vem normalmente na DANFE.

Esta frase está se referindo a um dos critérios para calcular o valor do imposto a ser pago, em relação a mercadorias adquiridas de contribuintes que estão no Regime Especial Unificado de Arrecadação de Tributos e Contribuições devidos pelas Microempresas e Empresas de Pequeno Porte, conhecido como "Simples Nacional". Nesse caso, o imposto a ser pago é baseado no valor indicado no documento fiscal da mercadoria, desde que ela seja destinada à industrialização ou comercialização

![[images/image70]][Crédito de ICMS | Comprar de empresa do Simples Nacional dá direito a crédito de ICMS?](https://www.youtube.com/watch?v=dD-NOTCJGc8)

**Se precisa destacar o crédito ICMS**

* Pode ser configurado na Natureza de Operação.  
  ![[images/image72]]

* Pode ser configurado no cadastro da empresa na aba Documentos Eletrônicos selecione a aba Conf.Extras.  
  ![[images/image73]]

## 

## **Uma NF de vários produtos, precisa gerar uma nota para cada** {#uma-nf-de-vários-produtos,-precisa-gerar-uma-nota-para-cada}

![[images/image74]]

* Se a NF não foi emitida:  
  * Pode excluir a nota fiscal para gerar outra corretamente  
  * Inicie a emissão de outra nota  
  * Selecione os pedidos para gerar uma nova nota fiscal( Tela: **Emitir Nota Fiscal Pedidos Faturados**)  
  * Em **Tipo Emissão** selecione a opção **Nota por Venda**  
  * Conclua o processo  
* Se a nota foi emitida, é necessário cancelar e começar a emitir da forma correta.

---

## **Configuração de Ordem de Serviço** **Opções de "Obrigar cadastrar Equipamento" e "Obrigar Cadastrar Defeito"** {#configuração-de-ordem-de-serviço-opções-de-"obrigar-cadastrar-equipamento"-e-"obrigar-cadastrar-defeito"}

Quando estão desmarcadas  salvam as informações como um texto livre. Ao marcar essas opções, elas são salvas como um registro que deve ser utilizado caso o aparelho retorne, por exemplo.   
Não há a obrigação de informar, o equipamento ou defeito, mas se informado ele pode ser salvo como um registro se as opções estiverem marcadas.

---

## **GERAR ARQUIVOS XML E ENVIAR AO CONTADOR** {#gerar-arquivos-xml-e-enviar-ao-contador}

![[images/image75]]

* No menu sistema temos o Agendamentos Envio Relatório. Nele você vai configurar o envio para a contabilidade periodicamente.

![[images/image76]]

* Em Documentos eletrônicos existe a possibilidade de gerar o arquivo de forma manual.

* Lembrando que para o envio automático precisa ter o envio de email configurado no cadastro da empresa.

![[images/image77]]

## 

## **CONFIGURAR AJUSTE FISCAL** {#configurar-ajuste-fiscal}

A Natureza de Operação define o modelo de transação (venda/compra) e determina o tipo de documento fiscal a ser emitido:

* Cupom Fiscal (para operações simplificadas, como vendas no varejo).  
* Nota Fiscal (NF) (para operações que exigem documentação fiscal completa).


Controle de Emissão: A Propriedade "Ajuste"  
Para especificar se a operação deve gerar documento fiscal, utilize a propriedade Ajuste:

| Valor do Ajuste | Comportamento do Sistema |
| :---- | :---- |
| 100% | Emite documento fiscal (NF ou Cupom). |
| 0% | Transação não gera documento |
| Vazio | Segue regras padrão do sistema (diferente de 0%) |

Exemplo:  
Se uma forma de pagamento tem ajuste em 100%, mas o tipo de documento vinculado tem ajuste em 0%, o sistema não emitirá o documento fiscal. Isso ocorre porque o ajuste do tipo de documento tem prioridade (desde que não esteja vazio).

**Observações Técnicas**

1. **0% ≠ Vazio:**  
* Inserir 0% é uma instrução explícita para não emitir.  
* Deixar o campo vazio permite que o sistema decida com base em outras regras cadastradas.  
2. **Hierarquia de Prioridades:**  
* 1º Configuração de venda.  
* 2º Tipo de Documento.  
* 3º Forma de Pagamento.  
* **4**º Cliente

**Na configuração do produto, marque a opção SISTEMA para que o produto da venda seja incluído nos itens da nota fiscal.**  
**![[images/image78]]**

1. **Configuração de Vendas:**  
   1. Entre na tela de **Movimentações\>Vendas\>Engrenagem\>Dados Principais**   
   2. Defina o Ajuste Padrão ideal para a situação.  
   3. Ao definir o ajuste através da Configuração de Vendas ele irá englobar qualquer tipo de transação, ou seja, com o ajuste em 100 ele irá emitir nota sempre na venda.

2. **Configuração Tipos Documentos**  
   1. Entre na tela **Cadastros\>Tipos Documentos\>Selecione o Documento**  
   2. Podemos definir individualmente em cada Tipo Documento o ajuste conforme o ideal para a situação.  
   3. Clique no documento que deseja alterar e clique na aba Configuração Venda e procure pelo campo Ajuste. Se o Ajuste estiver definido em 100 no Tipo Documento dinheiro, ao realizar a venda o utilizando ele emitirá nota.  
      

3. **Cadastro de Formas de pagamento.**  
   1. Entre na tela **Cadastro\>Formas de Pagamento**   
   2. Inclua uma forma de pagamento e configure o ajuste em 0![[images/image79]]  
   3. Para organizar as Formas de pagamento, coloque uma ordem numérica no início da descrição.  
   4. Em **Cadastro\>Vendas\>Configuração de Venda\>Dados Principais** localize a aba Opções 2 e marque “Obrigar FORMA DE PAGAMENTO ao finalizar”.  
   5. Ex: Ao finalizar uma venda em dinheiro, ele abrirá uma tela para escolher a Forma de Pagamento.  
      ![[images/image80]]  
4. **Configurar por cadastro de cliente**  
   1. Entre na tela **Cadastro\>Outras Pessoas\>Clientes**  
   2. Procure pelo campo ajuste e defina um valor  
      ![[images/image81]]  
      

##  **DIVISÃO DE CONTA c/ TAXA COUVERT** {#divisão-de-conta-c/-taxa-couvert}

Ao dividir conta em que já foi aplicado a taxa de couvert ele não aplica uma taxa para cada pessoa e sim divide o couvert entre eles.   
O indicado nesse caso é utilizar uma comanda para cada pessoa.

## **MOVIMENTAR/TRANSFERIR VALOR CAIXA** {#movimentar/transferir-valor-caixa}

Para movimentar o caixa, retirar o valor de uma conta para outra com finalidade de movimentar o caixa padrão. Quer que movimente o caixa padrão que é dinheiro.

Em **financeiro\>movimento de contas**  você tem a opção de **transferir\[F7\]**.  
**![[images/image82]]**

## 

## 

## **DEFINIR CAIXA POR PDV/USUÁRIO OU  VENDEDOR** {#definir-caixa-por-pdv/usuário-ou-vendedor}

A fim de visualizar no Saldo de Contas as movimentações de forma separada, seja por vendedores, por pdv, por grupo de vendas,etc. ou para abrirmos mais de um caixa:  
Podemos criar uma ou mais contas para suprir a necessidade, separando  essas movimentações no saldo de conta e possibilitando a abertura de mais caixas.  
Definindo a configuração de caixa no cadastro de usuário ou de vendedor a conta que desejamos, nós atribuímos as movimentações desse usuário ou vendedor à conta definida.

1. **Criar ou definir uma conta a ser utilizada.**  
   1. Primeiro precisamos definir qual conta utilizaremos ou se é preciso criar uma nova conta.  
   2. Para criar uma nova conta, basta ir em **Cadastros\>Contas** e clicar no botão de incluir ou na tecla F2.  
   3. Faça as configurações de acordo com as necessidades, defina uma descrição e um caixa destino(geralmente o cofre/caixa mestre)  
      ![[images/image83]]  
2. **De acordo com a necessidade ou regra de negócio, configure a conta na configuração caixa dos usuários ou vendedores.**  
   Por exemplo:  
   1. Se você precisa de uma leitura mais precisa das movimentações realizadas pelos vendedores externos.  
      1.  Você precisa ir no cadastro dessas pessoas e incluir na configuração de Caixa a conta que será para esse tipo.   
      2. É necessário abrir o caixa dessa conta no retaguarda antes que os vendedores realizem vendas.   
      3. É possível ter diversos vendedores utilizando uma só conta, ou uma conta por vendedor por ex.

   2. Se você precisa ter um caixa por PDV, ou uma conta que detenha as movimentações de todos os PDVs para que possa entender/controlar melhor o Saldo de contas.  
      1. Precisa ir no cadastro de usuário e definir na configuração Caixa a conta que será utilizada  
         ![[images/image84]]  
      2. Ao abrir um PDV e logar com o usuário que tem definido a conta Caixa você estará movimentando essa conta.  
      3. Dependendo da configuração da conta, ela te obrigará a abrir o caixa assim que logar.  
3. Após tudo configurado, basta que tenha concluído uma rotina de abertura e fechamento de caixa para que essas movimentações constem no Saldo de Contas.

## 

## **DESCONTAR DO CONTAS A PAGAR UM RECEBIMENTO** Descontar do salário uma compra/vale realizado pelo funcionário por ex. {#descontar-do-contas-a-pagar-um-recebimento-descontar-do-salário-uma-compra/vale-realizado-pelo-funcionário-por-ex.}

1. O funcionário faz um ou mais vale/compra na empresa para descontar no salário.  
   Para realizar o desconto precisamos do registro de **Pagamento** que se refere ao salário do funcionário na tela de Pagamentos  
   ![[images/image85]]  
   ![[images/image86]]  
2. Agora, precisamos gerar um **Recebimento** através de uma venda ou podemos incluir manualmente um recebimento na tela de Recebimentos  
   ![[images/image87]]  
   ![[images/image88]]  
3. Para abater o valor de Recebimento no Pagamento vá na tela de **Recebimentos**, selecione as **contas(pode ser uma ou mais)** que deseja abater e clique em **Receber**.   
   ![[images/image89]]  
   1. Na tela de Borderôs de Recebimentos, clique na aba **Pagamentos** e em **Selecionar**  
      ![[images/image90]]  
   2. Após clicar em selecionar, você terá uma tela que te permite escolher quais pagamentos deseja abater os recebimentos.  
   3. Com os pagamentos selecionados, confirme e salve.

## 

## **ITENS SUGERIDOS \- NOTA FISCAL** {#itens-sugeridos---nota-fiscal}

O produto sugerido é uma ferramenta para **indicar produtos que estão com estoque contábil maior que o estoque inventariado,** pois entende que  vendeu esses produtos sem transmitir NF.  
Assim, o produto sugerido ajuda a ajustar o estoque contábil do produto que está “sobrando” para aquele que não tem um estoque e que respeite a seguinte regra:  
O **preço custo \< preço venda** (o preço de venda tem um limite de no máximo \+100% que o custo do produto que está substituindo)

## **RELATÓRIO NO MOBILE**

A ferramenta Relatórios disponível no Apk é extremamente interessante para obter informações diretamente do mobile. Acompanhe o passo a passo para o funcionamento :

1. **Relatórios Próprios**  
   É necessário ter disponível no sistema relatórios que são próprios para a versão APK. Existem alguns no próprio sistema ou para download no painel da revenda.   
   ![[images/image91]]  
   1. Repare nesse relatório que pede para marcar algumas opções que veremos a seguir.

2. **Gerador de Relatórios**  
   No gerador de relatórios procuramos por aqueles que desejamos exportar para o App.  
   1. Você pode inserir um novo a partir de um arquivo .fr3 e colocá-lo na pasta correta  
   2. Clique no relatório e marque a opção de **Exportar para o App**  
   3. **Filtros APP**: para configurar as opções é necessário ter conhecimento do relatório, marcando corretamente os filtros utilizados pelo  mesmo.   
      No relatório do painel, por exemplo, já se especifica quais opções devem estar marcadas.

      ![[images/image92]]

3. **Configurar Usuário**  
   Precisamos atrelar no cadastro de usuário o vendedor que utilizamos no apk![[images/image93]]  
   1. Através do cadastro de usuário incluímos a permissão necessária para acessar o Relatório pelo APK.  
      1. Clique em Permissões  
      2. Selecione a empresa e clique em Alterar  
      3. Clique em Incluir ou pelo atalho F2 e adicione o relatório a lista de permissões  
      4. Se o usuário for **administrado**r o relatório estará disponível independente de adicionar o relatório nas permissões

![[images/image94]]

4. **Configurar APP**  
   1. Abra o app, faça login com o vendedor que está atrelado ao usuário que configuramos  
   2. Em Configurações clique em testar e salvar.  
      ![[images/image95]]

   3. Abra a ferramenta de relatórios  
      ![[images/image96]]

   4. Clique para atualizar, em seguida seus relatórios estarão disponíveis  
      ![[images/image97]]

## 

## **CONTROLE ENTREGA APK MOBILE** {#controle-entrega-apk-mobile}

![[images/image98]]  
![[images/image99]]  
![[images/image100]]

## 

## **CONFIGURAÇÃO BALANÇA** {#configuração-balança}

1. **CONFIGURAÇÃO PRODUTO**  
   1. Escolha o **Tipo Produto** Balança  
      1. Vai habilitar uma **aba Balança** que configuramos caso seja para uma balança que **utilize etiqueta**.  
      2. Na aba Balança configuramos o **Código Balança**, inserindo o mesmo código do produto configurado na balança e seu **Tipo**.  
   2. Na **Unidade Principal** marque a opção **pesável** para funcionar diretamente no sistema, bipando o produto e pesando a quantidade.

      **Obs:** 

* Produtos que são utilizados na **balança de etiqueta** configuramos o tipo produto balança e preenchemos as informações na aba balança;   
* Para produtos que são pesados em um caixa utilizando o sistema: configurar o tipo produto balança e a Unidade Principal configurada como pesável.

2. **CONFIGURAÇÃO DE VENDA**  
   1. Na configuração de venda, clique na **aba Balança**  
   2. As primeiras configurações se referem a **Balança Caixa**:  
      ![[images/image101]]  
      	 Selecionamos o modelo e preenchemos a Porta, Velocidade e Data Bits de acordo com as informações disponíveis no dispositivo instalado na máquina(geralmente no controle de dispositivos do windows obtemos as informações).   
   3. Clique em ativar, coloque um produto na balança e clique em ler peso.

   4. Abaixo temos a configuração da **Etiqueta de Balança**:  
      ![[images/image102]]  
      	Configuramos o funcionamento da etiqueta no sistema

	Para configurar o código de produtos de balanças no sistema, **defina o parâmetro "Tamanho"**, que determina a partir de qual casa decimal o código do produto será lido. Por exemplo, com um código completo de 6 dígitos "123456" e um "Tamanho" de 2, o código do produto começará a partir da 2ª casa, resultando em "3456".  O **código de balança é independente do código do produto**, portanto podemos usar códigos diferentes se necessário.  
	A configuração do "Tamanho" no sistema é crucial para garantir que o código do produto armazenado na balança seja corretamente identificado e corresponda ao código registrado no sistema.

**GERAR CARGAS BALANÇA**

1. Crie uma pasta em seu computador para gerar os arquivos  
2. Em **Cadastros\>Outros Produtos\>Cargos Balança** nós geramos os arquivos para serem importados para a balança  
3. Clique em Incluir   
4. Selecione o Modelo Balança com a opção compatível com sua balança  
5. Encontre o diretório que criou para guardar os arquivos  
6. Aperte em **Gerar Arquivo** e depois em Salvar

**Obs:**  
Para alguns modelos de balança é importante que no cadastro dos produtos que irão para a balança tenham o campo Setor definido.

**ALTERAR BALANÇA ELGIN PARA FUNCIONAR COMO OUTRA BALANA COMPATÍVEL**  
Algumas balanças não estão disponíveis(integradas ao sistema), sendo assim necessário fazer uma configuração interna na mesma para que ela tenha o comportamento de outro modelo.  
Ex: Configurando balança elgin   
![[images/image103]]  
![[images/image104]][Exemplo configurar internamente balança](https://www.youtube.com/watch?v=2_JkmG0kVtY)

## **INTEGRAÇÃO  PIX PSP** {#integração-pix-psp}

1. **CADASTRO DO PSP (PROVEDOR SERVIÇO PAGAMENTO)**  
   **![[images/image105]]**  
   1. No **Tipo** escolhemos o PSP que queremos configurar  
   2. Entre em contato com o provedor e solicite as informações necessárias  
   3. Preencha o cadastro do PSP de acordo com as informações e clique em **salvar**  
2. **CONFIGURAÇÃO DO PIX CONTROLES**  
   Em Financeiro\>Pix Controles, encontra-se tudo que é possível fazer com o PSP.   
   **![[images/image106]]**  
   1. Na aba Cadastros procure por **Pix Controles**  
   2. Configure as informações do recebedor(Para quem irá cair o pagamento)  
   3. No PSP Atual procure pelo PSP cadastrado que irá utilizar  
   4. Configure o diretório para salvar o Log do pix  
   5. Marque  o Ambiente que está trabalhando no momento  
3. **CONFIGURAR O TIPO DOCUMENTO**  
   ![[images/image107]]  
   1. Locais Utilizar marcar PIX PSP  
   2. Movimentar marcar Pix  
   3. Formas Pgto marcar 17=PIX  
   4. Em “**Configuração Venda**” existe a Venda Pix para atrelar o PSP a ser utilizado  
      ![[images/image108]]

## **CONFIGURAR PIX MAQUININHA** {#configurar-pix-maquininha}

Configura um tipo de documento próprio para o pix.

**Configure a Conta Bancária**  
Em  **Manutenção de Tipos de Documentos,** vá na aba **configuração de Venda**  
Outras Integrações  
Integração:

* **Stone DEEPLINK**: Para maquininha com app  
* **Stone Connect**: Quando a máquina Stone é TEF  
* **TEF APP**: Por maquininhas pinpad, se o cliente estiver utilizando um sistema por TEF

Necessário cadastrar a **Pessoa como Instituição Financeira** e inserir o CNPJ do banco.  
Na manutenção de conta acrescente a instituição financeira.

## 

## **PRODUTO DESMEMBRÁVEL** {#produto-desmembrável}

**Adicione e configure os produtos:**

1. Cadastre o produto que será desmembrado (Desmembrável)  
   ![[images/image109]]  
   1. Configure o produto com o **Tipo de Produto** Desmembrável  
   2. Observe que o tipo **Desmembrável habilita uma aba Produto desmembrados**  
   3. Este produto será a “matéria prima” para produzirmos os produtos desmembrados  
2. Produto desmembrado  
   1. Cadastre os produtos que serão gerados a partir do produto desmembrável  
   2. Esses serão o “produto final” após desmembrar.  
3. Retorne ao produto cadastrado como desmembrável e **acesse a aba Produtos Desmembrados**  
   **![[images/image110]]**  
   1. Nesta aba inclua os produtos que são gerados a partir da carcaça como no exemplo acima  
   2. Altere o fator de rendimento de cada produto em relação à carcaça

**Configurando a Ordem de Produção**  
Antes de prosseguir precisamos configurar o funcionamento da Ordem de Produção, pois a partir da ferramenta vamos “transformar” a carcaça nos produtos desmembrados  
![[images/image111]]  
Configurando dessa forma, sempre vamos incluir uma produção com status de Produzido, assim já movimentando o estoque dos produtos carcaça e desmembrado.

**Inserir um estoque de carcaça / Gerar Lote Produção \- Desmembrar**

1. Neste exemplo, crie uma Nota Fiscal Recebida de forma manual, insere  a Carcaça e Salvar.  
   **![[images/image112]]**

2. Em Documentos Fiscais Recebidos, clique em **Opções** \> **Gerar Lote Produção \- Desmembrar**  
   **![[images/image113]]**

3. Após confirmar para criar o lote de produção, abrirá a tela de Lote de Produção destacando as Ordens de Produção e os Insumos.  
   ![[images/image114]]  
4. É possível adicionar novos insumos, alterar o rendimento e/ou a Ordem de Serviço a partir desse momento. **Para concluir o processo basta Salvar.**

Podemos verificar a Ordem de Produção e também verificar em cada cadastro de produto a movimentação de estoque que foi realizada.

## 

## **GERANDO LOTE DE PRODUÇÃO AO VENDER PRODUTO** {#gerando-lote-de-produção-ao-vender-produto}

Esta rotina facilita a venda de produtos acabados sem a necessidade de gerar manualmente uma produção a cada venda.   
	Neste manual vamos configurar que ao vender ele gera automático a produção dando baixa nos insumos.

**CONFIGURAR NAT. OPERAÇÃO**![[images/image115]]

1. Em  **Cadastro\>Nat. Operação**  selecione para alterar ou inclua uma nova natureza de operação.   
2. Com a tela da Nat.Op. aberta clique na aba Avançado  
3. Escolha em que momento Gerar a Produção

	  
	**CONFIGURAÇÃO ORDEM DE PRODUÇÃO**  
![[images/image116]]

1. Em **Movimentações\>Ordens de Produção** clique na engrenagem de configuração   
2. Vamos configurar em que momento ocorrerá a baixa de estoque e se ela irá ocorrer, para esse exemplo utilizaremos todas as situações de **Quando movimentar Estoque**   
   **![[images/image117]]**  
3. Para que a Ordem de Produção seja **incluída com o Status de Produzido** marque as opções: Incluir com data de Início da Produção Preenchida e com Data de Produção preenchida  
   ![[images/image118]]

**REALIZANDO A VENDA**  
Agora, ao finalizar a venda com um produto que **tenha composição e utilizando a Nat.Operação** que configuramos, será gerado um lote de produção com os insumos do produto vendido movimentando seus estoques.

## **DIFERENÇA ENTRE POS E TEF** {#diferença-entre-pos-e-tef}

**O que é POS?**

POS é um equipamento que **realiza o pagamento em um terminal.** É muito comum para os usuários de cartão e, normalmente, está presente na maioria das atividades comerciais que utilizam esse tipo de pagamento. Elas são as **máquinas fornecidas por agências bancárias e adquirentes.**

Já o funcionamento dos terminais fixos se dá pela rede telefônica ou via internet, enquanto os sem fio se conectam por meio de chips de operadoras de telefonia ou através de uma estrutura própria como o WiFi do estabelecimento. Seu uso é tão comum por conta de sua praticidade e baixo custo.

Contudo, cada uma das máquinas de POS funciona ao se conectar diretamente à empresa que forneceu o terminal. Assim, para atender clientes com as mais diversas bandeiras de cartão será necessário contratar diferentes adquirentes, adicionando mais terminais ao estabelecimento, o que eleva os custos e também complica a administração dos pagamentos via cartão na empresa.

**O que é TEF?**

Esse mecanismo para pagamentos com cartão está mais associado a grandes redes comerciais ou estabelecimentos que recebem um grande fluxo de clientes, pois a centralização e os controles são uma necessidade quando o fluxo é muito grande. Para realizar as transações, o **equipamento de leitura de cartões, deverá estar conectado a uma aplicação de vendas**.  
Os sistemas deverão estar interligados, onde ao iniciar o processo na aplicação de venda, a **operação de pagamento acontece por meio de um terminal conectado ao sistema (PinPad) que realiza a leitura do cartão.** Uma grande característica do TEF é a conexão direta a várias empresas de cartões, por isso não necessita utilizar vários equipamentos para ler os cartões, trazendo mais segurança e rapidez nas transações.

## **TEF APP** {#tef-app}

**Vendedor**

* Configure um vendedor com o tipo usuário **TEF APP**;  
* Necessário atrelar a Maquina de Cartão a este vendedor.

![[images/image119]]

**Tipo Documento**

* Os tipos de documento precisam estar configurados com **integração TEF APP**  

![[images/image120]]

## **EMITIR NF PELO APLICATIVO/MAQUININHA** {#emitir-nf-pelo-aplicativo/maquininha}

Para que seja possível emitir Nota Fiscal a partir do aplicativo, seja ele em uma maquininha ou apk, precisamos configurar o vendedor, o tipo documento e adicionar arquivos à pasta do Servidor Força de vendas:

* **Cadastro do VENDEDOR:** No cadastro do vendedor configure para **Faturar** e **Emitir Nota Fiscal**  
  **![[images/image121]]**  
* **Cadastro Tipo documento:** No tipo documento utilizado no APP, parametrize para ajuste 100%  
  ![[images/image122]]  
* **Arquivos na pasta do Força de Vendas:** Adicione na pasta do servidor força de vendas os arquivos DLL do sistema Up e o Certificado Digital do Cliente.

## **DESTACAR QUANTIDADE DE PESSOAS NA MESA** {#destacar-quantidade-de-pessoas-na-mesa}

O controle de quantidade de pessoas em uma mesa para que por exemplo calcule corretamente a taxa de couvert podem ser feitas em dois momentos. 

**Faturando a Venda no PDV:**  
**![[images/image123]]**  
Na tela de faturamento, há um campo para preenchermos a quantidade de pessoas. Este campo é utilizado para calcular o **Valor da Comissão x Quantidade de Pessoas.** Este campo preenchido pode ser utilizado em relatórios.

**Pelo Aplicativo:**  
![[images/image124]]  
No controle de mesas, seleciona a mesa que deseja alterar a quantidade de pessoas, na parte de resumo dessa mesa clique para imprimir conta(conferência), ela irá abrir a tela para informar a quantidade de pessoas.  
O campo preenchido no APK para quantidade de pessoas alimenta o campo de pessoas do PDV(mesmo campo da tela de faturamento no retaguarda)

## **Devolução de Pedidos**

1.1 Vá em Devolução de Vendas ![[images/image125]]  
1.2 Clique em incluir ![[images/image126]]  
1.3.1 Clique em Motivo e selecione o Motivo da Devolução![[images/image127]]  
1.3.2 Selecione o Pedido que será Devolvido![[images/image128]]  
1.3.4 Logo após selecione ![[images/image129]]  
1.3.4.1 nessas opções será possível devolver um único item ou todos os itens do pedido selecionado.  
![[images/image130]]  
1.4 Ao clicar no botão irá ser exibido a seguinte tela:  
1.4.1: definir a quantidade que sera devolvida do produto ( parcial ou completa)   
1.4.2: clique em salvar  
![[images/image131]]

1.5: selecione se a devolução irá gerar alguma diferença para o cliente   
	1.5.1: clique em salvar  
![[images/image132]]

## **Devolução de Notas Fiscais**

1.1: Clique em Documentos Fiscais  
1.2: Clique em Notas Fiscais Emitidas  
1.3: Clique em Incluir   
1.4.Siga o Passo a Passo abaixo  
	1.4.1![[images/image133]]  
	1.4.2: Selecione  a operação ou crie uma nova → Clique no ( V ) para gerar o número→ Selecione o cliente → Outras Informações  
1.5: Selecione se a devolução será feita a partir de uma única nota ou de várias notas  
![[images/image134]]  
1.6: Selecione a nota que será devolvida, lembrando que ela precisa estar FATURADA para que haja a devolução da mesma.  
	1.6.1:   
Passo1: Selecione a nota  
Passo 2: A box Pesquisa Rápida é utilizada para selecionar todos os itens da nota fiscal.  
Passo 3: Existe a possibilidade de escolher um único item que será devolvido  
Passo 4: O campo \- Quantidade Digitada, se refere a quantidade que será devolvida  
Passo 5: Importar   
![[images/image135]]  
1.7: Logo após a importação, vá para o campo Nota Fiscal Eletrônica, clique em Transmitir e logo após em salvar.

![[images/image136]]

## **Como criar uma grid no pdv offiline**

Primeiro vai no usuário e de privilégio de administrador (isso se faz no servidor)  
![[images/image137]]

Depois faz a carga de dados no pdv Offiline, (pode deixar somente os usuário marcado para não demorar muito a carga de dados)  
![[images/image138]]

Na tela que voce quer criar a grid nova clica na engrenagem do lado do nome layout de grid, vai abrir a tela para criar a grid, depois voce vai em incluir para poder incluir uma nova grid, depois de feito isso faça as alterações visuais na grid e clica em salvar

![[images/image139]]

![[images/image140]]

Depois feito isso, caso não queria que o usuário tenha acesso para poder alterar o layout da grid e deixar somente na que voce criou agora, e so ir na configuração do usuário no PDV OFF, depois selecione o usuário, depois clica em visualizar, vai em layout de grid, pesquise a descrição do layout grid que voce acabou de criar e marca o checkbox não alterar.

![[images/image141]]

Com isso se voltar agora na mesma tela onde foi criada a grid pode constatar que não consegue mais alterar o layout da grid  
![[images/image142]]

## 















































































































































---
id: [CASO-178]
link: https://www.youtube.com/watch?v=2In73uzu2O8
setor: [Suporte, Implementação, Financeiro]
modulo: [Financeiro / Boleto Bancário via API]
tags: [sicredi, boleto-api, boleto-hibrido, integracao-bancaria, web-service, pix]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Emissão via API]]
2. [[#Parametrização de Dados de Cadastro da Conta]]
3. [[#Geração das Chaves de Acesso no Internet Banking (Client Secret)]]
4. [[#Provisionamento do Token de Aplicativo no Portal Developer (Key User)]]
5. [[#Configurações Avançadas e SSL da Guia Web Service]]
6. [[#Fluxo de Operação: Emissão, Remessa Web e Impressão Híbrida]]
7. [[#Fluxo de Liquidação e Cancelamento por Web Service (Retorno)]]
8. [[#Pontos Críticos e Regras de Validação]]

# Visão Geral da Emissão via API
A emissão de boletos bancários integrada via **API / Web Service** do Banco Sicredi substitui o modelo tradicional de geração e upload manual de arquivos de remessa (`.rem`) e download de arquivos de retorno (`.ret`). Sob esta arquitetura, o envio, o registro, a alteração e a baixa dos títulos ocorrem em tempo real via chamadas HTTP síncronas. O sistema suporta ainda a emissão do **Boleto Híbrido**, que anexa um QR Code Pix dinâmico ao corpo do documento impresso, viabilizando a liquidação instantânea.

# Parametrização de Dados de Cadastro da Conta
A configuração deve ser iniciada acessando a tela de **Cadastros > Contas**, localizando ou incluindo a conta bancária vinculada ao Sicredi.

### Campos Gerais e Layout
*   **Agência e Conta Corrente:** Preenchidos no padrão da instituição financeira.
*   **Código de Cedente:** Insira estritamente o número da conta corrente **sem o dígito verificador**.
*   **Carteira:** `1`
*   **Modalidade:** `1`
*   **Espécie de Documento:** `DM` (Duplicata Mercantil)
*   **Tipo de Carteira:** Selecione a opção **Web Service** para chavear o motor de geração de arquivos para chamadas de API.
*   **Operação:** `S`
*   **Layout:** Defina como **KAB 400** (exigido para a conformidade de payload da API).
*   **Responsável pela Emissão:** `Próprio Cliente`.
*   **Diretório de Remessa / Retorno:** Estes campos podem ser deixados em branco, visto que o tráfego de arquivos físicos em disco é eliminado pela transmissão via Web Service.
*   **Arquivo de Impressão (FastReport):** Mapeie o arquivo `boleto_pix.frx` localizado no subdiretório de boletos do sistema, permitindo a renderização estruturada do QR Code.

# Geração das Chaves de Acesso no Internet Banking (Client Secret)
Para preencher as propriedades de credenciais no ERP, o usuário deve extrair os tokens de autenticação diretamente nos portais do Sicredi.

### Passos para obter o Client ID e Client Secret:
1.  **Client ID (Regra do ERP):** Composto pela junção do **Número da Agência (sem o dígito)** + **Número da Conta Corrente (sem o dígito)**, informados de forma sequencial e sem espaços ou caracteres especiais.
2.  Acesse o portal do Internet Banking do Sicredi utilizando o navegador do cliente.
3.  Navegue até o menu **Cobrança** e selecione a opção **Código de Acesso > Gerar**.
4.  Marque a caixa de aceite dos termos jurídicos e avance. A tela renderizará um **QR Code de Autenticação**.
5.  No smartphone do cliente, abra o aplicativo Sicredi, acesse o menu **Segurança** (no canto inferior direito) e selecione o leitor de QR Code.
6.  Realize a leitura da tela do monitor. O Internet Banking atualizará a página de forma automática, exibindo uma string alfanumérica extensa contendo a chave **Client Secret**. Copie e cole esse dado no respectivo campo na aba de configurações do ERP.

# Provisionamento do Token de Aplicativo no Portal Developer (Key User)
O Sicredi exige um segundo nível de autenticação atrelado a um token de desenvolvedor, denominado **Key User**. Esta etapa é processada através do Portal do Desenvolvedor do Sicredi.

> [!tip] Centralização pela Revenda
> O cadastro no Portal do Desenvolvedor pode ser realizado de forma unificada utilizando o e-mail e CNPJ da própria revenda de software, permitindo gerar as chaves e gerenciar os aplicativos de múltiplos clientes finais sob um mesmo painel central.

### Registro do Aplicativo (App):
1.  Acesse o portal oficial do desenvolvedor do Sicredi e efetue o login.
2.  Vá em **Minha Conta > Minhas Apps** e clique em **Cadastrar Nova App**.
3.  No campo de nomenclatura, adote estritamente o padrão corporativo: `api_cobranca_AGENCIA_CONTA_sandbox` (ou `producao` conforme o ambiente). Preencha os campos de descrição com a razão social da empresa.
4.  Marque os escopos de autorização: **Open API** e **API Cobrança Boleto**.
5.  Clique em **Registrar**. O painel gerará um token identificado como *Client ID do App*. Copie o hash exibido **até o caractere de barra (`/`)**.

### Abertura de Chamado de Homologação / Liberação:
Após registrar o aplicativo, a chave permanece inativa. É obrigatório abrir um chamado para que a equipe de engenharia do banco valide o acesso:
1.  Dentro do portal do desenvolvedor, clique em **Suporte > Abrir Chamado**.
2.  Selecione o motivo: **API Cobrança de Boletos > Solicitar Acesso / Token**.
3.  Preencha os campos de assunto e descrição com o nome do aplicativo criado e defina o ambiente como **Produção**.
4.  Informe no campo de identificação o ID gerado na tela anterior.
5.  Envie o formulário. O Sicredi analisará a solicitação e responderá o ticket (tempo estimado superior a uma hora) disponibilizando a string do **Key User**. Insira esse hash no campo homônimo no ERP.

# Configurações Avançadas e SSL da Guia Web Service
Retornando à aba **Web Service / API** no cadastro de contas do ERP, preencha as propriedades estruturais da conexão de dados:

*   **Scope:** Informe o termo `cobranca` (obrigatoriamente em letras minúsculas e sem acentuação/caracteres especiais).
*   **SSL Lib:** Selecione a opção `httpOpenSSL` para garantir a criptografia TLS nas chamadas de endpoints.
*   **Versão do DF:** Selecione `V2` (layout atual de APIs REST do Sicredi).
*   **Ambiente:** Marque a flag **Produção**.
*   **Indicador de Pix / Boleto Híbrido:** Marque esta flag caso a conta possua uma chave Pix vinculada, forçando o envio dos metadados para que a API retorne a URL do QR Code Pix dinâmico.

# Fluxo de Operação: Emissão, Remessa Web e Impressão Híbrida

### Passo 1: Geração do Título
Acesse o módulo financeiro, crie uma movimentação de [[Financeiro / Contas a Receber]] e selecione a opção de gerar boleto bancário utilizando a conta do Sicredi API parametrizada. O boleto inicial será exibido na tela, porém, neste momento, ele **ainda não contém o QR Code Pix**, pois a chamada web não foi realizada.

### Passo 2: Registro e Transmissão em Tempo Real
1.  Acesse **Financeiro > Boletos Bancários > Remessa**.
2.  Filtre pelo banco Sicredi. O sistema listará os títulos gerados pendentes de envio.
3.  Marque o boleto desejado na grade e clique no botão **Web Service / Transmitir** na barra lateral direita.
4.  O ERP efetuará o handshake com o servidor do Sicredi enviando o JSON. Se validado, a API retornará o status de confirmação e os dados do Pix, exibindo a mensagem: `Remessa gerada com sucesso`.

### Passo 3: Impressão do Boleto Híbrido
*   Retorne ao módulo de impressão de boletos. Ao comandar a emissão física ou digital do documento, o layout carregará a linha digitável e o código de barras padrão na parte inferior e renderizará o **QR Code Pix Dinâmico no topo do boleto**.

# Fluxo de Liquidação e Cancelamento por Web Service (Retorno)

### Rotina de Retorno / Conciliação Bancária
Como não há processamento de arquivos `.ret`, a conciliação das baixas ocorre por varredura de histórico de API:
1.  Acesse o módulo de **Retorno Financeiro**.
2.  Clique no comando de execução via Web Service. O sistema fará uma chamada à API do Sicredi requisitando a lista de eventos e pagamentos ocorridos nos **últimos 15 dias**.
3.  Caso a API retorne liquidações (via código de barras ou Pix), o ERP processa a baixa automática do título correspondente no contas a receber, alimentando as contas patrimoniais.

### Estados do Boleto na API e Controle de Cancelamento

> [!warning] Ciclo de Vida e Travamento de Títulos
> Assim que o boleto é transmitido via Web Service, seu status inicial na SEFAZ/Banco passa a ser **Aguardando Confirmação**. Decorridos alguns minutos, o motor do Sicredi processa e altera o status para **Em Carteira**. 
> 
> *   **Regra de Bloqueio:** Enquanto o título permanecer sob o status de *Aguardando Confirmação*, a API do banco bloqueia qualquer ação de modificação. Se o operador tentar cancelar ou excluir o título no ERP durante este intervalo, o sistema retornará um erro impedindo a ação. O comando de cancelamento só será liberado e enviado com sucesso ao banco após o status transicionar para *Em Carteira*.

# Pontos Críticos e Regras de Validação

> [!danger] Quebra de Autenticação por Formatação do Campo Scope
> O preenchimento do campo **Scope** é case-sensitive no servidor do Sicredi. Escrever o termo com a primeira letra maiúscula (`Cobranca`), com acentuação (`cobrança`) ou inserir espaços adicionais interromperá a geração do token de portador (*Bearer Token*) durante as chamadas HTTP. Isso resultará em falhas críticas de autenticação em lote (Erros `HTTP 401 Unauthorized`), impedindo o faturamento de boletos por toda a empresa.

> [!warning] Validação da Chave Client ID Corporativa
> No campo Client ID, misturar o dígito verificador da agência ou da conta ou inserir hifens corromperá a chave criptográfica. Certifique-se de que o input contém apenas números limpos sequenciados.
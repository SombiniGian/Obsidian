---
id: CASO-152
link: https://www.youtube.com/watch?v=8dxX8EAogKQ&t=202s&pp=0gcJCUwLAYcqIYzv
setor:
  - Suporte
  - Implementação
  - Operacional
modulo:
  - Mobile / Portaria e Controle de Ingressos
tags:
  - android
  - portaria
  - check-in
  - check-out
  - comanda
  - bilheteria
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Módulo de Portaria Android]]
2. [[#Cenário 1: Check-in de Cliente com Ingresso Antecipado]]
3. [[#Cenário 2: Check-in de Cliente sem Ingresso (Venda na Portaria)]]
4. [[#Fluxo de Captura de Dados e Cadastro na Entrada]]
5. [[#Mecânica de Validação de Saída (Check-out)]]
6. [[#Pontos Críticos e Regras de Negócio]]

# Visão Geral do Módulo de Portaria Android
O módulo móvel de **Portaria e Controle de Ingressos** estende as rotinas de bilheteria e acesso do retaguarda Windows para dispositivos Android. A aplicação foi desenhada para operar em portarias de eventos, casas noturnas, shows ou estabelecimentos com consumo controlado, permitindo o registro de entradas (**Check-in**) de ingressos pré-vendidos, faturamento de acessos em tempo real, captação cadastral rápida (incluindo biometria facial/fotos de documentos) e a validação rígida de liberação de saída (**Check-out**) atrelada à quitação de débitos no caixa.

# Cenário 1: Check-in de Cliente com Ingresso Antecipado
Aplica-se quando o consumidor realizou a compra prévia do ticket (seja online ou em pontos de venda físicos).

1. O operador de portaria posiciona o cursor no campo **Comanda / Ingresso** da interface.
2. Realiza o input do identificador do bilhete (via digitação manual ou leitura do código de barras/QR Code).
3. Clica no botão **Check-in**.
4. **Validação do Sistema:** O ERP realiza uma varredura síncrona na tabela de ingressos ativos. Sendo o bilhete válido e não utilizado, o sistema retorna a mensagem verde `Entrada Liberada` e renderiza na tela o nome do cliente associado e a categoria do acesso (ex: `Entrada Normal`).
5. **Vínculo de Consumo:** Caso o estabelecimento opere com comandas internas obrigatórias, o sistema exige a inserção do número da comanda física que será entregue ao cliente.
6. Clique em **Registrar Entrada** para concluir o handshake. O bilhete é marcado como "Utilizado" no banco de dados e a comanda é ativada.

> [!info] Injeção Automatizada de Itens na Comanda
> De acordo com as parametrizações do menu de [[Cadastros / Natureza de Operação]] e Ingressos da retaguarda, ao associar a comanda ao ingresso no ato do check-in, o sistema injeta de forma automática o produto `Ingresso` ou taxas de consumo mínimo para dentro da conta do cliente, permitindo a apuração e cobrança posterior no fechamento do caixa.

# Cenário 2: Check-in de Cliente sem Ingresso (Venda na Portaria)
Aplica-se quando o cliente chega ao estabelecimento de forma espontânea, necessitando adquirir o direito de acesso no próprio ato da portaria.

1. O operador deixa o campo de código em branco e clica diretamente no botão **Check-in**.
2. O aplicativo abre a interface de localização de pessoas.
3. Insira o parâmetro de busca (Nome, CPF, RG ou Telefone) e clique em **Buscar**.
4. Após selecionar o cliente na grade (ou realizar um novo cadastro), clique em **Escolher**.
5. O sistema solicita a definição do **Tipo de Ingresso** (ex: `Inteira`, `Meia Entrada`, `Cortesia`, `Camarote`).
6. Insira o número da comanda física que será vinculada ao cliente.
7. Clique em **Registrar Entrada**.

# Fluxo de Captura de Dados e Cadastro na Entrada
Caso a busca por um cliente retorne o status `Clientes não encontrados`, o aplicativo permite a abertura da ficha cadastral de forma imediata na linha de frente da portaria.

*   **Travas de Obrigatoriedade:** O layout do formulário Android respeita de forma estrita as flags configuradas na retaguarda do ERP, podendo forçar o preenchimento obrigatório de campos como `CPF`, `RG`, `Telefone` ou `Endereço`.
*   **Expansão de Campos:** O botão **Outras Informações** expande a tela para preenchimento de dados de logradouro completo.
*   **Captura de Imagens:** A interface disponibiliza atalhos nativos para acionamento da câmera do dispositivo móvel, permitindo registrar a **Foto do Cliente** (reconhecimento facial/portaria) e a captura de imagens de documentos (**Frente e Verso**), enviando os arquivos de mídia em tempo real para o banco de dados do retaguarda.

# Mecânica de Validação de Saída (Check-out)
O fluxo de saída atua como a barreira de segurança financeira do estabelecimento, bloqueando a evasão de clientes inadimplentes.

1. No momento em que o cliente se direciona à roleta de saída, o porteiro digita ou bipa o número da comanda no aplicativo e clica em **Check-out**.
2. **Cenário de Bloqueio (Conta Aberta):** Se a comanda ainda possuir consumo pendente ou não tiver passado pelo fluxo de encerramento e faturamento no caixa fixo, o aplicativo intercepta a ação e exibe um alerta vermelho rígido: `Saída não liberada. Conta não finalizada`. A saída é eletronicamente travada.
3. **Cenário de Liberação (Conta Quitada):** Após o cliente efetuar o pagamento da comanda em um terminal de [[Mobile / PDV Android]] ou caixa físico, o operador da portaria repete a consulta. O sistema retornará o status `Saída Liberada. Registre a saída`.
4. O porteiro clica no botão **Registrar Saída**. O sistema altera o status da comanda para `Fechada/Disponível` no banco de dados e conclui a baixa do ciclo do cliente no evento.

# Pontos Críticos e Regras de Negócio

> [!warning] Parametrização da Chave de Entrada e Saída
> O comportamento dos campos de busca do aplicativo é flexível e depende da configuração global do módulo de portaria no retaguarda Windows. É possível definir se o código para a **Entrada (Check-in)** será validado pelo *Código do Ingresso*, *CPF* ou *ID interno*, e se a **Saída (Check-out)** buscará pelo número da *Comanda*, *Pedido* ou *CPF*. A falta de alinhamento entre as mídias físicas entregues aos clientes e essa parametrização impedirá a leitura dos códigos de barras na portaria.

> [!danger] Risco de Fraude por Reutilização de Ingressos em Modos Offline
> Diferente do faturamento varejista que suporta contingência offline, a rotina de portaria exige comunicação síncrona absoluta com o [[Servidor Força de Vendas]]. Caso a rede sem fio (Wi-Fi) da portaria sofra oscilações, o aplicativo móvel não conseguirá computar a baixa do token do ingresso em tempo real. Isso abre uma brecha crítica de segurança onde um mesmo ingresso impresso ou QR Code pode ser bipado em múltiplos smartphones simultaneamente na entrada, permitindo o acesso de pessoas duplicadas com o mesmo bilhete. Em caso de queda de rede, a portaria deve ser paralisada ou direcionada para validação manual via relatórios impressos.
---
id: [CASO-173]
link: https://www.youtube.com/watch?v=3K7ZB_JITHo&t=2s
setor: [Desenvolvimento, Operacional, Financeiro]
modulo: [Integração TEF / POS]
tags: [tef, stone-pos, tef-app, maquininha, meios-de-pagamento, contingência]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Integração TEF UP (TEF App)]]
2. [[#Parametrização Inicial: Usuários e Documentos]]
3. [[#Arquitetura de Comunicação: Servidor Força de Vendas]]
4. [[#Fluxo de Cobrança e Velocidade Transacional]]
5. [[#Gestão de Exceções e Tratamento de Falhas]]
    1. [[#Cancelamento na Maquininha]]
    2. [[#Queda do Servidor Força de Vendas no Momento do Pagamento]]
    3. [[#Cancelamento pelo Retaguarda (Venda Cancelada com Pagamento Aprovado)]]
6. [[#Pontos Críticos e Regras de Negócio]]

# Visão Geral da Integração TEF UP (TEF App)
O recurso **TEF App** (também conhecido como TEF UP) foi desenvolvido para substituir o antigo método de comunicação via *Stone Connect*. A solução nativa visa resolver problemas de cobranças represadas (agarradas) e mitigar a dependência da infraestrutura externa e burocrática da Pagar.me.

Neste novo modelo, a comunicação entre o sistema de retaguarda (PDV/Caixa) e a maquininha Smart POS da Stone ocorre de forma **direta e local**, utilizando exclusivamente a API do [[Servidor Força de Vendas]]. Isso confere ao sistema maior agilidade, autonomia e capacidade de tratar exceções de pagamento (estornos e conciliações) que antes ficavam isoladas no aplicativo do banco.

# Parametrização Inicial: Usuários e Documentos
Para habilitar o novo fluxo de trabalho, o gestor de TI ou o usuário administrador deve realizar dois ajustes primários no sistema:

### 1. Novo Perfil de Vendedor / Operador (Perfil TEF)
Foi inserido um novo escopo de usuário no cadastro de vendedores da retaguarda.
*   Acesse **Cadastros > Vendedores**.
*   Ao cadastrar o usuário que vai operar exclusivamente a maquininha, altere o campo "Tipo de Usuário" para **TEF**.
*   **Comportamento:** Ao logar no aplicativo Android da maquininha com este perfil, o sistema pula o menu principal e é direcionado automaticamente para a tela de `Aguardando Pagamentos...`, transformando o POS em um terminal passivo de recebimento dedicado.

### 2. Configuração do Tipo de Documento Financeiro
*   Acesse **Cadastros > Tipos de Documento / Espécies de Moeda** (ex: Cartão de Crédito).
*   Na aba de integrações de cartão, altere a flag da integração de *Stone Connect* ou *Deep link* para **TEF App**.
*   Ao salvar, o sistema redirecionará automaticamente os comandos de faturamento dessa espécie para o novo serviço de escuta.

# Arquitetura de Comunicação: Servidor Força de Vendas

> [!info] O Papel do Força de Vendas no Fluxo de Cartões
> Diferente do Stone Connect que utilizava URLs externas da adquirente (Webhooks), o TEF App utiliza a conexão contínua de soquete do **Servidor Força de Vendas**. Portanto, é mandatório que o executável deste servidor esteja ativo e rodando na máquina principal do cliente.

*   Se o servidor Força de Vendas for desligado, a maquininha perderá o sinal de escuta instantaneamente e a tela do aplicativo exibirá um alerta vermelho de erro de comunicação com botão para tentar **Reconectar**.

# Fluxo de Cobrança e Velocidade Transacional
A eliminação da rota externa resultou na diminuição da latência das transações.
1. O operador no retaguarda finaliza a venda selecionando a forma de pagamento (Cartão/TEF).
2. O sistema injeta a cobrança na fila local do Servidor Força de Vendas.
3. A maquininha da Stone, que está pingando no servidor local, captura a intenção de cobrança de forma quase imediata e "chama" a tela nativa do cartão.
4. O cliente insere a senha e o cartão. O comprovante é impresso.
5. O aplicativo móvel notifica o servidor e a retaguarda processa a baixa e a transmissão do cupom fiscal.

# Gestão de Exceções e Tratamento de Falhas

A equipe de engenharia implementou recursos avançados de recuperação para as três principais situações de risco que ocorriam na solução antiga:

### 1. Cancelamento na Maquininha
*   **Problema Antigo:** Se o cliente errasse a senha ou cancelasse pelo teclado da Stone, a cobrança entrava em *looping*, reabrindo na tela do POS até que o operador fosse ao PC e cancelasse lá.
*   **Nova Solução:** Ao clicar no botão `Cancelar` na interface da maquininha, o aplicativo mata o processo localmente e notifica o retaguarda, que aborta a escuta e exibe a mensagem de `Pagamento Cancelado`, liberando o caixa para uma nova tentativa imediatamente.

### 2. Queda do Servidor Força de Vendas no Momento do Pagamento
Se a energia do PC principal cair ou o serviço Força de Vendas travar **exatamente após o cliente digitar a senha na maquininha**:
1. O cartão será aprovado pelo banco e a maquininha imprimirá o recibo.
2. Porém, ao tentar devolver o *callback* de sucesso para o ERP, a maquininha não encontrará o servidor, gerando a mensagem: `Cobrança Não Enviada`.
3. **Resolução:** O pagamento fica represado localmente no cache do POS da Stone, travando novas escutas para evitar duplicidades. Quando o servidor no PC for reestabelecido, o operador na maquininha deve clicar em **Enviar Pagamentos**. O *callback* retido será disparado para a retaguarda, baixando o título atrasado e liberando o terminal.

### 3. Cancelamento pelo Retaguarda (Venda Cancelada com Pagamento Aprovado)
Este é o cenário de maior risco de quebra de caixa (*Pagamento Órfão*).
1. A cobrança chega na maquininha.
2. Por algum motivo (demora do cliente), o operador no computador (ERP) cancela a tela do TEF. O ERP desiste da venda.
3. No entanto, o cliente insere o cartão e paga na maquininha na sequência.
4. **Resolução (Conciliação Pendente):** O ERP salva esse pagamento bem-sucedido na tabela de logs financeiros órfãos. Quando o operador tentar passar a próxima venda em cartão (ou refazer a venda original), o sistema interromperá o fluxo com um pop-up de alerta: *`Existe um pagamento efetuado no valor de R$ X. Deseja adicionar esse pagamento à venda atual?`*
5. O operador pode escolher **Sim** (aproveitando o dinheiro do cliente que já caiu na conta para liquidar o cupom reagendado) ou **Não/Ignorar** (caso já tenha feito o estorno direto na maquininha pelo menu administrativo do banco).

# Pontos Críticos e Regras de Negócio

> [!warning] Perda de Controle da Interface (Restrição de SO)
> A partir do momento em que o aplicativo da UP invoca a tela nativa de processamento de cartão (a tela verde de inserção de senha da Stone), o aplicativo perde integralmente o controle sobre o hardware. Não é tecnicamente possível injetar um comando do PC para cancelar a tela da senha remotamente. A responsabilidade de abortar a transação na tela da maquininha cabe sempre ao operador físico do terminal POS.
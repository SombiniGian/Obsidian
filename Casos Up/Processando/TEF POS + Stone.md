---
id: [CASO-174]
link: https://www.youtube.com/watch?v=tQ0DiLPTURc&t=3s&pp=0gcJCUwLAYcqIYzv
setor: [Desenvolvimento, Operacional, Financeiro]
modulo: [Integração TEF / POS]
tags: [tef, stone-pos, stone-connect, maquininha, meios-de-pagamento, tef-app]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Integração TEF POS]]
2. [[#Configuração do Tipo de Documento]]
3. [[#Fluxo de Cobrança no Aplicativo (POS Stone)]]
4. [[#Tratamento de Cancelamentos e Sincronização]]
5. [[#Pontos Críticos e Roadmap de Desenvolvimento]]

# Visão Geral da Integração TEF POS
Devido a instabilidades e interrupções frequentes nos serviços da API do *Stone Connect*, a equipe de engenharia desenvolveu uma alternativa nativa para a comunicação com as maquininhas de cartão da Stone (Smart POS). A nova integração, denominada **TEF App**, elimina a dependência do barramento de comunicação do Stone Connect, realizando o tráfego de dados de cobrança diretamente entre o servidor do ERP e o aplicativo embarcado no terminal de pagamento.

Essa reestruturação arquitetural resultou em uma redução significativa na latência das transações, tornando a exibição da cobrança no visor da maquininha praticamente instantânea e não dependente de rotas de URLs externas.

# Configuração do Tipo de Documento
Para que o faturamento acione o novo gatilho de comunicação, é necessário remapear a rota de integração dos meios de pagamento na retaguarda.

1. Acesse **Cadastros > Tipos de Documento / Espécies de Moeda**.
2. Selecione a espécie de pagamento desejada (ex: `Cartão de Crédito` ou `Cartão de Débito`).
3. No campo de Integração/Gateway, altere a opção legada (como *Deep link* ou *Stone Connect*) para a nova opção: **TEF App**.
4. Salve o cadastro.

# Fluxo de Cobrança no Aplicativo (POS Stone)
O aplicativo Android embarcado na maquininha da Stone atua como um receptor em tempo real das intenções de venda geradas pelos caixas do estabelecimento.

1. No terminal Smart POS, o operador efetua o login no aplicativo mobile da UP Sistemas.
2. Acessa o menu lateral e clica na opção inferior **Pagamento TEF**.
3. O aplicativo entrará no status de `Aguardando Pagamentos...`, ficando em estado de escuta (*listening*) contínua no servidor.
4. Quando uma venda for finalizada no retaguarda ou em um terminal de [[PDV]] utilizando a forma de pagamento configurada para *TEF App*, a requisição de cobrança surgirá imediatamente na tela da maquininha.
5. O operador processa a inserção do cartão ou aproximação e digita a senha.
6. A maquininha imprime o comprovante físico nativo, o aplicativo exibe a notificação de `Pagamento efetuado` e retorna automaticamente à tela de escuta para a próxima cobrança. 
7. Simultaneamente, o ERP no retaguarda recebe o *callback* de liquidação e aciona automaticamente a transmissão da [[NFC-e]] para a SEFAZ.

> [!tip] Automação de Login no POS
> A interface nativa receberá uma *flag* de configuração no cadastro do vendedor/usuário para forçar o aplicativo a abrir diretamente na tela de **Pagamento TEF** logo após o login. Isso suprime a necessidade de navegação manual em menus para os operadores que atuam exclusivamente na função de caixa financeiro.

# Tratamento de Cancelamentos e Sincronização

A nova arquitetura do **TEF App** corrige uma deficiência grave existente no modelo anterior do *Stone Connect* referente ao fluxo de cancelamento de transações que não foram processadas.

### Cancelamento Direto na Maquininha (Fluxo Corrigido)
No antigo ambiente do Stone Connect, se o operador cancelasse a operação através da interface da maquininha (antes da inserção da senha), a cobrança entrava em *looping* e retornava repetidamente para a tela do POS até que fosse ativamente cancelada pelo terminal do ERP. 
* **Novo Comportamento:** Com o TEF App, ao tocar em **Cancelar** na tela da maquininha, o aplicativo mata o processo de escuta instantaneamente e notifica o servidor, abortando a cobrança no retaguarda de forma síncrona com o status de `Pagamento Cancelado`.

# Pontos Críticos e Roadmap de Desenvolvimento

> [!warning] Perda de Controle do Sistema no Cancelamento pelo Retaguarda
> Uma limitação técnica do sistema operacional Android embarcado na Stone é que, uma vez que a tela principal nativa de recebimento de cartão (*Deep Link*) sobrepõe a tela do aplicativo, o software ERP perde o controle da interface.
> 
> * **Risco Financeiro:** Se o operador de caixa cancelar a cobrança na tela do ERP (computador) *depois* que ela já foi despachada e está visível aguardando a senha na maquininha, a Stone continuará permitindo que o cliente insira o cartão e pague. O pagamento será processado na adquirente, mas o pedido no ERP estará baixado/cancelado, resultando em um recebimento "órfão" e inconsistência no fechamento de caixa.

> [!info] Solução de Contingência (Em Roadmap)
> Para solucionar a falta de sincronia gerada por cancelamentos indevidos a partir do retaguarda, o sistema será atualizado com um mecanismo de **Conciliação Manual de TEF**. Caso a maquininha processe um pagamento de uma venda já cancelada no ERP, o gestor financeiro poderá acessar um painel, capturar esse "pagamento órfão" e vinculá-lo a uma nova venda ou emitir a sua respectiva reversão controlada.
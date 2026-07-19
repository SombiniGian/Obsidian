---
id:
  - CASO-153
link: https://www.youtube.com/watch?v=-lnCOQZzxlY
setor:
  - Suporte
  - Desenvolvimento
  - Operacional
modulo:
  - Mobile / Aplicativo Garçom
tags:
  - android
  - restaurante
  - comanda
  - mesa
  - check-out
  - responsividade
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Módulo Móvel Restaurante]]
2. [[#Responsividade e Distribuição Visual (Modo Paisagem)]]
3. [[#Teclado Numérico Nativo Otimizado]]
4. [[#Unificação dos Mapas de Mesas e Comandas]]
5. [[#Atalhos Rápidos de Operação na Home]]
6. [[#Subtotal com Agrupamento Dinâmico de Itens]]
7. [[#Gestão e Controle de Limite de Crédito por Comanda]]
8. [[#Validação de Fluxo de Portaria: Check-in e Check-out]]
9. [[#Regras de Negócio e Pontos Críticos de Falha]]

# Visão Geral do Módulo Móvel Restaurante
O ecossistema móvel voltado para o segmento de food-service recebeu uma reestruturação funcional focada na redução de cliques e agilidade de atendimento para o garçom. As melhorias englobam o redesenho da interface para dispositivos de telas grandes (Tablets), criação de teclados de alta escala para mitigar erros operacionais do sistema operacional, unificação estrutural de regras fiscais de consumos e a portabilidade de travas de segurança financeiras que antes eram restritas ao painel de retaguarda Windows.

# Responsividade e Distribuição Visual (Modo Paisagem)
Visando cenários de operação onde o dispositivo Android fica fixado em totens ou suportes de mesas, o layout foi otimizado para o modo Paisagem (Horizontal). Os blocos visuais e botões de comando foram redistribuídos para aproveitar a área útil de telas de alta resolução, impedindo que os elementos fiquem esticados ou sobrepostos, comportamento observado também na emulação em ambiente Windows.

# Teclado Numérico Nativo Otimizado
Para acelerar a abertura de atendimentos, o sistema altera a forma de digitação de identificadores.

*   **Pré-requisito na Retaguarda:** No executável do [[Servidor Força de Vendas]], a flag **Usar teclado numérico** na seção de mesas e comandas deve estar ativa.
*   **Comportamento:** Ao tocar nos campos de digitação de Mesa ou Comanda, o sistema bloqueia a invocação do teclado alfanumérico padrão do Android. Em seu lugar, abre-se uma janela com botões numéricos expandidos. Caso a numeração utilize letras (ex: Comanda `A10`), a flag deve ser mantida desativada para preservar o teclado padrão do sistema operacional.

# Unificação dos Mapas de Mesas e Comandas
A aplicação móvel espelha a flexibilidade da retaguarda ERP, unificando a visualização gráfica dos consumos. O menu superior permite alternar instantaneamente entre as abas de **Mapa de Mesas** e **Mapa de Comandas**. O garçom visualiza o status de ocupação em tempo real (Disponível, Ocupada, Conta Impressa) de forma síncrona com os caixas fixos.

# Atalhos Rápidos de Operação na Home
Funções críticas de controle de fluxo de atendimento foram portadas diretamente para a tela inicial do aplicativo, dispensando a necessidade de reabrir o pedido do cliente para acioná-las:

1.  **Transferir (Mesa/Comanda):** O garçom digita o identificador de origem na Home e clica em **Transferir**. O aplicativo solicita o número do novo destino e migra a totalidade dos itens e observações de consumo de forma automática no banco.
2.  **Imprimir Conta (Fechamento):** O garçom digita o número da mesa e clica em **Conta**. O comando via API altera o status da mesa para `Liberando` (sinalizando a pré-conta aos demais caixas) e dispara a impressão física do extrato na impressora de produção vinculada.

# Subtotal com Agrupamento Dinâmico de Itens
Durante a permanência do cliente, o garçom pode consultar o andamento da conta por duas visões complementares:
*   **Exibir Detalhes:** Apresenta a ordem cronológica exata dos lançamentos. Se a mesa pediu 5 unidades de `Coca-Cola` em horários distintos, a tela renderizará 5 linhas isoladas.
*   **Subtotal (Nova Opção):** Processa o agrupamento cartesiano do carrinho em tempo de execução. Consolida os dados e exibe apenas uma linha simplificada: `Coca-Cola | Qtd: 5 | Total: R$ X`. Esse formato melhora a conferência rápida de valores junto ao cliente antes do fechamento.

# Gestão e Controle de Limite de Crédito por Comanda
Esta trava de conformidade previne inadimplências em casas noturnas e bares de grande rotatividade, limitando o consumo de comandas individuais ao teto configurado na retaguarda.

*   **Alteração de Teto Remota:** O garçom com privilégios de acesso pode digitar o número da comanda, clicar no botão **Limite** e redefinir o valor (ex: alterar de `R$ 160,00` para `R$ 170,00`) diretamente pelo celular.
*   **Mecanismo de Bloqueio:** Ao tentar lançar um item cujo subtotal force a conta a estourar o limite (ex: Conta atual de R$ 160,00 + prato de R$ 56,00 = R$ 216,00, ultrapassando o teto de R$ 170,00), o aplicativo intercepta a ação, exibe um pop-up de bloqueio rígido e impede a inserção e gravação do pedido.

# Validação de Fluxo de Portaria: Check-in e Check-out
O módulo estende os recursos do [[Controle de Ingressos / Bilheteria]] para portarias de estabelecimentos comerciais. O smartphone Android pode atuar como um terminal de validação de fluxo de pessoas na entrada e saída:

*   **Check-in:** Registra o ingresso do cliente associando a comanda ao seu CPF.
*   **Check-out:** Ao bipar ou digitar a comanda na saída da portaria e clicar em **Checkout**, o aplicativo consulta o barramento financeiro do ERP. Se o cliente tentar sair sem pagar, o sistema reporta o aviso: `Saída não liberada. Conta não finalizada`, orientando a retenção do cliente na roleta.

# Regras de Negócio e Pontos Críticos de Falha

> [!warning] Estorno e Alteração de Limites sem Log de Supervisor
> A concessão de acréscimo de limite de consumo em comandas diretamente pelo aplicativo do garçom deve ser restrita via grupo de permissões de usuários no retaguarda Windows. Liberar essa flag para garçons operacionais sem validação por [[Senha de Liberação Remota]] gera riscos de fraude, permitindo que clientes consumam valores acima da capacidade de quitação sem o conhecimento da gerência.

> [!danger] Latência de Sincronização em Comandas de Balcão e Modos Offline
> Diferente do processo de faturamento do [[Mobile / PDV Android]] tradicional que possui fila de contingência, o aplicativo móvel de restaurante trabalha em modo síncrono absoluto. Caso o Wi-Fi do estabelecimento sofro micro-quedas no momento em que o garçom comanda o fechamento ou a transferência de uma mesa, o aplicativo abortará o processo e exigirá a reedição, pois o banco de dados proíbe o represamento offline de dados de consumo de mesas para evitar duplicidade de comandas físicas.
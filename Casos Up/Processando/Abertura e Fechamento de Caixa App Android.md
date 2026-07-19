---
id:
  - CASO-144
link: https://www.youtube.com/watch?v=e0cxJXNm-xI
setor:
  - Suporte
  - Implementação
  - Operacional
modulo:
  - Mobile / Abertura e Fechamento de Caixa
tags:
  - android
  - frente-de-caixa
  - sangria
  - suprimento
  - força-de-vendas
  - fechamento
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Módulo de Caixa Android]]
2. [[#Pré-requisitos e Vinculação Estrutural no Retaguarda]]
3. [[#Fluxo de Abertura de Caixa e Suprimento Inicial]]
4. [[#Movimentações em Aberto: Sangria e Suprimento]]
5. [[#Consultas e Resumos de Movimentações por Espécie]]
6. [[#Fluxo de Fechamento de Caixa e Sincronização Síncrona]]
7. [[#Pontos Críticos e Regras de Negócio]]

# Visão Geral do Módulo de Caixa Android
O módulo móvel de **Abertura e Fechamento de Caixa** unifica o controle transacional financeiro das frentes de caixa descentralizadas no aplicativo Android (aplicando-se de forma idêntica para perfis de `Garçom`, `Vendedor` ou `PDV`). A rotina gerencia o fluxo de caixa local, permitindo o registro de aportes de capitais, retiradas, auditoria ao vivo de vendas por espécie e a sincronização síncrona dos estados de fechamento com o ERP de retaguarda.

# Pré-requisitos e Vinculação Estrutural no Retaguarda
Para que o controle de caixa seja ativado e isolado por funcionário no aplicativo, as seguintes amarrações devem ser realizadas no ERP Windows:

1.  Acesse o cadastro do usuário/vendedor móvel.
2.  Preencha rigorosamente o campo **Caixa do aplicativo do vendedor**. Esta configuração isola as movimentações de uma estação, garantindo que o `Vendedor A` opere e audite apenas o seu próprio saldo.
3.  **Configuração de Obrigatoriedade (Opcional):** No módulo de caixas do retaguarda, define-se se o sistema exigirá o input de um **Suprimento Inicial** obrigatório ao abrir o caixa e qual o **Tipo de Documento Padrão** (geralmente parametrizado como `Dinheiro`) será imputado nas movimentações automáticas de Sangria e Suprimento.

# Fluxo de Abertura de Caixa e Suprimento Inicial
O aplicativo móvel adota uma postura de flexibilidade controlada na captação de pedidos:

*   **Lançamento Livre:** O sistema **não bloqueia** o garçom ou vendedor de lançar produtos, orçamentos ou abrir comandas caso o caixa esteja fechado.
*   **Bloqueio Rígido no Faturamento:** No momento em que o operador clica no botão **Fechar Conta** ou tenta processar o pagamento final para concluir a venda, o ERP intercepta a ação e dispara o aviso: `Caixa não está aberto. Deseja abrir o caixa?`.
*   **Injeção de Capital (Abertura):** Ao clicar em **Sim**, a tela de abertura é invocada. Se a flag de obrigatoriedade estiver ativa na retaguarda, o aplicativo exigirá o preenchimento do campo **Valor de Suprimento** (ex: `R$ 5,00`). Clique em **Confirmar** para receber o status `Caixa aberto com sucesso` e liberar a tela de faturamento.

# Movimentações em Aberto: Sangria e Suprimento
Com o caixa operacional ativo, o usuário acessa o menu **Caixa** no aplicativo para injetar ou retirar valores do Spooler:

*   **Suprimento (Aporte):** Utilizado para troco adicional inserido no decorrer do expediente.
*   **Sangria (Retirada):** Utilizado para sangrar valores acumulados em cédulas para a tesouraria central (ex: retirada de `R$ 2,00`). O aplicativo deduz o valor do total em dinheiro em tempo real (ex: Reduz o saldo em caixa de `R$ 53,00` para `R$ 51,00`).

# Consultas e Resumos de Movimentações por Espécie
A interface do menu **Caixa** fornece ao operador uma visão consolidada de auditoria rápida antes de efetivar o encerramento do turno:

*   **Painel Consolidado:** Apresenta de forma visual o **Total Vendido**, somado ao montante de **Suprimento** e subtraído pelas linhas de **Sangria** (destacadas em vermelho), exibindo o saldo líquido atual em pátio.
*   **Abertura por Espécie (Broca de Dados):** O operador pode tocar diretamente sobre a linha de uma forma de pagamento na grade para inspecionar os cupons geradores:
    *   Toque em `Dinheiro`: O aplicativo abre uma janela secundária listando todas as vendas líquidas recebidas em papel moeda.
    *   Toque em `Depósito` ou `Cartão`: Lista exclusivamente as transações associadas àquela espécie.

# Fluxo de Fechamento de Caixa e Sincronização Síncrona
Ao encerrar as atividades, o operador executa a conferência cega ou assistida:

1.  Acesse o menu **Caixa** no aplicativo.
2.  **Impressão de Conferência:** O botão **Imprimir** gera um layout térmico de resumo de movimentações contendo a marca d'água superior explicativa `Caixa ainda não foi fechado`, servindo para conferência física de gaveta.
3.  Clique no botão **Fechar Caixa**. O aplicativo dispara a confirmação `Deseja fechar o caixa?`.
4.  Clique em **Sim**.
5.  **Mudança de Status:** O aplicativo processa a baixa, altera o status local para `Fechado` e bloqueia novos faturamentos. A interface retorna ao estado inicial, exibindo os botões de *Abrir Caixa*, *Histórico* e a opção **Imprimir Último Fechamento** (que reemite o cupom consolidado final).
6.  **Handshake com o ERP:** Se o dispositivo móvel estiver conectado à rede local ou internet com o [[Servidor Força de Vendas]] ativo, o status do lote de fechamento migra instantaneamente na retaguarda de `Em Aberto` para `Finalizado`, atualizando o módulo contábil e de tesouraria do ERP automaticamente.

# Pontos Críticos e Regras de Negócio

> [!warning] Turnos e Fechamentos por Períodos Fracionados
> Nesta release tecnológica, o aplicativo móvel respeita estritamente o fechamento bruto por abertura de operador (Caixa por Usuário). O controle refinado de **Turnos Modulares** ou **Fechamento por Turno do Dia** (comum em postos de combustíveis e conveniências de alta rotatividade) deve ser gerenciado de forma manual no retaguarda, pois a interface Android ainda não realiza a quebra fracionada de turnos na mesma sessão de usuário.

> [!danger] Indisponibilidade de Caixa Cego (X / Y de Impressão)
> O aplicativo móvel não possui integração nativa com rotinas de **Caixa Cego** (onde o operador é proibido de ver o saldo do sistema e deve digitar o valor físico que tem na gaveta para o ERP apurar quebras). As informações de totais por espécie ficam expostas ao funcionário na tela do Android. Caso a empresa possua políticas rígidas de compliance de auditoria de caixas, a permissão de acesso ao menu **Caixa** deve ser revogada para usuários operacionais no retaguarda, permitindo que eles apenas faturem e forçando o encerramento pelo supervisor.
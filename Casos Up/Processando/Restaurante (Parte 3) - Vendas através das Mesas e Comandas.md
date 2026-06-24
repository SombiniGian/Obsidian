---
id: [CASO-057]
link: https://www.youtube.com/watch?v=1ePQG1Qz89w
setor: [Suporte, Implantação]
modulo: [Restaurante]
tags:
  - venda-mesa
  - comanda-individual
  - pdv-touch
  - regras-faturamento
data_criacao: 2026-06-24
---

# Restaurante (Parte 3): Fluxo de Vendas através de Mesas e Comandas

Este documento técnico detalha os fluxos operacionais de venda do módulo de **Restaurante**, abordando a unificação de dados com o caixa central, os modos de isolamento de tela e as regras para trabalho exclusivo ou compartilhado entre mesas físicas e comandas eletrônicas.

---

## Sumário
1. [[#Unificação com o Módulo de Vendas Geral]]
2. [[#Parametrização e Modos de Exibição de Tela]]
3. [[#Fluxo de Venda Exclusivo por Mesas]]
4. [[#Fluxo de Venda Exclusivo por Comandas]]
5. [[#Operação Híbrida Múltiplas Comandas por Mesa]]
6. [[#Pontos Críticos e Validações]]

---

## Unificação com o Módulo de Vendas Geral

A arquitetura do sistema foi projetada de forma centralizada. Independentemente do canal de captura do pedido, todas as movimentações financeiras e de estoque convergem para o mesmo banco de dados.

* **Transparência de Módulos:** Um pedido iniciado no mapa de mesas do restaurante é tratado pelo sistema como uma venda padrão em aberto. Ele constará simultaneamente na tela geral de [[Pedidos de Venda]] do ERP.
* **Concorrência:** Não há distinção técnica ou atraso no processamento caso a empresa opere faturamentos simultâneos no **PDV Balcão** e no **Módulo Touch**.

---

## Parametrização e Modos de Exibição de Tela

O sistema permite configurar qual tipo de interface o operador visualizará ao interagir com uma mesa ou comanda.

* **Caminho de Configuração:** Propriedades do **Pedido de Venda**.

### Opções de Inicialização de Tela:
* **Balcão:** Abre a interface clássica de pedido de venda do ERP, focada em digitação rápida por teclado e comandos tradicionais.
* **Controle Restaurante:** Abre o mapa de mesas visual.
* **PDV (Frente de Caixa):** Direciona o clique diretamente para a tela de cupom fiscal simplificada do PDV.

> [!tip] Atalho Dinâmico de Interface (Alt + S)
> Mesmo que o sistema esteja configurado para abrir o formulário clássico, o operador pode alternar em tempo real para a tela simplificada de toque utilizando o comando de teclado **Alt + S**. Este atalho migra o layout instantaneamente para o formato de botões horizontais (*Touch*), mantendo os itens já lançados no carrinho.

---

## Fluxo de Venda Exclusivo por Mesas

Indicado para estabelecimentos que realizam a cobrança unificada por ponto físico de atendimento, desconsiderando cartões individuais.

* **Configuração:** No menu de parâmetros do restaurante, desmarque a flag **Usar Comandas** e mantenha ativa apenas a opção **Usar Mesas**.

### Procedimento de Lançamento e Filtros:
1. No painel visual, as mesas que possuem consumo ativo são realocadas automaticamente para o topo da listagem (frente do mapa) para facilitar o acompanhamento visual do salão.
2. Para abrir uma mesa sem procurá-la visualmente na grade, clique no comando **Incluir**, digite o número correspondente (ex: `30`) e pressione **Enter**.
3. Insira os produtos normalmente através do painel touch, digitação ou leitura de código de barras.
4. Ao clicar em **Gravar/Finalizar** e processar o recebimento financeiro (Dinheiro, Cartão, etc.), a mesa correspondente altera seu status para desocupada e retorna para sua posição original na grade de monitoramento.

---

## Fluxo de Venda Exclusivo por Comandas

Recomendado para bares, casas noturnas ou choperias onde o cliente transita pelo estabelecimento portando um cartão de identificação numérico e consome de forma individualizada.

* **Configuração:** Ative a flag **Usar Comandas** e desative o parâmetro de mesas nos menus de configuração técnica.

### Comportamento da Interface:
* A tela deixa de exibir a disposição física das mesas e passa a listar em formato de grade sequencial estritamente as **Comandas que possuem Saldo em Aberto**.
* Cada linha exibe o número do cartão e o valor parcial acumulado.
* Para retificar ou adicionar itens a uma conta ativa, o operador clica no botão **Alterar** e digite o número do cartão para abrir o carrinho correspondente.

---

## Operação Híbrida: Múltiplas Comandas por Mesa

Adequado para restaurantes de grande porte onde grupos de clientes compartilham o mesmo espaço físico (mesa), mas exigem o fechamento e controle de contas segregados.

* **Configuração:** Mantenha **ambas as flags ativas** nos parâmetros gerenciais do restaurante.

> [!info] Regra de Multiplicidade
> O banco de dados do sistema permite a coexistência de N comandas vinculadas ao mesmo identificador de mesa de forma simultânea. É viável ter, por exemplo, a `Mesa 03` associada à `Comanda 789` e, na linha inferior da grade, a mesma `Mesa 03` associada à `Comanda 781`.

### Fluxo de Alteração Híbrida:
Ao clicar no comando geral de **Alterar** em um cenário híbrido, o sistema abrirá um formulário de dupla validação, exigindo do operador a inserção sequencial do **Número da Mesa** e, em seguida, o **Número da Comanda** para garantir o direcionamento correto do item.

---

## Pontos Críticos e Validações

> [!warning] Riscos de Duplicidade e Conflito de Cadastro
> 1. **Reabertura de Comanda Ativa:** Se o sistema estiver configurado no modo híbrido e um garçom tentar abrir um cartão numérico (comanda) que já possui itens pendentes em outra mesa, o sistema bloqueará a operação ou emitirá um alerta técnico para evitar a fusão acidental de contas de clientes distintos.
> 2. **Configuração Incorreta de Preço Flexível:** Conforme observado na operação de lançamento, se o produto estiver com a flag de alteração de preço ativa na sua ficha cadastral, o sistema abrirá um pop-up de edição manual a cada clique no touch, reduzindo a velocidade do atendimento e abrindo margem para erros de digitação por parte do garçom. Certifique-se de travar os preços de tabela para o módulo de restaurante.


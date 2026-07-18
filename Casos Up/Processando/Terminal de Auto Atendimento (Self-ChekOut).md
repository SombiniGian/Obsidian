---
id: CASO-001
link: https://www.youtube.com/watch?v=T7sw506c4SE
setor: Desenvolvimento
modulo: Ponto de Venda / Autoatendimento
tags: [self-checkout, pdv, automacao-comercial, tef, pix]
data_criacao: 2026-07-18
---

## Sumário
- [[#1. Visão Geral do Módulo]]
- [[#2. Configuração e Pré-requisitos]]
- [[#3. Fluxo de Utilização (Jornada do Cliente)]]
- [[#4. Métodos de Pagamento Suportados]]
- [[#5. Integrações de Hardware e Prevenção de Falhas]]

## 1. Visão Geral do Módulo

O módulo de **Terminal de Autoatendimento** (Self-Checkout) foi arquitetado para permitir que o consumidor final realize a bipagem, a pesagem e o pagamento de suas próprias compras de maneira autônoma, através de uma interface otimizada para telas sensíveis ao toque (touchscreen). 

> [!info] Objetivo de Negócio
> O recurso visa reduzir atritos no fluxo de caixa (filas) e otimizar os custos operacionais do estabelecimento, descentralizando o processo de registro de vendas e repassando o controle da interface de atendimento para o cliente.

## 2. Configuração e Pré-requisitos

Para que a estação de trabalho inicie e opere exclusivamente no modo de autoatendimento, parâmetros específicos precisam ser ajustados no sistema de retaguarda.

1. Acesse as configurações atreladas ao **Pedido de Venda**.
2. Localize e ative a flag de configuração de **Autoatendimento**.
3. Clique em **Gravar**. A partir desta alteração, ao solicitar a inclusão de um novo pedido, a aplicação carregará automaticamente a interface bloqueada e focada no autoatendimento.

> [!warning] Atenção à Parametrização de Tipos de Documento
> No menu **Tipo de Documento**, o gestor deve vincular *apenas* modalidades eletrônicas (Cartão de Crédito, Cartão de Débito, PIX) à estação de autoatendimento. O recebimento em dinheiro em espécie deve ser bloqueado nessa interface, uma vez que terminais de autoatendimento padrão não possuem hardware (dispensadores) para devolução de troco.

## 3. Fluxo de Utilização (Jornada do Cliente)

A interface permanece em modo de espera, orientando o cliente a "tocar para passar sua compra". O fluxo de operação ocorre da seguinte maneira:

1. **Inserção de Itens:**
   - **Por Leitor de Código de Barras:** Quando o cliente passa um produto no scanner, o sistema intercepta o código, identifica o produto e levanta uma janela de confirmação para ajuste de quantidade. O cliente valida clicando em **Confirmar**.
   - **Por Navegação Visual:** Para itens não etiquetados, o cliente pode clicar no menu superior de **Grupos** (ex: Hortifruti, Padaria) e escolher manualmente o item desejado.

2. **Captura de Peso:**
   - Caso o item selecionado exija pesagem, a tela ficará em estado de espera ("Aguardando Peso"), realizando a leitura direta da [[Balança Eletrônica]] conectada à porta serial/USB.

3. **Identificação Fiscal (Opcional):**
   - Antes do pagamento, há uma função disponível na tela para o cliente informar o seu CPF. O dado é capturado e injetado diretamente no XML da [[Nota Fiscal Eletrônica]].

4. **Finalização:** 
   - Ao concluir a adição de todos os itens, o cliente clica no botão **Efetuar Pagamentos** para seguir para o fechamento.

## 4. Métodos de Pagamento Suportados

A tela de fechamento apresenta apenas as opções mapeadas nos pré-requisitos, acionando de forma assíncrona as respectivas APIs e middlewares de pagamento.

### Cartões de Crédito e Débito via [[TEF]]
- O software possui integração nativa com os principais gerenciadores de TEF (ex: **GetNet**, **PayGo**, **SiTef**).
- O cliente clica na opção do cartão desejado, e o sistema envia o payload de cobrança diretamente ao PinPad.
- Uma vez que o cliente conclui a transação no dispositivo físico (PinPad), o terminal consome o retorno positivo, emite a via fiscal e imprime os comprovantes, liberando a tela para a próxima venda sem intervenção manual.

### PIX Dinâmico
- O cliente clica em **Pagamento PIX**.
- O sistema renderiza imediatamente um QR Code dinâmico na tela.
- O cliente escaneia o código pelo aplicativo de sua instituição financeira.
- > [!tip] Dica de UX
  > A validação do pagamento (webhook ou polling) ocorre em tempo real. O sistema baixa a transação no milissegundo em que o banco confirma, indo direto para a etapa de emissão, garantindo alta fluidez.

## 5. Integrações de Hardware e Prevenção de Falhas

Um terminal de self-checkout robusto depende da estabilidade da comunicação com seus periféricos periféricos seriais e USB.

- **Scanner:** Responsável por agilizar o tempo de permanência do cliente na ilha.
- **Balança:** Transmite a carga via protocolo de comunicação contínua e a interface fica bloqueada até estabilizar a string de peso.
- **Impressora de Cupons:** Responsável pela emissão do comprovante do [[TEF]] e DANFE da [[Nota Fiscal]]. 

> [!warning] Ponto Crítico de Falha - Drivers de Impressão
> É estritamente obrigatório que a impressão esteja parametrizada no modo *Silent/Direct Print*. Se o sistema invocar a caixa de diálogo do Windows spooler (solicitando "escolher impressora"), o fluxo autônomo será quebrado e o terminal ficará travado esperando o clique de um mouse que o cliente final não possui, demandando suporte técnico local.
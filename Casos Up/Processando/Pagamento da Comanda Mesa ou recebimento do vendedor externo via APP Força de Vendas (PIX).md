---
id: [CASO-001]
link: https://www.youtube.com/watch?v=zQ2AfOU1J54
setor: Vendas e Atendimento
modulo: Força de Vendas / PDV Mobile
tags: [pix, pagamento, garçom, mobile, nfc-e, psp, automacao-comercial]
data_criacao: 2026-07-18
---

## Índice
1. [[#Visão Geral e Propósito]]
2. [[#Regras de Negócio e Validações]]
3. [[#Fluxo de Execução Operacional]]
4. [[#Integração de Caixa e Fiscal]]
5. [[#Mapeamento de Erros e Pontos Críticos]]

---

## Visão Geral e Propósito

A atualização no aplicativo de `[[Força de Vendas]]` (utilizado por garçons e vendedores externos) introduz a capacidade de finalizar vendas e liquidar pagamentos de `[[Comanda]]` ou Mesa diretamente no dispositivo móvel. 

O principal avanço arquitetônico é a geração de cobranças `[[PIX]]` dinâmicas na tela do aplicativo, integradas diretamente com o `[[PSP]]` (Provedor de Serviços de Pagamento). Isso descentraliza o fluxo de pagamento do caixa físico, otimizando o tempo de atendimento.

> [!info] Alteração de Interface (UI/UX)
> O botão anterior focado apenas em *Encerrar* (que mudava o status da mesa para azul no `[[Retaguarda]]` e imprimia uma prévia) foi substituído por **Imprimir conta**, e um novo botão **Fechar conta** foi introduzido para invocar a tela de liquidação financeira.

---

## Regras de Negócio e Validações

### 1. Pagamentos Múltiplos e Rateio
O sistema permite o registro de múltiplos tipos de documentos na mesma transação financeira (ex.: divisão da conta entre Dinheiro e PIX). O fluxo de cálculo de troco ou saldo devedor reage dinamicamente aos lançamentos.

### 2. Estratégia de Polling de Pagamento (PIX)
Para evitar sobrecarga no servidor de pagamentos e consumo excessivo de rede, o aplicativo adota um modelo de **verificação assíncrona sob demanda**.

> [!tip] Boa Prática de Rede e Performance
> O sistema **não** realiza requisições de consulta (polling automático via timer) para verificar se o PIX foi liquidado. A responsabilidade da verificação é delegada ao usuário (vendedor/garçom) através da ação explícita de clicar em **Consultar**. 

### 3. Gerenciamento de Estado da Cobrança
- **Geração:** Ao selecionar PIX, a cobrança é instanciada no servidor e o QR Code é exibido.
- **Cancelamento:** Se o cliente desistir da forma de pagamento, clicar em **Cancelar** inativa imediatamente o payload da cobrança no servidor, permitindo o uso de outro documento.
- **Retenção de Estado:** Se o usuário sair da tela de cobrança sem confirmar o pagamento, a cobrança adquire status "em aberto" e a interface indica pendência visualmente (em vermelho).

---

## Fluxo de Execução Operacional

O procedimento padrão para liquidação e liberação de uma mesa/comanda obedece ao seguinte pipeline:

1. **Acesso e Detalhamento:**
   - Acessar a mesa ativa (ex.: Mesa 51).
   - Clicar em **Exibir Detalhes** para visualizar os itens da comanda.
2. **Invocação do Checkout:**
   - Acionar o botão **Fechar conta**.
3. **Lançamento Financeiro:**
   - Selecionar o tipo de documento (Dinheiro, Cartão, PIX).
   - *Atalho:* Utilizar o botão de finalização rápida para abater o valor total em Dinheiro.
   - Para pagamentos híbridos, lançar as frações (ex.: R$ 0,05 em Dinheiro e R$ 0,95 no PIX).
4. **Processamento do PIX:**
   - Ao selecionar a forma de pagamento PIX, a tela exibe o QR Code dinâmico.
   - O cliente realiza o escaneamento e efetua a transação no seu aplicativo bancário.
5. **Validação e Conclusão:**
   - Após a confirmação do cliente, o vendedor clica no botão **Consultar**.
   - O sistema valida a transação contra a API do `[[PSP]]` e altera o status para *Salvo com Sucesso*.

---

## Integração de Caixa e Fiscal

A finalização do pedido oferece duas rotas de persistência e emissão documental:

### Rota A: Botão "Salvar"
- **Comportamento:** O pedido é baixado no servidor e a mesa é liberada.
- **Impressão:** O cupom não fiscal ou recibo de conferência é enviado para impressão automática no terminal do caixa central (físico).

### Rota B: Botão "Emitir"
- **Comportamento:** Inicia o processo de faturamento fiscal diretamente pelo client mobile.
- **Emissão:** O sistema gera o documento fiscal (ex.: `[[NFC-e]]`), autoriza junto à SEFAZ e renderiza o DANFE na tela.
- **Distribuição:** É possível realizar a impressão local via impressora Bluetooth pareada ao mobile, ou acionar o compartilhamento digital (PDF via WhatsApp, e-mail, etc).

> [!info] Apropriação Financeira (Caixas Individuais)
> As transações processadas via mobile respeitam o centro de custo do operador. Valores recebidos em dinheiro ou conciliados via PIX são direcionados ao controle de `[[Caixa]]` específico do usuário autenticado (ex.: Caixa 2 - Garçom A), garantindo auditoria correta no fechamento de turno.

---

## Mapeamento de Erros e Pontos Críticos

Para garantir a consistência do banco de dados e evitar fraudes ou perdas de sincronia, o sistema implementa hard-stops (bloqueios) nas seguintes situações:

> [!warning] Validação de Envio de Pedido com PIX Pendente
> **Cenário:** O operador gerou um QR Code PIX, retornou à tela de pedidos sem validar o pagamento e tentou salvar a venda.
> **Comportamento do Sistema:** O evento de `Submit` é bloqueado na camada de validação.
> **Retorno em Tela:** Exceção levantada com a mensagem: `"Existe cobrança PIX não confirmada"`.
> **Resolução:** O usuário deve localizar a forma de pagamento pendente na tela, reabrir os detalhes e clicar em **Consultar** para confirmar o recebimento, ou **Cancelar** para invalidar a intenção.
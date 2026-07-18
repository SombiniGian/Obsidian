---
id: CASO-001
link: https://www.youtube.com/watch?v=gJiw7KHctfc
setor: Vendas
modulo: Aplicativo Força de Vendas
tags: [nota-fiscal, faturamento, mobile, erp, danfe, boletos]
data_criacao: 2026-07-18
---

# Sumário
- [[#Visão Geral]]
- [[#Configuração de Pagamento Rápido]]
- [[#Fluxo de Faturamento e Emissão de Nota Fiscal]]
- [[#Geração e Compartilhamento de Documentos (DANFE e Boletos)]]
- [[#Configurações de Impressão no Servidor (ERP)]]

---

## Visão Geral

Este documento descreve as diretrizes técnicas e operacionais para a emissão de [[Nota Fiscal]] e a execução do processo de [[Faturamento]] diretamente pelo aplicativo mobile de **Força de Vendas**. O fluxo abrange desde a finalização do pedido, configuração de atalhos de pagamento, até a comunicação sincronizada com o [[Servidor]] central para geração de documentos fiscais e cobranças (Boletos).

> [!info] Informação
> A funcionalidade de emissão de notas fiscais mobile exige que o serviço de retaguarda (Servidor) esteja ativo e em comunicação constante com o aplicativo para validar e autorizar as transações junto à SEFAZ.

---

## Configuração de Pagamento Rápido

Para agilizar o fluxo de checkout durante uma venda em campo, o sistema permite a definição de um tipo de documento padrão (ex: Dinheiro). 

1. Acesse a tela de **Faturamento**.
2. No campo de tipo de documento, pressione e segure o registro desejado.
3. Esta ação abrirá a tela de configuração, permitindo marcar a opção de **Venda Rápida**.
4. Uma vez configurado, os próximos faturamentos carregarão automaticamente a forma de pagamento definida, eliminando a necessidade de seleção manual repetitiva.

> [!tip] Dica
> O uso do recurso de Venda Rápida é recomendado para operações de pronta-entrega onde o fluxo de recebimento em espécie é predominante.

---

## Fluxo de Faturamento e Emissão de Nota Fiscal

Ao concluir a inserção dos itens no pedido, o usuário é direcionado para a rotina de faturamento, onde as regras de negócio de finalização são aplicadas.

Existem três ações principais no momento de concluir a operação:

- **Salvar:** Mantém o pedido agrupado e com status "Faturado" localmente no dispositivo. O pedido *não* é sincronizado imediatamente com o servidor e permanece aberto para possíveis edições.
- **Enviar Pedido:** Transmite o pacote de dados (JSON/Payload) do pedido para o [[Servidor]]. O pedido é fechado, mas o documento fiscal não é gerado automaticamente.
- **Emitir Nota Fiscal:** Ação consolidada. Ao acionar este botão, o aplicativo dispara de forma sequencial o envio do pedido e, imediatamente após o retorno de sucesso do servidor, solicita a emissão da NF-e/NFC-e.

> [!warning] Atenção
> O comando **Emitir Nota Fiscal** aciona a sincronização obrigatória. Caso haja falha de conectividade ou indisponibilidade do servidor no momento do envio, o sistema deve registrar a exceção e reter o pedido localmente até o restabelecimento da rede.

---

## Geração e Compartilhamento de Documentos (DANFE e Boletos)

Após a comunicação bem-sucedida de emissão fiscal com o servidor, o aplicativo gerencia o retorno dos documentos.

### Visualização do DANFE
Uma vez autorizada, a [[DANFE]] é renderizada diretamente na tela do aplicativo.
- O usuário pode utilizar os botões de ação localizados no rodapé para **Compartilhar** (via WhatsApp, E-mail) ou **Imprimir** o documento via impressora térmica Bluetooth pareada.
- **Reimpressão:** Para visualizar a nota posteriormente, basta retornar aos detalhes do pedido e navegar até **Opções > Nota Fiscal**.

### Faturamento com Boletos
Se o pedido for faturado utilizando a forma de pagamento "Boleto", o sistema executará um fluxo de interface fracionado:
1. Após clicar em **Emitir Nota Fiscal**, a tela inicial de retorno apresentará primeiramente o(s) **Boleto(s)** gerado(s).
2. O usuário poderá compartilhar ou imprimir as vias de cobrança.
3. Ao fechar a visualização do boleto, o aplicativo exibirá a [[DANFE]] sequencialmente.
4. Cópias dos boletos podem ser recuperadas posteriormente através do menu **Opções > Boletos**.

---

## Configurações de Impressão no Servidor (ERP)

A flexibilidade de impressão mobile exige configurações de layout parametrizadas no retaguarda, evitando que formatos incompatíveis sejam enviados para as impressoras portáteis dos vendedores.

A configuração de layouts e relatórios não é global, mas sim atrelada ao [[Cadastro de Vendedor]].

### Procedimento de Parametrização:
1. No ERP, acesse o **Cadastro de Vendedor**.
2. Localize a seção de parametrização de relatórios/impressão.
3. Vincule o layout específico (gerado via gerador de relatórios) compatível com a largura e o modelo da impressora que aquele vendedor em particular utiliza em campo.

> [!info] Informação
> Esta arquitetura assegura que, ao solicitar a impressão do DANFE ou Boleto, a API de retaguarda empacote os dados utilizando o layout correto, prevenindo quebra de formatação ou dados truncados em diferentes hardwares de campo.
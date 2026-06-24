---
id: CASO-027
link: https://www.youtube.com/watch?v=QbvBA4qiOMY
setor: Recebimento, Estoque, Comercial
modulo: Controle de Estoque e Vendas
tags:
  - controle-de-lotes
  - numero-de-serie
  - xml-entrada
  - rastreabilidade
  - upsystem
data_criacao: 2026-06-24
---

# Fluxo de Compra e Venda com Controle de Lote e Série

Este documento técnico descreve as rotinas de entrada e saída de mercadorias utilizando a ferramenta de **Controle de Lotes e Números de Série** no sistema [[UpSystem]]. O módulo visa garantir a rastreabilidade total do produto, desde o recebimento fiscal (importação de XML) até a impressão do documento de venda e controle de termos de garantia.

---

## Sumário
1. [[#1. Entrada de Mercadorias e Vínculo de Lotes via XML]]
2. [[#2. Rastreabilidade no Cadastro do Produto]]
3. [[#3. Movimentação de Saída e Escolha do Lote na Venda]]
4. [[#4. Impressão do Comprovante e Controle de Garantia]]

---

## 1. Entrada de Mercadorias e Vínculo de Lotes via XML

A alimentação do estoque controlado por lote ou número de série inicia-se no recebimento fiscal, de forma automatizada por meio da importação do arquivo digital da nota do fornecedor `[00:00:06]`.

1. Acesse o menu de **Nota Fiscal Recebida** e clique para importar o arquivo **XML** `[00:00:11]`.
2. Após o sistema correlacionar os itens da nota com o estoque interno, acesse a aba específica chamada **Lotes** `[00:00:41]`.
3. Para cada produto importado, o operador deve especificar o lote correspondente:
   - **Caso de Lotes de Fabricação:** Informe o identificador do lote e associe a quantidade total adquirida (ex: 50 unidades) `[00:00:46]`.
   - **Caso de Números de Série (ex: Smartphones):** O operador deverá lançar individualmente os identificadores de série, vinculando a quantidade fracionada de 1 para cada registro de série exclusivo `[00:00:53]`.
4. O campo **Código do Fornecedor** (opcional) pode ser preenchido ao lado do número do lote para servir de indexador de busca rápida em consultas futuras `[00:01:01]`.
5. Conclua o recebimento para dar entrada física das quantidades segregadas no estoque `[00:01:32]`.

---

## 2. Rastreabilidade no Cadastro do Produto

Uma vez dada a entrada, o histórico de cada lote fica gravado de forma vitalícia no banco de dados, acessível diretamente pela ficha técnica do item `[00:01:37]`.

* Ao abrir o **Cadastro do Produto** e navegar até a aba **Lotes**, o sistema exibe um painel dividido em duas partes `[00:01:45]`:
  * **Painel Superior:** Exibe a listagem de todos os lotes criados para o item, apresentando de forma direta o **Saldo Atual de Estoque** específico daquele lote `[00:01:54]`.
  * **Painel Inferior:** Exibe a auditoria de **Movimentações do Lote**, registrando o histórico de entradas por notas fiscais, saídas por vendas, datas e operadores responsáveis `[00:01:58]`.

---

## 3. Movimentação de Saída e Escolha do Lote na Venda

No momento da venda, o sistema obriga o operador a determinar de qual lote a mercadoria será baixada física e digitalmente, evitando furos de inventário `[00:02:08]`.

![[Pasted image 20260624154744.png]]
1. Na tela de **Venda / Pedido**, ao bipar ou selecionar um produto configurado com esta diretriz, o ERP abre uma janela assistente de lotes `[00:02:08]`.
2. O assistente exibe o saldo disponível em cada lote e traz em colunas o **Nome do Fornecedor** e o **Código do Fornecedor** originais da entrada para orientar o vendedor `[00:02:18]`. 
3. O operador pode localizar o lote digitando o número dele, o código do fornecedor ou o próprio nome do fabricante no campo de pesquisa rápida `[00:02:29]`. 
4. Selecione o lote desejado, insira a quantidade que será vendida e confirme a inclusão no item de pedido `[00:02:41]`.
--- ## 4. Impressão do Comprovante e Controle de Garantia Após a finalização do pedido de venda, o identificador do lote ou o número de série é impresso de forma nativa no corpo do documento de saída `[00:03:06]`. * **Layout de Impressão:** O número do lote/série é apresentado de forma concatenada junto ao código e descrição do produto (ex: *PRODUTO X - LOTE: 1010*) `[00:03:12]`. * **Vínculo com Assistência e Garantia:** A exibição explícita do identificador no comprovante impresso serve como salvaguarda jurídica e comercial para a empresa. Em caso de troca ou acionamento de assistência técnica, o atendente valida se o número impresso no documento condiz com o produto físico devolvido, atestando o prazo de garantia (ex: garantia de 30 dias mediante apresentação deste documento) `[00:03:20]`.
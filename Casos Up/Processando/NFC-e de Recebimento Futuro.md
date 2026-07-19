
---
id: [CASO-177]
link: https://www.youtube.com/watch?v=Igt7y_i3Ips
setor: [Suporte, Faturamento, Fiscal]
modulo: [PDV / NFC-e / Recebimento Futuro]
tags: [nfc-e, recebimento-futuro, decreto-rs, meios-de-pagamento, tef, pix]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Decreto de Vinculação de Meios de Pagamento]]
2. [[#Pré-requisitos e Cadastro do Produto de Repasse]]
3. [[#Parametrização da Natureza de Operação Especial]]
4. [[#Vínculo do Produto no Tipo de Documento e Regras do Borderô]]
5. [[#Fluxo Operacional: Baixa de Título no Caixa e Transmissão da NFC-e]]
6. [[#Pontos Críticos e Regras de Validação Rejeições]]

# Visão Geral do Decreto de Vinculação de Meios de Pagamento
Esta documentação aborda a reengenharia fiscal implementada no sistema para atender às exigências do decreto instituído pela Secretaria da Fazenda do Estado do Rio Grande do Sul (SEFAZ-RS), focado na vinculação obrigatória entre o comprovante de pagamento eletrônico e o documento fiscal de venda. 

### O Problema Comercial do Fluxo Prévio
Sob a legislação vigente, transações pagas por meios eletrônicos instantâneos ou magnéticos ([[TEF]], Cartões e Pix) exigem que a impressora do ponto de venda emita simultaneamente o comprovante financeiro e a **NFC-e** contendo as tags de pagamento preenchidas. No entanto, um gargalo operacional ocorria em vendas a prazo na modalidade crediário/crediário próprio:
1. A mercadoria saía com uma NFC-e emitida sob a modalidade "A Prazo" (Sem pagamento eletrônico imediato).
2. Dias depois, o cliente retornava ao estabelecimento comercial e quitava as parcelas em aberto utilizando um cartão de crédito, cartão de débito ou Pix na máquina da loja.
3. O cruzamento de dados da SEFAZ identificava a entrada de recurso financeiro eletrônico na subconta da empresa sem o correspondente cupom fiscal emitido naquele exato instante, gerando penalidades fiscais.

### A Solução por Duplo Documento Fiscal
A rotina de **NFC-e de Recebimento Futuro** equaciona essa divergência. A venda original tramita e consome o estoque normalmente. No momento da baixa financeira posterior, caso o operador utilize um meio eletrônico, o sistema gera de forma automática uma nova NFC-e de serviço financeiro/repasse, atrelando os metadados da transação eletrônica ao fisco para fins de conformidade legal.

# Pré-requisitos e Cadastro do Produto de Repasse
Para habilitar a emissão do cupom no ato do recebimento, é mandatório criar um registro de produto virtual que servirá de lastro para o XML.

### Passos para Cadastro do Item:
1. Acesse o menu **Cadastros > Produtos** e clique em **Incluir**.
2. No campo **Descrição**, defina um termo alinhado com a contabilidade do cliente (ex: `Pagamento Futuro` ou `Recebimento de Título Crediário`).
3. Defina a **Unidade de Medida** padrão como `UN`.
4. **Regras Fiscais Obrigatórias (Decreto RS):**
   * **CFOP Interno:** Deve ser obrigatoriamente `5.949` (Outra saída de mercadoria ou prestação de serviço não especificado).
   * **Regime Simples Nacional:** Configure o **CSOSN** como `900`.
   * **Regime Normal (Lucro Presumido/Real):** Configure o **CST de ICMS** como `90`.
   * **Código de Benefício Fiscal:** Preencha rigorosamente com o código `RS052999` (especificado no layout do decreto do RS).

# Parametrização da Natureza de Operação Especial
Paralelamente ao produto, uma Natureza de Operação exclusiva deve ser estruturada para conduzir o comportamento do faturamento no borderô.

1. Acesse **Cadastros > Naturezas de Operação**.
2. Crie um registro (ex: `Pagamento e Parcelamento Futuro`).
3. Defina o **Modelo do Documento** como `65` (Nota Fiscal de Consumidor Eletrônica - NFC-e).
4. Informe o **CFOP** correspondente `5.949`.
5. Ative a flag **Gera Financeiro** e marque a opção para **Imprimir o Financeiro na Nota**. Esta instrução assegura que a amarração das duplicatas liquidadas seja injetada nas tags do arquivo XML transmitido à SEFAZ.

> [!info] Exceção Estrutural de Validação da SEFAZ
> Por padrão padrão, servidores da SEFAZ de outros estados rejeitam a emissão de NFC-e (Modelo 65) contendo o CFOP `5.949`. A SEFAZ-RS abriu uma exceção de validação técnica em seu motor de recepção de notas exclusivamente para dar suporte a este fluxo de conformidade de meios de pagamento eletrônicos.

# Vínculo do Produto no Tipo de Documento e Regras do Borderô
Após a criação das entidades bases, deve-se apontar ao sistema quais formas de pagamento eletrônico acionarão o gatilho de emissão.

### 1. Amarração por Tipo de Documento
* Acesse **Cadastros > Tipos de Documento / Espécies de Moeda** e localize os cadastros de `Pix`, `Cartão de Crédito` e `TEF`.
* Na guia de configurações adicionais de faturamento, localize o campo **Produto de Repasse / Pagamento Futuro** e selecione o item cadastrado anteriormente (`Pagamento Futuro`).

### 2. Parametrização Global do Borderô
* Acesse a tela de **Configurações do Sistema > Borderô de Recebimento**.
* No campo **Operação de Pagamento Eletrônico**, vincule a Natureza de Operação especial estruturada na etapa anterior (`Pagamento e Parcelamento Futuro`).

# Fluxo Operacional: Baixa de Título no Caixa e Transmissão da NFC-e

Com as amarrações consolidadas, o fluxo operacional no caixa torna-se transparente e automatizado para o operador.

```

[Módulo Contas a Receber] -> Selecionar Título do Cliente -> Clicar em Receber

|

v

[Selecionar Forma de Pagamento Eletrônica: Ex: Pix / Cartão]

|

v

[Clicar em Gravar/Salvar Borderô]

|

v

[Sistema dispara handshake e transmite NFC-e em Background]

````

### Comportamento Estrutural do Documento Impresso (Danfe NFC-e):
Ao validar a transação eletrônica, o sistema invoca a API de mensageria fiscal, transmitindo a NFC-e. Na Danfe emitida, o sistema insere de forma automática um bloco de **Informações Complementares / Observações do Fisco** contendo o detalhamento da conciliação do título:

```ini
# Conteúdo impresso automaticamente no corpo da NFC-e de Repasse
Título Liquidado: FAT-10723/01
Data de Vencimento Original: 15/07/2026
Valor Parcial/Total Quitado: R$ 85,00
NFC-e Originária da Venda: 001.000.543.210
````

> [!tip] Recebimentos Avulsos Manuais
> 
> Se a baixa no contas a receber corresponder a um lançamento financeiro manual avulso (uma entrada de recurso retroativa lançada em conta que não possua origem em um Pedido de Venda/Nota Fiscal), o sistema emitirá a NFC-e do pagamento eletrônico normalmente para cumprir o decreto, porém omitirá a linha com o número da nota fiscal de origem no bloco de observações, mantendo a integridade do XML.

# Pontos Críticos e Regras de Validação Rejeições

> [!warning] Comportamento Divergente na Baixa em Dinheiro
> 
> Caso o cliente realize o pagamento do crediário utilizando papel-moeda (**Dinheiro**), o operador selecionará a espécie correspondente no borderô. Como a moeda _Dinheiro_ não possui (e não deve possuir) um produto de repasse configurado em seu cadastro, o sistema processará a baixa do contas a receber de forma convencional no [[Financeiro / Contas a Receber]] e encerrará o fluxo **sem emitir nenhum cupom fiscal**, visto que transações em espécie estão fora do escopo do decreto de vinculação de pagamentos eletrônicos.

> [!danger] Rejeição por Omissão do Código de Benefício Fiscal (RS052999)
> 
> Se o cadastro do produto de pagamento futuro for realizado de forma incompleta, esquecendo-se de preencher o campo **Cód. Benefício Fiscal** na aba tributária, a SEFAZ-RS rejeitará o lote de transmissão instantaneamente retornando o erro: _Rejeição: Código de Benefício Fiscal não informado para CST/CSOSN_. Certifique-se de que a tag está preenchida antes de liberar os caixas para operação.

```
http://googleusercontent.com/youtube_content/1
```
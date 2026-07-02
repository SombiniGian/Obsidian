---
id: CASO-033
link: https://www.youtube.com/watch?v=pTcujjfK-l0&t=384s
setor: Suporte, Faturamento, Desenvolvimento
modulo: Frente de Caixa / PDV
tags:
  - nfce
  - emissao-fiscal
  - tratamento-de-erros
  - sefaz
  - regras-de-negocio
data_criacao: 2026-06-24
---

# Documentação Técnica: Emissão de NFC-e, Tratamento de Rejeições SEFAZ e Regras de Vínculo

Esta documentação detalha a arquitetura de funcionamento do fluxo de vendas e transmissão de Nota Fiscal de Consumidor Eletrônica ([[NFC-e]]) no PDV, explicitando a independência entre o registro comercial (Venda) e o registro fiscal (Nota), o tratamento de erros da [[SEFAZ]] e as regras de cancelamento e estorno.

---

## Sumário
1. [[#1. Separação Arquitetural: Venda vs. Nota Fiscal]]
2. [[#2. Fluxo Prático de Emissão e Regra de Venda a Prazo]]
3. [[#3. Tratamento de Exceções e Rejeições da SEFAZ]]
4. [[#4. Fluxo de Contingência e Correção Manual de Notas]]
5. [[#5. Estorno de Faturamento e Duplicidade de Vínculos]]

---

## 1. Separação Arquitetural: Venda vs. Nota Fiscal

O ERP adota um modelo descentralizado de persistência onde a entidade comercial e a entidade fiscal coexistem de forma independente no banco de dados.

* **Venda (Pedido):** Representa a baixa física de estoque, a comissão do vendedor e o fechamento do caixa gerencial (fluxo financeiro interno).
* **Nota Fiscal (NFC-e):** Representa o documento XML de relevância jurídica transmitido, validado e homologado pela SEFAZ.

> [!info] Autonomia de Entidades
> Devido a essa separação, o sistema permite que uma venda seja finalizada e fechada no caixa com status comutado, mesmo que a nota fiscal correspondente sofra rejeição ou falha de comunicação com os servidores do fisco. O erro fiscal não corrompe a integridade financeira do caixa diário do operador.

---

## 2. Fluxo Prático de Emissão e Regra de Venda a Prazo

O ciclo de fechamento padrão de uma venda em dinheiro ou cartão processa a transmissão automática e dispara o extrato da NFC-e para a impressora térmica local em poucos segundos.

### Regra de Validação de Crédito (Venda a Prazo)
Ao selecionar uma forma de pagamento do tipo "A Prazo" (como *Duplicata* ou *Crediário Interno*), o motor de regras do PDV executa uma validação impeditiva:
* **Bloqueio de Consumidor Anônimo:** O sistema impede que vendas a prazo sejam liquidadas utilizando o cadastro padrão de **Consumidor Final**.
* **Tratamento:** O operador é bloqueado por uma mensagem em tela. Para prosseguir com o faturamento a prazo, é obrigatório identificar nominalmente o **Cliente** na venda, vinculando o contas a receber a um CPF/CNPJ válido.

---

## 3. Tratamento de Exceções e Rejeições da SEFAZ

Quando ocorre um erro na validação dos dados fiscais (seja por oscilação nos servidores do fisco ou inconsistência cadastral do item), o ERP interrompe o envio assíncrono e captura o código de retorno da API de mensageria.

[ Gravação do Pedido (F9) ] 
| [ Tentativa de Envio NFC-e ] 
| { Resposta SEFAZ }
/
(Sucesso) (Rejeição 
/ 
Erro de Schema) 
/
[Imprime Danfe] [Captura Erro da API] -> [Abre Tela de Correção de Nota]

Exemplo Prático de Erro de Parâmetro Caso o campo **Indicador de Presença do Comprador** na [[Natureza de Operação]] seja modificado incorretamente para `0 - Não se aplica`, a SEFAZ rejeitará o lote imediatamente, visto que a NFC-e (Modelo 65) exige por padrão indicador de presença física ou entrega a domicílio. O sistema aborta o encerramento silencioso, apresenta o log do erro e força a abertura da tela de contingência fiscal. 

4. Fluxo de Contingência e Correção Manual de Notas Ao receber uma rejeição, o ERP direciona o foco do usuário para a tela administrativa de Notas Fiscais em modo de edição:
	1. A interface exibe os campos estruturados da nota (Dados do Destinatário, Transporte, Itens, Alíquotas e Totais). 
	2. O analista de suporte ou faturista pode corrigir o metadado rejeitado diretamente na interface (ex: corrigir a flag de presença do comprador ou alterar o NCM do produto). 
	3. Após retificar a informação, clica-se em **Salvar Nota**. O ERP reconstrói o arquivo XML, recalcula os hashes de segurança e executa uma nova tentativa de transmissão. 
> [!tip] Rastreamento de Notas Pendentes > Caso a nota não possa ser corrigida de imediato, ela permanecerá listada no painel fiscal com o status de **Sem Confirmação**. Isso permite que o PDV continue operando normalmente para os próximos clientes enquanto a retaguarda resolve a inconsistência tributária daquela nota específica. --- ## 5. Estorno de Faturamento e Duplicidade de Vínculos Se uma venda gerou uma nota fiscal com status *Sem Confirmação* (rejeitada/travada) e o cliente desistiu da compra, o operador deve efetuar o estorno do faturamento. ### Fluxo de Cancelamento de Faturamento 1. Na listagem de vendas, selecione o pedido travado e acione o comando **Cancelar Faturamento**. 2. O ERP exibe o alerta: *"O pedido possui vínculo com nota fiscal que não será excluída. Tem certeza que deseja cancelar o faturamento?"*. 3. Ao confirmar (e digitar a senha gerencial caso requerido), a Venda gerencial retorna ao status **Em Aberto** ou **Cancelado**, recompondo o saldo de estoque e limpando o fluxo do caixa.


> [!warning] Risco Crítico: Duplicidade de Notas Fiscais > Como as entidades são independentes, se o faturamento de uma venda for desfeito e o operador simplesmente reabrir o pedido e finalizá-lo novamente (F9) sem tratar a nota fiscal original que ficou travada em modo *Sem Confirmação*, o sistema gerará um **segundo registro de nota fiscal** para o mesmo pedido. O analista de suporte deve obrigatoriamente acessar o painel de notas e executar o comando de **Cancelar Nota Fiscal** na numeração rejeitada antiga para sanar a duplicidade e evitar passivos fiscais para a empresa.


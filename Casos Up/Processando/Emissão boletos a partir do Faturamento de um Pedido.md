---
id: CASO-021
link: https://www.youtube.com/watch?v=2EDlh07da_g
setor: Suporte, Faturamento
modulo: Pedidos e Financeiro
tags:
  - boleto-bancario
  - faturamento
  - formas-de-pagamento
  - contas-a-receber
  - upsystem
data_criacao: 2026-06-24
---

# Emissão de Boletos a partir do Faturamento de Pedidos

Este documento técnico descreve o processo de configuração de formas de pagamento e a rotina de emissão de boletos bancários diretamente no faturamento de um pedido de venda no sistema [[UpSystem]]. Detalha também a arquitetura de independência entre o título de contas a receber e o documento do boleto.

---

## Sumário
1. [[#Pré-requisitos e Configuração das Formas de Pagamento]]
2. [[#Fluxo de Execução e Emissão de Boletos]]
3. [[#Arquitetura de Vinculação Financeira e Regras de Negócio]]
4. [[#Pontos Críticos e Resolução de Problemas]]

---

## Pré-requisitos e Configuração das Formas de Pagamento

Para que o faturamento de um pedido consiga gerar boletos bancários automaticamente, a forma de pagamento selecionada precisa estar devidamente parametrizada na retaguarda do sistema.

1. Acesse o cadastro de **Formas de Pagamento**.
2. Identifique ou crie a forma de pagamento específica (ex: **Sicoob**, **Banco do Brasil**).
3. Defina o tipo de documento associado como **Boleto Bancário**.
4. Vincule obrigatoriamente a **Conta Bancária** correspondente que movimentará a carteira de cobrança.
5. Configure as demais diretrizes comerciais da forma de pagamento:
   - Quantidade de parcelas padrão.
   - Intervalo de dias entre as parcelas (ex: 30 dias).
   - Percentuais ou condições de desconto cadastrados para a nota fiscal, se aplicável.

> [!info] Multi-Banco
> O sistema é homologado e permite a coexistência de múltiplos bancos configurados simultaneamente. Um pedido pode gerar boletos do **Sicoob** e outro do **Banco do Brasil** na mesma rotina, dependendo unicamente da forma de pagamento atrelada ao documento de venda.

---

## Fluxo de Execução e Emissão de Boletos

A emissão ocorre no fechamento do pedido, integrando o setor de vendas e faturamento diretamente com a carteira bancária.

1. Acesse a tela de **Pedido de Venda** e selecione o pedido desejado.
2. Certifique-se de que o campo **Forma de Pagamento** está preenchido com a opção configurada para emitir boletos.
3. Ao verificar a aba financeira de recebimentos antes da emissão, o status constará temporariamente como um débito ou recebimento normal (sem numeração de boleto atribuída).
4. Clique no botão **Emitir Boleto**.
5. Uma janela ou caixa de **Confirmação** será exibida. Confirme a operação.
6. O sistema processará as parcelas, aplicando os juros e instruções bancárias previamente configuradas na carteira.
7. O pedido será atualizado automaticamente para o status de faturado.

> [!tip] Atalho Operacional
> A emissão do boleto realiza o gatilho duplo no sistema: gera fisicamente o documento de cobrança com os códigos de barra/linha digitável e conclui o faturamento do pedido de venda em um único clique processual.

---

## Arquitetura de Vinculação Financeira e Regras de Negócio

Um dos conceitos fundamentais da regra de negócio do ERP é o **desacoplamento** entre o contas a receber (título financeiro) e o boleto bancário (meio de cobrança).

[ Pedido de Venda ] │ ▼ [ Contas a Receber (Título) ] <─────── Vinculado ───────> [ Boleto Bancário ] (Mantém o débito ativo) (Documento de Cobrança)


- **Independência de Entidades:** Um título de conta a receber não é a mesma entidade de um boleto. O boleto é apenas um indexador de cobrança vinculado ao título principal. - **Persistência do Débito:** Caso um boleto venha a ser cancelado (por solicitação do cliente, alteração na modalidade para pagamento em cheque, ou necessidade de renegociação), a relação de débito no **Contas a Receber** permanece intacta. --- ## Pontos Críticos e Resolução de Problemas O gerenciamento inadequado do vínculo entre títulos e boletos pode gerar falhas operacionais graves na conciliação financeira. > [!warning] Ponto de Falha: Cancelamento Incorreto de Recebimentos > **Cenário:** O usuário precisa cancelar um boleto porque o cliente decidiu pagar em dinheiro ou cheque. > **Erro comum:** Cancelar o título de contas a receber diretamente. Isso zera a pendência do cliente indevidamente na inadimplência. > **Comportamento Correto:** Deve-se filtrar e cancelar estritamente o **Boleto Bancário** na tela de gerenciamento de boletos. O recebimento voltará ao estado original (débito aberto), permitindo que o operador liquide a pendência com a nova forma de pagamento escolhida pelo cliente, sem a necessidade de reemitir ou refazer a venda original. ### Tabela de Status e Ações Esperadas | Cenário | Ação no Sistema | Impacto no Contas a Receber | Impacto no Caixa/Banco | | :--- | :--- | :--- | :--- | | Cliente solicita prorrogação de prazo | Cancelar boleto atual e gerar novo pelo financeiro | Mantém o título original aberto com nova data | Sem movimentação até a liquidação | | Troca de Boleto para pagamento em Dinheiro | Cancelar o boleto no painel financeiro | Título permanece ativo aguardando baixa manual | Libera o título para recebimento em espécie |
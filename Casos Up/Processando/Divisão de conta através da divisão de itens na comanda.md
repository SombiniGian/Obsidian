---
id: CASO-043
link: https://www.youtube.com/watch?v=cZLiAbEZSbM
setor: Suporte
modulo: Restauração / PDV (Ponto de Venda)
tags:
  - divisao-de-conta
  - fechamento-de-mesa
  - faturamento
  - comanda
  - pdv
data_criacao: 2026-06-24
---

# Divisão de Conta por Itens na Comanda

Este documento técnico descreve o funcionamento, as regras de negócio e o fluxo operacional do recurso de divisão parcial de contas por meio da seleção de itens específicos no ERP da UP Sistemas. A funcionalidade atende a cenários complexos onde múltiplos clientes associados a uma mesma mesa ou comanda desejam pagar exclusivamente pelos produtos que consumiram, em vez de realizar a divisão puramente matemática/igualitária do saldo total.

## Sumário
- [[#Visão Geral da Funcionalidade]]
- [[#Fluxo Operacional de Fechamento]]
- [[#Regras de Negócio e Tratamento de Diferenças]]
- [[#Persistência e Histórico de Vendas]]
- [[#Pontos Críticos e Solução de Problemas]]

---

## Visão Geral da Funcionalidade

O recurso de divisão por itens atua de forma integrada ao módulo de [[Mapa de Mesas]] e ao [[PDV Tradicional]]. Ele estende a tela de encerramento de vendas, permitindo ao operador fracionar a conta atribuindo quantidades parciais ou totais de produtos a pagadores identificados nominalmente.

![[Divisão de conta através da divisão de itens na comanda.png]]

> [!info] Diferencial de Versão > Em versões anteriores do sistema, a divisão limitava-se a ratear o valor bruto pelo **Número de Pessoas**, gerando uma cota linear idêntica para todos. A nova ferramenta de **Divisão por Itens** permite uma auditoria precisa do consumo individual antes da geração do fluxo de caixa. 
>  Fluxo Operacional de Fechamento 
>   Passo 1: Acesso ao Encerramento 1. Na interface do **Mapa de Mesas**, localize e selecione a mesa ou comanda desejada. 2. Com os itens de consumo listados na tela, clique no botão **Encerramento** (ou pressione o atalho de fechamento configurado). 
>   Passo 2: Inicialização da Divisão 1. Na tela de finalização, identifique o botão **Divisão** localizado próximo aos campos de cálculo de permanência e número de pessoas. 2. Uma janela pop-up secundária será aberta, exibindo a relação completa de produtos ainda não liquidados da comanda. 3. No campo **Nome do Pagador**, digite a identificação do primeiro cliente (Ex: `Diego`). 
>   Passo 3: Atribuição de Consumo e Liquidação Parcial 1. Selecione os produtos e as quantidades correspondentes que o pagador atual consumirá (Ex: *1 Suco de Laranja e 1 Taça de Vinho*). 2. O sistema recalcula o subtotal dinamicamente no campo **Valor a Pagar**. 3. Clique em **Salvar**. O sistema retornará à tela principal de finalização, preenchendo automaticamente o nome do cliente no grid de pagadores e injetando o valor exato no campo **Valor de Pagamento**. 4. Informe o meio de pagamento utilizado pelo cliente (Dinheiro, Cartão de Crédito/Débito, Pix). 5. Processe o recebimento parcial. Uma vez liquidada a cota daquele pagador, a pendência imediata é baixada, mantendo o histórico registrado na lateral da tela. 
>   Passo 4: Resgate do Saldo Remanescente 1. Clique novamente em **Divisão** para tratar o próximo cliente da mesa. 2. Insira o nome do novo pagador (Ex: `Lucas`). 3. Para otimizar a operação, caso este cliente vá arcar com todo o saldo restante da mesa, clique no botão **Restante**. >
>    [!tip] Comportamento Visual dos Itens > Na listagem de divisão, o sistema utiliza cores para sinalizar o status de conferência dos produtos: > * **Itens em Amarelo/Coloridos:** Indicam que o produto sofreu divisão parcial (apenas algumas unidades das lançadas foram pagas). > * **Itens Omitidos/Riscados:** Indicam produtos cuja totalidade já foi associada a pagadores anteriores e devidamente processada. 4. Clique em **Salvar** e processe os múltiplos meios de pagamento para este segundo cliente na tela principal. 5. Após o saldo geral atingir `0,00`, clique em **Finalizar Venda** para realizar a emissão do documento fiscal (NFC-e / SAT) e liberar o número da mesa no mapa. 
>    Regras de Negócio e Tratamento de Diferenças O sistema possui uma inteligência interna de conciliação financeira para tratar situações em que um dos pagadores realiza um pagamento maior do que a soma estrita dos itens que selecionou (deixando "crédito" para amortizar o restante da mesa). 
>    Exemplo de Cenário Prático (Amortização Dinâmica) * **Total da Comanda:** R$ 56,35 * **Consumo Real do Pagador 1 (Diego):** R$ 23,17. * **Ação do Operador:** O cliente entrega uma cédula de R$ 30,00 e decide não receber o troco em dinheiro, aplicando o saldo excedente como desconto/ajuda na parte dos demais clientes da mesa. * **Ação do Sistema:** O sistema aceita a entrada de R$ 30,00 para o Pagador 1 e abate este valor do montante bruto total da mesa (R$ 56,35 - R$ 30,00 = R$ 26,35). * **Consumo Real do Pagador 2 (Lucas):** R$ 33,18. * **Resultado Dinâmico:** Ao abrir a divisão do Pagador 2, embora o valor nominal dos seus itens totalize R$ 33,18, o sistema injeta no campo de pagamento apenas **R$ 26,35**, absorvendo automaticamente a diferença paga a maior pelo cliente anterior. --- ## Persistência e Histórico de Vendas Após o fechamento completo da venda, toda a árvore de divisão estruturada permanece gravada no banco de dados para fins de auditoria e reimpressões de cupons gerenciais. 
>    Caminho de Consulta No módulo de retaguarda ou no menu de consultas do PDV, acesse: **Histórico de Vendas** > Selecione a venda correspondente através do número da nota ou ID da comanda. O sistema exibirá a aba de detalhes financeiros discriminando de forma clara: * O nome individual de cada pagador envolvido na transação. * A listagem de produtos que foram vinculados e baixados por cada CPF/Nome. * O método de pagamento exato utilizado por cada fração da conta (Ex: R$ 6,35 em Dinheiro e R$ 20,00 no Cartão para o Pagador X).
>    
>    
>    Pontos Críticos e Solução de Problemas > [!warning] Fechamento Prematuro de Cupom Fiscal > A transmissão do cupom fiscal (NFC-e ou SAT) só deve ocorrer após o encerramento do último pagador. Caso o operador finalize a venda antes de processar os pagamentos parciais de todos os membros da mesa, o sistema fechará a venda com saldo pendente (gerando inconsistência de caixa) ou impedirá a conclusão por falta de contrapartida financeira. ### Diagnósticos Frequentes | Sintoma | Causa Provável | Ação Corretiva | | :--- | :--- | :--- | | O botão **Divisão** encontra-se desabilitado na tela de fechamento. | A comanda está marcada em modo de edição exclusiva por outro terminal ou aplicativo móvel. | Certifique-se de que o aplicativo de força de vendas (garçom) sincronizou e liberou a mesa antes de iniciar o fechamento no PDV físico. | | O valor restante sugerido para o último pagador está negativo. | Os pagadores anteriores pagaram valores acumulados que superam o valor total bruto da comanda. | Verifique o histórico de recebimentos parciais na lateral do grid para identificar se houve digitação incorreta de valores em dinheiro ou cartões. | | Erro de integridade ao tentar reabrir mesa dividida por itens no [[Histórico de Vendas]]. | Registro corrompido na tabela de relacionamento do banco de dados (geralmente por quedas de energia no meio do processo de divisão). | Executar a validação e o gfix no banco de dados Firebird para corrigir inconsistências nas chaves estrangeiras que ligam os itens da venda aos pagadores cadastrados.

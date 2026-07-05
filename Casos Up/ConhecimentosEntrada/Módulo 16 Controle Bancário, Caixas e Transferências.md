Este módulo finaliza a documentação financeira abordando a gestão do numerário em espécie, a conciliação dos saldos das contas bancárias, as rotinas de fechamento de caixa e a custódia de cheques.

---

## 1. Gestão e Fechamento de Caixa

O sucesso do controle de caixa depende de uma parametrização rigorosa no "Cadastro de Contas". O sistema oferece travas de segurança para garantir a integridade da operação na frente de loja.

* **Parâmetros de Segurança e Auditoria:**
    * **Fechamento às Cegas:** Quando ativado, o sistema oculta do operador os valores sistêmicos totais computados no turno. O caixa é obrigado a contar o dinheiro físico e declarar a gaveta. O sistema então confronta o valor declarado com o valor sistêmico, evidenciando quebras de caixa (sobras ou faltas).
    * **Status de Conferência (Auditoria de Fechamento):** Caso a empresa possua um departamento de tesouraria, é possível marcar a opção "Sempre Conferir Fechamento". Assim, quando o operador fecha o caixa, ele não é consolidado imediatamente; ele transita para um status de "Conferência", exigindo que um supervisor audite e aprove o lote posteriormente.
    * **Travas de Movimentação:** É possível obrigar o preenchimento de senhas de gerente e "Histórico" justificado para toda operação de **Sangria** (retirada) ou **Suprimento** (entrada de troco).
* **Impressões Autômatas:** O sistema permite vincular layouts de impressão distintos para os recibos de abertura, fechamento, sangrias e suprimentos, além de automatizar o envio do demonstrativo de fechamento por e-mail para a gerência.

---

## 2. Correção de Divergências de Caixa (Processo de Tesouraria)

Um erro operacional comum é o operador finalizar a venda na forma de pagamento incorreta (ex: passou a venda em PIX, mas clicou em Dinheiro no sistema). O ERP oferece duas rotinas para correção desta divergência sem corromper o fluxo fiscal:

* **Correção via Movimentação de Contas (De-Para):** A tesouraria não precisa reabrir o caixa. Basta acessar as "Movimentações de Contas" e realizar lançamentos de ajuste: lança-se um Débito na conta "Caixa Dinheiro" e um Crédito na conta "Caixa PIX", equilibrando os saldos bancários e físicos da empresa.
* **Correção via Cancelamento de Fechamento:** Se o erro exigir a mudança estrita na venda original, o supervisor deve cancelar o fechamento do caixa afetado, acessar a movimentação específica, cancelar/corrigir a venda e fechar o caixa novamente (respeitando a competência da data original).

---

## 3. Saldo e Movimentação de Contas

Esta tela atua como o **Extrato Bancário e de Caixa** dentro do ERP, consolidando todas as entradas e saídas.

* **Visão Geral:** Exibe o saldo anterior, total de entradas, total de saídas e o saldo atual do período filtrado, abrangendo tanto os caixas físicos quanto as contas correntes cadastradas.
* **Movimentações Avulsas:** Permite a inserção manual de débitos e créditos que não nasceram de faturamentos ou compras (ex: taxas bancárias, rendimentos de aplicações). Esses lançamentos manuais exigem a vinculação de um Plano de Contas e Centro de Custo para integridade do DRE.
* **Transferências:** Ferramenta dedicada para movimentar valores entre contas de origem e destino (ex: Transferência do "Caixa Dinheiro Loja 1" para a conta do "Banco Itaú" após o depósito no final do dia).

---

## 4. Gestão e Controle de Cheques

Um submódulo isolado para o rastreio do ciclo de vida de cheques físicos.

* **Cheques Emitidos e Recebidos:** O cadastro de um cheque vincula dados como CMC7, banco, emitente, valor e a data de bom para (pré-datado).
* **Régua de Devolução:** Se um cheque depositado retornar sem fundos, o sistema controla as tentativas:
    * **1ª Devolução:** O cheque retorna, mas ainda pode ser reapresentado ao banco.
    * **2ª Devolução:** O cheque não pode mais ser reapresentado. O sistema altera o status do cheque e o transfere automaticamente para a "Cobrança", gerando o status de devedor e os juros sobre o título.
* **Borderô de Depósito:** Ferramenta para selecionar um lote de cheques pré-datados que venceram no dia e gerar a instrução consolidada de depósito bancário para o office-boy/tesouraria realizar a entrega física na agência.
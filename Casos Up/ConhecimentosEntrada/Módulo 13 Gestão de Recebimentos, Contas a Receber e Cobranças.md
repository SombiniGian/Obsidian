Este módulo detalha a arquitetura do "Contas a Receber" (Recebimentos), explicando como o sistema captura, organiza e permite a manipulação dos direitos de crédito da empresa, desde a venda inicial até a liquidação ou renegociação da dívida.

---

## 1. Arquitetura e Geração de Recebimentos

O módulo de Recebimentos atua como o repositório central de todas as entradas financeiras projetadas ou concretizadas da empresa.

* **Geração Automatizada:** A grande maioria dos títulos é alimentada automaticamente pelo motor do sistema. Sempre que uma movimentação de saída a prazo (Pedido de Venda, Ordem de Serviço, PDV) é finalizada, o sistema converte as condições de pagamento em parcelas no Contas a Receber.
* **Lançamento Manual:** O operador financeiro também possui a liberdade de incluir títulos avulsos que não nasceram de uma venda de mercadoria (ex: recebimento de aluguéis, devoluções de crédito).
* **Rastreabilidade e Vínculos:** Cada registro de recebimento mantém um cordão umbilical com sua origem. Através da opção **Visualizar Venda**, o analista financeiro consegue auditar exatamente qual pedido, produtos ou serviços originaram aquela cobrança, sem precisar sair da tela financeira.

### 1.1. Estrutura de Dados do Título
Um título a receber comporta múltiplas dimensões de controle gerencial:
* **Devedor (Cliente):** Entidade atrelada à dívida.
* **Plano de Contas e Centro de Custo:** Classificação da receita para posterior composição do DRE e relatórios de fluxo de caixa.
* **Acréscimos Legais:** Parametrização de Multas e Juros por atraso.
* **Comissionamento:** Vínculo direto com o vendedor que originou a receita (essencial para empresas que pagam comissão apenas na liquidação do título).
* **Anexos Visuais:** A aba "Fotos" permite anexar comprovantes de depósito, recibos assinados ou capturas de tela de transferências diretamente no título.

---

## 2. Operações de Manipulação de Títulos

A grid de opções do Recebimento entrega ferramentas de produtividade para o departamento de cobrança:

* **Desdobramento em Lote (Gerar Parcelas):** Permite pegar um recebimento base e desdobrá-lo em múltiplas parcelas de forma rápida. *Exemplo:* Lançar um contrato de serviço anual e gerar automaticamente 12 parcelas com vencimentos subsequentes.
* **Recálculo de Taxas (Cartão):** Caso haja alteração nas condições comerciais junto à adquirente do cartão após o lançamento da venda, o sistema permite recalcular retroativamente a taxa de administração nos títulos em aberto.
* **Comunicação Integrada:** Envio de lembretes de cobrança, recibos e notas promissórias diretamente para o WhatsApp do cliente a partir da tela de opções.

---

## 3. Liquidação e Borderô de Recebimento

O processo de liquidação (baixa) de um título obedece a uma hierarquia de segurança para evitar perdas financeiras e facilitar estornos.

* **Geração do Borderô:** Quando o operador realiza a baixa de um ou mais recebimentos (confirmando o pagamento), o sistema agrupa essas baixas em um **Borderô de Recebimento**. Este borderô funciona como um "lote de processamento".
* **Logística de Estorno (Reversão de Baixa):** O sistema impede a exclusão direta de um título já pago. Se o caixa cometeu um erro na baixa, ele deve acessar o módulo de *Borderô de Recebimento*, localizar o lote incorreto e **Cancelá-lo**. Ao cancelar o borderô, os recebimentos atrelados a ele retornam automaticamente ao status de "Em Aberto" na tela principal, prontos para correção.

---

## 4. Renegociação de Dívidas (Borderô de Negociação)

Ferramenta vital para a recuperação de crédito e gestão de inadimplência. O módulo permite reestruturar títulos vencidos criando novas condições.

* **Agrupamento de Dívidas:** O operador seleciona múltiplas parcelas em atraso de um mesmo cliente (ex: 10 boletos vencidos).
* **Reestruturação:** Ao iniciar a negociação, o sistema consolida o saldo devedor e permite a aplicação de novos juros, perdão de multas (descontos) e a repactuação do prazo.
* **Nova Emissão:** A dívida original é unificada em um **Borderô de Negociação**. A partir dele, o sistema "mata" os títulos antigos e gera novas parcelas em aberto, permitindo a impressão imediata de um novo carnê de pagamento ou contrato de confissão de dívida para o cliente assinar.

---

## 5. Auditoria Financeira

Seguindo o padrão arquitetônico do ERP, a tela de Recebimentos possui auditoria rígida.
* Qualquer alteração em datas de vencimento, valores de desconto concedidos ou mudança de status é registrada nos logs.
* O log captura o "Estado Anterior", "Estado Novo", a estampa de tempo (Data/Hora) e o ID do usuário, garantindo *compliance* total contra fraudes internas.
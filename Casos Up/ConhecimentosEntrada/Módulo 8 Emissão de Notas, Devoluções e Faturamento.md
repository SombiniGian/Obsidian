Este módulo documenta os processos de pós-venda operacionais dentro do sistema, abrangendo a emissão de documentos fiscais a partir de movimentações pré-existentes e o fluxo completo de logística reversa (devoluções) e estorno financeiro.

---

## 1. Emissão de Notas Fiscais a partir do Pedido

O sistema permite desvincular o momento da venda do momento da emissão fiscal, oferecendo flexibilidade para operações de caixa e backoffice.

* **Faturamento Automático vs. Manual:** Dependendo da configuração da Natureza de Operação, o sistema pode emitir a Nota Fiscal (NF-e/NFC-e) automaticamente ao finalizar o pedido, ou manter o pedido "Faturado" aguardando a emissão manual.
* **Emitir Nota de Pedido Faturado:** Através do menu de *Opções* no Pedido de Venda, o operador pode buscar um pedido já pago/fechado e gerar a nota fiscal correspondente.
* **Alternância de Natureza de Operação (Transição Fiscal):** Durante a emissão a partir de um pedido, o sistema permite alterar a operação fiscal base.
    * *Cenário de Uso:* Um pedido de venda foi feito originalmente como "Venda de Mercadoria", mas o usuário precisa emitir uma "Remessa para Conserto" ou transformar um "Cupom Fiscal (NFC-e)" já emitido em uma "Nota Fiscal Eletrônica (NF-e, Modelo 55)" para um cliente corporativo. A tela de emissão permite reclassificar a natureza antes de transmitir o XML à Sefaz.

---

## 2. Processo de Devolução (Logística Reversa)

A rotina de devolução foi desenhada para ser executada diretamente na frente de caixa (PDV) ou no retaguarda, garantindo a reintegração do estoque e o estorno contábil.

* **Acesso Facilitado:** A devolução pode ser acionada diretamente na tela Balcão/PDV. O operador busca o pedido original e o sistema carrega o espelho da venda.
* **Devolução Total ou Parcial:** * O sistema lista todos os itens do pedido original.
    * O operador pode selecionar itens específicos para devolução e ajustar a *quantidade exata* (ex: O cliente comprou 6 unidades, mas está devolvendo apenas 4. O sistema recalcula o estorno financeiro proporcional a essas 4 unidades).
* **Estorno de Comissões:** A devolução de um item aciona um gatilho financeiro que processa automaticamente o estorno ou o recálculo da comissão do vendedor associado àquela venda original.

---

## 3. Liquidação da Devolução (Destino do Valor)

Ao salvar uma devolução, o sistema exige que o operador informe o destino contábil e financeiro do valor que está sendo ressarcido ao cliente. Existem três opções de liquidação:

1. **Voltar Troco (Estorno em Caixa):** O sistema retira o valor do saldo do caixa atual (exigindo a escolha de qual conta caixa será debitada) e devolve o montante fisicamente/eletronicamente ao cliente.
2. **Gerar Crédito (Store Credit):** O valor é retido pela empresa e convertido em um saldo credor na conta do cliente para abater em compras futuras.
    * *Regra de Negócio Crítica:* O sistema **bloqueia** a geração de crédito se o cliente do pedido for "Consumidor Final" genérico. Para gerar crédito, é obrigatório identificar/cadastrar o cliente na base de dados para garantir o rastreio do saldo.
3. **Descartar Diferença:** Utilizado para ajustes sistêmicos onde o valor da devolução não será estornado nem convertido em crédito (ex: acordos comerciais específicos, perdas ou devoluções de bonificação).
https://www.youtube.com/watch?v=cZLiAbEZSbM
Este módulo detalha o funcionamento da ferramenta de **Divisão de Conta por Itens Selecionados** do ERP Código UP. O recurso foi projetado para estabelecimentos gastronômicos (como restaurantes e bares operando via comanda ou mapa de mesas) e também para o PDV tradicional, permitindo fracionar o pagamento com base no consumo individual real de cada cliente, em vez de uma divisão puramente matemática igualitária `[00:00:10]`, `[00:04:37]`.

### 1. Acesso à Tela de Divisão e Lógica de Consumo `[00:00:23]`

O fluxo se inicia a partir do mapa de mesas ou comandos em atendimento (ex: Mesa 20 contendo múltiplos produtos como sucos de laranja e taças de vinho) `[00:00:33]`.

- **Entrada no Encerramento:** O operador avança para a tela padrão de faturamento/fechamento `[00:00:52]`. Nesta interface, além da divisão matemática tradicional (onde digita-se o número de pessoas para calcular o valor exato por cota) `[00:01:02]`, o sistema disponibiliza o botão **"Divisão"** `[00:01:08]`.
    
- **Identificação por Nome do Pagador:** Ao clicar em dividir, o ERP abre um assistente de captura solicitando o nome do cliente corrente (ex: "Diego") `[00:01:18]`.
    
- **Seleção Unidirecional de Itens:** O operador marca na lista quais produtos específicos o cliente deseja liquidar (ex: "1 suco de laranja e 1 taça de vinho") `[00:01:30]`. O sistema calcula instantaneamente o subtotal parcial devido por aquela pessoa (ex: $R\$\,23,17$) `[00:01:37]`.
    

### 2. Fluxo de Caixa e Amortização de Valores Recorrentes `[00:01:47]`

Após salvar a seleção parcial, o ERP retorna à tela de finalização principal injetando o nome do pagador e o valor exato de sua cota diretamente no campo de pagamento `[00:01:47]`.

- **Tratamento de Pagamento Maior (Crédito Volante no Lote) `[00:01:55]`:** Se o cliente "Diego" deve $R\$\,23,17$ mas entrega uma nota de $R\$\,30,00$, o caixa realiza o lançamento normalmente `[00:01:55]`. O ERP liquida os itens vinculados a ele, encerra o seu cupom parcial e **retém a diferença de $R\$\,6,83$ como saldo credor ativo** para o fechamento do restante da comanda `[00:02:09]`.
    
- **Sinalização Visual de Status dos Itens `[00:02:24]`:** Ao abrir o painel para o próximo pagador (ex: "Lucas") `[00:02:24]`, a grade do ERP exibe códigos de cores para indicar o andamento da mesa `[00:02:58]`:
    
    - _Itens Verdes/Liquidados:_ Produtos que já foram totalmente pagos por clientes anteriores `[00:02:58]`.
        
    - _Itens Amarelos/Parciais:_ Produtos que tiveram apenas algumas unidades pagas (ex: havia 3 vinhos, 1 foi pago, restam 2) `[00:02:58]`.
        
- **Liquidação por Saldo Remanescente ("Restante") `[00:02:53]`:** O operador não precisa selecionar item por item para o último integrante da mesa; basta clicar no comando **"Restante"** para que o ERP puxe o saldo devedor restante da conta de forma automática `[00:02:53]`.
    

### 3. Abatimento Automático de Sobras Financeiras `[00:03:07]`

O motor de cálculo do ERP Código UP protege a cobrança recalculando os saldos pendentes com base nos valores totais já entregues no caixa:

$$\text{Valor Nominal do Lucas} = R\$\,33,18$$

$$\text{Crédito da Sobra do Diego} = R\$\,6,83$$

$$\mathbf{Total\;Lançado\;para\;o\;Lucas} = R\$\,33,18 - R\$\,6,83 = \mathbf{R\$\,26,35}$$

Dessa forma, o sistema exige que o "Lucas" pague apenas o valor líquido recalculado ($R\$\,26,35$) `[00:03:16]`. O operador pode fracionar esse recebimento final em múltiplas formas de pagamento (ex: uma parte em dinheiro e outra no cartão) `[00:03:27]`. Com o balanço zerado, a mesa é automaticamente liberada no mapa do salão `[00:03:49]`.

### 4. Auditoria de Divisão e Histórico de Vendas `[00:03:58]`

Após a finalização, a rastreabilidade do rateio é persistida no banco de dados para consultas gerenciais.

No menu de _Histórico de Vendas_, ao localizar o cupom fechado, o gestor tem acesso ao relatório completo da operação `[00:03:58]`. O ERP discrimina o fluxo contendo o nome de cada pagador, quais itens específicos compuseram a sua sub-conta, o valor nominal teórico que deveria pagar e o valor físico exato que foi entregue no caixa `[00:04:05]`, `[00:04:14]`. Esse registro pode ser impresso em formato de comprovante detalhado para conferência do cliente `[00:04:21]`.

ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link https://www.youtube.com/watch?v=cZLiAbEZSbM
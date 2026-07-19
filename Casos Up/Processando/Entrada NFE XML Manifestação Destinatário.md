---
id: [CASO-172]
link: https://www.youtube.com/watch?v=LdNEwnR4Emg&t=403s
setor: [Operacional, Logística, Faturamento]
modulo: [Vendas / Controle de Entregas]
tags: [entrega-futura, faturamento, controle-de-estoque, naturezas-de-operacao, expedicao]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Entrega Futura]]
2. [[#Cenário 1: Faturamento Total Imediato com Entrega Fracionada]]
3. [[#Cenário 2: Pedido de Controle com Faturamento por Entrega]]
4. [[#Mecânica de Desmembramento de Entregas (PDV e Retaguarda)]]
5. [[#Painel de Gerenciamento de Entregas Futuras]]
6. [[#Pontos Críticos e Validações Fiscais]]

# Visão Geral da Entrega Futura
O módulo de **Controle de Entregas Futuras** gerencia operações comerciais onde o cliente realiza uma compra global (pedido completo), mas a retirada ou envio das mercadorias ocorre de forma fracionada ao longo do tempo. O sistema soluciona o conflito entre o faturamento financeiro (quando o cliente paga) e a baixa patrimonial (quando o produto sai fisicamente do estoque), suportando diferentes arranjos através do motor de regras das Naturezas de Operação.

# Cenário 1: Faturamento Total Imediato com Entrega Fracionada
Neste modelo, o cliente paga por todas as mercadorias no ato da negociação, mas leva apenas uma parte dos itens na hora, solicitando o envio do restante em datas posteriores. 

### Parametrização da Natureza de Operação (Pedido Pai)
*   **Nome:** `Venda para Entrega Futura`
*   **Gera Financeiro:** **Ativo** (O contas a receber/caixa é gerado integralmente).
*   **Movimenta Estoque:** **Inativo** (O estoque não é baixado no pedido global, pois os itens ainda estão no galpão).

### Parametrização da Natureza de Operação (Pedido de Entrega)
*   **Nome:** `Remessa de Entrega Futura`
*   **Gera Financeiro:** **Inativo** (O cliente já pagou na nota pai).
*   **Movimenta Estoque:** **Ativo** (Executa a baixa física de cada item à medida que saem da loja).

> [!info] Configuração Padrão no ERP
> Para evitar que o operador precise preencher as naturezas manualmente em cada fracionamento, acesse **Configurações do Pedido de Venda > Aba Delivery/Entrega** e defina a "Natureza de Operação Padrão para Entregas". O sistema herdará automaticamente essa classificação em todas as remessas filhas.

# Cenário 2: Pedido de Controle com Faturamento por Entrega
Neste modelo, o cliente aprova uma lista fechada de materiais (ex: orçamento de obra), mas só paga pelo que for efetivamente despachado a cada frete.

### Parametrização da Natureza de Operação (Pedido Pai)
*   **Nome:** `Pedido de Controle / Faturar na Entrega`
*   **Gera Financeiro:** **Inativo**.
*   **Movimenta Estoque:** **Inativo**.
*   **Função:** Atua apenas como um agrupador de itens e bloqueio de orçamento.

### Parametrização da Natureza de Operação (Pedido de Entrega)
*   Neste cenário, a entrega atua como uma venda definitiva. O operador pode utilizar a própria natureza padrão de **Vendas**, pois cada remessa necessita gerar o seu respectivo boleto/recebimento no caixa e realizar a respectiva baixa de estoque.

# Mecânica de Desmembramento de Entregas (PDV e Retaguarda)
A tela de faturamento possui uma interface dedicada para gerenciar as frações da venda. 

1. Durante o lançamento do pedido, acione o atalho **ALT + E** ou clique em **Opções > Entregas**.
2. O painel exibirá o saldo total do pedido. Clique em **Incluir Entrega**.
3. A tela será dividida em duas colunas:
    * **Esquerda (Saldo Restante):** Lista todos os itens que ainda não foram expedidos.
    * **Direita (Itens da Entrega Atual):** Grade vazia aguardando a seleção.
4. Digite a quantidade desejada de um produto na coluna esquerda e confirme. O item será transferido para a coluna da direita, abatendo o saldo geral.
5. **Gravação:**
    * Clique em **Finalizar** caso a mercadoria esteja saindo fisicamente da loja naquele exato momento (gera a NF-e e altera o status para *Entregue*).
    * Clique em **Salvar** caso esteja apenas roteirizando e agendando o despacho para uma data futura (ex: dia 10). O status ficará como *Não Entregue / Em Aberto*.

# Painel de Gerenciamento de Entregas Futuras
Como as remessas de entrega geram novos números de "Pedidos Filhos" no banco de dados, consultar a tela padrão de faturamento pode gerar poluição visual (vários pedidos espalhados para a mesma venda).

Para centralizar a operação logística, acesse **Movimentações > Entregas Futuras**:
*   **Grade Superior (Pedidos Pai):** Exibe a lista consolidada das vendas originárias.
*   **Grade Inferior (Entregas Vinculadas):** Ao clicar em um pedido pai na grade superior, a parte inferior exibe instantaneamente todas as remessas atreladas àquela venda, mostrando a data agendada e o status (Aberto ou Finalizado).
*   A partir deste painel, a equipe de expedição pode filtrar as entregas do dia (ex: `10/09`), selecionar as remessas pendentes e clicar em **Finalizar Entrega** para gerar as notas fiscais de remessa de forma ágil, sem precisar reabrir as telas de venda originais.

# Pontos Críticos e Validações Fiscais

> [!warning] Tributação e Destaque de Impostos (Simples vs. Regime Normal)
> No Cenário 1 (Faturamento Total Antecipado), a regra de destaque de ICMS, PIS e COFINS gera conflitos tributários severos se não for validada pela contabilidade do cliente final.
> *   Normalmente, os impostos são destacados **integralmente na Nota Fiscal do Pedido Pai** (Natureza de Venda Futura), visto que o reconhecimento da receita ocorreu.
> *   As **Notas Fiscais de Remessa** subsequentes (que acompanham os caminhões) devem ser emitidas com CFOP específico de remessa de entrega futura e **sem destaque de impostos**, para não configurar bitributação. A incorreta parametrização das alíquotas nas naturezas de operação resultará no pagamento duplicado de impostos pelo lojista.
---
id: [CASO-002]
link: https://www.youtube.com/watch?v=1i5fiaKjcuk
setor: Desenvolvimento
modulo: Financeiro / Faturamento
tags: [plano-de-contas, erp, cmv, contabilidade, fluxo-de-caixa, estoque]
data_criacao: 2026-07-18
---

## Sumário
1. [[#1. Visão Geral da Operação de Saída]]
2. [[#2. Regras de Contabilização Financeira (Vendas)]]
	- [[#2.1. Vendas à Vista (Dinheiro ou PIX/Transferência)]]
	- [[#2.2. Vendas a Prazo (Boleto ou Crediário)]]
	- [[#2.3. Vendas no Cartão de Crédito]]
3. [[#3. Movimentação de Estoque e CMV (Custo da Mercadoria Vendida)]]
4. [[#4. Operações de Bonificação (Brindes)]]

---

## 1. Visão Geral da Operação de Saída

No contexto de sistemas ERP, a efetivação de uma saída de mercadoria (seja por venda ou bonificação) desencadeia uma série de eventos cruzados entre os módulos de [[Faturamento]], [[Financeiro]] e [[Estoque]]. 

Para manter o balancete e o demonstrativo de resultados corretos, o motor do sistema aplica o método das partidas dobradas (Débito e Crédito) em um **Plano de Contas** configurado, orquestrando as contas de origens e destinos com base na [[Natureza da Operação]], forma de pagamento e cadastro do produto.

> [!info] Regra Geral de Natureza das Contas
> - **Ativo / Despesas:** Débito (+) Aumenta | Crédito (-) Diminui
> - **Passivo / Receitas:** Crédito (+) Aumenta | Débito (-) Diminui

---

## 2. Regras de Contabilização Financeira (Vendas)

O destino dos valores da venda depende estritamente do Tipo de Documento gerado na finalização do pedido. O sistema sempre deve verificar primeiro a configuração amarrada à **Forma de Pagamento / Documento**. Se houver lacunas, deve recorrer ao que está definido na **Natureza da Operação**.

### 2.1. Vendas à Vista (Dinheiro ou PIX/Transferência)

Quando a operação é liquidada de imediato pelo cliente:
- **Débito:** Na conta configurada no módulo de **Caixa** (Ativo). Se for uma transferência, debita na respectiva conta bancária vinculada ao sistema. Aumenta o saldo em caixa.
- **Crédito:** Na conta de Receita parametrizada no documento, como `Vendas à Vista` (Receita). Aumenta o saldo de receita.

### 2.2. Vendas a Prazo (Boleto ou Crediário)

Se a venda gerou um título para pagamento futuro e o documento (como Boleto) não possui um plano de contas específico preenchido (vazio no cadastro), o sistema utiliza o plano de contas da [[Natureza da Operação]] (ex: `Venda Outros`).
- **Débito:** Na conta de `Contas a Receber` atrelada ao **cadastro do cliente** (Ativo).
- **Crédito:** Na conta de Receita correspondente, ex: `Vendas a Prazo` ou `Venda Outros` (Receita).

> [!warning] Atenção: Fallback de Plano de Contas
> Se a forma de pagamento/documento estiver sem plano de contas vinculado, o motor financeiro **deve** usar a conta de receita configurada na Natureza da Operação para evitar lançamentos orfãos e quebra do balancete.

### 2.3. Vendas no Cartão de Crédito

Operações em cartão possuem uma mudança fundamental de regra de negócio: o risco e a cobrança deixam de ser do cliente final e passam para a adquirente.
- **Débito:** **NÃO** debita o cadastro do cliente final. O débito é direcionado para a conta `Contas a Receber - [Nome da Administradora]` (ex: Cielo, Rede), configurada diretamente no cadastro da Administradora de Cartões.
- **Crédito:** Na conta de Receita `Vendas a Prazo`.

---

## 3. Movimentação de Estoque e CMV (Custo da Mercadoria Vendida)

A finalização financeira de uma venda **não** altera o estoque automaticamente; são rotinas paralelas geradas pelo mesmo evento. É estritamente na venda (e não na compra) que o sistema apropria a Despesa com o produto entregue.

O valor movimentado nesta etapa **não é o valor de venda**, mas sim o [[Custo Médio]] apurado a partir do histórico de entradas no cadastro do produto.

- **Débito:** `Custo com Mercadoria Vendida (CMV)` (Despesa). Ao debitar, aumenta-se a despesa do período.
- **Crédito:** `Estoque de Mercadorias` (Ativo). Ao creditar um ativo, reduz-se o saldo financeiro estocado.

> [!tip] Dica: Cálculo de Custo Médio
> O motor de estoque sempre deve calcular: `(Quantidade Atual * Custo Atual) + (Quantidade Nova * Custo Novo) / (Quantidade Atual + Quantidade Nova)`. Este é o valor unitário que deve ser multiplicado pela quantidade vendida para extrair os reais de crédito do estoque.

---

## 4. Operações de Bonificação (Brindes)

Quando uma saída é registrada com Natureza da Operação do tipo **Bonificação**, a lógica contábil ignora completamente o motor financeiro de contas a receber e caixa. 

**Como o sistema deve se comportar:**
1. O pedido **não** gera parcelas nem fluxo de caixa.
2. A baixa no estoque segue a regra do CMV, utilizando o preço de custo.
3. O lançamento contábil deve refletir uma perda programada (despesa) em contrapartida ao estoque.

**Lançamento Contábil:**
- **Débito:** `Bonificações Concedidas / Brindes` (Despesa). Aumenta a despesa.
- **Crédito:** `Estoque de Mercadorias` (Ativo). Diminui o estoque.

> [!info] Prática Contábil Alternativa
> Muitos gestores preferem alocar as "Bonificações" não como uma conta pai de Despesa, mas sim dentro do grupo de **Receitas**, atuando como uma conta redutora (conta de natureza devedora dentro de um grupo credor). Isso permite que o balancete apresente a Receita Bruta menos as Bonificações para apurar a Receita Líquida na mesma visão.
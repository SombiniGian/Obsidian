---
id: CASO-001
link: https://www.youtube.com/watch?v=Uk0m0jf-Reg
setor: Suporte e Implantação
modulo: Fiscal e Contábil
tags: [plano-de-contas, entradas, compras, partidas-dobradas, estoque, financeiro]
data_criacao: 2026-07-18
---

# Documentação Técnica: Plano de Contas nas Entradas de Mercadoria

## Sumário
1. [[#Conceito Base: Partidas Dobradas]]
2. [[#Cenário 1: Compra de Mercadoria (Geração Financeira)]]
3. [[#Cenário 2: Entrada por Bonificação (Sem Geração Financeira)]]
4. [[#Regras de Negócio Importantes]]

---

## Conceito Base: Partidas Dobradas

O sistema utiliza o princípio contábil de **Partidas Dobradas**, onde toda movimentação financeira ou de estoque exige obrigatoriamente, no mínimo, um lançamento a débito e um lançamento a crédito em contas distintas. 

> [!info] Tipos de Conta e Comportamentos (Regra de Ouro)
> O plano de contas é dividido em Ativos, Passivos, Receitas e Despesas. O comportamento de aumento ou diminuição de saldo depende estritamente da natureza da conta:
> - **Ativos (ex: Estoque):** Débito *aumenta* o saldo | Crédito *diminui* o saldo.
> - **Passivos (ex: Contas a Pagar):** Débito *diminui* o saldo | Crédito *aumenta* o saldo.
> - **Receitas (ex: Bonificações Recebidas):** Débito *diminui* o saldo | Crédito *aumenta* o saldo.
> - **Despesas (ex: Custo de Mercadoria):** Débito *aumenta* o saldo | Crédito *diminui* o saldo.

Essa lógica garante a rastreabilidade total para auditoria, indicando para onde o valor foi alocado (Débito) e a origem desse recurso ou obrigação gerada (Crédito).

---

## Cenário 1: Compra de Mercadoria (Geração Financeira)

Quando há uma entrada de nota fiscal referente a uma **Compra de Mercadoria**, ocorre o acréscimo de ativos no estoque e o reconhecimento simultâneo de uma obrigação (passivo) com o fornecedor.

### Fluxo de Lançamento Automático
*   **Conta Debitada:** `Estoque` (Ativo) -> O saldo financeiro estocado no sistema aumenta.
*   **Conta Creditada:** `Contas a Pagar` (Passivo) -> A obrigação financeira perante o fornecedor aumenta.

### Origem das Configurações
Para que a automação contábil funcione sem intervenção manual durante a inclusão da Nota Fiscal, o sistema realiza uma busca de cascata para encontrar as contas correspondentes:

1.  **Origem do Débito (Estoque):**
    O sistema busca a conta padrão configurada no painel principal: **Configurações de Plano de Contas** -> **Estoques** -> **Estoque Inicial**.
2.  **Origem do Crédito (Contas a Pagar):**
    Como esta operação *gera financeiro*, o sistema contorna as parametrizações da Natureza de Operação e puxa a conta credora diretamente do cadastro do fornecedor. Acesse **Pessoas** -> Selecione o Fornecedor -> aba **Plano de Contas**. 
    
> [!warning] Atenção à Falha de Lançamento
> Se o campo do plano de contas no cadastro da [[Pessoa]] (fornecedor) estiver vazio, a movimentação do contas a pagar não será lançada corretamente, quebrando a integridade da partida dobrada.

> [!tip] Dica de Parametrização da Natureza da Operação
> Para operações de compra faturada, no cadastro da **Natureza de Operação**, o parâmetro **Gera Financeiro** deve estar explicitamente marcado.

---

## Cenário 2: Entrada por Bonificação (Sem Geração Financeira)

Quando a empresa ganha uma mercadoria do fornecedor (ex: bonificação, brinde, amostra grátis), há um aumento físico e financeiro do estoque, mas **não** há geração de obrigação de pagamento (Contas a Pagar).

### Fluxo de Lançamento Automático
*   **Conta Debitada:** `Estoque` (Ativo) -> O saldo de mercadorias aumenta.
*   **Conta Creditada:** `Bonificações Recebidas` (Receita) -> O saldo de receitas é incrementado, refletindo o ganho patrimonial.

### Origem das Configurações
A ausência da obrigação financeira altera a cascata de busca de contas:

1.  **Origem do Débito (Estoque):**
    Permanece sendo resgatado das regras globais de **Configurações de Plano de Contas** -> **Estoques**.
2.  **Origem do Crédito (Bonificações Recebidas):**
    Sem geração de duplicatas para um fornecedor, o sistema **ignora** o cadastro de Pessoa. A conta de crédito passa a ser puxada diretamente de dentro do cadastro da **Natureza de Operação** que o usuário informou na nota (ex: operação de Bonificação Recebida).

---

## Regras de Negócio Importantes

### 1. Compras NÃO Geram Despesas Imediatas
> [!warning] Erro Comum de Interpretação Contábil
> É uma falha conceitual achar que registrar uma Nota Fiscal de Compra lança uma "Despesa" no sistema. A entrada de compra **apenas converte o valor monetário do seu passivo (Contas a Pagar) em um bem tangível no seu ativo (Estoque)**. A "despesa" associada a essa mercadoria será deduzida apenas no momento da baixa no estoque, ou seja, através da rotina de [[Vendas de Mercadoria]] e emissão do Custo da Mercadoria Vendida (CMV).

### 2. Gatilho de Lançamento: Nota Fiscal vs Pedido de Compra
A engine do sistema precisa saber em qual etapa do fluxo operacional o lançamento contábil deve ser "commitado". Isso é orquestrado pelas flags na **Natureza de Operação**:
- **Flag "Movimentar Estoque" MARCADA na Natureza:** O sistema presume que o usuário não adota o workflow prévio de [[Pedido de Compra]]. Assim, a efetivação das movimentações contábeis de débito e crédito é processada no momento em que se grava a **Nota Fiscal**.
- **Flag DESMARCADA:** O sistema entende que a corporação exige rigor processual; logo, a movimentação contábil ocorrerá de forma vinculada através da aprovação/faturamento do Pedido de Compra original.
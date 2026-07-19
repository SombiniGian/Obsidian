---
id:
  - CASO-207
link: https://www.youtube.com/watch?v=6esDjdhiSWU
setor:
  - Suporte
  - Implementação
  - Financeiro
modulo:
  - Estoque / Financeiro
tags:
  - plano-de-contas
  - entrada-de-nota
  - estoque
  - bonificacao
  - integracao-financeira
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Integração]]
2. [[#Origem dos Vínculos Contábeis]]
3. [[#Fluxo Operacional: Compra com Geração de Financeiro]]
4. [[#Fluxo Operacional: Entrada por Bonificação ou Brinde (Sem Financeiro)]]
5. [[#Validação de Saldos e Auditoria]]
6. [[#Pontos Críticos e Regras de Negócio]]

# Visão Geral da Integração
Esta documentação descreve o comportamento do sistema no momento da **Entrada de Nota Fiscal de Compra** e seu reflexo automatizado no [[Plano de Contas]]. O sistema realiza lançamentos contábeis gerenciais automáticos baseando-se no tipo de operação realizada: compras comerciais padrão (que geram obrigações financeiras) ou entradas não comerciais, como brindes e bonificações (que não geram obrigações a pagar).

# Origem dos Vínculos Contábeis
Para determinar quais contas do plano receberão os débitos e créditos, o motor de regras do sistema consulta duas fontes distintas de parametrização:

### 1. Cadastro de Pessoas (Fornecedor)
No cadastro de cada fornecedor, existem campos padrão pré-configurados que ditam as regras para lançamentos manuais ou automáticos:
*   **Contas a Receber**
*   **Crédito com Recebimento**
*   **Contas a Pagar:** Conta do [[Plano de Contas]] (Passivo) que representa a obrigação com aquele fornecedor específico.
*   **Receitas e Despesas:** Contas utilizadas para lançamentos manuais de caixa.

### 2. Natureza de Operação
Configuração atrelada ao tipo de nota fiscal emitida ou recebida. Contém o campo de amarração do plano de contas que será acionado caso a operação **não** gere parcelas financeiras (ex: CFOP de bonificação, brinde ou doação).

# Fluxo Operacional: Compra com Geração de Financeiro

Quando uma nota de compra com geração de duplicatas é lançada no sistema, o estoque é incrementado e uma obrigação é gerada no contas a pagar.

```json
{
  "movimentacao_compra_com_financeiro": {
    "tipo_operacao": "Entrada de Nota de Compra",
    "valor_total": 1000.00,
    "regra_origem_credito": "Cadastro do Fornecedor -> Campo: Contas a Pagar",
    "lancamentos": [
      {
        "tipo": "DEBITO",
        "conta_plano": "Ativo / Estoque de Mercadoria",
        "valor": 1000.00
      },
      {
        "tipo": "CREDITO",
        "conta_plano": "Passivo / Contas a Pagar",
        "valor": 1000.00
      }
    ]
  }
}
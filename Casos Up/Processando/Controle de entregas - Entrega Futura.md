---
id: [CASO-171]
link: https://www.youtube.com/watch?v=LdNEwnR4Emg&t=403s
setor: [Operacional, Logística, Faturamento]
modulo: [Vendas / Controle de Entregas]
tags: [entrega-futura, faturamento, controle-de-estoque, naturezas-de-operacao, expedicao]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Entrega Futura]]
2. [[#Cenário 1: Faturamento Antecipado e Entrega Fracionada]]
3. [[#Cenário 2: Orçamento com Faturamento sob Demanda (Entrega)]]
4. [[#Mecânica Operacional no Pedido de Venda]]
5. [[#Gestão Centralizada de Entregas Futuras]]
6. [[#Pontos Críticos e Validações Fiscais]]

# Visão Geral da Entrega Futura
A rotina de **Controle de Entregas** visa solucionar cenários de vendas fracionadas, permitindo a dissociação entre a emissão do título financeiro (contas a receber) e a efetiva movimentação física da mercadoria (baixa de estoque). A flexibilidade dessa operação é orquestrada através do cadastro e amarração de diferentes [[Naturezas de Operação]], permitindo que o sistema atenda desde recebimentos antecipados até controles orçamentários faturados etapa por etapa.

# Cenário 1: Faturamento Antecipado e Entrega Fracionada
Situação onde o cliente finaliza o pagamento de toda a compra no ato do pedido, mas leva fisicamente apenas uma parte dos produtos, agendando a entrega do restante para datas posteriores.

### 1. Parametrização da Natureza "Pai" (Venda Futura)
*   **Gera Financeiro:** Habilitado (Registra a totalidade da receita).
*   **Movimenta Estoque:** Desabilitado (A mercadoria permanece contabilizada no pátio da empresa).
*   **Impostos:** Geralmente com destaque total (a depender de orientação contábil).

### 2. Parametrização da Natureza "Filha" (Remessa de Entrega)
*   **Gera Financeiro:** Desabilitado (Evita a duplicidade de cobrança).
*   **Movimenta Estoque:** Habilitado (Gera a saída real dos itens).
*   **Impostos:** Normalmente sem destaque.

> [!tip] Parametrização Global para Agilidade
> Para automatizar a troca, acesse as **Configurações do Pedido de Venda > Aba Delivery/Entrega** e mapeie o campo **Entrega Futura**. O sistema preencherá automaticamente as entregas subsequentes com a natureza de remessa configurada.

# Cenário 2: Orçamento com Faturamento sob Demanda (Entrega)
Aplicado quando o cliente fecha um pacote de materiais (ex: materiais de construção para uma obra), mas o faturamento e o pagamento ocorrerão estritamente no momento em que as frações da carga forem despachadas.

### 1. Parametrização da Natureza "Pai" (Pedido de Controle)
*   **Gera Financeiro:** Desabilitado.
*   **Movimenta Estoque:** Desabilitado.
*   *Ação:* Congela a negociação e atua como uma tabela base.

### 2. Parametrização da Natureza "Filha" (Venda e Entrega)
*   **Gera Financeiro:** Habilitado.
*   **Movimenta Estoque:** Habilitado.
*   *Ação:* Transforma cada lote despachado em uma venda isolada.

# Mecânica Operacional no Pedido de Venda
A divisão da venda ocorre de forma visual dentro do módulo de faturamento.

1.  Lance os itens do pedido completo e altere a **Natureza de Operação** para a modalidade de controle/futura.
2.  Acione o atalho **ALT + E** ou clique em **Opções > Entregas**.
3.  Na tela de fracionamento, clique em **Incluir**.
4.  O painel exibe a **Coluna Esquerda** (saldo restante não entregue) e a **Coluna Direita** (itens da remessa atual).
5.  Selecione as quantidades na esquerda para transferi-las para a carga atual.
6.  **Ações de Fechamento:**
    *   **Finalizar:** Utilizado se a mercadoria está sendo expedida ou entregue no balcão naquele momento. Confirma a saída e dispara a [[NF-e]].
    *   **Salvar:** Utilizado para programar roteiros. A entrega fica registrada para a data combinada, mas com status `Não Entregue` (Em Aberto).

# Gestão Centralizada de Entregas Futuras
Evite acessar as entregas procurando pelos vários "Pedidos Filhos" gerados no balcão de vendas. O sistema conta com um módulo de despacho unificado.

*   Acesse **Movimentações > Entregas Futura**.
*   **Nível Superior:** Lista as negociações principais ("Pedidos Pai").
*   **Nível Inferior:** Ao clicar no pedido pai, a grade inferior lista detalhadamente todas as viagens atreladas, indicando o que já foi faturado e o que está pendente.
*   **Fluxo de Despacho:** O operador de expedição pode selecionar as entregas programadas para o dia e clicar diretamente em **Finalizar** neste painel para acionar o faturamento.

> [!info] Auditoria e Filtros
> A tela permite buscar entregas pendentes cruzando a **Data Programada** e a **Natureza de Operação** (ex: `10/09` + `Entrega Futura`). Isso gera um mapa logístico diário exato da frota.

# Pontos Críticos e Validações Fiscais

> [!warning] Validação Contábil de Impostos e CFOP
> A divisão entre faturamento financeiro e baixa de estoque expõe o lojista a riscos de bitributação. É crítico que a parametrização das alíquotas de ICMS e o CFOP das Naturezas de "Venda para Entrega Futura" e "Remessa de Entrega" sejam estritamente validados pelo contador da empresa para não recolher o imposto no pedido pai e novamente na remessa filha.
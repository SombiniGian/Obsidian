---
id:
  - CASO-210
link: https://www.youtube.com/watch?v=LUyzuUOmV8c
setor:
  - Suporte
  - Financeiro
  - Gestão
modulo:
  - Financeiro / DRE
tags:
  - dre
  - demonstrativo-financeiro
  - plano-de-contas
  - lucratividade
  - gestao-contabil
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do DRE]]
2. [[#Pré-requisitos Operacionais]]
3. [[#Criação e Cálculo do Demonstrativo]]
4. [[#Filtros e Recursos de Análise Visual]]
5. [[#Persistência e Comparativos Futuros]]

# Visão Geral do DRE
O **DRE (Demonstrativo de Resultado do Exercício)** é uma ferramenta gerencial essencial que consolida as informações financeiras da empresa dentro de um período customizado para evidenciar a formação do resultado líquido — ou seja, se a operação gerou **lucro** ou **prejuízo**. O demonstrativo agrupa e subtrai custos e despesas das receitas geradas, permitindo uma análise macro e micro de onde os recursos estão sendo consumidos e quais canais geram maior receita.

# Pré-requisitos Operacionais
Para que os dados exibidos no DRE sejam fidedignos e reflitam a realidade da empresa, é obrigatório que a estrutura do [[Plano de Contas]] esteja configurada corretamente. 
*   Todas as rotinas operacionais cotidianas — como o faturamento de pedidos de venda, a baixa de títulos e o lançamento de obrigações — devem estar vinculadas às contas analíticas correspondentes (ex: `Receitas com Vendas`, `Custo de Mercadoria Vendida (CMV)`, `Custo Fixo`, `Custo Variável`).
*   Se houver falha de parametrização ou lançamentos sem classificação no plano de contas, o DRE omitirá esses valores, resultando em um cálculo de resultado distorcido.

# Criação e Cálculo do Demonstrativo
O sistema permite gerar e salvar históricos de DRE para auditorias posteriores. O processo de criação compreende os seguintes passos:

1. Acesse o módulo **DRE (Demonstrativo de Resultado do Exercício)**.
2. Clique no botão **Incluir** para abrir um novo registro.
3. Preencha o campo **Descrição** com um identificador de formato livre (ex: `Agosto` ou `Ano de 2026`).
4. Defina o **Período** desejado inserindo a data inicial e a data final da análise. O sistema é flexível e permite intervalos diários, semanais, mensais ou anuais.
5. O processamento realiza a leitura em tempo real e exibe o resumo estruturado:
    *   **Total de Receitas:** Soma de todas as entradas operacionais e financeiras.
    *   **Total de Despesas:** Soma de todos os custos, despesas fixas e variáveis.
    *   **Resultado:** Indicador final líquido (Lucro se positivo, Prejuízo se negativo).

# Filtros e Recursos de Análise Visual

> [!info] Exibição de Contas Zeradas
> Por padrão, o sistema omite contas do plano que não registraram movimentação no intervalo selecionado para tornar a leitura mais limpa. Para realizar uma auditoria completa de toda a árvore contábil da empresa, marque a opção **Mostrar Zerados**. Isso expandirá a visualização exibindo todos os grupos de custos e despesas cadastrados.

> [!tip] Inclusão de Balanço Patrimonial Ligeiro
> Embora o foco nativo do DRE seja Receitas e Despesas, o operador pode marcar a opção **Ativos e Passivos**. Isso anexa ao relatório a situação patrimonial atualizada do período, exibindo dados como:
> *   Saldos em aberto de **Contas a Receber**.
> *   Valoração financeira de **Estoque** atual.
> *   Fluxo de movimentação acumulado nas contas de **Caixa e Bancos**.

A tela conta ainda com uma barra de **Pesquisa Rápida**, permitindo digitar palavras-chave (ex: `Vendas`) para filtrar e isolar ramos específicos da árvore de contas sob análise.

# Persistência e Comparativos Futuros
Ao acionar o botão de **Gravar/Salvar**, as configurações do DRE e seus respectivos filtros temporais ficam armazenados no banco de dados. Isso viabiliza a criação de uma linha do tempo histórica, permitindo consultar DRSs de meses ou anos anteriores a qualquer momento através da listagem principal.

> [!warning] Ponto de Atenção: Evolução do Recurso (Comparativo de DREs)
> O módulo foi estruturado para suportar uma futura tela de **Comparativo de Demonstrativos de Resultados**. Essa funcionalidade permitirá selecionar dois ou mais períodos gravados (ex: `Julho` vs. `Agosto`) para realizar uma análise horizontal de evolução da empresa, apontando percentualmente o aumento ou redução de despesas específicas (ex: se o custo com mercadorias ou despesas administrativas subiu) e a oscilação das margens de receita de um período em relação ao outro.
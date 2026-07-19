
---
id: [CASO-001]
link: https://www.youtube.com/?hl=pt&gl=BR&app=desktop
setor: [Suporte, Desenvolvimento, Financeiro]
modulo: [Financeiro / Plano de Contas]
tags: [plano-de-contas, configuracao-financeira, movimentacao-contabil, DRE]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Módulo]]
2. [[#Estrutura e Cadastro do Plano de Contas]]
3. [[#Configurações e Vínculos Obrigatórios]]
4. [[#Fluxo de Operação e Automatização]]
5. [[#Consultas e Relatórios (DRE)]]

# Visão Geral do Módulo
O módulo de **Plano de Contas** tem como objetivo centralizar, classificar e estruturar todas as movimentações financeiras da empresa (Ativos, Passivos, Receitas e Despesas). A correta parametrização deste recurso permite que lançamentos operacionais — tais como faturamento de vendas e registros de contas a pagar — gerem reflexos contábeis automáticos, viabilizando auditorias por meio de extratos dedicados e preparando a base de dados para a consolidação do [[Demonstrativo de Resultado do Exercício (DRE)]].

# Estrutura e Cadastro do Plano de Contas
A estrutura é organizada de forma hierárquica e customizável, dividida em quatro grandes grupos nativos:
*   **Ativos:** Contas que representam os bens e direitos (ex: saldos bancários, caixas físico, contas a receber).
*   **Passivos:** Contas que representam as obrigações e deveres (ex: fornecedores, contas a pagar).
*   **Receitas:** Entradas geradas pela atividade operacional ou financeira (ex: vendas de mercadorias).
*   **Despesas:** Saídas para manutenção da operação (ex: despesas administrativas, gastos com viagem).

### Criando uma Nova Conta Analítica
Para adicionar uma subconta ou despesa específica na árvore hierárquica:
1. Acesse o menu de cadastro do **Plano de Contas**.
2. Identifique o grupo pai adequado (ex: **Outras Despesas**).
3. Insira a descrição do novo item (ex: `Gasto com viagem`).
4. Confirme a gravação para disponibilizar a conta para uso nos demais módulos do sistema.

# Configurações e Vínculos Obrigatórios
Para que a automatização funcione sem erros, o **Plano de Contas** precisa ser previamente mapeado em múltiplos cadastros de apoio dentro do sistema. 

> [!warning] Atenção
> A ausência desses vínculos impedirá o lançamento automático na contabilidade gerencial no momento em que uma venda for faturada ou um título for pago, gerando inconsistências nos relatórios de saldos.

Abaixo estão as telas e os campos específicos que exigem amarração:

### 1. Cadastro de Pessoas (Clientes e Fornecedores)
Na aba **Plano de Contas** do registro da pessoa, informe:
*   Conta para lançamentos de **Contas a Receber** (Débito) e seu respectivo **Crédito com Recebimento**.
*   Conta para lançamentos de **Contas a Pagar** (Crédito) e seu respectivo **Crédito com Pagamento**.
*   Conta para **Cheques a Receber**.

### 2. Cadastro de Caixas e Contas Bancárias
*   **Caixa Físico:** Vincule a conta do plano correspondente (ex: `Caixa Principal`) para onde o saldo real deve ser direcionado.
*   **Contas Bancárias:** Vincule a conta principal do banco e preencha as abas adicionais indicando as contas de destino para:
    *   **Boletos a Receber**
    *   **Despesas Bancárias**
    *   **Cheques a Compensar**

### 3. Natureza de Operação (Fiscal / Vendas)
*   Configure em cada **Natureza de Operação** qual conta de receita do plano deve absorver os valores das vendas executadas sob aquela parametrização (ex: `Receitas com Vendas`).

# Fluxo de Operação e Automatização

### Cenário A: Faturamento Automático de Pedido de Venda
Quando um **Pedido de Venda** é criado e o operador executa a ação de **Faturar** gerando uma duplicata (boleto, por exemplo), o sistema realiza automaticamente um duplo lançamento na tabela de movimentações do plano de contas:

```json
{
  "movimentacao_contabil": {
    "origem": "Faturamento de Venda (Pedido 23)",
    "valor": 300.00,
    "lancamentos": [
      {
        "tipo": "DEBITO",
        "conta_plano": "Ativos / Contas a Receber",
        "historico": "Movimento referente parcela da venda 23"
      },
      {
        "tipo": "CREDITO",
        "conta_plano": "Receitas / Vendas de Mercadorias",
        "historico": "Movimento referente parcela da venda 23"
      }
    ]
  }
}

### Cenário B: Lançamento Manual de Despesa / Pagamento

Ao registrar um novo compromisso financeiro:

1. Acesse a tela de inclusão de contas a pagar.
    
2. Selecione o credor/fornecedor configurado.
    
3. No campo de classificação, selecione a conta analítica desejada (ex: `Gasto com viagem`).
    
4. Informe o valor do documento (ex: `100,00`).
    
5. Ao **Salvar/Incluir**, o sistema gera imediatamente a contrapartida:
    
    - **Débito:** Na conta de resultado correspondente (`Despesas / Outras Despesas / Gasto com viagem`).
        
    - **Crédito:** Na conta de obrigação passiva (`Passivos / Contas a Pagar`).
        

# Consultas e Relatórios (DRE)

### Saldo por Plano de Contas

A tela **Saldo por Plano de Contas** permite visualizar a saúde financeira consolidada dentro de um intervalo de datas parametrizável.

- **Filtro "Mostrar Zerado":** Ao desmarcar esta opção, a interface oculta todas as contas que não possuem movimentação no período, otimizando a leitura das informações com saldo ativo.
    

> [!tip] Dica
> 
> Utilize a árvore de expansão e retração (ícones de fechar/abrir os nós de Ativo, Passivo, Receitas e Despesas) para obter uma visão macro ou detalhada do desempenho da empresa rapidamente.

### Extrato de Plano de Contas

Para auditar a origem de um valor exibido no saldo, utilize a rotina de **Extrato de Plano de Contas**.

- **Como emitir:** Informe a conta analítica desejada (ex: `Gasto com viagem` ou `Receitas com Vendas`) e defina o período. O sistema retornará uma lista cronológica detalhando cada número de documento, histórico do lançamento e valor individualizado.
    

### Integração com o DRE

Todas as classificações realizadas no cotidiano operacional são a matéria-prima para o [[Demonstrativo de Resultado do Exercício (DRE)]]. No fechamento do mês, o sistema cruza as receitas e despesas registradas em suas respectivas ramificações para deduzir impostos, custos e despesas operacionais, exibindo de forma analítica o lucro líquido ou prejuízo do período avaliado.


http://googleusercontent.com/youtube_content/1
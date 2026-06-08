Este módulo abrange o controle das obrigações financeiras da empresa, a automação de despesas recorrentes, o fluxo de comissionamento da equipe comercial e as operações avançadas de acerto de contas (endosso).

---

## 1. Gestão de Pagamentos (Contas a Pagar)

A estrutura da tela de "Pagamentos" compartilha a mesma arquitetura lógica da tela de "Recebimentos", garantindo uma curva de aprendizado unificada para o analista financeiro.

* **Origem dos Lançamentos:**
  * **Automática:** Títulos gerados nativamente a partir da entrada de um XML de Fornecedor (Documentos Recebidos / Nota Fiscal de Compra).
  * **Manual:** Inserção avulsa para despesas operacionais (ex: conta de luz, aluguel, salários).
* **Ferramentas de Agilidade (Replicação):** O sistema possui funções nativas em *Opções* para **Duplicar** e **Replicar Pagamentos para o próximo mês**. Ideal para lançar rapidamente despesas fixas recorrentes sem precisar redigitar os dados.
* **Extração de Dados em Tela:** O analista não precisa acessar o módulo de relatórios para extrações simples. A própria tela (*grid*) possui opções para "Expandir Agrupamentos", "Exportar Grade" e "Imprimir Grade", entregando o extrato de contas a pagar do mês imediatamente.

## 2. Operação de Troca de Endosso (Acerto de Contas)

Uma rotina fundamental para empresas que permitem que seus funcionários ou fornecedores comprem na própria loja utilizando crediário.

* **Conceito Prático:** Permite cruzar um título do "Contas a Pagar" com um título do "Contas a Receber" para realizar um abatimento mútuo.
* **Cenário de Uso:** Um funcionário consumiu R$ 150,00 na loja durante o mês (gerando um Contas a Receber). Ao final do mês, a empresa possui a folha de pagamento deste funcionário (Contas a Pagar). O operador financeiro seleciona os títulos correspondentes e realiza a baixa casada, descontando o vale (dívida) do salário (crédito) sem movimentar dinheiro vivo no caixa.

## 3. Cobrança Recorrente e Mensalistas (Borderô de Cobrança)

Módulo focado em prestadores de serviços, escolas ou empresas de software (como o próprio ecossistema de revenda) que trabalham com faturamento mensal recorrente.

* **Parametrização no Cadastro:** O cliente deve estar assinalado com a *flag* "Mensalista" em seu cadastro principal.
* **Geração em Lote:** O operador configura uma "Modalidade de Cobrança" (ex: número de parcelas ou contrato infinito). No módulo de **Borderô de Cobrança**, o sistema puxa todos os clientes habilitados na respectiva modalidade.
* **Faturamento Massivo:** A partir deste único borderô, o sistema dispara a geração de três documentos simultâneos para todo o lote de clientes:
  1. Cria os novos títulos no Contas a Receber.
  2. Gera e transmite os Boletos Bancários.
  3. Emite os lotes de Notas Fiscais de Serviço (NFS-e), podendo inclusive disparar tudo por e-mail de forma configurada.

## 4. Apuração e Borderô de Comissão

A ferramenta automatiza o acerto financeiro com a equipe de vendas (vendedores, técnicos, representantes), calculando o saldo devido com base nas configurações da empresa.

* **Critérios de Apuração:** O sistema permite extrair o relatório de comissões baseado em duas regras de negócios primárias:
  * **Por Emissão (Competência):** A comissão é gerada no momento em que a venda/OS é finalizada, independentemente de o cliente ter pago ou não.
  * **Por Baixa (Caixa):** A comissão só é apurada e liberada quando o título do cliente é efetivamente pago e baixado no financeiro.
* **Composição do Cálculo:** O motor varre o período selecionado somando comissões de Vendas e Ordens de Serviço (OS), e deduzindo automaticamente os valores de **Devoluções** de mercadorias.
* **Geração Automática de Pagamento:** Após processar e conferir a apuração na tela, o operador clica em "Gerar Comissões". O sistema encerra o período para aqueles vendedores e gera automaticamente os títulos correspondentes no **Contas a Pagar**, prontos para liquidação pela tesouraria.
---
id: CASO-001
link: https://www.youtube.com/watch?v=gSAvVdiPdwY
setor: Vendas e Faturamento
modulo: Pedido de Venda / Financeiro
tags: [desconto-condicional, saldo-vendedor, boleto, faturamento, retaguarda, mobile]
data_criacao: 2026-07-18
---

# Documentação Funcional: Desconto Condicional em Boletos

## Sumário
- [[#Conceito e Objetivo]]
- [[#Pré-requisitos e Configurações Básicas]]
    - [[#Configuração do Vendedor]]
    - [[#Configuração da Natureza de Operação]]
- [[#Regras de Negócio e Comportamento do Sistema]]
- [[#Fluxo de Execução Sistema de Retaguarda (Desktop)]]
- [[#Fluxo de Execução Aplicativo Mobile (Força de Vendas)]]

---

## Conceito e Objetivo

O **Desconto Condicional** é uma ferramenta estratégica de incentivo à adimplência que permite conceder um abatimento financeiro apenas se o cliente realizar o pagamento do boleto até uma data pré-determinada (como o dia do vencimento ou dias específicos anteriores a ele). 

> [!info] O Paradigma do Saldo do Vendedor
> Para manter a saúde financeira da distribuidora/empresa, a funcionalidade atua com um sistema de créditos. O vendedor acumula um **Saldo Condicional** gerado dinamicamente a partir de suas negociações (ex: venda de produtos acima da tabela de preço padrão, ou percentual sobre o faturamento). O vendedor atua como um gestor desse saldo, só podendo repassar descontos aos clientes dentro do limite financeiro disponível em sua "conta" no ERP.

---

## Pré-requisitos e Configurações Básicas

Para que a opção de desconto seja exibida na finalização de um [[Pedido de Venda]], o sistema exige a parametrização prévia de duas entidades cruciais.

### Configuração do Vendedor

No **[[Cadastro de Vendedor]]**, deve-se habilitar e parametrizar as regras de acúmulo de crédito e prazos.

1. **Query Geradora de Saldo:** O sistema disponibiliza um campo de texto livre que executa instruções diretamente no banco de dados. Você deve incluir uma `query` SQL que definirá a regra de negócio para a geração desse crédito. O ERP fornecerá parâmetros automáticos de entrada e receberá as saídas para preencher a carteira do usuário.
2. **Dias Antes do Vencimento:** No campo **Dias Antes**, configure a defasagem temporal de validade do abatimento.

> [!tip] Dica de Configuração de Prazo
> Se a diretriz comercial for conceder o desconto se o cliente pagar o boleto *exatamente até a data de vencimento*, preencha o campo **Dias Antes** com o valor `0` (zero). Um valor como `5` significa que o título só terá redução se quitado até 5 dias antes do vencimento impresso.

### Configuração da Natureza de Operação

Nem todas as operações (ex: bonificações, devoluções) devem permitir concessão de abatimento financeiro.
1. Acesse a tela de **[[Natureza de Operação]]**.
2. Marque a flag que **permite Desconto Condicional**. Sem isso, a interface de totais ocultará os botões de crédito na geração de pedidos com essa natureza.

---

## Regras de Negócio e Comportamento do Sistema

* **Validação de Limite:** A arquitetura conta com uma trava rígida. O vendedor será bloqueado caso tente inserir um valor em reais (`R$`) ou percentual (`%`) superior ao saldo gerado via SQL. O sistema emitirá o aviso de **Limite Ultrapassado**.
* **Isolamento do Valor da Venda:** A aplicação do desconto condicional **não altera** o preço final dos itens ou do [[Pedido de Venda]] na base do sistema. Ele atua de forma inerte na venda e só é deflagrado e enviado como regra acessória na **[[Emissão de Boletos]]**.
* **Rateio Automático de Parcelas:** Caso a forma de pagamento demande parcelamento (ex: faturamento com duas duplicatas), a rotina do ERP fará a divisão igualitária do desconto pelos boletos. Um desconto de R$ 35,00 em um pedido com duas parcelas refletirá em um abatimento de R$ 17,50 por boleto.

> [!warning] Atenção: Trava de Integridade do Pedido
> Após a inserção do Desconto Condicional na aba de totais, **o sistema bloqueia qualquer alteração nos itens, valores ou estrutura do pedido**. Esta regra previne fraudes e inconsistências entre o saldo deduzido e o valor do pedido. Caso seja necessária qualquer alteração na venda, o usuário deve, primeiramente, retornar à aba de fechamento, informar `0` no campo de desconto e só então realizar as edições.

---

## Fluxo de Execução: Sistema de Retaguarda (Desktop)

A retaguarda consolida a venda sob as regras de proteção de saldo explicadas anteriormente.

1. Inicie a inclusão de um novo pedido e defina o cliente.
2. É obrigatório selecionar uma **Natureza de Operação** validada para descontos condicionais.
3. Insira todos os produtos, defina as quantidades e, em seguida, configure a aba de **Forma de Pagamento**.
4. Acesse a aba de totalizadores. Nela, verifique a visualização do quadro de **Desconto Condicional**, que evidenciará o saldo instantâneo disponível do vendedor logado.
5. Insira o valor desejado (por percentual ou valor fechado).
6. Clique em **Salvar**. A partir de agora o saldo global do vendedor foi deduzido em segundo plano.
7. Encaminhe o pedido para o módulo de **[[Faturamento]]**.
8. Na geração financeira, verifique o PDF do documento. O layout mostrará no corpo descritivo a instrução parametrizada (ex: "Conceder desconto de R$ X para pagamentos até a data Y").

---

## Fluxo de Execução: Aplicativo Mobile (Força de Vendas)

O aplicativo conta com suporte para atualizar os saldos e espelhar integralmente o comportamento do desktop de forma remota.

1. Após o login, o *dashboard* inicial do vendedor substituirá o "Saldo Flex" tradicional, exibindo em destaque o **Saldo Condicional**.
2. Abra um novo orçamento/pedido e adicione o cabeçalho comercial (Cliente, **Natureza de Operação** e **Forma de Pagamento**).
3. Após inserir todos os SKUs, navegue para a tela **Totais**.
4. O campo correspondente estará disponível. Se o dispositivo estiver **online**, ele fará uma requisição *live* ao servidor, garantindo a posição exata da carteira do vendedor. Caso esteja offline, utilizará a memória transacional da última sincronização.
5. Digite o valor do desconto e clique em **Aplicar Desconto**.
6. A tela entra em modo de bloqueio para edições de inventário. O saldo total da interface do aplicativo já apresentará o abatimento do saldo na mesma hora.
7. Após o envio para o servidor, a impressão do boleto — mesmo que gerada no ambiente mobile — já computará o rateio nas parcelas vinculadas ao documento financeiro gerado.
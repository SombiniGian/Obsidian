---
id: CASO-001
link: https://www.youtube.com/watch?v=EsjGMFQM9yg
setor: Suporte
modulo: Faturamento / PDV
tags: [configuracao, pdv, estacao_trabalho, rotina_vendas]
data_criacao: 2026-07-18
---

# Configuração de Estação de Trabalho como PDV Direto

Esta documentação detalha o comportamento, fluxo de operação e parametrização do sistema quando uma estação de trabalho é configurada para iniciar diretamente na tela de **Ponto de Venda (PDV)**.

## Sumário
- [[#Pré-requisitos e Comportamento de Inicialização]]
- [[#Fluxo de Operação no PDV]]
- [[#Tratamento de Pedidos em Aberto]]
- [[#Limitações e Restrições do Modo PDV]]

---

## Pré-requisitos e Comportamento de Inicialização

A definição do tipo de estação determina a interface primária apresentada ao usuário assim que o login no [[ERP]] é realizado.

> [!info] Conceito Chave
> Quando o parâmetro **Tipo de Estação** está definido como **PDV**, o sistema ignora o menu principal padrão e carrega automaticamente a tela de vendas de forma nativa e persistente sempre que o operador acessar o sistema.

> [!warning] Atenção antes da configuração
> Certifique-se de realizar todas as manutenções cadastrais, configurações tributárias e parametrizações gerais do sistema **antes** de ativar esta opção na estação. Após a ativação, o acesso aos menus administrativos fica restrito nesta máquina.

---

## Fluxo de Operação no PDV

O terminal opera com foco em agilidade, otimizando o fluxo de atendimento ao cliente final.

### Registro e Emissão de Vendas
1. O sistema inicia diretamente com o cursor posicionado para a inserção de produtos.
2. Insira os itens através do código interno, código de barras ou busca nominal.
3. Para concluir o processo básico, avance para a tela de fechamento, selecione a modalidade de pagamento (Dinheiro, Cartão, etc.) e confirme. O sistema exibirá o cálculo automático de **Troco** sempre que o valor recebido for maior que o total da venda.

---

## Tratamento de Pedidos em Aberto

O modo PDV permite a retenção temporária e a retomada de atendimentos não finalizados, funcionalidade útil para cenários de [[Consignação]] ou interrupção de atendimento na fila.

### Como Salvar e Retomar um Pedido
* **Gravação Temporária:** É possível salvar um pedido em estado "Aberto" sem exigir a sua liquidação imediata.
* **Pesquisa e Resgate:** Para recuperar o documento, utilize o botão ou atalho de **Pesquisar Pedido**. A interface listará os registros pendentes. Selecione o pedido desejado e clique em **Abrir**.
* **Modificação:** O sistema reabre a estrutura do pedido, permitindo a inclusão de novos itens ou a alteração de quantidades antes do fechamento definitivo.

---

## Limitações e Restrições do Modo PDV

Para garantir a segurança da operação de caixa e evitar desvios de função do operador, este modo possui bloqueios nativos de interface.

> [!warning] Pontos Críticos e Restrições
> * **Acesso a Configurações:** Sob este modo de operação, as opções de **Configurações de Venda** e painéis de parametrização do sistema ficam completamente ocultos e inacessíveis para evitar alterações indevidas por parte do operador.
> * **Pedidos Finalizados:** Ao consultar um pedido que já foi liquidado/encerrado, o sistema assume o status de **Apenas Visualização**. O botão e a permissão para realizar novas vendas ou edições sobre este documento específico são desabilitados pela interface.

Se houver necessidade de reconfigurar o comportamento da gaveta de dinheiro, impressora fiscal ou tabelas de preço, será necessário reverter temporariamente o tipo de estação nas configurações globais por meio de uma estação administrativa.

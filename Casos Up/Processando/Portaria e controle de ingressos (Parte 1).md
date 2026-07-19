---
id: CASO-212
link: https://www.youtube.com/watch?v=OBLF_swZOtM
setor: Suporte / Implantação
modulo: Restaurante / Controle de Ingressos e Portaria
tags:
  - portaria
  - comanda
  - ingressos
  - configuracao
data_criacao: 2026-07-18
---

## Sumário
1. [[#Visão Geral do Módulo]]
2. [[#Cadastro de Tipos de Ingresso]]
3. [[#Controle e Inclusão de Ingressos]]
4. [[#Mapeamento e Vínculo com Comandas]]
5. [[#Parâmetros e Configurações Globais]]
6. [[#Operação de Portaria (Entrada e Saída)]]
7. [[#Pontos de Falha e Validações Críticas]]

---

## Visão Geral do Módulo

O módulo de **Controle de Ingressos e Portaria** do Oxystem foi desenvolvido para gerenciar o fluxo de acesso de clientes a estabelecimentos como casas de festas, shows, bares e restaurantes. A ferramenta é altamente flexível, permitindo cobrir cenários que vão desde a venda antecipada de ingressos com validação de código de barras até o controle simples de portaria de restaurantes via entrega e fechamento de [[Comandas]].

> [!info] Informação
> A dinâmica do sistema adapta-se conforme o perfil do estabelecimento: impede a evasão de clientes em locais com consumo interno e agiliza o fluxo de bilheteria em eventos com cobrança diária ou recorrente.

---

## Cadastro de Tipos de Ingresso

O gerenciamento inicial do acesso baseia-se no cadastro estruturado de modalidades de ingressos. O acesso a esta funcionalidade ocorre no menu do **Módulo Restaurante**, localizando a opção de cadastro correspondente.

### Campos e Regras de Negócio:
* **Descrição do Ingresso**: Identificação clara do tipo (ex: "Ingresso Masculino Inteiro", "Cortesia", "Show do Rappa").
* **Evento Todos os Dias**: Opção ideal para bares ou restaurantes que possuem cobrança regular de portaria/couvert artístico fixo diário.
* **Data e Hora do Evento**: Para eventos e shows com data/hora específicas, o ingresso fica restrito ao período determinado.
* **Valor**: Preço de venda a ser lançado no financeiro no momento da emissão.

---

## Controle e Inclusão de Ingressos

A tela de **Controle de Ingresso** centraliza o monitoramento de todos os acessos vendidos e emitidos no sistema. 

### Ciclo de Vida do Status do Ingresso:
* **Em Aberto**: O cliente adquiriu o ingresso, mas ainda não realizou a validação física na portaria do estabelecimento.
* **Entrado**: A entrada do cliente foi validada; o portador encontra-se ativamente no interior do recinto.
* **Finalizado**: O processo de saída foi concluído (e o consumo pago, quando aplicável).
* **Cancelado**: A venda do ingresso foi desfeita e invalidada para acesso.

### Fluxo de Inclusão Manual:
1. Acesse a tela de inclusão e selecione o cliente (pesquisa padrão ou digitação direta do **CPF**).
2. Se o **CPF** já constar na base, os dados do cliente serão carregados automaticamente.
3. Insira o tipo de ingresso desejado.
4. Defina a **Forma de Pagamento** (dinheiro, cartão, etc.). O sistema permite definir o acerto financeiro direto na inclusão ou postergar para a saída do cliente.

---

## Mapeamento e Vínculo com Comandas

Para estabelecimentos que operam com consumo interno atrelado à entrada, o sistema automatiza o vínculo entre a validação do ingresso e a abertura de contas de consumo no [[Mapa de Mesas]].
[Inclusão/Leitura do Ingresso]
│ 
▼ [Validação de Entrada]──► (Obriga digitação do número da Comanda) 
│ 
▼ [Abertura Automática no Mapa de Mesas] ──► Lançamento de Itens via Caixa/Garçom

> [!tip] Dica > Quando a portaria executa o comando de entrada e digita o número da comanda física entregue ao cliente, o terminal do caixa ou o dispositivo do garçom já reconhece instantaneamente aquela numeração como ativa, permitindo o lançamento imediato de itens (ex: bebidas, porções). 
 
>## Parâmetros e Configurações Globais As regras de validação da portaria respondem diretamente às marcações feitas na aba **Ingresso** dentro das configurações gerais do pedido de venda: * **Obrigatatório Ingresso**: Quando ativo, impede que operadores ou garçons iniciem uma comanda ou pedido no sistema que não esteja previamente associado a um ingresso validado na portaria. * **Obrigatatório Comanda**: Força o preenchimento do número da comanda física assim que a portaria der a entrada no ingresso. * **Obrigatatório Código do Ingresso**: Exige a inserção de um identificador único (ou leitura de código de barras) para salvar ou validar o ingresso. * **Receber pagamento ao incluir ingresso**: Registra o fluxo financeiro de forma imediata na emissão do ticket. * **Registrar entrada ao incluir**: Ideal para eventos sem venda antecipada; ao salvar a venda do ingresso, o sistema altera o status do cliente diretamente para **Entrado**. * **Registrar saída ao finalizar a comanda**: Automação que altera o status do ingresso para **Finalizado** assim que o operador do caixa fecha a conta da comanda, eliminando a necessidade de uma segunda validação de saída na portaria. * **Tipo de Busca (Entrada / Saída)**: Define qual chave de busca o operador usará nas telas de conferência rápida (Código do Ingresso, Código Interno, CPF, Número da Comanda ou Número do Pedido). --- ## Operação de Portaria (Entrada e Saída) A tela de **Portaria** atua como uma interface de contingência otimizada e simplificada para uso em monitores ou terminais dedicados nos acessos físicos do estabelecimento. ### Ações Disponíveis: 1. **Novo Ingresso**: Atalho para vendas rápidas de ingressos diretamente na fila de entrada. 2. **Registrar Entrada**: Abre o campo de busca parametrizado. O operador digita ou bipa a informação (ex: código `160`). Se o código for válido e estiver **Em Aberto**, o sistema solicita o número da comanda correspondente e altera o status para **Entrado**. 3. **Registrar Saída**: Utilizado no portão de saída do estabelecimento. O operador digita o parâmetro configurado (ex: o número da comanda). O sistema valida se o pedido financeiro correspondente já foi faturado e fechado pelo caixa. --- ## Pontos de Falha e Validações Críticas


> [!warning] Atenção: Validações de Segurança contra Fraudes e Evasão > * **Ingresso Não Localizado**: Ocorre se o código digitado ou bipado não constar no banco de dados do dia ou do evento atual. > * **Ingresso já Utilizado**: Caso um código com status **Entrado** ou **Finalizado** seja bipado novamente na entrada, o sistema bloqueia o acesso e exibe o horário exato em que a primeira entrada foi registrada, evitando a falsificação por cópias/xerox de ingressos. > * **Pedido em Aberto na Saída**: Se o cliente tentar passar pela portaria de saída e o operador digitar a comanda correspondente a um pedido que **não foi faturado** no caixa, o sistema emitirá o alerta técnico: `"Pedido não finalizado, não é possível registrar a saída"`. O portador deve ser reencaminhado ao caixa para acerto.





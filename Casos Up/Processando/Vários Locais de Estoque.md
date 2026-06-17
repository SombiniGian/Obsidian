https://www.youtube.com/watch?v=SbN02Qu57Zc&pp=0gcJCT4LAYcqIYzv

Este módulo detalha as diretrizes operacionais, a parametrização fiscal e o fluxo de movimentação para o controle de **Vários Locais de Estoque (Múltiplos Depósitos)** no ERP Código UP. O recurso foi desenvolvido para empresas que necessitam gerenciar e rastrear o saldo de um mesmo produto distribuído entre diferentes espaços físicos (ex: gôndola/salão de vendas, depósito central, almoxarifado ou veículos de frota) de forma isolada `[00:00:08]`, `[00:00:21]`.

### 1. Habilitação e Visualização Segmentada `[00:00:52]`

Para ativar a fragmentação física do inventário no sistema, o integrador ou administrador deve parametrizar a visualização correta `[00:00:52]`:

- **Ativação da Flag de Controle:** É necessário marcar a opção **"Estoque por Empresa"** nas configurações gerais do sistema `[00:01:00]`.
    
- **Exibição na Ficha do Item:** Após a ativação, o ERP altera a parte inferior da tela de cadastro de produtos. Passa a ser exibida uma grade detalhada listando cada empresa ativa na base de dados, acompanhada de seus respectivos locais de estoque cadastrados e as quantidades específicas de saldo contidas em cada um (ex: o Produto 141 exibe saldos separados para o "Estoque Principal" e para o "Depósito 2") `[00:01:06]`, `[00:01:13]`.
    
- **Cadastro de Almoxarifados:** No menu _Local Estoque_, o gestor pode criar quantos pontos de armazenamento julgar necessários para a operação logística `[00:01:24]`. Durante o processo de atualização do ERP, um local denominado "Estoque Principal" é gerado de forma automática para agrupar o saldo preexistente, garantindo compatibilidade para clientes que não utilizam a função `[00:01:59]`, `[00:02:05]`.
    

### 2. Vinculação Automatizada via Natureza de Operação (CFOP) `[00:01:34]`

Para evitar que o operador de caixa ou faturista precise selecionar manualmente de qual depósito a mercadoria está saindo a cada venda, o ERP Código UP integra essa inteligência ao motor fiscal do sistema `[00:01:34]`:

- **Amarração na Regra Fiscal:** Dentro do cadastro de _Natureza de Operação_ (ex: regras de Venda de Mercadorias, Remessas, etc.), o administrador deve predefinir o **Local do Estoque Padrão** atrelado àquela operação `[00:01:43]`, `[00:01:53]`.
    
- **Comportamento no PDV e Faturamento:** Quando o Frente de Caixa (PDV) processa um cupom ou o comercial emite uma NF-e, o ERP consulta a Natureza de Operação aplicada. Ele realiza a baixa de estoque de forma automatizada no depósito correspondente configurado (ex: vendas de balcão baixam do "Estoque Principal") `[00:02:12]`, `[00:02:18]`. Caso nenhuma regra esteja preenchida na natureza, o sistema utiliza o "Estoque Principal" como _fallback_ (padrão de contingência) `[00:01:59]`.
    

### 3. Onipresença do Campo de Estoque nas Telas do Sistema `[00:02:25]`

Com o recurso ativo, todas as interfaces que geram fluxo de entrada, saída ou contagem de mercadorias passam a exibir obrigatoriamente o campo de seleção do almoxarifado responsável `[00:02:25]`. Isso inclui as rotinas de `[00:02:32]`:

- Inventários e Módulos de Ajuste de Estoque;
    
- Pedidos de Compra e Notas Fiscais Recebidas (Entradas);
    
- Pedidos de Venda e Notas Fiscais Emitidas (Saídas).
    

### 4. Módulo de Transferência entre Locais e Empresas `[00:03:04]`

Para realizar o remanejamento físico de itens sem gerar uma operação de compra ou venda comercial, o ERP disponibiliza a ferramenta de **Transferência de Estoque** `[00:03:04]`.

```
+------------------------------------------------------------------------+
|                      MÓDULO DE TRANSFERÊNCIA DE ESTOQUE                |
+------------------------------------------------------------------------+
|                                                                        |
|  [Selecione a Empresa de Origem] ──► [Selecione o Local de Origem]      |
|                                        (Ex: Estoque Principal)         |
|                                                  │                     |
|                                                  ▼                     |
|  [Selecione a Empresa de Destino] ─► [Selecione o Local de Destino]     |
|                                        (Ex: Depósito 2)                |
|                                                  │                     |
|                                                  ▼                     |
|  [Insira os Itens e Quantidades] ──► [Efetue a Transferência no Sistema] |
|                                                                        |
+------------------------------------------------------------------------+
```

Essa rotina permite equilibrar os saldos do inventário de duas formas `[00:03:21]`:

1. **Transferência Intraempresa:** Movimentação de produtos entre depósitos da mesma empresa (ex: retirando do _Estoque Principal_ e enviando para o _Depósito 2_) `[00:03:27]`.
    
2. **Transferência Interempresa:** Movimentação de saldo de estoque entre CNPJs / empresas diferentes cadastrados na mesma base de dados `[00:03:21]`, `[00:03:36]`.
    

### 5. Boas Práticas e Auditoria Fiscal `[00:03:42]`

O faturamento de Notas Fiscais Eletrônicas exige atenção redobrada quanto à conciliação de saldos `[00:03:42]`. Ao emitir uma nota fiscal, os itens herdam o local de estoque com base na Natureza de Operação `[00:03:55]`, `[00:04:03]`.

O sistema permite que o emissor altere manualmente o local do estoque item por item na nota, caso haja necessidade de retirar a mercadoria de um depósito específico `[00:04:24]`. Como boa prática, o sistema orienta que, se não houver saldo suficiente no local configurado para a emissão fiscal, o gestor deve rodar a rotina de _Transferência de Estoque_ previamente, abastecendo o almoxarifado correto antes de consolidar a operação de saída `[00:04:11]`,
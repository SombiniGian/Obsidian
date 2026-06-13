Este módulo detalha o funcionamento e as regras de negócio da ferramenta centralizada de **Precificação de Produtos** do ERP Código UP. O recurso foi projetado para desacoplar a gestão financeira de preços da rotina de recebimento físico de mercadorias, permitindo realizar reajustes em lote, aplicar markup inteligente e gerenciar exceções como promoções ou produtos com preços vinculados `[00:01:05]`.

### 1. Desacoplamento Operacional (Notas Fiscais vs. Gestão de Preços) `[00:00:17]`

Originalmente, o cálculo de custo de mercadorias e a sugestão de preços ocorriam exclusivamente de forma interna, no ato de lançamento da Nota Fiscal de Entrada ou do Pedido de Compra `[00:00:25]`.

A criação da tela externa de _Precificação de Produtos_ (localizada no menu _Movimentações > Compras_) resolve um problema comum em empresas de médio porte: **a segregação de funções** `[00:00:07]`. Muitas vezes, o operador do almoxarifado responsável por dar entrada na nota fiscal e conferir o físico não possui alçada ou conhecimento estratégico para alterar a tabela de preços de venda da empresa `[00:01:10]`. Com este painel, o gestor financeiro ou comercial pode auditar e aplicar as alterações de preços de um período inteiro em uma única tela, sem precisar abrir os documentos fiscais individualmente `[00:01:05]`.

### 2. Indicadores Visuais e Auditoria de Margens (Grid Dinâmica) `[00:01:18]`

A interface de precificação utiliza códigos de cores baseados em semáforos (_KPIs_) para alertar o gestor sobre a saúde das margens de lucro de cada item, cruzando o comportamento do **Markup Desejado** contra o valor praticado `[00:01:32]`:

- **Status de Margem (Markup):**
    
    - 🟡 **Amarelo:** Alerta de faixa intermediária. O preço praticado está em um patamar razoável, situado entre as margens mínima e máxima aceitáveis para o produto `[00:01:42]`.
        
    - 🔴 **Vermelho:** Alerta crítico. O preço de venda atual está abaixo da margem mínima permitida pelo markup cadastrado, indicando prejuízo ou perda de rentabilidade operacional `[00:01:52]`.
        
    - 🟢 **Verde/Boa Margem:** Indica que o preço atual está acima da margem máxima, garantindo o retorno financeiro planejado `[00:01:52]`.
        
- **Comportamento do Custo `[00:02:01]`:** O sistema monitora as oscilações de mercado indicando visualmente se o _Custo Novo_ gerado pela última entrada de mercadoria é **Maior** 📈 ou **Menor** 📉 em relação ao _Custo Anterior_ registrado no banco de dados.
    

### 3. Filtros Estratégicos de Reajuste em Lote `[00:02:15]`

A ferramenta permite criar visões de dados focadas em correções de urgência. O gestor pode combinar os filtros da grade para isolar os produtos mais vulneráveis da seguinte forma `[00:02:15]`:

1. **Filtro de Preço Inalterado:** `Preço de Venda Novo` **=** `Preço de Venda Anterior` (Garante a seleção apenas de itens cujos preços de balcão ainda não foram reajustados) `[00:02:24]`.
    
2. **Filtro de Custo Inflacionado:** `Custo Novo` **>** `Custo Anterior` (Filtra apenas mercadorias que ficaram mais caras na última compra) `[00:02:31]`.
    

Ao executar esse cruzamento, o ERP gera um relatório em tempo real com todos os produtos que sofreram aumento de custo do fornecedor, mas que continuam sendo vendidos pelo preço antigo, apontando os gargalos de margem da empresa `[00:02:42]`.

### 4. Métodos de Atualização e Automação de Preços `[00:03:03]`

O sistema disponibiliza três fluxos para a entrada de novos preços de venda:

- **Edição Manual Direta na Grade `[00:03:13]`:** O operador pode digitar o valor diretamente na linha do produto. Se o valor inserido for igual ao calculado matematicamente pelo sistema, o status muda para **"Sugerido"** `[00:03:29]`. Se o operador definir uma margem comercial por conta própria, o status é classificado como **"Preço Alterado"** `[00:03:37]`.
    
- **Aplicação Massiva Automatizada ("Aplicar Sugerido") `[00:03:46]`:** O comando permite selecionar todos ou um bloco de produtos e acionar o gatilho automático. O motor do ERP captura o _Custo Novo_, processa o _Markup Desejado_ cadastrado no perfil do item e injeta o resultado diretamente na coluna de novo preço de venda, agilizando reajustes em massa `[00:03:57]`.
    
- **Módulo de Composição de Preço `[00:04:09]`:** Alternativa voltada para indústrias ou empresas que utilizam a estratégia de precificação por **Margem de Contribuição** em vez de markup simples, calculando o preço final com base em variáveis de custos fixos e variáveis rateados `[00:04:18]`.
    

### 5. Tratamento de Exceções de Cadastro `[00:04:27]`

Para evitar erros humanos de faturamento, a tela de precificação realiza dupla validação ao processar um item:

- **Identificação de Promoções Ativas `[00:04:27]`:** O painel indica se o produto está sob vigência de regras promocionais (ex: promoção por quantidade ou atacado) `[00:04:41]`. O operador pode abrir a ficha do produto diretamente pela tela para auditar os critérios e prazos de validade da promoção antes de reajustar o preço base `[00:04:50]`.
    
- **Bloqueio e Gestão de "Produtos de Ligação" (Preços Vinculados) `[00:04:50]`:** Itens que pertencem a uma mesma grade ou família comercial (ex: camisetas do mesmo modelo, porém de cores ou tamanhos diferentes) são parametrizados dentro de um subgrupo sob uma regra de ligação de preços `[00:05:26]`.
    
    - _Trava de Segurança:_ Se o operador tentar alterar o preço de venda de forma individual diretamente na linha desse produto, o ERP **bloqueia a gravação** e exibe uma mensagem informando que o item faz parte de uma estrutura de preços ligados `[00:05:49]`.
        
    - _Resolução em Lote:_ Para atualizar esses itens, o gestor clica no botão de atalho da ligação `[00:05:59]`. O sistema abre uma subjanela contendo estritamente os produtos daquela família vinculada `[00:06:08]`. Ao definir o novo preço nesse painel (ex: r$ 50,00) e aplicar, o ERP replica o valor em cascata para todos os produtos associados de forma simultânea, mantendo a padronização das tabelas comerciais `[00:06:15]`.
Este módulo detalha as diretrizes operacionais, o fluxo de entrada e a rastreabilidade na comercialização de mercadorias com **Controle de Lote e Número de Série** no ERP Código UP. O recurso é voltado para atender a exigências fiscais e controles de garantia (ex: eletrônicos, celulares ou medicamentos) `[00:00:53]`, `[00:03:26]`.

### 1. Entrada de Estoque Automatizada (Importação de XML) `[00:00:06]`

O ciclo de vida do lote inicia-se na rotina de recebimento de mercadorias através do módulo de Nota Fiscal de Entrada.

- **Vinculação e Carga de Itens `[00:00:11]`:** O operador realiza a importação do arquivo `.xml` emitido pelo fornecedor `[00:00:17]`. Caso os produtos já estejam cadastrados e parametrizados no banco de dados com a flag de controle de lote ativa, o ERP habilita a aba complementar de rastreabilidade `[00:00:32]`.
    
- **Injeção de Identificadores (Lote vs. Série) `[00:00:41]`:** Na aba _Lotes_, o faturista insere os dados de identificação para cada item da grade:
    
    - _Modelo Fracionado (Lote):_ Lançamento de um código identificador único associado a uma quantidade volumétrica (ex: um código de lote para 50 unidades do produto) `[00:00:46]`.
        
    - _Modelo Unitário (Número de Série):_ Indicado para produtos como celulares ou equipamentos eletrônicos. O operador desmembra a quantidade importada registrando individualmente um número de série por unidade física (ex: para uma quantidade de 50, registram-se 50 números de série independentes) `[00:00:53]`.
        
- **Mapeamento de Códigos de Terceiros `[00:01:01]`:** O sistema permite a indexação do código interno de lote do próprio fornecedor `[00:01:07]`. Essa informação facilita a triangulação de dados em caso de auditorias ou devoluções de fábrica `[00:01:13]`.
    

### 2. Auditoria e Controle de Saldos por Sub-Entidades `[00:01:37]`

No cadastro do produto, a aba _Lote_ funciona como um livro-razão (_Kardex_) específico daquela sub-entidade `[00:01:45]`.

Diferente do estoque global do produto, o ERP segmenta os dados exibindo o saldo real e isolado de cada lote ativo (ex: o produto pode possuir 150 unidades no total, mas distribuídas em 3 lotes de 50) `[00:01:29]`, `[00:01:54]`. Logo abaixo da grade de saldos por lote, o sistema exibe a trilha de auditoria contendo estritamente as movimentações de entrada e saída atreladas àquele lote selecionado, garantindo rastreabilidade ponta a ponta `[00:02:00]`.

### 3. Fluxo de Saída na Tela de Vendas (Separação na Grade) `[00:02:08]`

Ao bipar ou selecionar um item que possui controle de lote no Pedido de Venda, o ERP interrompe o fluxo padrão para que o operador realize a indicação física da peça que está saindo `[00:02:08]`.

- **Painel de Busca Cruzada de Lotes `[00:02:18]`:** Uma janela assistente é exibida listando todos os lotes que possuem saldo disponível para o item `[00:02:18]`.
    
- **Filtros de Localização de Lote `[00:02:24]`:** Para agilizar o atendimento no balcão, o operador pode filtrar os lotes digitando o código interno, o número de série ou o nome do fornecedor original da mercadoria `[00:02:35]`.
    
- **Múltiplos Lotes no Mesmo Item `[00:02:55]`:** Se a quantidade vendida for superior ao saldo de um único lote, o sistema permite fracionar a saída inserindo o mesmo produto mais de uma vez no pedido, vinculando cada linha a um lote/série diferente até suprir a demanda da venda `[00:02:55]`.
    

### 4. Impressão do Pedido e Termos de Garantia `[00:03:06]`

Após a finalização e liquidação da venda, o ERP Código UP injeta os dados de rastreabilidade diretamente no documento de saída impresso para o cliente.

- **Concatenação de Código `[00:03:06]`:** O número do lote ou o número de série é impresso de forma concatenada junto ao código principal e descrição do produto (ex: `[CódigoProduto] - LOTE: [NúmeroLote]`) `[00:03:12]`.
    
- **Validação de Garantia Legal `[00:03:20]`:** O layout de impressão do pedido pode ser customizado para exibir cláusulas de garantia logo abaixo do registro do lote (ex: _"Para acionar a garantia de 30 dias deste eletrônico, apresente este documento constando o Número de Série"_), servindo como documento de proteção jurídica para a empresa e clareza para o consumidor final
**Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: https://www.youtube.com/watch?v=QbvBA4qiOMY
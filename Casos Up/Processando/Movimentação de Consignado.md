Este módulo detalha as diretrizes operacionais, o fluxo de saídas, o acerto de estoque e o faturamento financeiro para a **Movimentação de Mercadorias em Consignação** no ERP Código UP. O recurso é projetado para indústrias e distribuidoras que cedem produtos a clientes ou revendedores para posterior prestação de contas `[00:00:00]`.

### 1. Abertura do Consignado e Envio de Itens `[00:00:00]`

O ciclo se inicia com o registro do documento de saída em consignação para o cliente desejado.

- **Parametrização Comercial Automatizada `[00:00:16]`:** Ao selecionar o cliente, o ERP permite a alteração em lote de tabelas de preço específicas para aquela operação, recalculando os valores dos itens incluídos `[00:00:16]`.
    
- **Lançamento de Produtos e Conversão de Unidades `[00:00:29]`:** O operador inclui os produtos salvos na grade, contando com o suporte do motor do ERP para conversão de unidades de medida (ex: caixas para unidades individuais) sempre que houver necessidade logística `[00:00:36]`.
    
- **Registro de Histórico de Impressão `[00:00:44]`:** O sistema carimba e exibe no grid a data e hora exatas de impressão de cada via física do documento de consignação, garantindo auditoria e controle de saída física das peças `[00:00:44]`.
    

### 2. Rotina de Devoluções e Itens Restantes `[00:01:45]`

No momento da prestação de contas, o revendedor retorna ao estabelecimento para informar o balanço do que foi de fato comercializado em campo.

- **Trava de Segurança de Estoque Consignado `[00:01:57]`:** Na aba _Devoluções_, a ferramenta de pesquisa do ERP **bloqueia a inserção de produtos aleatórios** `[00:01:57]`. O operador consegue localizar e devolver estritamente os itens que constam como "Em Consignação" para aquele cliente e contrato específico `[00:02:04]`.
    
- **Painel de Auditoria de Itens Restantes `[00:02:13]`:** O ERP mantém uma grade de saldo elástica (Livro de Restantes) que calcula em tempo real a equação de estoque do contrato `[00:02:13]`:
    
    $$\text{Quantidade Inicial} - \text{Quantidade Devolvida} = \text{Saldo Restante}$$
    
- **Transição Automatizada de Status do Contrato `[00:02:22]`:** * Se o cliente retornar apenas uma parte dos produtos, o sistema altera o status do lote para **"Parcialmente Devolvido"** `[00:02:41]`.
    
    - Caso todas as peças restantes sejam devolvidas ou liquidadas, o contrato avança para o status **"Totalmente Resolvido"** `[00:02:27]`.
        

### 3. Análise Gráfica de Performance `[00:03:14]`

A tela de movimentação disponibiliza um painel estatístico integrado para avaliação da carteira de revenda `[00:03:14]`.

- **Indicadores de Escoamento de Estoque `[00:03:14]`:** O sistema calcula e exibe as métricas de percentual de mercadorias devolvidas versus mercadorias efetivamente vendidas `[00:03:14]`.
    
- **Filtros Gráficos Dinâmicos por Cliente `[00:03:25]`:** Ao filtrar um cliente específico no topo da tela, o gráfico consome os dados presentes na grid ativa para desenhar mapas visuais de desempenho, auxiliando a gerência a identificar quais parceiros possuem melhor taxa de conversão de vendas `[00:03:33]`.
    

### 4. Fechamento Financeiro, Comissões e Faturamento `[00:03:45]`

O encerramento do contrato de consignação consolida as movimentações em faturamento financeiro oficial e baixa definitiva de estoque.

- **Agrupamento Histórico por Data `[00:03:45]`:** A aba de _Fechamento_ organiza de forma cronológica todas as entregas e devoluções parciais vinculadas ao contrato, facilitando a conferência ponta a ponta pelo faturista `[00:04:09]`.
    
- **Motor de Cálculo de Comissões e Descontos `[00:04:22]`:** O sistema calcula o valor líquido vendido (ex: $R\$\,69,32$ de saldo apurado) `[00:03:57]`. Caso o operador aplique um desconto administrativo nesta tela, o ERP **deduz o valor diretamente da base de cálculo de comissão** do vendedor ou do revendedor parceiro, blindando as margens de lucro da empresa `[00:04:36]`.
    
- **Geração de Contas a Receber `[00:04:45]`:** O sistema dispara o assistente de cobrança onde define-se a forma de pagamento (dinheiro, boleto, cartão), inserção de observações de texto e prazos de vencimento, gerando um código de lançamento financeiro exclusivo no Contas a Receber `[00:04:54]`.
    
- **Conversão em Pedido de Venda Oficial `[00:05:03]`:** Com as finanças validadas, o comando **"Gerar Venda"** encerra a consignação e converte o saldo vendido automaticamente em um **Pedido de Venda (com numeração de controle própria, ex: Pedido 51)** `[00:05:16]`, `[00:06:16]`. A partir deste pedido oficial, o caixa realiza o recebimento e a emissão da respectiva Nota Fiscal Eletrônica (NF-e)
ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link https://www.youtube.com/watch?v=g58YmDXDTT0
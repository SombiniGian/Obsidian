

Este módulo detalha o funcionamento e as regras de negócio da ferramenta de **Geração Automática de Lote de Produção no Ato da Venda** do ERP Código UP. O recurso é ideal para indústrias, confecções ou empresas que trabalham no modelo de produção por demanda (_Make-to-Order_), onde a venda de um produto acabado dispara automaticamente uma ordem ou lote de fabricação para o setor industrial.

### 1. Conceito de Produção por Demanda (Just-in-Time)

Tradicionalmente, os sistemas ERP exigem que a equipe de planejamento (PCP) crie manualmente uma Ordem de Produção (OP) para depois disponibilizar o estoque para venda.

Esta ferramenta automatiza o processo: no momento em que o vendedor finaliza um Pedido de Venda no balcão ou no comercial, o ERP identifica que o produto comercializado é de fabricação própria e **gera dinamicamente um Lote de Produção correspondente**. Isso otimiza o fluxo de comunicação entre o setor comercial e a fábrica, garantindo que cada item vendido entre imediatamente na fila de execução.

### 2. Configuração e Parametrização no Cadastro do Produto

Para que o gatilho automático funcione no momento da venda, o produto precisa estar configurado com os seguintes critérios no banco de dados:

- **Fórmula / Estrutura do Produto (BOM - Bill of Materials):** O produto principal (acabado) deve ter a sua ficha técnica cadastrada, contendo a lista e a quantidade exata de insumos, matérias-primas ou componentes necessários para a sua fabricação.
    
- **Flag de Geração Automática:** No perfil de inventário ou PCP do item, deve ser ativada a opção que vincula a venda diretamente à abertura de lote.
    

### 3. O Fluxo Operacional Integrado

O ciclo de dados ocorre de forma linear através dos seguintes passos:

1. **Abertura do Pedido:** O operador lança o produto acabado na tela de vendas e define a quantidade solicitada pelo cliente.
    
2. **Disparo do Gatilho:** Ao fechar ou faturar a venda, o motor do ERP Código UP cria um registro de **Lote de Produção** na retaguarda industrial, herdando o número do pedido de venda como referência de rastreabilidade.
    
3. **Empenhamento de Matéria-Prima:** O sistema analisa a ficha técnica do produto e realiza o empenho automático (reserva) das matérias-primas no estoque. Se houver falta de algum insumo, alertas são gerados para o setor de compras.
    
4. **Acompanhamento da Fábrica:** O setor fabril recebe a listagem dos lotes gerados automaticamente, contendo as especificações de quantidade e prazos atrelados ao pedido do cliente.
    

### 4. Rastreabilidade e Vantagens Gerenciais

- **Vínculo Direto (Pedido vs. Lote):** O gestor consegue rastrear exatamente qual lote de fábrica foi responsável por atender a um determinado pedido de cliente, facilitando o controle de qualidade e a estimativa real do prazo de entrega.
    
- **Redução de Estoque Parado:** Evita a superprodução, fazendo com que a empresa produza estritamente o que já foi vendido, melhorando o fluxo de caixa e o giro de estoque de produtos acabados.
    
- **Automação de Baixa:** Assim que o lote de produção é finalizado na fábrica, o sistema faz a entrada do produto acabado no estoque e a baixa definitiva das matérias-primas consumidas, alimentando o custo real de fabricação.****

ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link https://www.youtube.com/watch?v=yHdVRO36xko

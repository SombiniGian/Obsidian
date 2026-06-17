Este módulo detalha as diretrizes operacionais, a flexibilidade de regras de negócio e o fluxo de inventário da ferramenta de **Outras Movimentações de Estoque** do ERP Código UP. O recurso foi desenvolvido para gerir os fluxos internos de mercadorias que não derivam de operações comerciais de compra ou venda tradicionais, tais como quebras, perdas de produção, descards por validade, consumos internos ou trocas de mercadorias `[00:00:07]`.

### 1. Cadastro e Parametrização dos Tipos de Movimentação `[00:00:20]`

Para garantir a organização e a auditoria dos ajustes de inventário, o sistema permite a criação de um catálogo personalizado de motivos de movimentação `[00:00:20]` através do preenchimento dos seguintes critérios:

- **Sentido Físico do Fluxo:** O administrador define se o tipo de movimentação configurado representará uma **Entrada** (incremento de saldo) ou uma **Saída** (redução de saldo) no inventário `[00:00:35]`.
    
- **Definição de Gatilho Principal:** É possível marcar uma das regras como a "Movimentação Principal" `[00:00:41]`. Esta seleção faz com que o ERP pré-carregue esse motivo automaticamente sempre que o utilizador abrir o ecrã de novos lançamentos, acelerando o processo operacional `[00:00:41]`.
    
- **Identificação de Terceiros e Auditoria:** O sistema permite configurar se a rotina exige ou não a vinculação obrigatória de uma pessoa (colaborador, fornecedor ou cliente) no momento do lançamento `[00:00:48]`.
    

### 2. Motor de Automatização por Percentagem Atual `[00:00:48]`

O ERP Código UP inclui um recurso de automação baseado em proporções de inventário, ideal para o controlo de quebras estatísticas ou resíduos industriais previsíveis `[00:00:48]`:

- **Cálculo Proporcional Automático:** O gestor pode fixar uma percentagem padrão atrelada ao tipo de movimentação (ex: _Perda de Produção_ configurada com o fator de **10%**) `[00:00:54]`.
    
- **Ação no Lançamento:** Quando o utilizador cria um lançamento e seleciona um produto com 100 unidades em stock, o motor do sistema calcula e preenche a quantidade de ajuste automaticamente para **10 unidades** (10%) `[00:01:00]`, `[00:01:08]`. Se o stock atual for de 80 unidades, o sistema sugere a baixa automática de 8 unidades `[00:01:13]`.
    
- **Flexibilidade de Sobrescrita:** Apesar da sugestão automatizada calculada pelo ERP `[00:01:56]`, o ecrã mantém o campo aberto, permitindo que o operador altere manualmente o valor para a quantidade física real verificada (ex: ajustar de 10 para 11 unidades) se houver divergência `[00:02:04]`.
    

### 3. Execução de Lançamentos e Operações de Troca `[00:01:21]`

A interface de lançamentos centraliza a execução de ajustes simples ou compostos numa única janela de trabalho:

- **Pré-carregamento Dinâmico:** Ao iniciar um registo, o ERP preenche automaticamente a data corrente e herda os parâmetros fiscais e físicos do tipo de movimentação principal `[00:01:21]`, `[00:01:29]`.
    
- **Camada Dupla de Observações:** Para garantir a clareza nas auditorias, o operador pode inserir justificações de texto em dois níveis: uma observação geral para o cabeçalho de todo o lote e observações específicas linha a linha para cada item incluído `[00:02:10]`.
    
- **Operação de Troca Multidirecional:** O ecrã suporta o lançamento de múltiplos itens num único documento de ajuste `[00:02:17]`. Isto possibilita simular uma rotina de **Troca de Produtos**, onde o operador adiciona uma linha com o sentido de _Saída_ (para dar baixa no produto defeituoso devolvido) e uma linha com o sentido de _Entrada_ (para o produto que está a ser introduzido no stock), equilibrando o inventário sem burocracia `[00:02:26]`, `[00:02:32]`.
    

### 4. Rastreabilidade e Relatórios de Auditoria `[00:02:40]`

Assim que o documento é guardado no ecrã de _Outras Movimentações_, o ERP consolida os dados e atualiza as tabelas do sistema em tempo real `[00:02:40]`:

- **Log de Utilizador:** A grade de histórico regista de forma inviolável o valor financeiro da movimentação, as quantidades exatas e o nome do **utilizador/operador** que assinou o lançamento `[00:02:40]`, `[00:02:48]`.
    
- **Kardex do Produto:** Ao abrir a ficha individual do produto movimentado, a aba de histórico de stock exibe a linha do movimento de ajuste com o seu respetivo descritivo, garantindo total clareza e transparência para a equipa de auditoria e inventário da empresa `[00:02:48]`, `[00:02:55]`.
    

ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: [Assista ao vídeo no YouTube](https://www.youtube.com/watch?v=lcF3vph1Mz4).
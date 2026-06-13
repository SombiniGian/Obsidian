Este módulo detalha as diretrizes de parametrização, os fluxos operacionais e os impactos contábeis/fiscais do processamento de **Inventário de Estoque** no ERP Código UP.

### 1. Parametrização Global e Diretrizes de Escopo `[00:00:01]`

O módulo de inventário, localizado no menu de _Movimentações_, centraliza as rotinas de contagem física e alinhamento de saldos, permitindo isolar os objetivos fiscais das correções logísticas operacionais `[00:00:09]`.

- **Definição de Data de Competência:** O operador estabelece a data-base para o congelamento do estoque (ex: fechamento anual em 31 de dezembro), servindo como referência temporal para auditorias `[00:00:16]`.
    
- **Indexadores de Custo para Avaliação Financeira `[00:00:25]`:** O sistema permite selecionar a métrica de valorização das mercadorias para o cálculo do ativo em estoque:
    
    - _Custo Atual do Produto:_ Considera o último preço de custo registrado.
        
    - _Custo Médio Ponderado:_ **Indicado para fins contábeis**, pois calcula o preço médio com base no histórico de entradas e saídas `[00:00:33]`.
        
    - _Preço de Venda:_ Avalia o estoque com base no potencial de faturamento do varejo `[00:00:33]`.
        
- **Desacoplamento de Impacto (Ajuste de Estoque Físico) `[00:00:54]`:** Uma trava crítica define a finalidade do processamento:
    
    - _Modo Apenas Fiscal (Não):_ Os valores e quantidades informados são utilizados exclusivamente para preenchimento de obrigações legais (como o **Bloco H do SPED Fiscal** e **SINTEGRA**), sem alterar as quantidades correntes nos cadastros dos produtos `[00:01:02]`.
        
    - _Modo de Ajuste Físico (Sim):_ O sistema processa as diferenças detectadas e sobrescreve os saldos dos produtos no banco de dados `[00:01:17]`. Permite selecionar o impacto isolado no _Estoque Gerencial_, no _Estoque Contábil_ ou em _Ambos_ simultaneamente `[00:01:23]`.
        

### 2. Motor de Filtragem, Captura e Manipulação Financeira `[00:01:30]`

O processo de carga dos dados é flexível, permitindo a execução de inventários parciais (por amostragem) ou globais.

- **Filtros Avançados de Captura `[00:01:45]`:** A janela de seleção de itens permite isolar a contagem por _Status do produto, Grupo econômico, Marca específica_ ou filtragem por comportamento de saldo (capturar apenas itens com estoque positivo ou saldo negativo) `[00:01:56]`.
    
- **Manipulação de Valorização Geral (Fator de Correção) `[00:01:30]`:** O motor do inventário possui um recurso para aplicar acréscimos ou descontos percentuais em massa sobre o valor total avaliado do estoque, atendendo a necessidades específicas de depreciação ou reajustes de balanço `[00:01:38]`.
    

### 3. Execução da Contagem e Injeção de Dados `[00:02:54]`

Na grade de inventário, o sistema exibe o saldo computado atual e disponibiliza a coluna **Novo Estoque** para a inserção das quantidades físicas reais apuradas em campo `[00:02:54]`. Itens inseridos indevidamente ou que não fazem parte do escopo daquela contagem podem ser removidos individualmente por meio do botão de exclusão da grade `[00:03:15]`.

### 4. Integração de Banco de Dados e Trilha de Auditoria Físico-Contábil `[00:03:25]`

Ao salvar e processar o inventário com a opção de ajuste ativada, o ERP executa transações simultâneas nas tabelas de controle de estoque do Firebird.

- **Gravação do Delta de Estoque `[00:03:25]`:** O sistema atualiza os saldos físicos nas colunas correspondentes (Contábil e Gerencial) dos produtos envolvidos `[00:03:25]`.
    
- **Geração Automática de Linha de Movimentação (Kardex) `[00:03:32]`:** O ERP injeta um registro de auditoria permanente na tabela de movimentações de estoque de cada item:
    
    - A operação é classificada sob a rubrica **"Acerto de Estoque"** `[00:03:32]`.
        
    - É gravado o código de origem (ID do Inventário correspondente), amarrando o novo saldo à contagem que o originou e garantindo total rastreabilidade para auditorias contábeis `[00:03:44]`.
        

### 5. Destinação Fiscal (SPED / SINTEGRA) `[00:03:55]`

Uma vez finalizado, o documento de inventário fica disponível no banco de dados como uma entidade estática. No momento da geração dos arquivos fiscais do período, o módulo do **SPED Fiscal** importa os dados desse inventário específico, processando e estruturando os registros necessários para a prestação de contas junto à SEFAZ `[00:04:03]`.
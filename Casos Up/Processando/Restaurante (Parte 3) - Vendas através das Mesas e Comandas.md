Este módulo detalha as diretrizes operacionais, a unificação de ecrãs de faturação e a flexibilidade de fluxos para **Vendas através de Mesas e Comandas** no módulo de Restaurante do ERP Código UP. O recurso foi desenhado para centralizar todos os canais de atendimento num único motor de vendas, permitindo transitar entre interfaces táteis e tradicionais sem perda de dados `[00:00:00]`, `[00:01:01]`.

### 1. Unificação do Fluxo e Modos de Visualização `[00:00:36]`

No ERP Código UP, independentemente de o pedido ser iniciado no mapa de mesas, via comanda ou no balcão, **todos os lançamentos convergem para a mesma tabela central de vendas** `[00:00:36]`, `[00:00:52]`. O sistema oferece ao utilizador a liberdade de escolher a interface de trabalho ideal:

- **Modo Faturação Tradicional:** Exibe o ecrã padrão de pedidos do sistema, repleto de grelhas e controlos detalhados de dados, ideal para caixas habituados ao fluxo convencional do ERP `[00:01:07]`, `[00:01:31]`.
    
- **Modo Tátil (Touch Screen):** Interface otimizada para monitores táteis ou dispositivos móveis. O operador pode alternar instantaneamente entre a tela convencional e o menu tátil utilizando o atalho **`Alt + S`** no teclado `[00:02:14]`, `[00:02:50]`.
    

### 2. Operação Exclusiva por Mapa de Mesas `[00:00:12]`

Para estabelecimentos que operam estritamente com atendimento local em mesas e não utilizam cartões de consumo individuais, o sistema permite isolar o fluxo:

- **Simplificação do Painel:** Nas configurações do módulo de restaurante, o administrador pode desativar a flag de controlo de comandas `[00:00:12]`. Com isto, ao clicar sobre qualquer bloco numérico do mapa, o ERP abre diretamente o carrinho de compras daquela mesa, eliminando etapas de digitação `[00:00:24]`.
    
- **Abertura Rápida por Código:** Para evitar a navegação manual em ecrãs com muitas mesas, o operador pode clicar no botão **"Incluir"** e digitar diretamente o número da mesa desejada (ex: introduzir `30` e premir `Enter`) para iniciar os lançamentos `[00:03:39]`, `[00:03:48]`.
    
- **Ordenação Inteligente de Consumo:** O mapa reorganiza os blocos dinamicamente, posicionando as **mesas ativas com consumo corrente nas primeiras linhas do ecrã**, otimizando a monitorização visual do salão `[00:04:09]`.
    

### 3. Operação Exclusiva por Comandas (Sem Mesas) `[00:04:52]`

Indicado para estabelecimentos como discotecas, bares de balcão ou padarias, onde o cliente consome em pé ou circula pelo espaço utilizando um cartão numerado:

- **Habilitação do Fluxo:** O gestor desativa a obrigatoriedade das mesas e ativa o controlo por comandas `[00:04:52]`. A interface gráfica altera-se para exibir uma listagem sequencial apenas com os cartões que possuem contas abertas e valores pendentes `[00:05:11]`.
    
- **Pesquisa e Ajuste:** Para adicionar novos produtos ou consultar o extrato de um cliente, o caixa clica em **"Alterar"** e digita o número do cartão (comanda). O sistema localiza o lote de itens e abre o ecrã de vendas imediatamente `[00:05:44]`, `[00:05:51]`.
    

### 4. Operação Híbrida: Várias Comandas na Mesma Mesa `[00:06:13]`

Para restaurantes tradicionais onde grupos de amigos partilham a mesma mesa física mas exigem a divisão estrita de contas por consumo individual desde o início do atendimento, o ERP ativa o modo híbrido `[00:06:13]`:

- **Vínculo Multi-Comanda:** O operador pode abrir múltiplos pedidos referenciando a mesma coordenada física (ex: abrir a Mesa 3 associada à Comanda 789 e, em seguida, abrir a mesma Mesa 3 associada à Comanda 7891) `[00:06:18]`, `[00:06:39]`.
    
- **Grelha de Separação:** O mapa gráfico passará a exibir duas linhas distintas para a mesma mesa, permitindo lançar e faturar os consumos de forma isolada `[00:06:46]`.
    
- **Regra de Consulta Técnica:** Por motivos de segurança e integridade, quando o modo híbrido está ligado e o operador clica no botão "Alterar", o sistema ignora a busca pelo número da mesa e **solicita obrigatoriamente o número exato da comanda** para evitar o lançamento de itens no cartão errado `[00:07:08]`, `[00:07:19]`.
    

### 5. Finalização e Recebimento de Valores `[00:03:02]`

A liquidação financeira da conta pode ser realizada diretamente na interface de atendimento `[00:03:02]`:

1. O operador insere o meio de pagamento (dinheiro, cartão, etc.) e processa a baixa `[00:03:02]`.
    
2. O sistema emite o documento fiscal correspondente e atualiza a base de dados `[00:03:16]`.
    
3. O bloco da mesa ou comanda altera instantaneamente o seu status para "Disponível" (cor verde padrão de vazio), libertando o espaço para o próximo cliente `[00:03:33]`.
    

ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: [Assista ao vídeo no YouTube](https://www.youtube.com/watch?v=1ePQG1Qz89w).
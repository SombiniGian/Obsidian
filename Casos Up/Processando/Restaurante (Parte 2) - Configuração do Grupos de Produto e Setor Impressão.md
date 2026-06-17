Este módulo detalha as diretrizes operacionais, a parametrização de interface e a lógica de roteamento de pedidos para a **Configuração de Grupos de Produtos, Setores de Impressão e Controlo de Status** no módulo de Restaurante do ERP Código UP `[00:00:00]`. O recurso visa otimizar o atendimento em ecrãs táteis (_Touch Screen_) e automatizar a comunicação entre o salão, a cozinha e a copa `[00:01:14]`, `[00:03:13]`.

### 1. Parametrização e Ordenação dos Grupos de Produtos no Touch `[00:00:10]`

Para facilitar a localização dos itens no momento da venda, o sistema permite customizar a disposição dos grupos no ecrã tátil:

- **Filtros de Exibição:** No menu de _Grupo de Produtos_, o gestor define quais categorias devem ser exibidas ou ocultadas no ecrã de vendas do restaurante `[00:00:28]`.
    
- **Ordem de Execução:** O utilizador pode definir a ordem de prioridade de cada grupo (ex: posicionar o grupo "Mais Vendidos" ou "Bebidas" nas primeiras posições) para agilizar o fluxo de cliques do operador `[00:00:36]`, `[00:00:45]`.
    
- **Identificação Visual:** O sistema permite carregar uma imagem personalizada para cada botão de grupo através do clique com o botão direito do rato, tornando o menu mais intuitivo `[00:01:05]`.
    

### 2. Cadastro do Produto e Vinculação ao Tipo "Restaurante" `[00:01:14]`

A ativação das propriedades de alimentação exige que o item seja classificado corretamente na sua ficha cadastral `[00:01:14]`:

- **Modificação de Tipo:** O campo **Tipo de Produto** deve ser configurado obrigatoriamente como **"RESTAURANTE"** `[00:02:03]`. Esta ação liberta uma aba complementar de especificações onde se gerem os modificadores (adicionais como queijo/bacon, remoções como retirar salada e modos de preparo como o ponto da carne) `[00:02:13]`, `[00:02:31]`.
    
- **Ativação do Controlo de Status:** É nesta aba que se liga a flag **"Controlar Status Preparo"** `[00:03:13]`. Se estiver ativa, o item entra no fluxo de monitorização da cozinha; caso contrário (como uma água ou cerveja de balcão), o item salta etapas e assume o status de entregue imediatamente `[00:03:13]`, `[00:10:19]`.
    

### 3. Arquitetura de Redirecionamento por Setores de Impressão `[00:02:41]`

O ERP soluciona o problema logístico de comunicação interna enviando cada item do pedido estritamente para o seu local de preparação física `[00:02:41]`:

```
+------------------------------------------------------------------------+
|                  FLUXO DE ROTEAMENTO DE IMPRESSÃO                      |
+------------------------------------------------------------------------+
|                                                                        |
|                       [ Operador Salva o Pedido ]                      |
|                                    │                                   |
|               ┌────────────────────┴────────────────────┐              |
|               ▼                                         ▼              |
|        Produto: X-Bacon                         Produto: Chopp         |
|   Vínculo: SETOR COZINHA                    Vínculo: SETOR COPA        |
|               │                                         │              |
|               ▼                                         ▼              |
|   Impressora da Cozinha                      Impressora do Balcão/Bar  |
|   (Imprime Talão de Preparo)                (Imprime Talão de Bebidas) |
|          [00:03:13]                                [00:05:44]          |
+------------------------------------------------------------------------+
```

- **Mapeamento de Hardware:** No menu de impressoras, o sistema faz uma varredura na rede local e cataloga todas as impressoras térmicas instaladas no sistema operativo `[00:03:45]`, `[00:04:05]`.
    
- **Criação de Setores:** No menu _Cadastro de Setores_, o utilizador cria as divisões logísticas (ex: Setor 1 - Cozinha, Setor 2 - Copa) e associa cada setor à sua respetiva impressora física `[00:04:16]`, `[00:04:25]`. O sistema permite ainda vincular mais do que uma impressora ao mesmo setor se for necessária a impressão de segundas vias `[00:05:55]`, `[00:06:11]`.
    
- **Configuração de Layout:** Através do gerador de relatórios, define-se o layout de impressão (ex: modelo "Impressão Preparar Produtos") e parametriza-se o disparo direto para a porta de rede, evitando que o ecrã de seleção do Windows bloqueie o fluxo do operador `[00:04:48]`, `[00:05:29]`.
    

### 4. Métodos Dinâmicos de Lançamento de Itens `[00:07:40]`

A interface de atendimento do restaurante disponibiliza três formas simultâneas para a inserção de produtos na mesa ou comanda, adaptando-se ao perfil do operador `[00:07:40]`:

1. **Navegação Visual (Touch):** Clique direto nos botões dos grupos (organizados alfabeticamente) e seleção do produto por imagem ou texto `[00:07:15]`, `[00:07:26]`.
    
2. **Leitura de Código de Barras:** Utilização de um leitor ótico diretamente no ecrã de vendas. Ao bipar o item, o ERP abre automaticamente uma janela rápida para a inserção da quantidade desejada `[00:07:47]`, `[00:07:54]`.
    
3. **Digitação de Código Rápido (Cardápio):** Introdução direta do número de indexação do produto (ex: digitar `10` para o hambúrguer). Este método é ideal para estabelecimentos que utilizam códigos fixos no menu impresso, revelando-se o fluxo mais célere do sistema `[00:08:13]`, `[00:08:19]`.
    

### 5. Gestão Visual do Ciclo de Vida do Pedido (Status) `[00:09:10]`

Quando o operador guarda a venda, os itens que possuem controlo de status ativado passam a ser monitorizados por um código de cores no ecrã de gestão `[00:09:10]`, `[00:09:39]`:

- **Sinalização Amarela (Aguardando):** O produto deu entrada no sistema, o talão de produção foi impresso no setor correspondente, e o item encontra-se na fila de espera para ser confetado pela equipa de cozinha `[00:09:47]`.
    
- **Sinalização Vermelha (Pronto):** Ao clicar sobre o item, o operador ou o ecrã da cozinha altera o estado para "Pronto" `[00:09:55]`. Isto indica visualmente ao funcionário de sala que o prato já foi finalizado e está pronto no balcão de expedição para ser transportado até à mesa do cliente `[00:10:05]`.
    
- **Sinalização Branca (Entregue):** Assim que o funcionário confirma a entrega física do produto na mesa, o status passa para "Entregue" e o item assume a cor branca, encerrando o ciclo de vida de produção do item no lote `[00:10:10]`.
    

ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: [Assista ao vídeo no YouTube](https://www.youtube.com/watch?v=9ACMVSadk7M&t=392s).
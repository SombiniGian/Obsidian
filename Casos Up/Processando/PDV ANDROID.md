
---
id: [CASO-176]
link: https://www.youtube.com/watch?v=jn6MB5IDtkg
setor: [Suporte, Desenvolvimento, Operacional]
modulo: [Mobile / PDV Android]
tags: [android, pdv-mobile, autoatendimento, responsividade, stone-pos, sincronizacao]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do PDV Android]]
2. [[#Novos Perfis de Usuários na Retaguarda]]
3. [[#Interface e Mecânica de Navegação]]
4. [[#Mecanismo de Adição, Agrupamento e Complementos]]
5. [[#Fluxo Financeiro e Calculadora Responsiva]]
6. [[#Arquitetura de Sincronização e Impressão (Online vs. Contingência)]]
7. [[#Regras de Negócio e Pontos Críticos de Falha]]

# Visão Geral do PDV Android
O **PDV Android** é uma aplicação móvel multiplataforma projetada para otimizar o fluxo de faturamento rápido em balcões, ilhas de atendimento, terminais de autoatendimento e dispositivos POS integrados (como as maquininhas inteligentes **Stone**). O módulo foca na experiência de venda direta: o operador adiciona os itens ao carrinho e realiza a quitação financeira imediata, não sendo permitido salvar orçamentos ou manter vendas em aberto. O sistema conta com inteligência de layout responsivo, adaptando a disposição dos blocos automaticamente caso o hardware opere em modo Retrato (vertical) ou Paisagem (horizontal).

# Novos Perfis de Usuários na Retaguarda
Para controlar o comportamento de inicialização do aplicativo e blindar o acesso a recursos restritos da retaguarda, foram introduzidos novos tipos de perfis de usabilidade no **Cadastro de Vendedores/Usuários** do ERP principal:

*   **PDV:** Perfil restrito para operadores de caixa móvel. Ao realizar o login no Android, a aplicação salta a tela de menus e **abre diretamente na interface do PDV**. O operador fica bloqueado de acessar as demais áreas do software. Ao efetuar o logoff, o sistema retorna à tela de credenciais.
*   **Fichas:** Indicado para cenários de eventos, festivais ou praças de alimentação. O fluxo de digitação é idêntico ao PDV, contudo, ao confirmar o recebimento do dinheiro ou cartão, o sistema dispara a impressão isolada de **Fichas de Produtos** (uma via por item) para que o cliente realize a retirada física diretamente no balcão de entrega.
*   **Autoatendimento (Totem):** Transforma o dispositivo em um terminal de autoatendimento direto para o cliente final. Opera de forma análoga ao perfil de *Fichas*, forçando a exibição de todas as árvores de complementos e opcionais na tela de forma assistida. Ao final da transação, realiza a impressão do comprovante, mas omite a emissão de fichas separadas por produto (comportamento nativo desta versão, sujeito a revisões de roadmap).

# Interface e Mecânica de Navegação
A interface gráfica foi concebida sob o conceito de **Design Responsivo**, otimizando a área útil de tela conforme o tamanho e orientação do dispositivo:

### Comportamento por Orientação de Tela:
*   **Modo Retrato (Vertical / Smartphones padrão):** A aplicação adota uma navegação baseada em **Abas Inferiores**. A primeira aba exibe o cardápio e a árvore de grupos; a segunda aba concentra o resumo dos itens inseridos no carrinho; e a terceira gerencia os metadados da venda (dados do cliente).
*   **Modo Paisagem (Horizontal / Tablets e POS horizontais):** O layout divide a tela em duas colunas fixas simultâneas. A coluna da esquerda exibe o catálogo de produtos e os botões de grupos, enquanto a coluna da direita mantém visível o espelho do carrinho de compras com o subtotal e o botão de fechamento em tempo real.

### Mecanismo de Pesquisa Inteligente
A barra de pesquisa superior utiliza indexação cruzada. Ao digitar um termo, o sistema varre simultaneamente três níveis hierárquicos:
1.  **Nome do Produto** (ex: `Coca-Cola`).
2.  **Nome do Grupo** (ex: `Bebidas`).
3.  **Nome do Subgrupo** (ex: `Refrigerantes`).
Se o operador pesquisar por `Bebidas`, a grade isolará o grupo correspondente e renderizará todos os produtos contidos nele de uma só vez, agilizando a localização no balcão. A interface dispõe ainda de uma guia dedicada aos itens marcados como **Favoritos** na retaguarda.

# Mecanismo de Adição, Agrupamento e Complementos

### Ações de Toque no Produto:
*   **Toque Rápido:** Adiciona uma unidade do produto diretamente ao carrinho de compras (exibindo uma animação gráfica do item caindo no cesto) e mantém o usuário na tela do cardápio para continuar a venda.
*   **Toque Longo (Pressionar e Segurar):** Invoca uma tela auxiliar centralizada que permite ao operador digitar manualmente a quantidade desejada através de um teclado numérico com botões expandidos.

### Tratamento de Complementos e Opcionais
Se o produto selecionado possuir complementos atrelados em seu cadastro no ERP (ex: `Churrasquinho`), o sistema intercepta o toque e abre a janela de modificadores:
*   **Complementos Obrigatórios:** O sistema exige a seleção de pelo menos uma opção (ex: Ponto da carne: `Mal passado`) para liberar o botão de confirmação e permitir a inserção do item no carrinho.
*   **Perfis de Exibição:** No perfil de *Vendedor Padrão/PDV*, o sistema exibe apenas as telas de complementos obrigatórios para agilizar o atendimento. No perfil de *Autoatendimento*, a aplicação força a passagem sequencial por todas as telas de opcionais (mesmo as não obrigatórias), maximizando a oferta de adicionais ao cliente final.

### Regras de Agrupamento de Itens no Carrinho
O aplicativo herda em tempo real a configuração de agrupamento definida na retaguarda do ERP:
*   **Itens Secos / Industriais:** Se a flag estiver ativa na retaguarda, ao clicar três vezes seguidas em `Cerveja Lata`, o carrinho exibirá apenas uma linha contendo `Quantidade: 3` e o valor totalizado.
*   **Itens de Cozinha / Produção:** Produtos que demandam preparação (setor de restaurante) e possuem complementos específicos **nunca são agrupados**, mesmo que a flag geral esteja ativa. Se o operador adicionar dois `Churrasquinhos`, o carrinho exibirá duas linhas isoladas, visto que cada espeto pode carregar complementos e pontos de preparo distintos.

# Fluxo Financeiro e Calculadora Responsiva
Ao avançar para a tela de encerramento da venda, o sistema lista os botões correspondentes às formas de pagamento homologadas (Dinheiro, Cartão de Crédito, Cartão de Débito, Pix, Depósito, A Prazo).

### Teclado Numérico Customizado (Calculadora Interna)
Para mitigar falhas operacionais e acelerar a digitação em telas touch screen, a equipe de engenharia eliminou a invocação do teclado numérico padrão do sistema operacional Android. Foi desenvolvida uma **calculadora nativa com botões de alta escala**. 
*   A calculadora é inteligente e 100% responsiva: no modo paisagem, ela se reposiciona na lateral esquerda dos botões de pagamento, evitando oclusão de dados.

### Pagamentos Mistos (Múltiplas Formas)
O PDV suporta a divisão do valor da venda em mais de uma espécie financeira:
1. O operador seleciona a primeira forma (ex: `Dinheiro`).
2. Utiliza a calculadora nativa para reduzir o valor (ex: Venda de R$ 50,00, informa que recebeu R$ 20,00).
3. O sistema computa o saldo residual de R$ 30,00 e mantém a tela aberta.
4. O operador clica na segunda forma de pagamento (ex: `Cartão de Débito`) para absorver o restante do valor e autorizar o encerramento da venda.

### Vendas na Modalidade "A Prazo"
Ao selecionar a opção `A Prazo` (Crediário), o sistema consulta as regras comerciais do cliente na retaguarda. Se parametrizado para tal, abrirá um pop-up questionando o **Número de Parcelas**. O operador pode clicar sobre cada vencimento gerado para realizar ajustes manuais de data e valor antes da conclusão.

# Arquitetura de Sincronização e Impressão (Online vs. Contingência)

O aplicativo foi projetado para operar sob o conceito de resiliência de rede, gerenciando o envio de dados conforme o status de conexão com a API do **Servidor Força de Vendas**.

```mermaid
graph TD
    A[Finalizar Venda no PDV Android] --> B{API Força de Vendas Online?}
    B -- Sim --> C[Transmite Venda em Tempo Real]
    C --> D[Puxa Layout Customizado do FastReport do Servidor]
    C --> E[Limpa Carrinho e Abre Nova Venda]
    B -- Não --> F[Salva Venda na Fila de Contingência Local]
    F --> G[Gera Impressão em Layout de Emergência Local]
    G --> E
````

### Recuperação de Lotes em Contingência

Os pedidos represados na fila de falha de conexão (Modo Offline involuntário) não sofrem perda de dados.

1. O operador deve acessar o menu lateral e navegar até **Histórico de Vendas > Não Enviados**.
    
2. A tela listará todos os cupons cujo handshake com a API falhou durante o dia.
    
3. Após reestabelecer o sinal de rede ou reativar o servidor de força de vendas na central, o operador clica em **Selecionar Todos > Enviar**.
    
4. O aplicativo processa o envio do lote em background, limpa a fila de pendências local e insere as movimentações no relatório de fechamento na retaguarda.
    

> [!warning] Restrição de Edição de Histórico no Modo PDV
> 
> Para garantir a governança fiscal da empresa, quando o aplicativo estiver rodando sob o tipo de usuário **PDV**, o acesso ao histórico de vendas permite estritamente a **Consulta e Reimpressão** dos documentos. O botão de **Alterar/Editar** pedidos salvos fica totalmente oculto e inativo nesta interface.

# Regras de Negócio e Pontos Críticos de Falha

> [!danger] Bloqueio de Envio por Caixa Fechado ou Ausente
> 
> O motor de regras da API na retaguarda exige que toda movimentação financeira recebida via terminal móvel seja associada a um caixa gerencial ativo no ERP.
> 
> - **Regra de Validação:** Se o cadastro do vendedor na retaguarda não possuir um terminal associado (campo `Caixa App` em branco) ou se o respectivo caixa no ERP estiver com o status de **Fechado**, o servidor recusará o recebimento dos pedidos transmitidos pelo Android. O aplicativo emitirá um alerta de erro na tela e reterá a venda na fila de contingência até que o supervisor realize a abertura do caixa correspondente na retaguarda.
>     

> [!warning] Fluxo Exclusivo de Venda Avulsa para Garçons (Módulo Restaurante)
> 
> Caso o aplicativo esteja configurado para a operação de restaurante (perfil garçom lançando em mesas), o sistema disponibiliza um atalho no rodapé chamado **Venda PDV**. Este recurso serve para realizar **Vendas Avulsas de Balcão** (ex: um cliente que compra um chocolate e paga imediatamente no caixa, sem ocupar uma mesa).
> 
> - **Ponto de Atenção:** Diferente do operador de PDV fixo, o perfil de garçom opera em modo síncrono rígido. Ao tentar processar uma venda avulsa através do atalho de PDV, o sistema **exige conectividade em tempo real**. Se a conexão com o servidor do restaurante cair neste momento, o aplicativo bloqueará a gravação da venda de balcão e exibirá uma mensagem de erro imediata, não permitindo o represamento em lote offline para este perfil de usuário.
>     

```
http://googleusercontent.com/youtube_content/1
```
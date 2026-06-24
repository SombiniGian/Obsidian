---
id: [CASO-055]
link: https://www.youtube.com/watch?v=9ACMVSadk7M
setor: [Suporte, Implantação]
modulo: [Restaurante]
tags:
  - impressao-setor
  - grupos-produtos
  - touch-screen
  - status-preparo
data_criacao: 2026-06-24
---

# Restaurante (Parte 2): Configuração de Grupos, Setores de Impressão e Status de Preparo

Este documento técnico detalha as diretrizes para a estruturação do menu visual **Touch Screen**, parametrização do roteamento de impressão por setor (cozinha, bar, etc.) e o gerenciamento do fluxo de vida/status dos itens de consumo dentro do módulo de **Restaurante**.

---

## Sumário
1. [[#Configuração Visual e Ordenação dos Grupos de Produtos]]
2. [[#Cadastro de Impressoras e Setores de Preparo]]
3. [[#Vínculo do Produto ao Setor de Impressão]]
4. [[#Métodos de Lançamento na Interface Touch Screen]]
5. [[#Ciclo de Vida e Controle de Status dos Itens]]
6. [[#Pontos Críticos e Validações]]

---

## Configuração Visual e Ordenação dos Grupos de Produtos

Para que a interface gráfica do ponto de venda (**PDV Touch**) exiba os botões de atalho de forma ergonômica, é necessário parametrizar o comportamento de exibição de cada grupo.

* **Caminho de Acesso:** Menu **Grupo de Produtos**.

### Parâmetros de Interface:
* **Mostrar no Touch:** Flag que valida se o grupo correspondente deve ou não ser renderizado em tela na interface do restaurante.
* **Ordem do Touch:** Valor numérico sequencial que define a prioridade de exibição do botão (ex: definir peso `1` para o grupo de mais vendidos ou lanches rápidos garante sua fixação no topo da tela).
* **Carga de Imagem:** Através do menu de contexto (clique com o **Botão Direito** sobre o grupo), é possível carregar um arquivo de imagem para ilustrar o botão na interface.

---

## Cadastro de Impressoras e Setores de Preparo

O sistema gerencia de forma segmentada o destino físico das impressões de produção através do mapeamento de dispositivos e agrupamentos logísticos.

### 1. Cadastro de Impressoras:
Antes de criar os setores, as impressoras térmicas devem estar devidamente instaladas no spooler do Windows ou mapeadas na rede interna. No menu de impressoras do sistema, a ferramenta de **Pesquisa** fará uma varredura automática, listando todos os drivers de impressão disponíveis no sistema operacional para seleção.

### 2. Cadastro de Setores:
* **Caminho de Acesso:** Menu **Cadastro de Setores**.
* **Definição:** Cria os destinos de produção (ex: `Cozinha`, `Copa`, `Churrasqueira`, `Balcão`) e vincula quais impressoras físicas responderão por aquele setor, permitindo que um setor envie dados para mais de uma impressora simultaneamente se necessário.
* **Layout de Impressão:** Associa o relatório de conferência (ex: `Impressão Preparar Produtos`). Recomenda-se configurar o comportamento para envio direto ao dispositivo sem abertura de preview de tela para otimizar o fluxo operacional.

---

## Vínculo do Produto ao Setor de Impressão

Para que o roteamento de comandos funcione, a ficha técnica do item comercializado precisa estar classificada corretamente.

1. Acesse o **Cadastro de Produtos**.
2. Modifique o campo **Tipo de Produto** para `Restaurante/Bar`. Esta flag habilita de forma dinâmica a aba estrutural **Restaurante** na ficha do produto.
3. Na aba Restaurante, defina o campo **Setor de Impressão** vinculando-o ao setor responsável por processar o item (ex: um `X-Bacon` deve ser direcionado à `Cozinha`).
4. Ative a flag **Controlar Status de Preparo** caso o produto passe por etapas de fabricação.

> [!info] Recursos de Detalhamento de Itens
> Nesta mesma aba estrutural são amarradas as regras para aplicação de **Complementos** (ex: adicionar queijo, bacon adicional), **Retiradas** (ex: remover salada) e inserção de **Modos de Preparo** fixos (ex: ponto da carne).

---

## Métodos de Lançamento na Interface Touch Screen

A tela de atendimento do restaurante exibe os grupos na ordem numérica configurada e os produtos internos dispostos em ordem alfabética. O operador conta com três metodologias distintas para inserção de itens em uma mesa ou comanda:

* **Navegação Touch Visual:** O operador localiza o grupo desejado nas abas laterais e clica diretamente sobre o ícone do produto.
* **Código de Barras / EAN:** O sistema mantém o campo de captura ativo em segundo plano. Caso um leitor de código de barras capture um código EAN (ex: latas de refrigerante ou água), o produto é inserido no grid instantaneamente, abrindo apenas o pop-up para ajuste de quantidade.
* **Digitação por Código Reduzido:** Caso o estabelecimento utilize cardápios com indexação numérica rápida, o operador pode digitar o código numérico reduzido do produto diretamente no teclado. O sistema processa e insere o item de forma ágil, superando a velocidade da navegação por toque.

---

## Ciclo de Vida e Controle de Status dos Itens

Quando uma comanda ou mesa é salva no terminal de vendas, o sistema gera os comandos de impressão específicos para cada impressora de setor correspondente e altera a cor dos marcadores na tela de acompanhamento gerencial.

### Estados do Fluxo de Produção:

┌─────────────────────────┐ ┌─────────────────────────┐ ┌─────────────────────────┐ │ Aguardando (Amarelo) │ ───> │ Pronto (Vermelho) │ ───> │ Entregue (Branco) │ 
│ Item em preparação │                             │ Aguardando retirada │       │ Entregue ao cliente │ └─────────────────────────┘ └─────────────────────────┘ └─────────────────────────┘

* **Aguardando (Marcador Amarelo):** O produto foi impresso no setor correspondente e encontra-se na fila de produção interna da cozinha ou copa. * **Pronto (Marcador Vermelho):** A produção do item foi concluída pelo setor. Ele está pronto no balcão de expedição aguardando o garçom realizar a retirada para entrega. * **Entregue (Marcador Branco / Padrão):** O item foi servido com sucesso na mesa do consumidor. 
>[!tip] Itens de Pronta Entrega > Para produtos que dispensam preparação fabril (ex: águas minerais ou cervejas em lata), o sistema pula automaticamente o estágio amarelo e vermelho, classificando o lançamento diretamente no status **Entregue (Branco)** assim que ele é computado pelo operador. --- ## Pontos Críticos e Validações > [!warning] Riscos de Queda de Comunicação e Fila Oculta > 1. **Bloqueio de Spooler do Windows:** Se a impressora vinculada a um setor perder conexão física (cabo desconectado ou queda de energia), o Windows reterá os comandos na fila. Ao reestabelecer o sinal, todos os pedidos acumulados serão impressos de uma vez, gerando duplicidade visual de produção. > 2. **Configuração de Pré-visualização:** Certifique-se de que a flag de "Visualizar" no cadastro do setor de impressão esteja desmarcada em ambiente de produção. Se mantida ativa, o sistema travará a tela do operador a cada fechamento de mesa esperando uma interação humana para liberar a impressão, anulando o automatismo entre balcão e cozinha.


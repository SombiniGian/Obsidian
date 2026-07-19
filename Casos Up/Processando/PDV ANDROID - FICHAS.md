
---
id: [CASO-175]
link: https://www.youtube.com/watch?v=BJLC-Bh5dls&t=11s
setor: [Suporte, Desenvolvimento, Operacional]
modulo: [Mobile / PDV Android]
tags: [android, pdv-mobile, impressao-de-fichas, stone-pos, configuracao-de-fonte, restaurante]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Operação por Fichas]]
2. [[#Mecânica de Lançamento e Herança de Opcionais]]
3. [[#Fluxo de Fechamento e Disparo de Impressão]]
4. [[#Layout e Configurações de Dimensionamento de Fonte]]
5. [[#Regras de Negócio e Pontos Críticos de Falha]]

# Visão Geral da Operação por Fichas
A modalidade de **PDV Android - Fichas** é uma extensão do [[Mobile / PDV Android]] projetada para o ecossistema de atendimento rápido em balcões (*Fast Food*), praças de alimentação, bilheterias de eventos e festivais. O fluxo consiste na centralização do recebimento financeiro: o cliente escolhe os produtos, realiza o pagamento em um terminal POS móvel ou totem, e o sistema emite de forma automática **Fichas de Atendimento Individuais** separadas por item do carrinho. Essas vias impressas servem como contrapartida física e comprovante de liberação para que o cliente realize a retirada do produto diretamente nos respectivos balcões de expedição, copa ou cozinha.

# Mecânica de Lançamento e Herança de Opcionais
Ao operar o aplicativo logado com um perfil de usuário do tipo **Fichas**, a interface herda em tempo real as árvores de complementos, pontos de preparo e opcionais parametrizadas na retaguarda do ERP para os setores de restaurante:

### Fluxo de Inserção de Itens Complexos:
1.  **Item Industrial/Bebida:** O operador toca em `Coca-Cola`. O item é inserido diretamente no carrinho sem interrupções.
2.  **Item Fracionado/Composição:** O operador seleciona `Pizza`. O aplicativo abre de forma sequencial as janelas para a escolha obrigatória ou opcional do tipo de massa e tipo de borda.
3.  **Item de Cozinha com Adicionais:** O operador seleciona `Churrasquinho de Bacon`. O sistema exige a indicação do ponto da carne (ex: `Mal passado`) e abre a grade de modificadores onde podem ser inseridos acréscimos (ex: `Adicionar Bacon`) ou exclusões de ingredientes (ex: `Retirar Cebola`).

Todas as observações inseridas na tela do Android são compiladas estruturalmente sob o formato JSON e atreladas à linha do produto para guiar os profissionais da linha de produção na montagem do prato.

# Fluxo de Fechamento e Disparo de Impressão
Ao concluir a adição dos itens ao carrinho de compras, o processo de faturamento e materialização das fichas segue a seguinte ordem síncrona de processamento:

```

[Carrinho do PDV Android] -> Avançar para Tela de Pagamento

|

v

[Selecionar Forma de Pago: Ex: Cartão de Crédito]

|

v

[Informar Número de Parcelas (Se Aplicável)]

|

v

[Processar Handshake TEF / Autorizar Transação]

|

v

[Impressão Automática 01: Comprovante Financeiro do Cartão]

|

v

[Disparo em Background: Transmissão da NFC-e à SEFAZ]

|

v

[Pop-up: Deseja Imprimir o Cupom Fiscal? Não / Sim]

|

v

[Impressão Automática 02: Fichas Individuais de Produtos por Ordem de Item]

|

v

[Limpeza Automática de Tela: Pronto para o Próximo Cliente]

````

O fechamento financeiro do cartão de crédito aciona o lote de impressão na bobina térmica acoplada da própria maquininha inteligente (ex: **Stone POS**). O sistema emite primeiro a via do cartão e, após a decisão do operador de imprimir ou omitir o cupom fiscal completo (NFC-e), o mecanismo de bobina ejeta as fichas fracionadas uma a uma por item vendido.

# Layout e Configurações de Dimensionamento de Fonte
A legibilidade das fichas de produtos é um fator crítico para evitar gargalos operacionais e erros de montagem na cozinha do estabelecimento. O layout padrão do sistema adota uma estrutura em blocos visuais limpos, onde cada ficha contém:
*   Nome em destaque do item principal (ex: `COCA-COLA`).
*   Sub-bloco com os complementos detalhados em recuo (ex: `Massa: Fina`, `Borda: Catupiry`, `Sem Cebola`).

```json
{
  "configuracao_fonte_impressao_fichas": {
    "caminho_menu": "Menu Administrador -> Pedidos -> Configuração de Fontes",
    "parametros_padrao": {
      "fonte_cabecalho": 28,
      "fonte_itens": 25
    },
    "regra_de_renderizacao": "O sistema aplica a 'fonte_cabecalho' estritamente para o nome do produto principal e a 'fonte_itens' para a descrição detalhada dos opcionais e complementos."
  }
}
````

### Ajuste de Escala Visual

Caso o cliente final relate que os textos estão pequenos para leitura em ambientes escuros de eventos, o analista de suporte ou o usuário gestor pode redefinir o tamanho das letras.

1. Efetue o login com um usuário com permissões de **Administrador** no aplicativo Android.
    
2. Acesse o menu lateral de **Pedidos**.
    
3. Localize as variáveis de tamanho de fonte. Caso as letras necessitem de maior legibilidade, altere os valores padrão (conforme payload acima) para escalas maiores (ex: Cabeçalho `32` / Itens `28`). Os novos tamanhos serão adotados na próxima ficha emitida.
    

# Regras de Negócio e Pontos Críticos de Falha

> [!warning] Fragmentação da Bobina de Impressão
> 
> Diferente do cupom fiscal unificado, a rotina de fichas executa um corte físico na guilhotina ou impõe comandos de quebra de papel para cada item individualizado do carrinho. Se uma venda contiver 1 `Coca-Cola`, 1 `Pizza` e 1 `Churrasquinho`, o hardware ejetará **três pedaços de papéis isolados** sequenciais. O operador de caixa deve estar treinado para recolher e organizar as vias de forma correta antes de entregá-las ao consumidor, mitigando o risco de omitir a entrega de um dos bilhetes de produto adquiridos.

> [!danger] Travamento da Fila de Impressão por Falha de Comunicação
> 
> Caso a API de retaguarda esteja configurada para processar a validação do leiaute de impressão de forma online (via servidor centralizado rodando FastReport) e a internet sofra uma queda repentina após a aprovação do cartão de crédito, o aplicativo não conseguirá desenhar o layout rico das fichas.
> 
> - **Comportamento de Contingência:** Para não paralisar a fila de atendimento do evento, o sistema chaveará o comportamento de impressão de forma automática para o **Modo de Impressão Local**. O layout das fichas será convertido para texto puro estruturado (ESC/POS nativo do Android), garantindo a entrega do papel físico ao cliente mesmo com o servidor de retaguarda inacessível.
>     

```
http://googleusercontent.com/youtube_content/1
```
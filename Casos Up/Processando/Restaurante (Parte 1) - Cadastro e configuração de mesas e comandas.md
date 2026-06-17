Este módulo detalha as diretrizes operacionais, os modos de atendimento e as regras de temporização do ecossistema de **Cadastro e Configuração de Mesas e Comandas** no módulo de Restaurante do ERP Código UP `[00:00:00]`. O recurso centraliza a gestão de salão e balcão num painel unificado, otimizando o fluxo de atendimento dos empregados de mesa e caixas `[00:00:22]`.

### 1. Modos de Operação do Sistema de Restauração `[00:00:49]`

O ERP exibe flexibilidade na retaguarda, permitindo que o estabelecimento adote três metodologias de atendimento em simultâneo ou isoladamente `[00:00:49]`:

- **Mapa de Mesas (Gestão de Salão):** Interface gráfica que espelha o layout físico do salão, exibindo os blocos de consumo em tempo real `[00:00:49]`.
    
- **Controlo por Comandas Individuais:** Indicado para operações baseadas em cartões numerados ou comandas impressas `[00:00:55]`. O sistema suporta múltiplas comandas ativas associadas à mesma mesa física (ex: Mesa 5 contendo a comanda 101 e 102) `[00:05:53]`.
    
- **Módulo Delivery (Entregas):** Painel independente para a captura e acompanhamento de pedidos para fora do estabelecimento `[00:01:15]`, `[00:06:00]`.
    

### 2. Cadastro Massivo de Mesas e Customização Visual `[00:01:15]`

Para simplificar a implantação inicial da ferramenta nas empresas, o sistema disponibiliza um assistente de inserção automática `[00:01:15]`:

- **Criação em Lote:** Em vez de registar uma mesa por uma, o operador insere o intervalo desejado (ex: criar da mesa 51 à mesa 70) para que o ERP popule o banco de dados instantaneamente `[00:01:36]`, `[00:01:52]`.
    
- **Regras de Negócio Cadastrais:** Cada mesa aceita descritivos personalizados, códigos alfa-numéricos (letras e números) e a flag de inativação, caso o estabelecimento reduza a capacidade de atendimento física `[00:02:03]`.
    
- **Ajuste do Painel de Visibilidade:** Na configuração do mapa, o gestor define o número máximo de linhas e colunas para obter o enquadramento ideal no monitor `[00:03:17]`. O sistema suporta a inclusão de imagens de fundo para indicar os estados de "Mesa Vazia" ou "Mesa Ocupada", embora a remoção de imagens otimize o aproveitamento de espaço do ecrã `[00:02:31]`, `[00:03:05]`.
    

### 3. Automação de Segurança e Regras de Alertas (Status das Mesas) `[00:03:23]`

O ERP Código UP possui uma camada de inteligência baseada em cronómetros que faz a varredura do salão de forma assíncrona (com tempo de atualização parametrizável em segundos) `[00:03:23]`, `[00:03:32]`:

- **Fecho Automático por Omissão (Trava Touch):** Projetado para ecrãs partilhados instalados no balcão. Se um empregado de mesa iniciar o lançamento de um pedido e abandonar o ecrã sem concluir a operação, **o sistema grava e fecha a comanda automaticamente** após o tempo limite definido (ex: 10 segundos) `[00:04:16]`, `[00:04:40]`. Isto previne que o funcionário seguinte insira itens por engano na mesa do colega `[00:04:16]`.
    
- **Alerta Amarelo (Mesa Ociosa):** Disparado quando a mesa atinge o tempo limite estipulado desde o último pedido (ex: 1 minuto) `[00:04:51]`, `[00:09:21]`. O bloco altera a sua cor para amarelo no mapa, sinalizando aos funcionários que aquela mesa necessita de atenção ou de novas ofertas `[00:04:59]`.
    
- **Alerta Vermelho (Atenção Crítica):** Ativado quando o tempo sem consumo ultrapassa o limite severo (ex: 30 minutos) `[00:05:20]`, `[00:09:30]`. O bloco assume a cor vermelha, alertando a gerência para uma possível mesa esquecida ou risco de abandono do cliente sem o pagamento da conta `[00:05:29]`.
    

### 4. Segurança na Identificação do Empregado de Mesa (Vendedor) `[00:06:00]`

A auditoria e comissão dos lançamentos operam sob duas lógicas de comportamento configuráveis `[00:06:00]`:

```
+------------------------------------------------------------------------+
|                   MÉTODOS DE IDENTIFICAÇÃO DE VENDEDOR                 |
+------------------------------------------------------------------------+
|                                                                        |
|  [ MODO A - POSTO COLETIVO ]            [ MODO B - POSTO EXCLUSIVO ]   |
|   Vários funcionários usam o             Cada computador/tablet é      |
|   mesmo ecrã de balcão.                  usado por um único funcionário.|
|              │                                         │               |
|              ▼                                         ▼               |
|   Toda a nova venda pede o                  O utilizador está amarrado |
|   Código do Vendedor no Touch.              ao Cadastro do Usuário.    |
|   (Exige digitação a cada ciclo)            (Ignora a tela de código)  |
|          [00:06:47]                                [00:07:18]          |
+------------------------------------------------------------------------+
```

- **Estação de Trabalho Coletiva (Modo Touch Balcão):** Ideal quando múltiplos empregados de mesa utilizam o mesmo terminal físico `[00:06:47]`. O ERP força a abertura de um teclado tátil numérico a cada novo atendimento, exigindo que o funcionário introduza o seu código individual antes de selecionar a mesa ou comanda `[00:06:11]`, `[00:08:05]`.
    
- **Estação de Trabalho Exclusiva (Modo Tablet/Individual):** Ideal quando o funcionário possui o seu próprio dispositivo móvel de atendimento `[00:07:37]`. Nas configurações do sistema, o administrador acede ao _Cadastro de Usuários_ e vincula o utilizador diretamente ao código do vendedor correspondente `[00:07:18]`, `[00:07:29]`. Ao efetuar o login, o ERP assume essa identidade por defeito e suprime o ecrã de pedido de código, acelerando o lançamento tátil `[00:10:21]`.
    

ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: [Assista ao vídeo no YouTube](https://www.youtube.com/watch?v=maOauuYQAL8&t=5s).
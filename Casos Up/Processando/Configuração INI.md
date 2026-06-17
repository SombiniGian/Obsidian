Este módulo detalha a função e a parametrização do **Ficheiro de Configuração `config.ini`** no ERP Código UP, um componente crítico para a conectividade do sistema e para a definição do comportamento da estação de trabalho `[00:00:00]`.

### 1. O Papel do Ficheiro `config.ini` `[00:00:08]`

Localizado na pasta de instalação, este ficheiro armazena as definições fundamentais que permitem ao ERP localizar os recursos necessários para arrancar `[00:00:08]`:

- **Caminho da Base de Dados:** Define onde está o ficheiro do banco de dados (geralmente Firebird).
    
- **DLL do Firebird:** Aponta para a biblioteca de ligação ao servidor de dados `[00:00:19]`.
    
- **Tipo de Estação:** Define se a máquina irá operar em modo "Normal" ou "PDV" (Ponto de Venda) `[00:00:29]`.
    

Quando o utilizador opta por instalar o sistema como "Servidor", o ERP cria automaticamente este ficheiro `[00:00:38]`. Caso contrário, ou numa instalação em "Estação de Trabalho", o sistema abrirá um assistente de configuração no arranque para que o utilizador indique o caminho do servidor onde os dados residem `[00:01:28]`.

### 2. Modos de Operação da Estação `[00:02:10]`

Através da tela de **Configuração da Estação**, é possível determinar o comportamento da máquina para otimizar o fluxo de trabalho `[00:02:10]`:

- **Modo Normal:** O utilizador tem acesso à tela principal do ERP, todos os menus, cadastros e módulos de gestão `[00:03:03]`.
    
- **Modo PDV (Ponto de Venda):** Recomendado para caixas ou terminais de atendimento. Ao iniciar o sistema neste modo, **o software ignora o menu principal e abre diretamente a tela de venda de balcão** `[00:02:30]`, `[00:03:12]`. Isto aumenta a segurança e simplifica a operação, impedindo que o operador de caixa aceda a áreas administrativas sem necessidade `[00:03:20]`.
    

> **Nota:** Todas as alterações feitas nesta configuração apenas surtem efeito no arranque seguinte do sistema `[00:02:49]`.

### 3. Acesso de Suporte: O Utilizador `suporte123` `[00:03:29]`

O ERP inclui um utilizador de sistema, **`suporte123`**, destinado exclusivamente a operações de manutenção e configuração técnica `[00:03:29]`, `[00:04:19]`:

- **Finalidade:** Permite aceder a menus de configuração avançada que não estão visíveis para utilizadores comuns `[00:04:11]`.
    
- **Restrições de Segurança:** Este utilizador **não possui permissão para realizar movimentações operacionais** (como faturar, cadastrar clientes ou emitir notas) `[00:04:48]`, `[00:05:06]`. Se tentar realizar qualquer operação comercial, o sistema bloqueará a ação `[00:04:56]`.
    
- **Uso Recomendado:** Esta senha deve ser tratada como sigilosa, ficando restrita apenas aos técnicos responsáveis pelo suporte do sistema `[00:04:19]`.
    

ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: [Assista ao vídeo no YouTube](https://www.youtube.com/watch?v=wxQE6ZDhXg8&t=2s).
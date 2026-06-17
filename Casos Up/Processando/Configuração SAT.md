Este módulo detalha as diretrizes operacionais, a arquitetura de rede e os passos de parametrização para a implementação do **SAT (Sistema Autenticador e Transmissor de Cupons Fiscais)** no ERP Código UP `[00:00:00]`. O recurso permite a gestão completa da emissão de cupões eletrónicos fiscais, desde a configuração local do equipamento até a centralização em servidores dedicados `[00:00:00]`, `[00:02:12]`.

### 1. Configuração Cadastral da Empresa `[00:00:12]`

Antes de iniciar a parte técnica do equipamento, é mandatório configurar os dados da empresa no ERP `[00:00:12]`:

- **Dados do Emitente:** Devem ser informados os dados fiscais da empresa que serão vinculados ao hardware SAT `[00:00:22]`.
    
- **Assinatura Digital (Software House):** É necessária para vincular a aplicação ao equipamento. O sistema disponibiliza um botão que gera esta assinatura automaticamente, mas, para ambiente de produção, requer que o certificado digital e o CNPJ da Software House estejam corretamente parametrizados `[00:00:42]`, `[00:01:01]`.
    

### 2. Arquitetura de Comunicação: Local vs. Servidor `[00:01:31]`

O ERP permite flexibilidade no posicionamento físico do hardware SAT na rede `[00:01:31]`:

- **Conexão Local:** O equipamento está ligado diretamente à estação onde o ERP está a ser utilizado `[00:02:22]`.
    
- **Conexão em Servidor Dedicado:** O hardware SAT está ligado a uma máquina específica na rede `[00:02:32]`. Neste caso, configura-se o **IP e a porta** do servidor SAT no ERP para que todas as outras estações da rede comuniquem com este ponto centralizado `[00:02:39]`.
    

### 3. Parametrização Técnica do Equipamento (Dll e Rede) `[00:03:09]`

As configurações específicas do hardware, geralmente fornecidas pelo fabricante, devem ser inseridas no painel de _Configuração SAT_ `[00:03:09]`:

- **DLL de Comunicação:** É o ponto mais crítico. Deve-se apontar para o ficheiro `.dll` específico do fabricante do hardware `[00:03:45]`. O sistema alerta que é comum existir conflito de nomes entre DLLs de diferentes fornecedores `[00:03:52]`.
    
- **Rede e Proxy:** O sistema gera ficheiros XML de configuração de rede para o equipamento conforme a topologia local (configurações de rede, IP, gateway) `[00:04:11]`, `[00:04:37]`.
    
- **Impressão:** Suporta duas modalidades: impressão direta via porta física (modelo/porta da impressora) ou via _Gerador de Relatórios_ (personalizável pela revenda) `[00:04:54]`, `[00:05:03]`.
    

### 4. Processo de Ativação e Homologação (Sefaz) `[00:06:26]`

O ciclo de vida do equipamento SAT exige processos obrigatórios junto ao fisco paulista `[00:07:25]`:

1. **Ativação:** Realizada via comandos da DLL (interface de ativação do equipamento), onde se configura a rede e o código de ativação fornecido pelo fabricante `[00:06:32]`, `[00:06:46]`. Este passo é feito apenas uma vez `[00:06:57]`.
    
2. **Vinculação:** O CNPJ da Software House deve estar cadastrado no portal do Sefaz-SP, vinculando-se o CNPJ do emitente ao equipamento SAT em questão `[00:07:32]`.
    
3. **Teste de Comunicação:** O sistema disponibiliza um botão de "Teste de Fim a Fim" que gera um XML de teste, envia ao equipamento e valida o retorno, garantindo que o ciclo de emissão está operacional `[00:07:53]`, `[00:08:04]`.
    

### 5. Otimização com o "Servidor SAT" (Background) `[00:08:38]`

Para ambientes com múltiplos pontos de venda, utiliza-se a aplicação auxiliar _Servidor SAT_ `[00:08:38]`:

- **Funcionamento:** O servidor roda minimizado na máquina onde o hardware está ligado `[00:09:08]`. Ele gere a fila de comandos e a comunicação com o banco de dados da empresa `[00:09:26]`.
    
- **Comandos de Monitorização:** Disponibiliza logs operacionais e estatísticas de uso (consultar status operacional, verificar se está conectado ou bloqueado) `[00:08:30]`, `[00:10:49]`.
    
- **Vantagem:** Permite que as estações "clientes" comuniquem com o servidor em rede sem a necessidade de ter a DLL ou configurações complexas espalhadas em todas as máquinas da loja `[00:11:08]`.
    

ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: [Assista ao vídeo no YouTube](https://www.youtube.com/watch?v=e7omZ0gkq5o).
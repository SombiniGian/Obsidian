Este vídeo detalha o procedimento de instalação e a estrutura de diretórios do ERP **Up System**, bem como as configurações iniciais necessárias para o primeiro arranque do software `[00:00:00]`.

### 1. Procedimento de Instalação `[00:00:13]`

O instalador do ERP segue um padrão convencional de ambiente Windows, sendo intuitivo e direto `[00:00:13]`:

- **Diretório de Destino:** Por predefinição, o sistema é instalado na unidade `C:\UpSystem`, mas o utilizador tem liberdade para alterar a pasta de destino conforme a política de TI da empresa `[00:00:21]`.
    
- **Arquitetura Servidor/Estação:** O instalador oferece uma opção crítica: **"Instalar Banco de Dados"** `[00:00:42]`.
    
    - **Servidor (Principal):** Deve manter esta opção marcada para que o sistema instale o motor de base de dados local.
        
    - **Estação de Trabalho (Cliente):** Se o banco de dados já estiver centralizado noutro servidor na rede, deve desmarcar esta opção para instalar apenas os ficheiros da aplicação `[00:00:49]`.
        

### 2. Estrutura de Diretórios e Ficheiros `[00:01:38]`

Após a conclusão da instalação, a pasta `UpSystem` contém uma estrutura organizada para garantir a integridade do sistema `[00:01:38]`:

- **Ficheiros de Sistema (.exe e .dll):** Conjunto de bibliotecas dinâmicas essenciais para a execução e comunicação dos diversos módulos `[00:01:12]`.
    
- **Pasta de Banco de Dados:** Contém os ficheiros de dados (apenas se a opção de servidor foi selecionada durante a instalação) `[00:01:48]`.
    
- **Documentos Fiscais:** Uma estrutura de subpastas vital para o funcionamento fiscal, contendo ficheiros de **esquema (XSD) para validação de documentos** e layouts de impressão `[00:02:05]`, `[00:02:13]`.
    

### 3. Configuração Inicial e Primeiro Arranque `[00:02:24]`

Ao abrir o sistema pela primeira vez, será apresentada uma notificação de sistema alertando que é necessário atualizar os dados da empresa `[00:02:24]`.

- **Cadastro de Empresa:** É obrigatório preencher todas as informações fiscais (CNPJ, Razão Social, Endereço). O sistema permite utilizar dados de "TESTE" (ex: preencher com "TESTE" nos campos de nome) apenas para fins de experimentação, mas recomenda-se o preenchimento rigoroso para ambientes reais `[00:02:31]`, `[00:02:41]`.
    
- **Configuração de Caminhos Fiscais:** Dentro das configurações do sistema, os diretórios de emissão de NF-e, NFC-e e SAT já vêm pré-configurados apontando para a pasta local de instalação. É responsabilidade do administrador validar se esses caminhos estão acessíveis e corretos `[00:02:50]`, `[00:03:02]`.
    
- **Configurações Padrão:** O ERP já traz pré-carregados diversos cadastros base (naturezas de operação, formas de pagamento, tipos de documentos), o que agiliza o processo de implementação inicial `[00:03:54]`, `[00:04:05]`.
    

ℹ️ **Nota de Apoio:** Se restarem dúvidas sobre como prosseguir com a parametrização específica para o seu negócio após a instalação, poderá consultar os outros módulos formativos disponíveis no canal ou aceder à demonstração completa neste link: [Assista ao vídeo no YouTube](https://www.youtube.com/watch?v=oBL6Ykv6mQE).
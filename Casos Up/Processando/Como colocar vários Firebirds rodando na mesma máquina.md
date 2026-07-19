---
id:
  - CASO-181
link: https://www.youtube.com/watch?v=PP45iBGkDtI
setor:
  - Suporte
  - Infraestrutura
  - Implementação
modulo:
  - Banco de Dados / Firebird
tags:
  - firebird
  - banco-de-dados
  - instalacao
  - vpn
  - multi-versao
  - infraestrutura
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Arquitetura Multi-Versão]]
2. [[#Pré-requisitos e Processo de Instalação]]
3. [[#Alteração de Portas Lógicas do Sistema]]
4. [[#Criação de Serviços via Prompt de Comando (CMD)]]
5. [[#Compatibilidade de Client (DLLs) e IDEs]]
6. [[#Ajustes de Tipos de Dados no Firebird 4.0]]
7. [[#Regras de Conexão no ERP e Arquivos de Configuração]]

# Visão Geral da Arquitetura Multi-Versão
A coexistência de múltiplas instâncias do banco de dados Firebird em um mesmo servidor físico ou máquina local é um cenário comum em implantações de ERP. Este procedimento é frequentemente exigido quando o cliente já possui sistemas legados de terceiros utilizando versões antigas do banco de dados (ex: `2.5`, `1.5`) e a implantação do novo sistema UP Sistemas exige uma versão moderna e de alto desempenho (ex: `3.0`, `4.0` ou futuras versões `5.0`). 

A chave para habilitar o funcionamento simultâneo sem gerar conflitos de barramento ou travamento de processos reside no **isolamento de diretórios**, na **distribuição de portas lógicas exclusivas** de comunicação TCP/IP e na **renomeação das chaves de serviços do Windows**.

# Pré-requisitos e Processo de Instalação

> [!warning] Validação de Serviços Ativos de Terceiros
> Caso a máquina de destino já possua uma versão do Firebird instalada e ativa atendendo a outro software, o instalador padrão pode gerar erros de travamento de arquivos em uso. Antes de iniciar, acesse o painel de **Serviços do Windows (services.msc)**, localize o serviço legado do Firebird e clique em **Parar**. Prossiga com as novas instalações e reinicie o serviço legado após a conclusão dos procedimentos.

### Sequência de Instalação das Instâncias:
1. Execute o instalador do Firebird 3.0. Siga os passos no modo padrão mantendo senhas e diretórios sugeridos.
2. Na última janela do instalador, **desmarque obrigatoriamente** a opção **Iniciar o serviço agora** (Start service now) e finalize.
3. Execute o instalador do Firebird 4.0. Siga as etapas idênticas, e na conclusão, também **desmarque** a opção de inicialização do serviço.

# Alteração de Portas Lógicas do Sistema
Por padrão padrão, toda instância do Firebird tenta escutar e responder na porta **3050**. Para isolar o Firebird 3.0 e permitir que a versão 4.0 assuma a porta nativa, é necessário modificar o arquivo de parametrização da versão 3.0.

1. Navegue até a pasta de instalação da instância que deseja alterar (ex: `C:\Program Files\Firebird\Firebird_3_0`).
2. Localize o arquivo `firebird.conf` e abra-o para edição.
3. Utilize o comando de busca (Ctrl + F) e pesquise pelo termo `3050`.
4. Identifique a linha contendo o parâmetro `#RemoteServicePort = 3050`.
5. Remova o caractere `#` (que atua como comentário de linha) e modifique o valor para a nova porta desejada (ex: `3053`).

```ini
# Configuração alterada no arquivo firebird.conf da versão 3.0
RemoteServicePort = 3053
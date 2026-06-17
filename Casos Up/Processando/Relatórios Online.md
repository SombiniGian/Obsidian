Este módulo detalha as diretrizes operacionais, a arquitetura de rede e os recursos gerenciais da ferramenta de **Relatórios Online** do ERP Código UP. O módulo foi desenvolvido como uma aplicação complementar (Ferramenta Extra) para permitir que proprietários e gestores monitorizem os dados financeiros e operacionais da empresa em tempo real a partir de qualquer dispositivo conectado à Internet, sem a necessidade de instalar o ERP completo no terminal de consulta `[00:00:30]`, `[00:00:48]`.

### 1. Ecossistema de Ferramentas Extras e Distribuição `[00:00:00]`

O utilitário de Relatórios Online faz parte de um pacote de aplicações modulares disponibilizado pela Código UP para expandir as capacidades do sistema principal `[00:00:04]`.

Esses módulos ficam concentrados e disponíveis para download no painel da revenda (na aba _Downloads Extras_), que engloba outras soluções específicas, como drivers de integração para teclados Gertec e módulos de pesagem para restaurantes self-service `[00:00:11]`, `[00:02:32]`.

### 2. Arquitetura de Instalação e Infraestrutura de Rede `[00:00:59]`

A ferramenta opera como um servidor web local e leve, que consome os dados diretamente do banco de dados principal da empresa `[00:01:30]`:

- **Instalação do Executável:** O instalador deve ser descarregado e colado diretamente dentro da pasta raiz do ERP na máquina que atua como o servidor local da empresa `[00:00:59]`.
    
- **Inicialização do Serviço:** Ao executar o ficheiro, o sistema inicia um serviço de background que abre uma porta de comunicação web na rede local `[00:01:08]`.
    
- **Porta de Comunicação Padrão:** Por defeito, a aplicação utiliza a porta **`8077`** (ex: acessada internamente via `http://IP_DO_SERVIDOR:8077`) `[00:01:16]`. Esta porta é customizável caso ocorram conflitos de rede no ambiente do cliente `[00:01:25]`.
    
- **Configuração para Acesso Externo (Nuvem):** Para habilitar o acesso fora da empresa de qualquer parte do mundo, a revenda técnica deve efetuar o redirecionamento de portas (_Port Forwarding_) no modem/router da empresa, apontando para o IP do servidor local, e associar um serviço de IP Fixo ou DNS Dinâmico (DDNS) `[00:01:38]`, `[00:01:45]`.
    

### 3. Interface Responsiva e Acessibilidade Multidispositivo `[00:01:52]`

Uma das principais vantagens deste módulo é o desenvolvimento do seu front-end baseado em layouts fluidos:

- **Responsividade Total:** A interface web adapta-se automaticamente ao tamanho do ecrã do utilizador, sendo ideal para consultas rápidas através de **smartphones, tablets** ou computadores portáteis `[00:01:52]`.
    
- **Sincronização em Tempo Real:** Como a aplicação web faz consultas diretas na base de dados do servidor físico local, não existem atrasos de sincronização por nuvem. Os dados de vendas e caixas apresentados ao gestor refletem o estado atualizado do estabelecimento no exato segundo da consulta `[00:01:30]`.
    

### 4. Portefólio de Relatórios Gerenciais Disponíveis `[00:01:52]`

O painel online resume os principais indicadores de desempenho do negócio necessários para auditoria remota e tomada de decisões seguras `[00:02:20]`:

- **Análise de Faturamento Comercial:** Relatórios detalhados de análise de vendas e desempenho segmentado por grupos de produtos `[00:01:52]`, `[00:02:00]`.
    
- **Fluxo de Caixa e Tesouraria:** Consultas de contas a receber e contas a pagar para acompanhamento da saúde financeira `[00:02:00]`.
    
- **Auditoria de Fechamento de Caixa:** O gestor pode listar de forma remota todos os fechos de caixa efetuados pelos operadores, entrar num registo diário específico e auditar os valores apurados detalhadamente por forma de pagamento (ex: montante recebido em dinheiro, cartões, etc.) `[00:02:09]`, `[00:02:13]`.
    
- **Exportação de Dados:** Os relatórios contam com ferramentas nativas que permitem exportar as grelhas de dados diretamente para ficheiros do formato **Microsoft Excel**, facilitando auditorias externas ou cruzamentos contabilísticos `[00:02:27]`.
    

ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: [Assista ao vídeo no YouTube](https://www.youtube.com/watch?v=Q8QsC_Y4Pp0&t=2s).
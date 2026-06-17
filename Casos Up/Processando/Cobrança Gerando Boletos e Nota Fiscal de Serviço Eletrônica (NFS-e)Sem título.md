Este módulo detalha as diretrizes operacionais, a parametrização fiscal e o processamento em lote da ferramenta de **Faturamento de Contratos, Emissão de Boletos e Nota Fiscal de Serviço Eletrônica (NFS-e)** no ERP Código UP. O recurso foi projetado para empresas que operam com receitas recorrentes (ex: mensalidades, prestação de serviços continuados ou assinaturas), automatizando a régua de cobrança e a transmissão fiscal de forma massiva `[00:00:12]`.

### 1. Parametrização Cadastral e Configuração de Vínculos `[00:00:12]`

Antes de rodar a rotina de faturamento em lote, o sistema exige a estruturação das regras de negócio na retaguarda para garantir a integridade dos dados fiscais e financeiros:

- **Configuração do Modelo de Contrato:** O administrador define o tipo de cobrança e a periodicidade padrão (ex: carteira de clientes "Mensalistas") `[00:00:14]`.
    
- **Vínculo Bancário e Tributário:** Cada modelo de cobrança é associado a uma conta bancária ativa (para registro dos boletos) e a uma Natureza de Operação de Serviço padrão, pré-configurada com o código de atividade municipal exigido pela prefeitura do contribuinte `[00:00:19]`.
    
- **Saneamento do Cadastro de Serviços:** Na ficha do serviço prestado, o ERP exige o preenchimento obrigatório da alíquota do Imposto Sobre Serviços (ISS), além das retenções federais quando aplicável (PIS, COFINS, CSLL, IRRF), garantindo que o cálculo do valor líquido da NFS-e ocorra sem intervenção manual `[00:00:39]`.
    

### 2. Geração Massiva do Borderô de Cobrança `[00:01:21]`

A centralização das cobranças é gerenciada através da tela de processamento de borderôs, eliminando a necessidade de lançar faturas individualmente cliente por cliente:

1. **Seleção de Competência:** O operador acessa o painel de inclusão de borderô e informa o mês e ano de referência que deseja faturar (ex: Competência `06/2026`) `[00:01:26]`.
    
2. **Varredura Automatizada:** O motor de busca do ERP realiza uma varredura no banco de dados e traz em grade todos os clientes ativos associados àquele modelo de contrato `[00:01:32]`.
    
3. **Processamento do Lote:** Ao acionar o comando **"Gerar"**, o sistema consolida as informações da carteira e cria as faturas teóricas do período em segundos `[00:01:34]`.
    

### 3. Faturamento Financeiro e Emissão de Boletos `[00:01:42]`

Com o borderô gerado e conferido pelo setor financeiro, o sistema inicia o fluxo de liquidação interna e geração de títulos de cobrança:

- **Injeção no Contas a Receber:** O operador aciona o comando **"Faturar"** `[00:01:42]`. Neste momento, o ERP realiza o lançamento simultâneo de todos os títulos financeiros na agenda de Contas a Receber da empresa, alimentando o fluxo de caixa futuro.
    
- **Geração Automática do Lote de Boletos:** Imediatamente após o faturamento, o sistema processa a comunicação com o banco e gera o lote de boletos bancários contendo as linhas digitáveis, códigos de barras, instruções de juros/multa e prazos de vencimento individuais `[00:01:48]`.
    

### 4. Transmissão em Lote e Homologação da NFS-e `[00:01:58]`

Após a geração financeira, o ERP Código UP aciona o seu motor de comunicação com a Secretaria de Finanças do município para legalizar os serviços prestados:

- **Seleção Fiscal:** O operador seleciona os registros faturados no grid e clica no gatilho **"Emitir NFS-e"** `[00:01:59]`.
    
- **Transmissão Assíncrona e Geração de RPS:** O sistema inicia o envio em lote das informações para o Web Service da prefeitura `[00:02:31]`. O monitor de transmissão exibe o progresso em tempo real, gerando os Recibos Provisórios de Serviços (RPS) e aguardando o retorno da prefeitura para convertê-los em notas fiscais convertidas e homologadas com sucesso `[00:02:33]`.
    
- **Visualização e Impressão:** Concluída a homologação, o sistema atualiza o status na grade e disponibiliza o espelho da NFS-e para visualização na tela ou impressão direta do documento de arrecadação municipal `[00:04:19]`.
    

### 5. Régua de Distribuição e Tratamento de Exceções de Envio `[00:04:35]`

Para encerrar a rotina operacional, o sistema executa o fluxo de entrega dos documentos ao destinatário final:

- **Disparo Automatizado por E-mail:** O ERP conta com uma rotina que realiza o disparo automatizado de e-mails para a lista de clientes faturados. Em uma única mensagem organizada, o sistema anexa o boleto PDF para pagamento e o link/espelho da nota fiscal de serviço eletrônica homologada `[00:04:42]`.
    
- **Tratamento de Falhas e Logs de Erro:** Se houver qualquer barreira no envio das mensagens (ex: e-mail do cliente incorreto ou rejeição nas credenciais e protocolo SMTP do provedor da empresa), o ERP interrompe a fila daquele registro específico e **exibe um alerta detalhado na tela** indicando a falha de autenticação `[00:04:51]`. Isso permite que o suporte ou o operador identifique o erro imediatamente, ajuste as configurações e reenvie o documento sem comprometer o andamento dos demais e-mails do lote.

Para assistir ao passo a passo detalhado, você pode acessar o vídeo completo pelo link: [https://www.youtube.com/watch?v=gWdr8g_slq4](https://www.youtube.com/watch?v=gWdr8g_slq4)[[]]


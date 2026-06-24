---
id: [CASO-002]
link: https://www.youtube.com/watch?v=gWdr8g_slq4
setor: [Financeiro, Faturamento]
modulo: [Cobrança, Fiscal]
tags:
  - nfs-e
  - boleto-bancario
  - borderou-cobranca
  - emissao-lote
data_criacao: 2026-06-24
---

# Processamento de Borderô: Geração de Boletos e Emissão de NFS-e em Lote

Este documento descreve o fluxo técnico e operacional para a geração automatizada de boletos bancários e emissão de Notas Fiscais de Serviço Eletrônicas (NFS-e) a partir do módulo de **Borderô de Cobrança**. A rotina visa otimizar o faturamento mensal de contratos ou cobranças recorrentes, eliminando a digitação manual.

---

## Sumário
1. [[#Configuração Padrão do Borderô]]
2. [[#Hierarquia e Regras de Preenchimento do Serviço]]
3. [[#Fluxo de Execução Técnica]]
4. [[#Monitoramento da Transmissão e Status da NFS-e]]
5. [[#Impressão e Distribuição por E-mail]]
6. [[#Tratamento de Erros e Pontos de Falha]]

---

## Configuração Padrão do Borderô

Antes de gerar os registros de faturamento, é necessário parametrizar os dados estruturais que servirão como base (*fallback*) para o processamento.

* **Caminho de Acesso:** Na tela do **Borderô de Cobrança**, acesse o botão de **Configuração** (ícone de engrenagem).

### Campos Obrigatórios:
* **Tipo Cobrança Padrão:** Define a modalidade da cobrança (ex: `MENSALISTA`).
* **Operação para NFS-e:** Associa a [[Natureza de Operação]] responsável pelas regras fiscais de prestação de serviço.
* **Serviço para NFS-e:** Associa o código estrutural do serviço cadastrado no catálogo de [[Produtos/Serviços]] do sistema, o qual contém as alíquotas de ISS, PIS, COFINS, CSLL e o Código Federal de Serviço.

---

## Hierarquia e Regras de Preenchimento do Serviço

O sistema trabalha com uma regra de herança piramidal para determinar qual código de serviço e alíquota serão enviados para a Prefeitura na emissão da NFS-e:

[Cadastro do Cliente (Serviço Específico)] -> (Se vazio, adota:) [Configuração do Borderô (Serviço Padrão)]

> [!info] Exceção por Cliente > Se um cliente específico demandar uma tributação diferenciada ou um texto de retenção exclusivo, configure o campo **Serviço Mensalista NFS-e** diretamente na aba **Serviços** dentro do **Cadastro do Cliente**. Essa configuração individual anula o serviço padrão do borderô apenas para este cliente. --- ## Fluxo de Execução Técnica A rotina de processamento segue uma ordem cronológica rígida de dependência de dados:

┌──────────────┐ ┌─────────────────┐ ┌────────────────┐
│ 1. Gerar │ ───> │ 2. Gerar │ ───> │ 3. Emitir │ 
│ Cobranças │ │ Financeiro (F5) │ │ NFS-e (F8) │ 
└──────────────┘ └─────────────────┘ └────────────────┘

1. Na tela principal do borderô, clique em **Incluir**. 
2. Filtre e selecione a competência desejada (ex: `DEZEMBRO / 2020`) e clique em **Gerar Cobrança**. 
3. Com as cobranças listadas na grade, execute o comando **Financeiro (F5)** para criar os lançamentos correspondentes no Contas a Receber. 
4. (Opcional) Utilize o comando **Boletos (F6)** para realizar o registro e emissão dos boletos bancários em lote. 
5. Selecione os registros financeiros gerados e clique no botão **Emitir NFS-e (F8)**. O sistema abrirá a aba interna **Notas Fiscais de Serviço**. 
--- ## Monitoramento da Transmissão e Status da NFS-e Após disparar o lote através do botão **Transmitir (F5)**, o sistema inicia a comunicação síncrona/assíncrona com a API da prefeitura homologada. > [!info] Performance de Transmissão > A transmissão de NFS-e tende a ser mais lenta que a de NF-e (produtos), pois depende do tempo de resposta dos servidores dedicados de cada município, processando nota por nota sequencialmente.

---### Legenda de Status do Lote: * **Ícone Verde (Confirmado):** Nota autorizada com sucesso. O número da NFS-e e o código de autenticação são gravados no banco de dados. * **Ícone Laranja (Pendente/Erro):** A nota foi rejeitada pela prefeitura ou houve falha de comunicação. O motivo da rejeição será exibido detalhadamente na tela. 

--- ## Impressão e Distribuição por E-mail Após a autorização do lote, o sistema habilita os comandos de saída em massa: * **Imprimir (F6):** Renderiza o espelho de todas as notas autorizadas em lote na tela, prontas para impressão física ou salvamento em PDF. * **E-mail (F7):** Dispara automaticamente o arquivo XML e o link/PDF da NFS-e para os endereços eletrônicos mapeados no cadastro dos tomadores de serviço.

--- ## Tratamento de Erros e Pontos de Falha > [!warning] Validações Críticas de Lançamento > 
1. **Ausência de E-mail Cadastrado:** Se o lote de e-mails contiver algum cliente sem endereço configurado, o processo de envio em lote será interrompido e um log de erro do protocolo SMTP (ex: `501 Syntax error`) será gerado, detalhando qual registro falhou. >
2. **Correção de Notas Rejeitadas:** Caso uma nota mude para o status laranja (Erro), o usuário deve selecionar o item, clicar em **Alterar (F3)**, corrigir o dado incorreto (como CPF/CNPJ inválido, endereço sem número ou código de serviço incompatível) e acionar novamente o botão **Transmitir**.
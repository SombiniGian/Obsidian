---
id: CASO-024
link: https://www.youtube.com/watch?v=7YhAEYcWDVk
setor: Suporte, Desenvolvimento, Faturamento
modulo: Integração Fiscal e NF-e
tags:
  - nfe
  - contingencia
  - sefaz
  - erro-transmissao
  - upsystem
data_criacao: 2026-06-24
---

# Fluxo de Contingência e Resolução de Erros na Transmissão de NF-e

Este documento técnico descreve os procedimentos operacionais e as regras de negócio integradas ao [[UpSystem]] para o tratamento de falhas, rejeições e acionamento dos modos de contingência durante a emissão de Notas Fiscais Eletrônicas (NF-e) junto à [[SEFAZ]].

---

## Sumário
1. [[#1. Diagnóstico de Erros de Conexão e Rejeições]]
2. [[#2. Configuração e Ativação do Modo de Contingência]]
3. [[#3. Fluxo de Transmissão Pós-Contingência]]
4. [[#4. Validações de Integridade e Pontos Críticos]]

---

## 1. Diagnóstico de Erros de Conexão e Rejeições

O processo de faturamento e transmissão síncrona ou assíncrona pode ser interrompido por instabilidades na infraestrutura da [[SEFAZ]] ou por inconsistências nos dados do emitente/destinatário. O sistema mapeia os retornos em duas categorias principais:

* **Rejeições Fiscais:** Retornos com códigos de status específicos (ex: Rejeição 204: Duplicidade de NF-e). O título permanece bloqueado para impressão do DANFE até a devida correção.
* **Erros de Time-out/Conexão:** Falha de comunicação gerada por queda de internet local ou indisponibilidade dos servidores do fisco (erros de HTTP 500 ou 403).

> [!warning] Ponto de Atenção: Bloqueio de Documentos Vinculados
> Quando ocorre uma rejeição ou falha de transmissão da nota fiscal, o ERP bloqueia automaticamente as rotinas subsequentes, como a geração da cobrança bancária na carteira de [[Boletos Bancários]]. O boleto só é liberado após a validação e recebimento do protocolo de autorização de uso.

---

## 2. Configuração e Ativação do Modo de Contingência

Quando a indisponibilidade do integrador estadual inviabiliza o faturamento em lote das cargas ou pedidos e o tempo de resposta ultrapassa os limites operacionais, deve-se acionar o regime de contingência (geralmente [[SVC-AN]] ou [[SVC-RS]], dependendo da UF do emitente).

1. Acesse o menu **Cadastros > Contas/Configurações Fiscais** ou o painel de **Gerenciamento de NF-e**.
2. Localize os parâmetros de **Tipo de Emissão**.
3. Altere o status de **1 - Normal** para a modalidade de contingência adequada (ex: **6 - Contingência SVC-AN** ou **7 - Contingência SVC-RS**).
4. Insira a **Justificativa de Entrada em Contingência**, detalhando o motivo da alteração (mínimo de 15 caracteres exigidos pelo fisco).
5. Clique em **Gravar** para replicar a configuração para as próximas transmissões.

---

## 3. Fluxo de Transmissão Pós-Contingência

Com o modo de contingência ativo, o fluxo de faturamento intercepta o destino do arquivo XML:
[ Faturamento de Pedido ] ──> [ Tipo Emissão = SVC ] ──> [ Transmissão para Servidor Virtual ] │ ▼ [ Impressão do DANFE Liberada ]

1. Retorne à tela de **Faturamento de Carga** ou **Pedidos**.
2. Selecione os documentos pendentes de envio e clique no botão **Transmitir Notas**.
3. O sistema gerará o XML alterando a tag `<tpEmis>` para refletir o ambiente de contingência ativo. 
4. Após a assinatura com o certificado digital, o lote é enviado para a estrutura da estrutura virtual autorizadora.
5. Sendo validado com sucesso, o sistema altera o status do faturamento e realiza a liberação imediata para a impressão do DANFE e emissão das cobranças.

--- 
## 4. Validações de Integridade e Pontos Críticos O uso do ambiente de contingência exige atenção redobrada do operador para evitar problemas de conciliação e duplicidade de numeração. > [!tip] Retorno ao Modo Normal > Assim que os serviços do servidor principal da [[SEFAZ]] estadual forem restabelecidos, o usuário deve obrigatoriamente acessar o painel de configurações fiscais e retornar o campo **Tipo de Emissão** para **1 - Normal**, evitando o uso desnecessário do ambiente de contingência. 
### Tabela de Tratamento de Inconsistências | Código do Erro / Cenário | Causa Provável | Ação Corretiva Esperada | | :--- | :--- | :--- | | **Rejeição: Duplicidade** | O número da nota já foi enviado em lote anterior que caiu antes do retorno. | Executar a rotina de **Consultar Chave de Acesso** para atualizar o protocolo de autorização local. | | **Falha de Conexão Sem Retorno** | Queda de pacotes no momento do fechamento do lote HTTP. | Aguardar o tempo de varredura e tentar retransmitir em lote reduzido ou ativar contingência se persistir por mais de 15 minutos. | | **Erro de Certificado Digital** | Certificado vencido, desconectado (A3) ou sem permissão de leitura no diretório. | Verificar a validade do arquivo `.pfx` ou a conexão da mídia física na máquina servidora. |
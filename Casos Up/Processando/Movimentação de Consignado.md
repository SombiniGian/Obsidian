---
id: CASO-028
link: https://www.youtube.com/watch?v=g58YmDXDTT0
setor: Suporte, Implantação, Faturamento
modulo: Vendas e Integração Fiscal
tags:
  - nfs-e
  - faturamento
  - configuracao-fiscal
  - issqn
  - upsystem
data_criacao: 2026-06-24
---

# Configuração e Emissão de Nota Fiscal de Serviço Eletrônica (NFS-e)

Este documento técnico descreve o fluxo completo de parametrização fiscal, vínculo de provedores municipais e execução do faturamento de Notas Fiscais de Serviço Eletrônicas (NFS-e) no ambiente [[UpSystem]]. O objetivo é guiar o analista de suporte na resolução de rejeições de schemas e na correta amarração de impostos municipais.

---

## Sumário
1. [[#1. Parâmetros da Empresa e Vínculo com Provedores Municipais]]
2. [[#2. Cadastro de Serviços e Alíquotas de ISSQN]]
3. [[#3. Fluxo de Emissão e Faturamento de Ordem de Serviço]]
4. [[#4. Validações de Schemas e Pontos Críticos de Falha]]

---

## 1. Parâmetros da Empresa e Vínculo com Provedores Municipais

Diferente da NF-e (modelo 55), que possui um padrão nacional único gerenciado pela [[SEFAZ]] estadual, a NFS-e responde a legislações municipais. O sistema intercepta o comportamento do arquivo XML com base no provedor de tecnologia contratado pela prefeitura do emitente (ex: Fiorilli, GovDigital, IPM, Tecnosistemas).

1. Acesse o menu **Cadastros > Empresa / Parâmetros Fiscais**.
2. Identifique os campos de identificação municipal:
   - **Inscrição Municipal:** Deve ser preenchida sem pontos ou traços.
   - **Código de Tomador / Regime Especial de Tributação:** Define se a empresa possui benefícios como Microempresa Municipal ou Estimativa.
3. No campo **Provedor NFS-e**, selecione a empresa homologada responsável pela recepção dos lotes no município (ex: *Fiorilli* para Sertãozinho/SP).
4. Configure os caminhos de diretórios locais na aba de arquivos para gravação dos arquivos de envio de **Lote RPS** (Recibo Provisório de Serviços) e leitura do protocolo de conversão em NFS-e.

> [!info] Natureza da Operação
> A correta classificação da Natureza da Operação (ex: *1 - Tributação no município*, *2 - Tributação fora do município*, *3 - Isenção*) é o principal fator de validação do arquivo. Uma configuração incorreta gera rejeição imediata no lote de RPS enviado.

---

## 2. Cadastro de Serviços e Alíquotas de ISSQN

A estrutura tributária do serviço prestado deve estar vinculada à tabela da Lei Complementar nº 116/2003 para garantir a integridade fiscal do XML.

1. Acesse **Cadastros > Serviços**.
2. No cadastro do item, preencha compulsoriamente o **Código LC 116** (Item da Lista de Serviços - ex: *07.02* para Execução de Obras).
3. Preencha o **Código de Tributação Municipal (CTISS)** exigido especificamente pelo layout da prefeitura configurada.
4. Informe a alíquota padrão de **ISSQN** (Imposto Sobre Serviços de Qualquer Natureza).
5. Se aplicável para o perfil de clientes da empresa, configure os percentuais de retenção na fonte para os impostos federais ([[PIS]], [[COFINS]], [[CSLL]] e [[INSS]]).

> [!warning] Retenção de ISS em Operações de Subempreitada
> Quando o serviço é executado em município terceiro e a legislação exige a retenção do imposto por parte do tomador, a flag **"ISS Retido Fonte"** deve ser marcada na ordem de serviço. Isso altera a tag `<IdentifRetencao>` no XML para sinalizar que o valor do imposto será deduzido do total líquido a receber.

---

## 3. Fluxo de Emissão e Faturamento de Ordem de Serviço

O gatilho para a geração do RPS e posterior conversão em NFS-e ocorre no encerramento do documento de prestação de serviços.

1. Acesse o módulo de **Movimentações > Ordem de Serviço** ou **Pedido de Serviço**.
2. Insira o cliente tomador e certifique-se de que o **CPF/CNPJ**, **Inscrição Municipal** (se houver) e o código **IBGE** da cidade estão preenchidos corretamente no cadastro do parceiro.
3. Adicione os itens de serviço configurados na seção anterior.
4. Escolha a [[Formas de Pagamento]] apropriada e clique no botão **Faturar Documento**.
5. O sistema gerará um registro temporário de **RPS** e abrirá a tela de transmissão.
6. Clique em **Transmitir Lote**. O sistema assinará o documento usando o [[Certificado Digital]] da empresa (A1 ou A3) e enviará o lote para o Web Service da prefeitura.
7. Sendo aceito, o sistema atualiza o status para **"Serviço Convertido / Nota Autorizada"**, liberando a impressão do espelho da NFS-e.

---

## 4. Validações de Schemas e Pontos Críticos de Falha

As inconsistências no módulo de serviço geralmente resultam do desalinhamento de layouts específicos de cada município.

> [!warning] Ponto de Falha: Rejeição por Falta de Assinatura no Lote ou no RPS
> **Sintoma:** O provedor retorna erro informando que o XML enviado não possui assinatura válida, mesmo com o certificado digital ativo.
> **Causa:** Determinadas prefeituras exigem que a assinatura digital seja aplicada tanto na tag raiz do Lote de RPS quanto em cada RPS individualmente dentro do arquivo. Outras exigem apenas no Lote.
> **Solução:** Acesse o menu de suporte técnico em **Configurações Fiscais > Opções Avançadas do Provedor** e altere as chaves de controle de validação (ex: alterar a flag `AssinarRPS` para `True`), forçando a dupla assinatura antes da transmissão.

### Tabela de Erros de Transmissão Comuns

| Código do Erro / Mensagem | Causa Provável | Ação Esperada do Operador |
| :--- | :--- | :--- |
| **Código do Item da Lista de Serviço Inexistente** | O código LC 116 informado no cadastro de serviço não foi atualizado ou aceito pela prefeitura local. | Validar o código com a contabilidade da empresa e corrigir o campo no cadastro de serviços. |
| **Erro HTTP 500 / Timeout** | O servidor da prefeitura ou do provedor contratado está fora do ar ou em manutenção técnica. | Aguardar a estabilização e utilizar a rotina de **Consultar Lote de RPS** para verificar se o lote enviado anteriormente foi processado. |
| **CNPJ do Prestador não autorizado** | O cadastro da empresa na prefeitura não possui liberação para emissão via Web Service (ambiente de integração de terceiros desativado). | O cliente deve acessar o portal web da prefeitura e autorizar a emissão de notas via sistema integrado de terceiros (API/RPS). |
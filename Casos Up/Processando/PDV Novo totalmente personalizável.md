---
id: CASO-025
link: https://www.youtube.com/watch?v=eZLAMLHAm2k
setor: Suporte, Faturamento, Retaguarda
modulo: Integração NF-e e Configurações Fiscais
tags:
  - nfe
  - erro-transmissao
  - rejeicao-sefaz
  - certificado-digital
  - upsystem
data_criacao: 2026-06-24
---

# Resolução de Inconsistências e Certificação Digital na Transmissão de NF-e

Este documento técnico aborda os procedimentos operacionais para identificação, diagnóstico e correção de falhas de comunicação e rejeições de Notas Fiscais Eletrônicas (NF-e) no ambiente [[UpSystem]]. Detalha a validação de parâmetros fiscais, manutenção do ciclo de vida dos certificados e fluxos corretivos junto à [[SEFAZ]].

---

## Sumário
1. [[#1. Diagnóstico de Rejeições Comuns da SEFAZ]]
2. [[#2. Gerenciamento e Instalação do Certificado Digital]]
3. [[#3. Configurações de Schemas e Regras de Negócio]]
4. [[#4. Fluxo de Tratamento de Falhas e Contingência]]

---

## 1. Diagnóstico de Rejeições Comuns da SEFAZ

O processo de faturamento pode ser interrompido por validações de regras de negócio impostas pelos servidores do fisco. A correta interpretação dos códigos de retorno reduz o tempo de parada do setor de expedição.

* **Rejeição 204 (Duplicidade de NF-e):** Ocorre quando o número do documento fiscal enviado já foi autorizado anteriormente pelo emitente. 
* **Rejeição 539 (Duplicidade com Diferença na Chave de Accesso):** Indica que a numeração da nota já existe na base da SEFAZ, mas associada a dados de produtos, valores ou destinatários distintos.
* **Erros de Schema (XML Inválido):** Falha gerada quando campos obrigatórios do cadastro do cliente (como CPF/CNPJ, Inscrição Estadual ou Endereço) ou do produto (como NCM, CFOP ou Alíquotas) não cumprem as exigências estruturais da legislação vigente.

> [!warning] Trava de Segurança Financeira
> O sistema possui um vínculo de integridade que impede a emissão de documentos de cobrança no módulo de [[Boletos Bancários]] caso a nota fiscal atrelada ao pedido sofra rejeição. A liberação do boleto e do DANFE para impressão é estritamente condicionada ao status de **Autorizada o Uso**.

---

## 2. Gerenciamento e Instalação do Certificado Digital

A assinatura digital do arquivo XML é o elemento legal que garante a autoria e a integridade da NF-e. Falhas de transmissão frequentemente derivam de problemas na leitura ou validade da certificação padrão.

1. Acesse o menu **Cadastros > Configurações Fiscais / Empresa**.
2. Localize a seção dedicada aos parâmetros do **Certificado Digital**.
3. O sistema suporta dois modelos principais de certificação:
   - **Modelo A1:** Arquivo digital criptografado (geralmente formato `.pfx` ou `.p12`) instalado diretamente no servidor ou estação de trabalho. Apresenta maior estabilidade em faturamentos em lote, como na rotina de [[Cargas e Distribuição]].
   - **Modelo A3:** Mídia física (cartão inteligente ou token USB). Requer a presença constante do hardware conectado à máquina e digitação periódica do PIN de segurança.
4. Para atualizar ou vincular um novo certificado, clique em **Selecionar Certificado**, navegue até o arquivo ou repositório do Windows, informe a senha de instalação e clique em **Gravar**.

> [!info] Validade do Certificado
> Certificados expirados rompem imediatamente o canal de comunicação segura (SSL/TLS) com a SEFAZ, resultando em erros genéricos de conexão HTTP ou falhas de "Cryptographic Service Provider". A verificação preventiva da data de vencimento deve ser realizada diretamente na retaguarda do sistema.

---

## 3. Configurações de Schemas e Regras de Negócio

Para garantir que o arquivo XML gerado pelo ERP seja compatível com as atualizações periódicas das Notas Técnicas da SEFAZ, os pacotes de **Schemas (arquivos .xsd)** devem estar atualizados no diretório de instalação do sistema.

* No painel de controle fiscal, valide o caminho configurado para a pasta de Schemas.
* Se o sistema apresentar erros de estrutura de tags (ex: *Elemento inválido para o layout atual*), verifique se a versão ativa atende às exigências vigentes no estado do emitente.
* **Campos Críticos de Validação:**
  - **Inscrição Estadual (IE):** Deve estar ativa e regularizada no Cadastro Centralizado de Contribuintes (CCC). Isenções precisam ser explicitamente sinalizadas alterando a flag do cliente para "Contribuinte Isento".
  - **Tributação (Regime Tributário):** Empresas do Simples Nacional utilizam códigos de CSOSN, enquanto empresas do Regime Normal utilizam códigos de CST para o cálculo do ICMS.

---

## 4. Fluxo de Tratamento de Falhas e Contingência

Quando a falha de transmissão não está associada a erros cadastrais, mas sim à indisponibilidade de comunicação com o servidor da SEFAZ estadual, o operador deve executar o protocolo de contingência para evitar o bloqueio do fluxo de expedição logística.
[ Iniciar Transmissão ] ──> Erro de Conexão / Time-out (15min+) │ ▼ [ Ativar Modo Contingência ] │ (Configurações Fiscais) │ ▼ [ Alterar tpEmis para SVC ] │ ▼ [ Transmitir e Liberar DANFE ]

1. Se o erro de comunicação persistir por mais de 15 minutos, aceda ao menu **Parâmetros Fiscais da Empresa**. 
2. Altere o campo **Tipo de Emissão** do status **1 - Normal** para o correspondente da sua região (ex: **6 - SVC-AN** ou **7 - SVC-RS**). 
3. Insira obrigatoriamente a justificativa de entrada em contingência no campo de texto apresentado pelo sistema. 
4. Salve as alterações e retorne à tela de faturamento. 
5. Selecione as notas e clique em **Transmitir**. O XML será direcionado para a estrutura do servidor virtual de contingência, permitindo a liberação imediata do tráfego das mercadorias. 

>[!tip] Retorno à Operação Padrão > O modo de contingência é um regime de exceção temporário. Assim que a estabilidade do servidor principal da SEFAZ estadual for reestabelecida, o usuário deve acessar novamente a tela de configurações e reverter o parâmetro para **1 - Normal**, garantindo a conformidade e evitando rejeições por uso indevido da estrutura virtual.


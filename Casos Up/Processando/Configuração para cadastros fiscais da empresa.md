---
id: CASO-034
link: https://www.youtube.com/watch?v=Jb2_Tun9Zpw&t=13s
setor: Suporte, Implantação, Faturamento
modulo: Configurações Fiscais da Empresa
tags:
  - certificado-digital
  - nfce
  - nfe
  - sefaz
  - contingencia
data_criacao: 2026-06-24
---

# Documentação Técnica: Infraestrutura Fiscal, Certificado Digital e Parâmetros de Mensageria

Esta documentação provê os requisitos lógicos, parametrizações de diretórios, criptografia de dados e arquitetura de contingência para a validação fiscal das notas eletrônicas ([[NF-e]], [[NFC-e]], [[MDF-e]], [[CT-e]]) no núcleo de retaguarda do ERP.

---

## Sumário
1. [[#1. Configuração Cadastral Core e Dados do Contador]]
2. [[#2. Instanciação do Certificado Digital e Documentos Eletrônicos (Web Services)]]
3. [[#3. Parâmetros Específicos do Módulo NFC-e / NF-e]]
4. [[#4. Configurações Globais, Comunicação e Validações]]

---

## 1. Configuração Cadastral Core e Dados do Contador

As informações cadastrais primárias da empresa funcionam como chaves de validação primordiais nos nós dos arquivos XML gerados pelo sistema. A integridade da emissão de documentos fiscais eletrônicos está diretamente vinculada ao preenchimento correto desses dados.

* **Acesso:** **Ficha Cadastral da Empresa**.
* **Campos Mandatórios / Obrigatórios:** **CNPJ/CPF**, **Razão Social**, **Inscrição Estadual (IE)**, **Inscrição Municipal (IM)** e endereço logradouro completo; também dados do contador (exigidos para geração de arquivos como [[SPED]] e [[Sintegra]]).
* **Aba SPED/SINTEGRA:** Centraliza o registro cadastral dos dados do Contador (Nome, CPF, Registro CRC, Telefone e Endereço). Essas tags são injetadas de forma automática na exportação de arquivos fiscais mensais de escrituração do estabelecimento.
* **Regra de Validação:** O **CNPJ** cadastrado nesta tela deve ser idêntico ao CNPJ contido no [[Certificado Digital]] vinculado. Divergências gerarão rejeição imediata da [[SEFAZ]] no momento da abertura do canal de comunicação SSL.

---

## 2. Instanciação do Certificado Digital e Documentos Eletrônicos (Web Services)

A assinatura dos documentos e o handshake com a SEFAZ exigem a parametrização do Certificado Digital. O painel de **Configurações de Documentos Eletrônicos** centraliza os parâmetros de comunicação com o Web Service fiscal.

### Ambiente e Certificado Digital
* **Ambiente:** Alterna entre **Homologação** (testes sem validade jurídica) e **Produção** (emissão oficial).
* **Vinculação do Certificado Digital:** O sistema expõe duas metodologias equivalentes para a leitura da chave criptográfica:
  1. **Modelo A1 via Arquivo (.pfx / .p12):** Indicação direta do caminho do arquivo físico (diretório local ou de rede) com a digitação da senha de criptografia correspondente.
  2. **Modelo A1/A3 via repositório Windows:** Seleção do certificado previamente instalado no repositório do Windows (Capicom), com captura/injeção automática do número de série do componente.

```
[ Instanciação do Certificado ]
              |
  { Escolha do Modelo de Armazenamento }
         /                    \
(Modelo A1 via Arquivo .PFX)   (Modelo A1/A3 via Windows)
         |                              |
[ Aponta Caminho do Arquivo Físico ]   [ Abre Repositório Windows (Capicom) ]
         |                              |
[ Informa Senha de Criptografia ]      [ Captura Serial de Forma Automática ]
```

> [!info] Repositório de Arquivos
> Por padrão, o sistema preenche e aponta as pastas de schemas, XMLs salvos, retornos e logs para os subdiretórios criados no diretório nativo de instalação do sistema. Caso seja necessária uma arquitetura cliente-servidor onde múltiplos terminais compartilham os arquivos, deve-se alterar os caminhos utilizando o padrão de rede UNC ou apontando para o IP do servidor local.

---

## 3. Parâmetros Específicos do Módulo NFC-e / NF-e

Cada aba fiscal ([[NF-e]], [[NFC-e]], [[MDF-e]], [[CT-e]]) herda os mesmos padrões lógicos de configuração, necessitando de atenção especial aos seguintes campos:

### Contingência e Tipo de Emissão
* **Normal:** Envio imediato em tempo real ao Web Service.
* **Offline (Contingência):** Deve ser ativado em cenários de queda de internet ou instabilidade crítica da SEFAZ.
* **Justificativa Obrigatória:** Ao alterar o tipo de emissão para **Offline**, o campo **Justificativa** torna-se obrigatório. A ausência de um texto explicativo (mínimo legal exigido pelo fisco) impedirá a gravação e a validação do XML.

### Controle de Numeração e Impressão
* **Sequenciamento Histórico:** O campo **Último Número Emitido** determina o ponto de partida do sequenciamento. Se a empresa já emitia notas em outro software e parou no número 40, deve-se preencher `40` nesta tela para que o sistema gere a próxima nota como `41`.
* **Ambientes Isolados:** A numeração em ambiente de Homologação é independente da numeração do ambiente de Produção.
* **Código CSC:** O preenchimento do **CSC (Código de Segurança do Contribuinte)** e seu respectivo **IdCSC** (fornecidos pela SEFAZ via contador) é estritamente obrigatório para a validação do QR Code impresso no DANFE da NFC-e.

> [!warning] Alerta de Numeração
> Alterar ou retroceder manualmente o número da nota em uso sem a devida validação prévia na SEFAZ causará erros graves de **Rejeição: Duplicidade de NF-e** ou **Quebra de Sequência**, bloqueando o fluxo de faturamento do Frente de Caixa.

---

## 4. Configurações Globais, Comunicação e Validações

### Envio de E-mails e Timeouts
* **SMTP Nativo:** Permite configurar o servidor de e-mail de saída (ex: `smtp.gmail.com`, porta e senha de aplicativo) para disparo automatizado do XML e da DANFE ao cliente final.
* **Tentativas e Retorno:** Configura o limite de tentativas de reenvio em caso de falha de oscilação de rede e o tempo limite de espera de resposta da SEFAZ.
* **Protocolos:** Recomenda-se manter a marcação ativa do protocolo de criptografia **SSL/TLS** para conformidade com os requisitos de segurança dos servidores integrados.

### Parâmetros de Validação do Cadastro de Produtos
No painel secundário de preferências fiscais da empresa, existem flags limitadores para o cadastro de itens:

* **Validar dados fiscais no cadastro do produto:**
  - **Ativado (Recomendado):** O sistema impede que o usuário salve novos produtos caso campos fiscais obrigatórios (como [[NCM]], [[CSOSN]], [[CST]], e alíquotas) estejam em branco ou inválidos.
  - **Desativado:** Permite salvar cadastros incompletos. Útil apenas se a empresa operar o software de modo puramente gerencial (sem emissão fiscal).

> [!tip] Melhor Prática de Implantação
> Mantenha a flag **Validar dados fiscais no cadastro do produto** sempre ativa e configure uma **Tributação Padrão** padrão nesta mesma tela (ex: regime Simples Nacional - Não Tributado). Assim, todo novo produto inserido herdará uma base fiscal segura por padrão, mitigando rejeições futuras no PDV por negligência operacional do usuário.

Para aplicar as modificações executadas em tela, clique no botão **Salvar**.

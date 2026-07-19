---
id: CASO-217
link: https://www.youtube.com/watch?v=gEYSJ-6OIIY
setor: Suporte
modulo: Configurações Fiscais
tags:
  - cte
  - certificado_digital
  - configuracao_fiscal
  - transportadora
data_criacao: 2026-07-18
---

# Configuração de Documentos Fiscais Eletrônicos (CT-e)

Este guia prático documenta o passo a passo para a parametrização inicial do módulo de emissão de Conhecimento de Transporte Eletrônico (**CT-e**) no sistema, abrangendo desde o primeiro acesso pós-instalação até o vínculo do certificado digital e diretórios operacionais.

## Sumário
- [[#Atualização de Banco de Dados e Cadastro Inicial]]
- [[#Parametrização do Certificado Digital]]
- [[#Configuração Técnica do Módulo CT-e]]
- [[#Sequenciamento Numérico e Configurações de E-mail]]

---

## Atualização de Banco de Dados e Cadastro Inicial

Ao executar o sistema pela primeira vez após rodar o instalador padrão, a rotina de verificação estrutural é acionada automaticamente.

1. **Atualização do Banco:** Caso o sistema detecte a necessidade de reestruturação de tabelas, a janela de atualização será exibida. Clique no botão **Atualizar** para compatibilizar a base de dados. Se o banco já estiver na versão mais recente, a interface avançará diretamente para a tela de parametrização da empresa.
2. **Identificação do Emitente:** É obrigatório o preenchimento dos dados da empresa emitente (Razão Social, CNPJ/CPF e Inscrição Estadual).
3. **Registro de Transportador:** Para empresas do setor logístico, acesse os campos específicos e preencha o **Registro de Transportadores Nacionais** (RNTRC). O preenchimento do código **IOT** (Id de Operação de Transporte) também está disponível nesta seção.

---

## Parametrização do Certificado Digital

A assinatura dos arquivos XML exige um certificado digital válido (padrão ICP-Brasil). O sistema oferece dois métodos de leitura na aba de **Documentos Eletrônicos**:

### Opção 1: Certificado Digital Tipo A1 (Arquivo .PFX)
Permite vincular o certificado sem a necessidade de instalação prévia no repositório do Windows.
* Marque a opção de leitura por arquivo.
* Clique no botão de busca para selecionar o arquivo `.pfx` ou `.p12`.
* Insira a senha de criptografia da chave privada (definida no momento da exportação do certificado).

### Opção 2: Certificado Digital Instalado (Repositório Windows)
Indicado para certificados do tipo A1 já instalados ou cartões/tokens do tipo A3.
* Clique no campo de seleção de certificados para abrir a listagem do sistema operacional.
* Escolha o certificado correspondente à empresa emitente.

> [!warning] Validação de Ambiente
> Certifique-se de definir corretamente o campo **Ambiente** como **Homologação** (para a realização de testes de emissão sem valor fiscal) ou **Produção** (para emissão real com validade jurídica). Selecione também a **UF** correspondente à circunscrição do emitente (ex: Minas Gerais).

---

## Configuração Técnica do Módulo CT-e

Navegue até a aba interna específica de **CT-e** para mapear os arquivos e layouts de transmissão.

### Versão e Tipo de Emissão
* **Versão:** Definir como **3.0** (ou a versão vigente distribuída pela SEFAZ).
* **Tipo de Emissão:** O padrão deve ser mantido como **Normal**. A opção **Contingência** (como o SVC-AN / SVC-RS) só deve ser ativada quando os servidores centrais da SEFAZ estiverem fora do ar, exigindo a inserção manual de um justificativa detalhada para a ativação do regime especial.
* **Modelo e Série:** O modelo padrão para Conhecimento de Transporte é o **57**. Informe a série fiscal designada pela contabilidade (ex: `1`).

### Mapeamento de Diretórios (Pastas do Sistema)
Para fins de organização, recomenda-se criar uma estrutura de pastas centralizada no disco local do servidor (ex: dentro de uma pasta raiz chamada `CT-e` ou `DF-e`).

* **Caminho de Resposta:** Defina o diretório onde o componente fiscal gravará os retornos das consultas e recibos da SEFAZ.
* **Esquemas (Schemas):** Indique a pasta contendo os arquivos `.xsd` que realizam a validação estrutural do XML antes do envio. Esses arquivos de esquema são fornecidos junto ao pacote de instalação do sistema.
* **Arquivo de Impressão (DACTE):** Selecione o arquivo de layout do DACTE (geralmente em formato específico de relatório ou `.fr3`) que é enviado junto com os arquivos de instalação para a renderização gráfica do documento.

> [!tip] Armazenamento de Segurança
> Embora o sistema ofereça o campo para salvar os XMLs de transmissão localmente em disco, o sistema realiza nativamente a gravação e armazenamento de toda a estrutura do XML assinado diretamente dentro do banco de dados, garantindo maior segurança contra perdas físicas.

---

## Sequenciamento Numérico e Configurações de E-mail

### Continuidade de Numeração (Empresas em Migração)
Se o cliente estiver migrando de outro software emissor e já possuir históricos de emissão, o sequenciamento deve ser respeitado para evitar rejeições por duplicidade.
* Localize o campo **Último Número**.
* Informe o número exato do último CT-e que foi autorizado em produção no software antigo. O sistema calculará o próximo número incrementando `+1` de forma automática. Se for uma empresa nova, mantenha o campo zerado para iniciar a partir do número `1`.

### Parametrização de Envio Automático (SMTP)
Na aba lateral de configurações gerais ou de e-mail, insira as credenciais do servidor de saída da empresa para habilitar o envio automático do XML e do PDF do DACTE para os tomadores do serviço e clientes envolvidos na operação de transporte:
* **Host SMTP** (ex: `smtp.provedor.com`)
* **Porta** (ex: `465` ou `587`)
* **Usuário / E-mail de autenticação**
* **Senha**
* **Código IBGE:** Garanta o preenchimento correto do código IBGE do município da empresa para evitar conflitos na geração das tags de localidade do documento fiscal.
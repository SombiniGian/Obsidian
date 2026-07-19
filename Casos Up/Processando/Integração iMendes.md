---
id:
  - CASO-145
link: https://www.youtube.com/watch?v=NBWsm9IshRU
setor:
  - Suporte
  - Implementação
  - Fiscal
modulo:
  - Cadastros / Integração iMendes
tags:
  - imendes
  - integracao-fiscal
  - tributacao
  - auditoria-ncm
  - ncm
  - cadastro-de-produtos
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Integração iMendes]]
2. [[#Passo 1: Credenciamento e Configuração da Empresa]]
3. [[#Passo 2: Consulta e Atualização em Massa de Produtos]]
4. [[#Passo 3: Consulta e Ajuste de Produto Individual]]
5. [[#Pontos Críticos e Regras de Negócio]]

# Visão Geral da Integração iMendes
A integração com a plataforma **iMendes** automatiza a auditoria, saneamento e atualização fiscal da base de dados de produtos do ERP. Através do consumo direto das APIs da iMendes, o sistema valida códigos [[NCM]], alíquotas de impostos (ICMS, PIS, COFINS) e códigos [[CST/CSOSN]], mitigando riscos de autuações fiscais por preenchimento de alíquotas obsoletas e reduzindo a carga de trabalho manual em empresas do regime normal (Lucro Presumido e Lucro Real).

# Passo 1: Credenciamento e Configuração da Empresa
Antes de disparar requisições contra as APIs de auditoria tributária, os parâmetros de autenticação devem ser salvos na retaguarda.

1. Acesse o menu **Cadastros > Empresas** (ou clique na aba **Empresas** na listagem rápida).
2. Selecione a filial desejada e clique no botão **Alterar**.
3. Navegue até a aba **Configuração iMendes**.
4. Realize o preenchimento das variáveis fornecidas no contrato com a auditoria:
   * **Ambiente:** Selecione a opção `Produção`.
   * **CNPJ Base iMendes:** CNPJ da empresa autorizado para as consultas.
   * **Login:** Usuário de acesso à API.
   * **Senha:** Chave/Token de criptografia.
5. Clique no botão **Consultar Situação** para forçar um teste de *handshake* e certificar a conectividade. Estará tudo correto, clique em **Salvar**.

# Passo 2: Consulta e Atualização em Massa de Produtos
A rotina permite auditar múltiplos itens simultaneamente através das grades de listagem.

1. Acesse o menu **Cadastros > Produtos**.
2. Clique no botão **Opções** localizado no menu inferior da grade e ative a flag **Alteração em Massa** (o sistema liberará caixas de marcação múltipla ao lado de cada registro).
3. Marque as caixas dos produtos que deseja auditar tributariamente.
4. Clique novamente no botão **Opções** e selecione a rota: **Tributação iMendes**.
5. O ERP exibirá uma barra de progresso com a string `Criando lista para consulta iMendes`, seguida de `Aguarde consultando Tributação iMendes`.
6. **Interface de Retorno:** Concluído o processo, o ERP redirecionará o usuário para uma janela exclusiva chamada **Painel iMendes - Visualizar**. Nesta tela, serão listados todos os produtos consultados com seus novos status de conformidade tributária.
7. Para inspecionar as correções de alíquotas aplicadas em uma linha específica, selecione o produto na grade e tecle **F4** (ou clique em **Visualizar**). O sistema abrirá a janela de manutenção exibindo a aba **Dados Fiscais** com os campos atualizados pela inteligência iMendes.

# Passo 3: Consulta e Ajuste de Produto Individual
Caso o estabelecimento realize o cadastro isolado de uma nova mercadoria e queira validar as alíquotas imediatamente, a consulta pode ser acionada de forma unitária.

1. Na listagem de **Produtos**, posicione o cursor sobre o item desejado.
2. Tecle **F3** (ou clique em **Alterar**) para entrar na tela de edição do item.
3. Navegue até a aba superior **Documentos Fiscais**.
4. Localize e clique no botão **Tributação iMendes** presente dentro da área fiscal da ficha técnica.
5. O sistema exibirá o pop-up de processamento em tempo real `Aguarde consultando Tributação iMendes`.
6. Os campos fiscais (como alíquotas internas, diferimentos ou substituição tributária) serão populados na tela com as respostas do servidor da iMendes.
7. Clique no botão **Gravar** para consolidar os dados na base Firebird.

# Pontos Críticos e Regras de Negócio

> [!warning] Validação pelo Código de Barras (EAN)
> O motor de buscas da iMendes utiliza o **Código de Barras (EAN-13)** gravado no produto como chave primária de indexação para localizar as regras tributárias exatas perante a indústria. Produtos cadastrados sem código de barras (em branco) ou utilizando códigos gerados internamente de forma sequencial (ex: códigos iniciados por `200` para balanças) retornarão com erros de processamento ou falhas de localização nas APIs da iMendes, mantendo a tributação antiga inalterada.
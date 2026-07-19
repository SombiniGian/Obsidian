---
id:
  - CASO-201
link: https://www.youtube.com/watch?v=iD0cBcoU_c0&t=2s
setor:
  - Suporte
  - Faturamento
  - Fiscal
modulo:
  - Fiscal / GNRE
tags:
  - gnre
  - guia-de-recolhimento
  - icms-st
  - difal
  - integracao-fiscal
  - sefaz
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da GNRE]]
2. [[#Configurações Globais no Cadastro de Empresas]]
3. [[#Mecânica de Campos Dinâmicos por UF e Receita]]
4. [[#Fluxo de Carga e Sincronização de Tabelas Oficiais]]
5. [[#Emissão e Campos Adicionais Obrigatórios]]
6. [[#Pontos Críticos e Regras de Validação]]

# Visão Geral da GNRE
A **GNRE (Guia Nacional de Recolhimento de Tributos Estaduais)** é o documento fiscal digital utilizado para realizar o pagamento de impostos devidos a Unidades da Federação (UFs) distintas da UF de origem do emitente. É amplamente empregada no recolhimento de ICMS por Substituição Tributária (ICMS-ST) por operação e no Diferencial de Alíquota (DIFAL) nas vendas interestaduais destinadas a consumidor final. O submódulo no sistema centraliza a geração, transmissão e impressão dessas guias de forma integrada com a SEFAZ de destino.

# Configurações Globais no Cadastro de Empresas
Antes de iniciar a geração de guias, o administrador deve parametrizar as variáveis estruturais de comunicação com o portal da GNRE.
1. Acesse o menu **Cadastro de Empresas** e localize a aba **GNRE**.
2. Preencha as propriedades obrigatórias:
    * **Versão:** Define a versão do layout de comunicação XML aceito pela SEFAZ de destino.
    * **Diretório dos Esquemas (Schemas):** Caminho local ou de rede contendo os arquivos `.xsd` que realizam a validação estrutural do XML antes do envio (similar à parametrização da [[NF-e]]).
    * **Arquivo de Relatório (.frx):** Mapeamento do arquivo de layout de impressão (ex: FastReport) responsável por formatar e gerar o PDF impresso da guia de recolhimento.

# Mecânica de Campos Dinâmicos por UF e Receita
Diferente de outros documentos fiscais com regras rígidas e uniformes, a estrutura de preenchimento da GNRE é **altamente dinâmica**. Cada Estado (UF) possui total autonomia para exigir ou dispensar campos de acordo com o código da receita tributária selecionado.

O motor de regras do sistema altera a interface em tempo real com base no binômio **UF de Destino** + **Código de Receita**:
* **Caso 1 (Minas Gerais - Substituição Tributária):** Ao selecionar a UF `MG` e o código de `Substituição Tributária`, o sistema bloqueia os campos de detalhamento ou produto por falta de exigência legal do fisco mineiro.
* **Caso 2 (Pernambuco - Comunicação/Transporte):** Ao migrar para a UF `PE` com receita de comunicação, o sistema habilita campos específicos de identificação de convênios/protocolos.
* **Caso 3 (Tocantins / Goiás):** Ao selecionar estas UFs, o sistema abre automaticamente os combos de **Detalhamento da Receita** e **Produto**, obrigando o operador a classificar o subgrupo econômico da mercadoria transportada.

# Fluxo de Carga e Sincronização de Tabelas Oficiais
Para garantir que o sistema conheça exatamente quais campos ativar e quais códigos estão vigentes em cada UF sem a necessidade de atualizações manuais de código (Hardcode), o módulo consome um web service de consulta de regras da GNRE.

1. Acesse a tela de **Configurações / Tabelas GNRE**.
2. Na primeira execução (onde a grade de regras e códigos de receita estará vazia), clique no botão **Atualizar Dados**.
3. O sistema disparará uma requisição síncrona ao servidor central da GNRE, baixando a matriz atualizada de dependências tributárias de todas as UFs e salvando-a no banco de dados local.

# Emissão e Campos Adicionais Obrigatórios
Ao acessar a tela de emissão em **Documentos Fiscais > GNRE** e realizar a inserção de um registro, o operador deve atentar-se às **Informações Adicionais / Campos Complementares**, que também são dinâmicos:

* **Chave de Acesso da NF-e:** Campo obrigatório para a grande maioria das receitas por operação, exigindo o vínculo da chave de 44 dígitos da nota fiscal que originou o imposto.
* **Observações:** Texto livre para inserção de dados de decretos ou notas de empenho.
* **Campos do Tipo Data:** Determinadas receitas exigem a inserção expressa da data de emissão do documento de origem ou a data limite de vencimento para cálculo de acréscimos legais.

# Pontos Críticos e Regras de Validação

> [!warning] Validação de Campos Adicionais em Branco
> Se o operador selecionar uma UF que exige a chave de acesso da NF-e e tentar salvar o registro sem preenchê-la, o sistema emitirá um erro de validação local antes do envio. Caso consiga forçar a transmissão, a SEFAZ de destino rejeitará o lote com a mensagem: `Campo adicional X obrigatório não informado`.

> [!danger] Desatualização da Matriz de Regras (Botão Atualizar)
> Sempre que um estado criar um novo código de receita ou alterar a exigência de um produto na guia, as transmissões começarão a falhar por rejeição de código inválido. Para solucionar o problema, o suporte ou o usuário deve obrigatoriamente executar a rotina de **Atualizar Dados** para que o sistema remapeie a nova árvore de validações do fisco.
---
id: CASO-214
link: https://www.youtube.com/watch?v=J1ry6DycKDM
setor: Suporte
modulo: Faturamento / MDF-e
tags: [mdfe, cte, configuracao, importacao_cte, vinculo]
data_criacao: 2026-07-18
---

# Estrutura e Pré-requisitos para Configuração e Vínculo de MDF-e

Este documento descreve os fluxos operacionais, os pré-requisitos técnicos e os procedimentos de validação necessários para a geração do Manifesto Eletrônico de Documentos Fiscais (**MDF-e**) por meio do agrupamento e importação de Conhecimentos de Transporte Eletrônicos (**CT-e**).

## Sumário
- [[#Pré-requisitos Fiscais e Estruturais]]
- [[#Fluxo de Inclusão e Importação de Documentos]]
- [[#Comportamento e Consistência dos Dados de Logística]]
- [[#Pontos de Atenção e Validação de Transmissão]]

---

## Pré-requisitos Fiscais e Estruturais

A correta geração do arquivo magnético do manifesto depende estritamente do estado físico e fiscal dos documentos originários na base de dados do [[ERP]].

> [!warning] Validação Física do XML
> Para realizar o agrupamento no manifesto, não basta que o CT-e esteja marcado com o status "Transmitido" no banco de dados. O sistema exige a existência real e a integridade do arquivo **XML assinado e autorizado** no diretório físico de armazenamento. Caso o arquivo físico esteja ausente, o processo de importação e amarração será interrompido.

---

## Fluxo de Inclusão e Importação de Documentos

O processo centraliza os conhecimentos autorizados para consolidar a carga que acobertará o transporte intermunicipal ou interestadual.

### Passo a Passo da Rotina
1. Acesse o módulo de manifestos e clique no botão **Incluir**.
2. Com a tela de preenchimento aberta, localize e clique na função **Importar**.
3. O painel de busca aplicará o filtro com base em intervalos de **Data** e no status de autorização dos documentos.
4. O operador pode utilizar a caixa de seleção global (**Selecionar Todos**) ou marcar individualmente os CT-es que compõem a rota logística do veículo.
5. Clique em **Confirmar** para transferir a amarração das chaves de acesso para a grade do MDF-e.

---

## Comportamento e Consistência dos Dados de Logística

Após o gatilho de importação, o sistema realiza a leitura dos metadados dos CT-es selecionados para auto-popular os campos de carregamento e descarregamento.

### Distribuição por Localidade
* **Cidades de Descarregamento:** A interface agrupa e exibe as cidades de destino com base nos endereços dos tomadores/destinatários contidos nos CT-es. Ao selecionar uma cidade específica na árvore de navegação lateral, o sistema filtra e exibe apenas os documentos pertencentes àquela localidade.

### Vínculo Automático de Frota
* **Tração e Reboque:** Se os cadastros de [[Veículos]] e motoristas estiverem devidamente preenchidos e associados aos CT-es de origem, o sistema realiza a herança de dados, preenchendo os campos de placa, UF e condutor de forma automática na aba do modal rodoviário. Caso contrário, o operador deverá realizar a inserção manual diretamente no bloco de transporte do manifesto.

---

## Pontos de Atenção e Validação de Transmissão

> [!info] Conceito Chave: Validação de Região
> O MDF-e exige que todos os documentos vinculados pertençam à mesma rota ou fluxo logístico coerente com o encerramento do manifesto. Certifique-se de que a abrangência das cidades importadas respeita as regras de validação da SEFAZ para evitar rejeições de percurso.

> [!tip] Fluxo de Correção de Erros
> Se a tentativa de transmissão resultar em falha por falta de XML, execute a rotina de sincronização de arquivos para re-escrever o XML autorizado na pasta correspondente antes de tentar um novo envio do manifesto.


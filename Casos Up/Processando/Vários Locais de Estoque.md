---
id: [CASO-001]
link: https://www.youtube.com/watch?v=SbN02Qu57Zc
setor: [Suporte, Desenvolvimento, Logística]
modulo: [Estoque]
tags:
  - múltiplos-locais
  - transferência-estoque
  - natureza-operacao
data_criacao: 2026-06-24
---

# Controle de Múltiplos Locais de Estoque

O sistema possui uma funcionalidade que viabiliza a gestão descentralizada do inventário, permitindo que uma mesma empresa controle o saldo de produtos distribuídos em múltiplos locais (ex: gôndola, loja física, depósitos distintos). Caso haja mais de uma empresa cadastrada na mesma base de dados, cada organização gerenciará sua própria estrutura de depósitos de forma isolada.

---

## Sumário
1. [[#Pré-requisitos e Configurações Iniciais]]
2. [[#Cadastro de Depósitos]]
3. [[#Vinculação Automática via Natureza de Operação]]
4. [[#Movimentações e Transferência de Estoque]]
5. [[#Comportamento nas Telas do Sistema]]
6. [[#Pontos Críticos e Validações]]

---

## Pré-requisitos e Configurações Iniciais

Para ativar a separação visual e o controle segregado do inventário por filial e depósito, é mandatório habilitar o parâmetro geral do sistema.

1. Acesse as configurações globais de inventário.
2. Ative a opção **Estoque por empresa**.

> [!info] Impacto Visual
> Com esta opção ativa, a visualização na ficha técnica do produto passará a exibir detalhadamente o saldo dividido por empresa e seus respectivos locais cadastrados (ex: Empresa 1 - Depósito Geral, Empresa 1 - Estoque Principal).

---

## Cadastro de Depósitos

O gerenciamento e a criação dos novos almoxarifados ou pontos de armazenamento são realizados em um menu dedicado.

* **Caminho de Acesso:** Menu **Local Estoque**.
* **Capacidade:** O sistema permite a criação de N locais de forma ilimitada conforme a necessidade logística da operação.

> [!tip] Retrocompatibilidade
> Durante o processo de atualização do sistema para a versão com suporte a múltiplos locais, um registro inicial denominado **Estoque Principal** é gerado de forma automatizada. Caso o cliente não utilize a função multi-depósito, a rotina padrão permanece inalterada, centralizando tudo no local padrão.

---

## Vinculação Automática via Natureza de Operação

A correta baixa ou entrada de produtos de forma automatizada nas frentes de caixa (PDV) e no faturamento depende diretamente da parametrização das regras fiscais.

1. Acesse o cadastro de **Natureza de Operação** (ex: Venda de Mercadorias - NF-e / NFC-e).
2. Localize o campo **Local do Estoque**.
3. Defina qual depósito deve sofrer o impacto da movimentação daquela operação técnica.

> [!warning] Validação de Fallback
> Se o campo de local de estoque for deixado em branco na natureza de operação selecionada, o sistema adotará por *fallback* o **Estoque Principal**. Recomenda-se preencher este campo explicitamente para evitar descompasso em operações que faturem especificamente a partir de um depósito secundário.

---

## Movimentações e Transferência de Estoque

Para realizar o balanceamento de saldo e o remanejamento físico de itens entre galpões ou entre empresas sem a necessidade de emitir um fluxo de venda simulado, utiliza-se a rotina dedicada de movimentação interna.

* **Caminho de Acesso:** Menu **Transferência de Estoque**.

### Fluxo de Execução:
1. Selecione a **Empresa de Origem** e o **Local de Estoque de Origem**.
2. Selecione a **Empresa de Destino** e o **Local de Estoque de Destino** (suporta transferências intercompany ou internas).
3. Insira os itens e informe as quantidades a serem transferidas.
4. Confirme a gravação para que o processamento do saldo ocorra instantaneamente em ambas as pontas.

---

## Comportamento nas Telas do Sistema

Todas as rotinas operacionais que interferem no comportamento de inventário foram atualizadas para exibir a origem/destino do saldo. O campo passará a constar obrigatoriamente nas seguintes interfaces:

* **Inventário / Balanço de Estoque**
* **Pedido de Compra**
* **Pedido de Venda**
* **Nota Fiscal Emitida (Saídas)**
* **Nota Fiscal Recebida (Entradas/Compras)**

> [!info] Lançamento de Itens em Notas Fiscais
> Ao realizar a digitação ou importação de uma Nota Fiscal, o campo de local de estoque dentro do grid de itens será preenchido automaticamente com base na regra definida na [[#Vinculação Automática via Natureza de Operação|Natureza de Operação]], permitindo alteração manual item a item caso o usuário tenha a devida permissão e ciência da operação.

---

## Pontos Críticos e Validações

> [!warning] Riscos de Ruptura de Estoque e Erros de Faturamento
> 1. **Faturamento sem Saldo Local:** Se a emissão de notas for configurada para um local padrão (ex: Estoque Principal) mas o produto físico estiver alocado no Depósito 2, o sistema poderá bloquear a venda por falta de saldo ou gerar um saldo negativo no local principal.
> 2. **Alinhamento Operacional:** É uma boa prática realizar a [[#Movimentações e Transferência de Estoque|Transferência de Estoque]] prévia para o depósito padrão de vendas antes de iniciar os fluxos de faturamento automáticos, garantindo a integridade dos dados fiscais e físicos.
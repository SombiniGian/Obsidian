---
id: CASO-UP-CONFIG-004
link: https://www.youtube.com/watch?v=PSFIRDwYxF4
setor: Suporte, Implantação, Fiscal
modulo: Movimentações (Inventário de Estoque)
tags:
  - up-system
  - inventario-estoque
  - sped-fiscal
  - sintegra
  - acerto-estoque
  - custo-medio
data_criacao: 2026-06-24
---

# Processamento e Parametrização de Inventário de Estoque

Este documento estabelece as diretrizes técnicas para a criação, manipulação e consolidação do Inventário de Estoque no ERP da Código UP Sistemas. O módulo gerencia o balanço físico de mercadorias, permitindo o alinhamento de saldos gerenciais/contábeis e a exportação de dados para obrigações fiscais.

---

## Sumário
1. [[#1. Fluxo de Inicialização e Definição de Escopo]]
2. [[#2. Regras de Valorização de Estoque]]
3. [[#3. Destinação do Inventário: Ajuste de Saldo vs. Finalidade Fiscal]]
4. [[#4. Manipulação de Itens e Ajustes em Lote]]
5. [[#5. Validação de Lançamentos na Ficha Cardex]]

---

## 1. Fluxo de Inicialização e Definição de Escopo

O lançamento de inventário é executado de forma centralizada para congelar e redefinir as quantidades de produtos em uma determinada data de competência.

### 1.1 Processo de Abertura
Para iniciar um novo lote de contagem, o operador deve seguir o caminho de interface padrão no ERP:

<Sequence>
  <Step title="Acessar o Menu de Movimentações" subtitle="Navegação Básica">
    No menu superior do sistema, clique em <b>Movimentações</b> e selecione a opção <b>Inventário de Estoque</b>.
  </Step>
  <Step title="Iniciar Novo Registro" subtitle="Inclusão">
    Clique no botão <b>Incluir</b> para abrir o formulário de parametrização do novo inventário.
  </Step>
  <Step title="Definir a Data de Competência" subtitle="Referência Temporal">
    Preencha o campo <b>Data do Inventário</b> com o dia limite da contagem física (ex: 31 de dezembro para fechamentos anuais de balanço).
  </Step>
</Sequence>

---

## 2. Regras de Valorização de Estoque

No momento da criação do inventário, é obrigatório determinar qual indexador financeiro será associado ao cálculo patrimonial das mercadorias. O ERP disponibiliza quatro modalidades de precificação:

* **Custo Atual:** Baseia-se no último valor de compra registrado na ficha do produto.
* **Custo Médio:** Indicador ponderado que recalcula o valor unitário a cada entrada de nota fiscal por média móvel. **(Configuração homologada e recomendada para fins contábeis e fiscais).**
* **Preço de Venda:** Utiliza o valor nominal de prateleira da tabela de preços ativa.

> [!info] Diretriz Contábil
> O uso do **Custo Médio** assegura a conformidade com as exigências da Receita Federal para a composição do Bloco H do [[Sped Fiscal]] e registros do [[Sintegra]], refletindo o valor real investido em estoque ativo.

---

## 3. Destinação do Inventário: Ajuste de Saldo vs. Finalidade Fiscal

Uma das configurações mais críticas do módulo reside no campo **Acertar Estoque**, o qual define se o documento gerará movimentações físicas de entrada/saída nas fichas dos produtos ou se funcionará estritamente como um espelho de dados declaratórios.
```
[Configuração: Acertar Estoque]
                            │
   ┌────────────────────────┴────────────────────────┐
   ▼                                                 ▼
 [NÃO]                                            [SIM]
```

┌───────────┐ ┌───────────┐ │ Apenas │ │ Atualiza │ │ Declaração│ │ Saldos │ │ Fiscal │ │ Físicos │ └───────────┘ └───────────┘ │ │ ▼ ▼ Gera Bloco H sem Afeta Tipo de Estoque: alterar o Kardex - Gerencial - Contábil - Ambos



### 3.1 Opção: Não Acertar Estoque (`Acertar Estoque = Não`)
* **Comportamento:** O ERP salva as quantidades digitadas pelo operador em tabelas isoladas de inventário. Os saldos atuais da tela de [[Cadastro de Produtos]] permanecem inalterados.
* **Aplicação:** Utilizado quando a empresa precisa gerar o livro de registro de inventário retroativo para auditorias fiscais, mas já retomou a operação diária de vendas e não pode sofrer retrocessos nos saldos atuais de gôndola.

### 3.2 Opção: Acertar Estoque (`Acertar Estoque = Sim`)
* **Comportamento:** O processamento grava registros de ajuste na conta-corrente de estoque de cada item. O sistema exige a especificação de qual ambiente físico sofrerá a intervenção:
  * **Gerencial:** Modifica apenas o saldo interno de controle logístico.
  * **Contábil:** Modifica o saldo oficial associado à emissão de Notas Fiscais.
  * **Ambos:** Aplica a nova quantidade simultaneamente nas duas camadas de saldo.

---

## 4. Manipulação de Itens e Ajustes em Lote

O preenchimento da lista de produtos a serem inventariados é otimizado através de assistentes de carga em lote e filtros dinâmicos de grade.

### 4.1 Captura de Itens via Filtros Avançados
Ao acionar o botão **Selecionar**, a interface do ERP exibe um painel de consulta no qual o usuário pode isolar o universo de contagem por:
* Status cadastral (Ativos/Inativos).
* **Grupo de Produtos** ou Marca.
* Filtro de Linha Base (Mercadorias apenas com saldo positivo, apenas com saldo negativo ou zerados).

> [!tip] Inventários Rotativos
> Para empresas que realizam contagens parciais (inventários rotativos de segurança), selecione apenas um **Grupo de Produtos** específico por vez. Isso evita o travamento operacional de outros setores da empresa durante a validação.

### 4.2 Alteração de Valor Patrimonial em Lote
O painel de inventário dispõe de campos para **Manipulação de Valor em Lote**, permitindo aplicar acréscimos ou defasagens percentuais diretamente sobre o montante final apurado:
* **Diminuir Percentual:** Aplica uma taxa de depreciação sobre o custo total (ex: informar `10%` para reduzir o valor de ativos obsoletos).
* **Aumentar Percentual:** Adiciona margem de valorização sobre a base de custo dos itens informados.

### 4.3 Digitação de Quantidades e Descarte
* Na coluna **Novo Estoque**, o operador deve inserir a quantidade exata apurada na contagem física.
* Itens adicionados incorretamente à listagem de contagem podem ser eliminados individualmente por meio do botão **Excluir** posicionado na barra lateral do grid.

---

## 5. Validação de Lançamentos na Ficha Cardex

Quando o inventário é salvo com a opção de ajuste de saldo ativada, o ERP gera automaticamente contrapartidas de correção no extrato de movimentação do produto.

### 5.1 Estrutura do Log de Movimentação (Kardex)
Ao inspecionar a aba de histórico de estoque dentro do [[Cadastro de Produtos]], a auditoria exibirá uma linha com o seguinte padrão técnico:

```ini
[Movimentacao_Estoque]
ID_Movimentacao = 007
Tipo_Operacao = "Acerto de Estoque"
Origem = "Inventário"
Codigo_Inventario_Origem = [ID_DO_INVENTARIO]
Saldo_Contabil_Resultante = [Valor_Digitado_No_Inventario]
Saldo_Gerencial_Resultante = [Valor_Digitado_No_Inventario]
````

> [!warning] Ponto de Atenção para Exportação Fiscal Durante o fechamento do período fiscal da empresa, o módulo de geração de arquivos magnéticos do [[Sped Fiscal]] consultará diretamente o ID deste inventário processado. O sistema filtrará apenas as mercadorias contidas nele, convertendo as quantidades consolidadas nas respectivas linhas do Registro Bloco H de forma automatizada, desde que o código do inventário seja referenciado na rotina de exportação.
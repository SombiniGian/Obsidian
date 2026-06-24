---
id:
link: https://www.youtube.com/watch?v=yHdVRO36xko
setor: Suporte
modulo: Produção
tags:
  - ordem-de-producao
  - lote-de-producao
  - automacao-pdv
  - controle-de-estoque
  - insumos
data_criacao: 2026-06-24
---

# Sumário
1. [[#Visão Geral do Fluxo Automatizado]]
2. [[#Pré-requisitos e Estrutura de Produtos]]
3. [[#Configuração da Natureza de Operação]]
4. [[#Configuração das Ordens de Produção]]
5. [[#Validação Prática no PDV]]
6. [[#Análise Pós-Venda e Rastreabilidade]]

---

# Visão Geral do Fluxo Automatizado

Esta documentação detalha o procedimento para automatizar a criação e o fechamento de uma **Ordem de Produção (OP)** ou **Lote de Produção** de forma diretamente vinculada à venda de um produto acabado no ponto de venda (PDV).

Este fluxo é ideal para negócios como padarias, restaurantes e lanchonetes, onde a produção ocorre simultaneamente ou imediatamente após a venda, eliminando a necessidade de o operador lançar manualmente as ordens de fabricação. O sistema realiza as seguintes ações coordenadas ao finalizar a venda:

1. Identifica os produtos vendidos que possuem uma ficha técnica de composição ativa.
2. Gera automaticamente uma Ordem de Produção correspondente à quantidade vendida.
3. Alimenta o estoque do produto acabado.
4. Deduz os insumos (matérias-primas) de acordo com os coeficientes definidos na composição.
5. Registra a saída final do produto acabado decorrente da venda.

---

# Pré-requisitos e Estrutura de Produtos

Para que o automatismo ocorra, o produto principal deve estar devidamente parametrizado com o tipo **Produto Acabado** e conter sua respectiva árvore de componentes cadastrada na aba de insumos.

> [!info] Exemplo Prático de Ficha Técnica
> No caso de um produto do tipo **Omelete**, a composição estruturada no sistema deve prever as quantidades proporcionais por unidade produzida:
> - **Ovo**: 2 Unidades
> - **Orégano**: 1 Pacote
> - **Sal**: 10 Gramas

> [!warning] Validação Crítica de Composição
> O sistema gera Ordens de Produção automáticas **única e exclusivamente** para itens que possuam insumos vinculados à sua ficha técnica. Produtos normais de revenda que venham a ser incluídos na mesma venda (ex: barra de cereal, bebidas) serão processados normalmente pela rotina padrão de escoamento e não acionarão o módulo de produção.

---

# Configuração da Natureza de Operação

A parametrização que vincula a venda à geração automática da OP é efetuada no cadastro de regras fiscais de saída.

1. Acesse o menu de parametrização e abra a **Natureza de Operação** utilizada para as vendas no PDV.
2. Navegue até a aba **Configuração**.
3. Localize o campo **Gerar Ordem de Produção**.
4. Modifique a opção para **Ao faturar o pedido**.
5. Clique em **Salvar**.

---

# Configuração das Ordens de Produção

Para evitar que as ordens geradas fiquem paradas com o status "Em Aberto", exigindo intervenção manual para baixa, é necessário forçar a execução imediata no módulo fabril.

1. Navegue até o menu de **Movimentações** > **Ordens de Produção**.
2. Clique no botão de **Configuração** localizado no painel de controle da tela.
3. Configure os gatilhos de estoque da seguinte forma:
   - **Quando movimentar estoque de inventário de Produto Produzido**: Defina como **FINALIZAR**.
   - **Quando movimentar estoque de inventário de Insumos**: Defina como **FINALIZAR**.
4. Marque obrigatoriamente a opção: **Incluir com data de Produção já preenchida**.

> [!tip] Comportamento Esperado do Sistema
> Ao marcar a opção de inclusão com a data de produção preenchida, o sistema ignora o status inicial "Em Aberto". A ordem é gerada, executa instantaneamente o processamento dos estoques e adquire diretamente o status de **PRODUZIDO**.

---

# Validação Prática no PDV

O fluxo operacional executado no terminal de vendas segue a rotina padrão de atendimento, sem sobrecarga para o operador de caixa:

1. No terminal de **Caixa Livre**, inicie uma nova venda.
2. Bip ou pesquise pelo produto acabado (ex: **Omelete**).
3. Insira opcionalmente um item de revenda direta (ex: **Barra de Cereal**) para testar a separação de comportamentos.
4. Proceda com as condições de pagamento e acione a finalização da operação.
5. O sistema efetuará a transmissão e a validação do documento fiscal eletrônico (NFC-e / NF-e).

---

# Análise Pós-Venda e Rastreabilidade

Após a conclusão da venda, os registros podem ser auditados nos módulos gerenciais do ERP para garantir a integridade dos dados e o controle dos custos de produção.

### Tela de Ordens de Produção
Ao acessar **Movimentações** > **Ordens de Produção** e atualizar o grid, uma nova linha será exibida contendo o status **PRODUZIDO**. O sistema preenche os metadados de rastreio:
- **Origem**: Definida automaticamente como `VENDA`.
- **Código da Origem**: Registra o número exato do documento de venda gerado pelo PDV (ex: Venda `881`).

Ao abrir os detalhes da OP, o sistema exibe de forma clara e analítica os impactos causados:

| Tipo do Item | Nome do Item | Quantidade Movimentada | Impacto no Estoque |
| :--- | :--- | :--- | :--- |
| **Produto Acabado** | Omelete | 1,000 UN | Entrada (Produção) / Saída (Venda) |
| **Insumo** | Ovo | 2,000 UN | Saída por Consumo Industrial |
| **Insumo** | Orégano Pacote | 1,000 PCT | Saída por Consumo Industrial |
| **Insumo** | Sal | 10,000 G | Saída por Consumo Industrial |

### Tela de Lote de Produção
No menu de **Lote de Produção**, o agrupamento das ordens geradas por aquela operação também estará disponível, mantendo a amarração estrita com o código de origem gerado no PDV, permitindo auditorias rápidas de rentabilidade e consumo de matéria-prima.
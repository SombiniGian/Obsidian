---
id: CASO-001
link: https://www.youtube.com/watch?v=NMpL_RqdEHg
setor: Suporte
modulo: Cadastro de Produtos e Pedido de Venda
tags: [erp, conversao-unidade, precificacao, pedido-venda, regras-de-negocio]
data_criacao: 2026-07-18
---

## Sumário
1. [[#1. Visão Geral e Regra de Negócio]]
2. [[#2. Pré-requisitos e Restrições de Módulo]]
3. [[#3. Configuração Analítica: Cadastro de Produto]]
4. [[#4. Execução Operacional: Pedido de Venda Padrão]]

### 1. Visão Geral e Regra de Negócio

Esta documentação detalha a engenharia de precificação necessária para permitir a venda de uma embalagem agregada (como caixas ou fardos) aplicando o desconto e a negociação diretamente no **preço unitário** (ou preço de volume), ao invés de lançar o desconto apenas sobre o valor finalizado da caixa.

> [!info] Contexto Operacional
> Em transações comerciais, especialmente com perfil atacadista ou industrial, o acordo comercial frequentemente é fixado no valor da fração.
> **Exemplo Prático:**
> - Produto X: R$ 1,00/unidade.
> - Caixa Padrão (20 unidades): R$ 20,00.
> - **Cenário:** O cliente compra 10 caixas e o vendedor fecha o custo unitário em R$ 0,50. O sistema deve ser capaz de aceitar a entrada de "R$ 0,50" por unidade e recalcular automaticamente a caixa para R$ 10,00, mantendo a integridade fiscal e estatística da venda.

### 2. Pré-requisitos e Restrições de Módulo

> [!warning] Atenção: Limitação de Escopo Arquitetural
> Este fluxo de conversão avançada e recálculo condicional de volumes é suportado **exclusivamente** no módulo de **[[Pedido de Venda Padrão]]** (usado no backoffice ou retaguarda). 
> Este recurso de fracionamento de valor em tempo real **não é suportado** na interface de **[[PDV]]** (Frente de Caixa), a qual exige a emissão pelo valor fechado.

### 3. Configuração Analítica: Cadastro de Produto

Para que o motor de cálculo do pedido interprete as matrizes de conversão corretamente e ative o campo de valor por volume, o _setup_ do produto exige regras específicas.

1. Acesse o **Cadastro do Produto** e navegue até a aba de **Conversão de Unidades**.
2. Crie ou selecione a unidade secundária (ex: selecionando "Caixa").
3. Defina a quantidade associada na conversão (ex: preencher com **20**).
4. **Passo Crítico:** No campo **Volume**, você deve obrigatoriamente preencher com a mesma quantidade do fator de conversão (neste caso, **20**). O ERP expõe esse dado no faturamento para descobrir a cota de cálculo interno de cada peça dentro da caixa.
5. Deixe o campo **Preço de Venda** da aba de conversão **em branco**.

> [!tip] Dica de Motor de Precificação
> Quando o campo **Preço de Venda** dentro da matriz de conversão é deixado vazio, força-se um _fallback_ seguro no sistema. O motor de cálculo fará o _fetch_ automático do preço unitário padrão no cadastro principal e fará a multiplicação dinâmica pelo fator da conversão. Isso reduz manutenção redundante de tabelas de preços.

### 4. Execução Operacional: Pedido de Venda Padrão

Uma vez parametrizada a conversão atrelada a volumes, a interface do pedido libera as opções de reengenharia de valor no ato da inclusão do item.

1. Abra a tela de **Pedido de Venda Padrão** e inicie o preenchimento do cabeçalho.
2. Na aba de produtos, clique em **Incluir Item**.
3. Localize o produto configurado.
4. Ao chegar no campo de unidade de medida, altere para a conversão parametrizada (ex: **Caixa**).
   - *Comportamento Esperado do Sistema:* O ERP multiplicará o volume (20) pelo preço base (R$ 1,00) e travará o preço da caixa temporariamente em R$ 20,00.
5. Na parte inferior da janela de inclusão de itens, verifique o surgimento do sub-painel de Volumes apontando a proporção de 20 para 1.
6. Edite o campo **Preço do Volume** informando o novo valor negociado na unidade (neste exemplo, de R$ 1,00 para **R$ 0,50**).
   - *Comportamento Esperado do Sistema:* A aplicação processará a lógica reversa, multiplicando os 20 volumes pelo novo unitário estipulado (R$ 0,50) e alterando o preço macro da Caixa de forma silenciosa para **R$ 10,00**.
7. Informe a quantidade final de caixas para o pedido (ex: 10).
8. Clique em **Salvar** o item.

> [!warning] Falsos Positivos no Recálculo
> Caso você observe inconsistências marginais no preço final da caixa (ex: batendo R$ 9,80 ao invés dos R$ 10,00 previstos), verifique a **Forma de Pagamento** alocada no cabeçalho do pedido. Se o pedido estiver configurado em **Dinheiro** ou outra modalidade atrelada a regras de descontos sistêmicos globais pré-configurados, o sistema injetará esse desconto no cálculo do item de forma cumulativa.
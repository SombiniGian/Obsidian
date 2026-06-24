---
id: CASO-026
link: https://www.youtube.com/watch?v=J53MXVqSt9U&t=68s
setor: Compras, Comercial, Retaguarda
modulo: Precificação e Custos
tags:
  - precificacao
  - margem-lucro
  - markup
  - custo-produto
  - produtos-ligados
  - upsystem
data_criacao: 2026-06-24
---

# Central de Precificação de Produtos

Este documento técnico descreve o funcionamento e as diretrizes operacionais da tela **Central de Precificação de Produtos** no sistema [[UpSystem]]. Esta ferramenta isola e centraliza o processo de análise de custos e atualização de preços de venda, eliminando a necessidade de gerenciar essas alterações individualmente dentro de cada nota fiscal de entrada ou pedido de compra.

---

## Sumário
1. [[#1. Conceito e Separação de Papéis]]
2. [[#2. Regras de Cores e Alertas de Status]]
3. [[#3. Filtros Avançados de Margem e Custos]]
4. [[#4. Métodos de Atualização de Preço]]
5. [[#5. Gestão de Produtos com Preços Ligados (Subgrupos)]]

---

## 1. Conceito e Separação de Papéis

Anteriormente, o cálculo do custo e a definição do preço de venda ocorriam obrigatoriamente de forma interna no lançamento da nota fiscal de entrada ou do pedido de compra `[00:00:25]`. 

A **Central de Precificação** (localizada no menu **Movimentações > Compras > Precificação de Produtos**) atua de forma externa `[00:00:07]`. Esta arquitetura resolve o conflito operacional em empresas onde o colaborador responsável pelo recebimento/lançamento físico da nota fiscal não possui alçada ou competência comercial para definir as margens de lucro e preços de venda da empresa `[00:01:05]`.

---

## 2. Regras de Cores e Alertas de Status

O grid da ferramenta conta com indicadores visuais baseados nas parametrizações de markup e margens de contribuição `[00:01:32]`:

### Alertas de Markup / Preço de Venda `[00:01:32]`
* <span style="color:red; font-weight:bold;">Vermelho:</span> Preço de venda praticado está **abaixo do limite mínimo** tolerável para a rentabilidade do item `[00:01:42]`.
* <span style="color:yellow; background-color:black; font-weight:bold;">&nbsp;Amarelo&nbsp;</span> Preço de venda está em um nível **razoável** (entre o limite mínimo e o máximo estipulado) `[00:01:32]`.
* <span style="color:green; font-weight:bold;">Verde / Status Normal:</span> Preço de venda está acima do mínimo, garantindo uma boa margem de lucro `[00:01:52]`.

### Alertas de Tendência de Custo `[00:01:52]`
O sistema compara o custo da última entrada contra o custo histórico armazenado, identificando dinamicamente se o **Custo Novo** é maior, menor ou igual ao custo anterior `[00:01:52]`.

---

## 3. Filtros Avançados de Margem e Custos

Para otimizar o tempo do gestor comercial, o grid personalizável permite criar filtros focados na recuperação de margem perdida `[00:01:18]`.

> [!tip] Filtro de Alerta de Defasagem (Preço Inalterado com Custo em Alta) `[00:02:16]`
> Para localizar produtos que perderam margem de lucro devido a reajustes de fornecedores, aplique a seguinte combinação de filtros no topo do grid:
> 1. **Preço de Venda Novo** = `Igual ao Preço de Venda Anterior` (indica que o preço ainda não foi reajustado na tabela vigente) `[00:02:16]`.
> 2. **Tendência de Custo** = `Custo Maior` (isola apenas os itens que sofreram aumento de custo na última compra) `[00:02:31]`.
> 
> *Resultado:* O sistema listará na tela todos os produtos que estão com o preço defasado e necessitam de correção imediata para não gerar prejuízo operacional `[00:02:42]`.

---

## 4. Métodos de Atualização de Preço

A alteração do preço de venda pode ser executada por três métodos distintos dentro da central:

1. **Alteração Manual Direta:** O usuário digita o novo valor diretamente na célula correspondente no grid `[00:03:13]`. O status da linha é alterado para **"Preço Alterado"** `[00:03:37]`.
2. **Aplicação do Preço Sugerido em Lote:** Selecionando múltiplos produtos, o operador pode clicar em **Aplicar Sugerido** `[00:03:46]`. O sistema realiza o cálculo automático:
   $$\text{Preço Sugerido} = \text{Custo Novo} \times \text{Markup Desejado}$$
   O valor resultante é preenchido na coluna de preço novo e o status muda para **"Sugerido"** `[00:03:29]`.
3. **Composição por Margem de Contribuição:** Indicado para empresas que precificam com base no índice de margem de contribuição em substituição ao markup tradicional (detalhado em documentação complementar) `[00:04:09]`.

> [!info] Consulta de Promoções Ativas `[00:04:33]`
> Caso um item apresente comportamento divergente de preço, o gestor pode dar um duplo clique ou acionar a opção de abrir o cadastro do produto diretamente pela tela para avaliar regras especiais, como **Promoções por Quantidade** ativas `[00:04:41]`.

---

## 5. Gestão de Produtos com Preços Ligados (Subgrupos)

O sistema possui uma trava de segurança para produtos que pertencem a subgrupos configurados com **Preço de Ligação** `[00:04:50]`. Esta regra é comumente utilizada para produtos que possuem variações (ex: sabores, cores ou aromas diferentes) mas que comercialmente precisam manter rigorosamente o mesmo preço de venda.

[ Central de Precificação ] 
│ (Tenta reajustar)
│
▼ 
[ Produto Pertence a Subgrupo Ligado? ] 
			/ \ (Sim)  (Não) /
\ [ TRAVA DE SEGURANÇA ] [ Permite Alteração ]
* **Comportamento de Bloqueio:** Se o operador tentar alterar o preço novo diretamente na linha de um item ligado, o sistema exibirá uma mensagem de bloqueio informando que o produto não permite reajuste isolado `[00:05:35]`. * **Procedimento Correto de Ajuste:** 1. Identifique a coluna indicadora de subgrupo de ligação no grid. 2. Clique no botão **Abrir Ligação** (ou abrir subgrupo) `[00:05:59]`. 3. Uma janela auxiliar exibirá todos os itens que compõem aquela família vinculada `[00:06:08]`. 4. Informe o novo valor unificado no campo de ajuste superior (ex: R$ 50,00) e clique em aplicar `[00:06:15]`. 5. O sistema replicará o novo preço de venda simultaneamente para todos os produtos associados ao subgrupo de ligação, mantendo a integridade comercial da tabela `[00:06:26]`.
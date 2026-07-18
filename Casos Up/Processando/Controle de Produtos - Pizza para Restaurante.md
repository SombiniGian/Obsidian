---
id: CASO-001
link: https://www.youtube.com/watch?v=CqmDR_S98Lc
setor: Suporte
modulo: Produtos e Restaurante
tags: [pizza, insumos, ordem-de-producao, pdv, composicao-de-preco]
data_criacao: 2026-07-18
---

## Sumário
- [[#Visão Geral e Propósito]]
- [[#Cadastro de Sabores e Estrutura do Produto]]
- [[#Regras de Composição de Preço]]
- [[#Gestão de Insumos e Baixa Proporcional]]
- [[#Configuração de Complementos (Massas e Bordas)]]
- [[#Fluxo de Venda e Ordem de Produção]]

## Visão Geral e Propósito

O módulo de controle de pizzas introduz uma nova camada de complexidade para a gestão de produtos compostos e fracionados dentro do sistema. Embora tenha sido arquitetado com foco em pizzarias (controle de tamanhos, pedaços, múltiplos sabores e bordas), a sua estrutura lógica permite que seja utilizado para outros tipos de produtos.

> [!tip] Aplicabilidade Estendida
> A mecânica de sabores pode ser aplicada a produtos que não são pizzas, como pastéis (ex: pastel de carne, queijo, camarão). Nesses casos, o produto é configurado para ter apenas 1 pedaço e limite de 1 sabor, permitindo que o cliente utilize a mesma interface de seleção de sabores e formação de preços sem precisar de cadastros duplicados.

A propriedade (flag) de **Pizza** no cadastro do produto possui, no momento, efeito puramente informativo. Ela é útil para filtros em relatórios internos e será uma chave fundamental para futuras integrações de cardápio com plataformas de delivery (como o iFood), mas não altera o comportamento de cálculo do faturamento se ativada ou desativada.

## Cadastro de Sabores e Estrutura do Produto

A arquitetura do cadastro foi dividida para evitar redundâncias no banco de dados e facilitar a manutenção. O usuário não deve cadastrar "Pizza Grande de Calabresa" como um produto único, mas sim separar o conceito de "Tamanho Base" do conceito de "Sabor".

### 1. Cadastro Base de Sabores
Os sabores disponíveis no estabelecimento são cadastrados globalmente, ficando disponíveis para vinculação posterior.
- **Caminho:** **Outros produtos** > **Sabores**
- **Campos principais:** Descrição, Status (Ativar/Inativar) e Foto.

### 2. Vinculação ao Produto Principal (Tamanhos)
Os produtos finais faturáveis devem representar os *Tamanhos* (ex: Pizza Grande, Pizza Média). 
- **Caminho:** **Cadastro de Produto** > Aba **Restaurante**
- Dentro desta aba, define-se a quantidade total de pedaços daquele tamanho (ex: Pizza Grande = 8 pedaços) e o limite máximo de sabores permitidos por montagem (ex: máximo de 2 ou 4 sabores).
- Os sabores globais são então incluídos na lista específica deste produto. É possível definir a **ordem** de exibição de cada sabor na interface do [[PDV Touch]]; caso seja deixada em branco, o sistema os apresentará em ordem alfabética.

## Regras de Composição de Preço

A precificação de produtos com múltiplos sabores é uma das regras de negócio centrais, gerenciada diretamente na tela de vinculação do sabor ao tamanho da pizza.

O sistema permite duas abordagens principais para calcular o valor final de uma pizza fracionada (ex: meio a meio):
1. **Maior Preço:** O valor final da pizza inteira será igual ao valor do sabor mais caro escolhido na composição.
2. **Soma dos Pedaços (Proporcional):** O sistema calcula a fração do valor de cada sabor e realiza a soma exata (ex: 50% do valor da calabresa + 50% do valor do bacon).

> [!warning] Comportamento de Preço Zerado no Sabor
> Ao adicionar um sabor na aba **Restaurante**, se o campo de preço for deixado como `0,00`, o sistema assumirá dinamicamente o **Preço de Venda** configurado nos dados principais do produto. (Exemplo: se a Pizza Grande base custa R$ 55,00, todos os sabores vinculados com preço zerado herdarão o valor de R$ 55,00).

## Gestão de Insumos e Baixa Proporcional

O controle rigoroso de estoque para produtos montados (fichas técnicas dinâmicas) é assegurado através da distinção arquitetural entre **Insumos Globais** e **Insumos Específicos do Sabor**.

### Insumos Globais (Base do Produto)
São os ingredientes consumidos independentemente do sabor escolhido. Devem ser cadastrados diretamente na raiz do produto principal.
- *Exemplo de Uso:* Toda Pizza Grande consome `1 Unidade de Massa Base` e `300g de Queijo Muçarela`. Independentemente de a pizza ser de Calabresa ou Portuguesa, o sistema fará a baixa dessas quantidades.

### Insumos Específicos (Por Sabor)
São configurados selecionando o sabor específico e clicando em **Incluir Insumo** dentro da aba **Restaurante**. As quantidades informadas aqui devem representar o consumo caso a pizza fosse 100% daquele sabor.
- *Exemplo de Uso:* O sabor Calabresa consome `100g de Calabresa Fatiada`. O sabor Bacon consome `100g de Bacon em Cubos`.

> [!info] Mecanismo de Baixa Proporcional
> O principal diferencial da engine de baixa de estoque é o cálculo fracionado automático. Se um cliente pede uma pizza Grande de 2 sabores (Meia Calabresa, Meio Bacon), o sistema divide o consumo do insumo específico pela proporção do sabor. Ao invés de baixar 100g de cada, a transação registrará a saída de **50g de Calabresa** e **50g de Bacon**, mantendo a baixa integral dos insumos globais (1 Massa, 300g Queijo).

## Configuração de Complementos (Massas e Bordas)

Para lidar com opcionais e variações construtivas obrigatórias (sem poluir a lista de sabores ou o cadastro de produtos), o módulo reutiliza a estrutura do `[[Grupo de Complementos]]`.

1. **Criação do Grupo:** Cadastram-se agrupadores funcionais, como "Tipo de Massa" e "Bordas".
2. **Regras de Obrigatoriedade:** Configuram-se as travas de mínimo e máximo de itens. 
   - *Exemplo Prático:* No grupo "Massas", define-se Mínimo `1` e Máximo `1`. Isso força o operador do caixa a selecionar exatamente um tipo de massa para conseguir avançar a venda.
3. **Precificação Adicional:** Itens dentro do grupo podem ter custo zero (ex: "Massa Tradicional", "Sem Borda") ou agregar valor monetário ao montante final do produto (ex: "Borda de Catupiry + R$ 3,00").

## Fluxo de Venda e Ordem de Produção

### Operação no PDV Touch
1. O operador inicia o fluxo selecionando o tamanho desejado (ex: clicando no atalho **Pizza Grande**).
2. O sistema intercepta a venda e abre uma modal exigindo a composição dos sabores. A interface respeita a trava do limite máximo configurado (se o operador tentar incluir 3 sabores em uma pizza parametrizada para no máximo 2, a ação é bloqueada).
3. Após a definição das proporções, o sistema valida os `[[Grupo de Complementos]]` obrigatórios, forçando a seleção da borda e da massa.
4. O preço de venda é calculado em tempo real (baseado na diretriz de Maior Preço ou Soma dos Pedaços) e injetado no carrinho.

### Ordem de Produção (Lote de Produção)
Se o ambiente estiver parametrizado para gerar um `[[Lote de Produção]]` automaticamente mediante faturamento ou emissão de pedido, o processo ocorrerá em background silenciosamente.

Ao inspecionar a **Ordem de Produção** gerada, a ficha técnica explodida apresentará a receita consolidada. O documento descriminará visualmente as quantias fracionadas exatas de insumo que devem ser utilizadas pela cozinha e que sofreram baixa proporcional no módulo de estoques, garantindo precisão técnica entre o que foi vendido e o que deve ser produzido.
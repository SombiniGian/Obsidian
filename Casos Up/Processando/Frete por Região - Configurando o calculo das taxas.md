---
id: CASO-044
link: https://www.youtube.com/watch?v=g3zan5z8xZQ
setor: Suporte
modulo: Delivery / Força de Vendas
tags:
  - taxa-de-entrega
  - configuracao-frete
  - bairros
  - delivery
  - regras-de-negocio
data_criacao: 2026-06-24
---

# Configuração de Frete por Região e Matriz de Bairros

Este documento técnico descreve o funcionamento, a parametrização e as regras de fallback do motor de cálculo de taxas de entrega baseadas na regionalização de bairros no módulo de [[Delivery]] da UP Sistemas. A funcionalidade automatiza a atribuição de custos de frete na inicialização do pedido de venda com base no endereço cadastrado do cliente.

## Sumário
- [[#Visão Geral e Arquitetura do Cálculo]]
- [[#Parametrização do Sistema]]
- [[#Fluxo de Execução da Venda]]
- [[#Matriz de Contingência e Fallback]]
- [[#Pontos Críticos e Validações]]

---

## Visão Geral e Arquitetura do Cálculo

O cálculo de frete por região permite segmentar a área de cobertura do estabelecimento em polígonos lógicos (Regiões), onde cada região possui um valor de taxa fixo e uma lista de bairros vinculados. O sistema executa uma busca exata por string para determinar o custo de entrega no momento do lançamento do pedido.

![[Frete por Região - Configurando o calculo das taxas.png]]

Parametrização do Sistema Para o correto funcionamento do módulo, a configuração deve ser executada em duas etapas obrigatórias: a definição da taxa global de contingência e a modelagem das regiões de atendimento. 
 1. Configuração Global do Módulo Delivery 1. No menu de configurações do sistema de retaguarda, acesse as opções de **Configuração do Delivery**. 2. Localize o campo **Taxa de Entrega Padrão** (ou **Taxa de Entrega** geral da empresa). 3. Insira o valor base de frete (Ex: `4,00`). Este valor atuará como a última instância de cálculo caso o endereço do cliente não possua correspondência específica de bairro. 
 2. Cadastro e Estruturação das Regiões 1. Acesse o menu **Cadastros** > **Regiões** (ou módulo equivalente de zoneamento). 2. Clique em **Novo** para criar um agrupamento ou selecione uma região existente para **Alterar**. 3. Defina os seguintes campos fundamentais: * **Nome da Região:** Identificação amigável do setor (Ex: `Região Central`, `Zona Norte`). * **Valor/Taxa:** Custo monetário associado à entrega para as localidades desta região (Ex: `5,00` ou `7,00`). * **Lista de Bairros:** Campo de texto estruturado onde os nomes dos bairros devem ser digitados **um embaixo do outro**, utilizando estritamente a tecla `Enter` como caractere delimitador de quebra de linha. > 
 [!tip] Exemplo de Preenchimento da Lista de Bairros > ```text > Centro > São Bernardo > Vila Nova >

> Certifique-se de não inserir espaços em branco no início ou no fim das linhas e evite pontuações como vírgulas ou pontos-e-vírgulas ao final de cada bairro.

## Fluxo de Execução da Venda

Durante o atendimento no [[PDV Tradicional]] ou na fila de pedidos de delivery, o processo segue os seguintes passos operacionais:

1. O operador inicia o atendimento e faz a busca do cliente por telefone ou insere um novo registro.
    
2. Ao preencher ou carregar os dados de endereço do cliente, o sistema faz a validação do campo **Bairro**.
    
3. **Cenário A - Correspondência Regional 1:** O bairro identificado pertence à `Região Central` (Taxa: R$ 5,00). O sistema altera o status da venda e injeta o acréscimo de **R$ 5,00** à nota de forma automatizada.
    
4. **Cenário B - Correspondência Regional 2:** O bairro identificado pertence à região `Dornelas` (Taxa: R$ 7,00). O sistema altera a região interna e vincula a taxa de **R$ 7,00**.
    

## Matriz de Contingência e Fallback

Caso o cliente possua um bairro cadastrado que não esteja listado em nenhuma das regiões configuradas na retaguarda (Ex: bairro `João XXIII`), o comportamento esperado do sistema segue as seguintes prioridades:

1. O sistema faz a varredura completa nas listas de todas as regiões ativas.
    
2. Ao falhar em encontrar correspondência literal, o sistema **não bloqueia a venda** e **não zera a taxa**.
    
3. O motor de cálculo aciona o modo de fallback e recupera o valor parametrizado na **Taxa de Entrega Padrão** da empresa (Ex: **R$ 4,00**).
    
4. O valor padrão é aplicado ao subtotal do pedido de entrega para mitigar prejuízos operacionais com fretes não cobrados.
    

## Pontos Críticos e Validações

> [!warning] Sensibilidade a Erros de Digitação (Case Sensitivity e Acentuação) O mecanismo de busca de bairros realiza uma comparação de texto direta. Divergências de digitação entre o texto cadastrado na ficha do cliente e o texto inserido na lista da região quebrarão a automação.
> 
> - **Exemplo de falha:** Se na região estiver cadastrado `Sao Bernardo` (sem acento) e no cliente estiver `São Bernardo` (com acento), o sistema não correlacionará os registros e aplicará a taxa padrão de fallback de forma errônea.



---
id: CASO-UP-CONFIG-003
link: https://www.youtube.com/watch?v=8YTvz7S20Z8
setor: Suporte, Implantação, Comercial
modulo: Movimentações (Pedido de Venda)
tags:
  - up-system
  - pedido-de-venda
  - controle-estoque
  - formas-de-pagamento
  - integracao-tablet
  - auditoria
data_criacao: 2026-06-24
---

# Configurações e Operação do Módulo de Pedido de Venda

Este documento estabelece as diretrizes técnicas e operacionais para a emissão de Pedidos de Venda no ERP da Código UP Sistemas, cobrindo o comportamento dinâmico de filtros, validação cadastral de clientes, parametrização de formas de pagamento, regras de controle de estoque visual e logs de liberação financeira.

---

## Sumário
1. [[#1. Otimização de Performance e Filtros de Inicialização]]
2. [[#2. Regras de Negócio no Cabeçalho do Pedido]]
3. [[#3. Parametrização Dinâmica de Formas de Pagamento]]
4. [[#4. Engenharia de Itens e Indicadores Visuais de Estoque]]
5. [[#5. Mecanismo de Bloqueio, Liberação e Trilha de Auditoria]]
6. [[#6. Configurações Globais do Módulo]]

---

## 1. Otimização de Performance e Filtros de Inicialização

Diferente das telas de cadastros estáticos ([[Cadastro de Pessoas]] e [[Cadastro de Produtos]]), que carregam a totalidade dos registros do banco de dados, as telas de movimentações comerciais utilizam travas automáticas de performance.

### 1.1 Comportamento Padrão da Grade (*Grid*)
* **Carga Inicial Restrita:** Ao abrir a tela de Pedidos de Venda, o sistema renderiza por padrão apenas os registros com o status **Aberto** vinculados ao período vigente. Essa abordagem evita gargalos de memória à medida que o banco de dados cresce com o histórico de faturamento.
* **Filtros Avançados de Escopo:** A barra de ferramentas superior disponibiliza seletores para expandir a consulta: por intervalo de datas customizado, status específicos (Faturado, Cancelado, Bloqueado) ou por clientes/vendedores.
* **Pesquisa Global Localizada:** A caixa de pesquisa rápida opera exclusivamente sobre o conjunto de dados *já retornado pelo filtro ativo*. Para localizar um pedido antigo que não está visível, é obrigatório ajustar o filtro de data ou status antes de executar a busca.

---

## 2. Regras de Negócio no Cabeçalho do Pedido

A inicialização do documento comercial aciona gatilhos de herança de dados com base no cadastro do cliente selecionado.
[Seleção do Cliente] ──> [Gatilho de Herança] ──> [Preenchimento Automático] ├── Tabela de Preço ├── Vendedor Padrão ├── Forma de Pagamento └── Mensagem de Alerta (Pop-up)


### 2.1 Campos e Comportamentos Automatizados
* **Natureza de Operação (CFOP):** Assumida automaticamente conforme a parametrização padrão definida nos parâmetros gerais do sistema.
* **Origem da Movimentação:** O sistema diferencia pedidos originados internamente daqueles sincronizados via **Tablet/Força de Vendas**. Pedidos externos herdam o número identificador do dispositivo móvel no campo específico de controle de integração.
* **Mensagens de Alerta Cadastrais:** Se o cliente possuir informações críticas registradas no campo **Mensagem de Alerta** (ex: *"Apenas entrega após confirmação de PIX"* ou *"Restrição com o setor financeiro"*), o ERP interromperá o fluxo operacional exibindo um pop-up de bloqueio visual que exige a confirmação do operador para prosseguir.
* **Sincronização de Dados de Clientes:** Caso o operador modifique o cliente com o pedido em andamento, o sistema disparará uma validação interativa questionando se deseja atualizar a tabela de preços, os descontos e as condições de pagamento em conformidade com as diretrizes do novo cliente selecionado.

---

## 3. Parametrização Dinâmica de Formas de Pagamento

O sistema permite criar condições comerciais em tempo de execução sem a necessidade de fechar a tela corrente, utilizando o botão **"+" (Inclusão Rápida)** posicionado ao lado do seletor da forma de pagamento.

### 3.1 Regras de Validação das Formas de Pagamento
* **Vencimento Interno vs. Emissão Fiscal:** Permite parametrizar se o fluxo financeiro gerará parcelas a prazo (ex: 30 dias) enquanto a Nota Fiscal correspondente é emitida com a modalidade à vista (conforme exigências de regras fiscais específicas).
* **Filtro por Tipo de Documento:** Condiciona quais carteiras financeiras (Dinheiro, Cheque, Boleto, Cartão) são válidas para aquela condição. Apenas os documentos configurados como "A Prazo" no sistema serão elegíveis para parcelamento.
* **Restrições para Força de Vendas (Tablet):** É possível definir um **Valor Mínimo** por parcela ou pedido para que a condição seja exibida nos dispositivos móveis (ex: a condição *Boleto 30 Dias* só fica visível no tablet para pedidos acima de R$ 200,00).

### 3.2 Despesas Acessórias e Trava de Segurança
* **Taxas de Administração / Cobrança:** Permite embutir despesas acessórias (como taxa de emissão de boleto) de forma automática caso o pedido não atinja um determinado valor limite de corte (ex: cobrar taxa de R$ 3,00 se o pedido for inferior a R$ 300,00).
* **Segurança de Modificação:** Flags de controle que determinam se o usuário final possui permissão para aplicar acréscimos ou descontos adicionais manualmente sobre a tabela de preços vigente ao utilizar a respectiva forma de pagamento.

---

## 4. Engenharia de Itens e Indicadores Visuais de Estoque

A grade de inclusão de itens conta com inteligência de cores em tempo real na coluna **Quantidade**, fornecendo cenários de tomada de decisão imediata ao vendedor sobre a disponibilidade física das mercadorias.

### 4.1 Matriz de Cores de Disponibilidade de Estoque

| Cor Indicadora | Cenário Operacional | Impacto no Faturamento |
| :--- | :--- | :--- |
| <font color="green">**Verde**</font> | **Estoque Disponível Total** | Quantidade solicitada está integralmente livre no estoque físico e sem reservas de outros pedidos. |
| <font color="yellow">**Amarelo**</font> | **Estoque Comprometido / Reservado** | Existe saldo físico na empresa para atender ao volume, porém a mercadoria já se encontra empenhada ou reservada para outros pedidos pendentes de faturamento. O operador precisará priorizar qual venda será atendida. |
| <font color="red">**Vermelho**</font> | **Estoque Insuficiente / Negativo** | O saldo em estoque físico é nulo ou menor do que a quantidade digitada. O bloqueio depende da configuração global do sistema de permitir ou não estoque negativo. |

> [!tip] Customização do Grid de Itens
> Utilizando os recursos de engenharia de visualização de grades do sistema, é recomendável arrastar as colunas **Estoque Depósito**, **Estoque Reservado** e **Estoque Disponível** para posições adjacentes à coluna **Quantidade**, executando o clique com botão direito e acionando **Salvar Grade** para consolidar essa disposição.

### 4.2 Conta Corrente de Descontos e Saldo Flex
O sistema monitora a relação comercial entre acréscimos e descontos item a item através do conceito de **Saldo Flex** do vendedor. Se um item recebe 10% de desconto e outro recebe um acréscimo de valor que sobrepuje o abatimento anterior, o saldo da operação é balanceado positivamente, registrando o histórico na composição financeira do documento.

---

## 5. Mecanismo de Bloqueio, Liberação e Trilha de Auditoria

Ao finalizar a inserção de itens e tentar salvar o pedido, o ERP executa rotinas de consistência financeira periféricas baseadas na saúde financeira do cliente.

```

[Salvar Pedido] ──> [Validação Financeira] ──> [Bloqueio por Inadimplência] └── Exige Senha de Liberação (Supervisor)

````

### 5.1 Bloqueio Automático por Inadimplência
* Se o cliente possuir títulos com parcelas vencidas em aberto no módulo [[Financeiro]], o pedido será gravado obrigatoriamente com o status **Bloqueado**.
* O desbloqueio exige uma intervenção administrativa (Inserção de **Senha de Liberação** de nível supervisor ou superior).

### 5.2 Rastreabilidade e Auditoria Histórica de Liberações
Uma vez efetuada a liberação do pedido por senha, o sistema grava de forma imutável nos logs do documento:
* Identificação do usuário responsável pela liberação (Supervisor).
* O timestamp exato (Data e Hora) da concessão da autorização.
* O motivo originário do travamento (ex: *Cliente com títulos vencidos*).
* Histórico de recalque de impostos e preços resultantes de trocas de formas de pagamento após a abertura inicial do pedido.

> [!warning] Consistência de Dados em Recálculos
> Se houver alteração posterior na forma de pagamento que conceda descontos automáticos parametrizados, o usuário deve acionar a função **Recalcular Pedido**. Esse comando recalcula as tabelas de preços e zera distorções no Saldo Flex, registrando o evento na aba de **Auditoria**.

---

## 6. Configurações Globais do Módulo

O comportamento operacional do formulário de pedidos é regido por uma tela de parâmetros gerais avançados.

```ini
[Configuracoes_Pedidos]
Bloquear_Estoque_Negativo = True
Permitir_Alterar_Valor_Unitario = False
Bloquear_Inadimplentes = True
Percentual_Desconto_Maximo = 15.00
Percentual_Acrescimo_Padrao = 0.00
Caminho_Template_Impressao = "C:\Sistemas\UP\Templates\PedidoVenda.frx"
````

### 6.1 Principais Parâmetros de Controle

- **Bloquear Estoque Negativo:** Impede a gravação do pedido caso o item esteja sinalizado na cor vermelha.
    
- **Mudar Valor Unitário:** Define se o vendedor tem autonomia para sobrescrever o preço de tabela do produto na inclusão do item.
    
- **Desconto Máximo / Acréscimo Padrão:** Tetos operacionais de flexibilização de preços por perfil de usuário.
    
- **Caminho do Arquivo de Impressão:** Apontamento do diretório de rede contendo o layout customizado do relatório do pedido utilizado para conferência e logística.
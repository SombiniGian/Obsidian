---
id: [CASO-001]
link: https://www.youtube.com/watch?v=dBfezWDDObQ
setor: Suprimentos
modulo: Cotação de Compra
tags: [cotação, compras, fornecedores, automatização, suprimentos]
data_criacao: 2026-07-18
---

# Documentação Técnica: Módulo de Cotação de Compra

## Sumário
1. [Visão Geral do Módulo](#visão-geral-do-módulo)
2. [Pré-requisitos e Configurações](#pré-requisitos-e-configurações)
3. [Fluxo Operacional de Cotação](#fluxo-operacional-de-cotação)
   - [3.1. Inclusão de Produtos](#31-inclusão-de-produtos)
   - [3.2. Vinculação de Fornecedores](#32-vinculação-de-fornecedores)
   - [3.3. Geração e Envio de Planilhas](#33-geração-e-envio-de-planilhas)
   - [3.4. Retorno e Importação de Dados](#34-retorno-e-importação-de-dados)
   - [3.5. Apuração de Vencedores](#35-apuração-de-vencedores)
4. [Finalização e Integração](#finalização-e-integração)

---

## Visão Geral do Módulo

O módulo de **Cotação de Compra** foi projetado para otimizar o processo de aquisição de mercadorias quando a empresa possui múltiplos fornecedores para os mesmos produtos. O sistema automatiza a pesquisa de preços, prazos de entrega e condições de pagamento por meio da exportação e importação de planilhas padronizadas, culminando na geração automática de um ou mais `[[Pedido de Compra]]`.

> [!info] Propósito
> Reduzir o tempo de análise de propostas comerciais e garantir a compra baseada em critérios lógicos (melhor preço, menor prazo de entrega ou melhor prazo de pagamento).

---

## Pré-requisitos e Configurações

Antes de iniciar uma nova cotação, a tela de configuração do módulo exige a parametrização de variáveis globais que ditarão o comportamento padrão do sistema durante o fluxo.

* **Dias de Prazo de Resposta:** Define o *lead time* da cotação. Adiciona um número X de dias à data atual para estabelecer a data limite de retorno do fornecedor.
* **Diretório de Planilhas:** Caminho de rede ou disco local onde o sistema salvará os arquivos Excel gerados.
* **Critério de Desempate/Escolha Padrão:** Define a métrica inicial de apuração (ex: *Melhor Preço*, *Melhor Data de Entrega*, *Melhor Prazo de Pagamento*).
* **Templates de Comunicação:** Assunto e corpo de mensagem padrão utilizados no disparo de e-mails para os fornecedores.

> [!warning] Atenção: Cadastro de Fornecedores
> Para que a funcionalidade de envio direto por e-mail funcione, os registros no módulo de `[[Cadastro de Fornecedor]]` devem possuir endereços de e-mail válidos previamente preenchidos.

---

## Fluxo Operacional de Cotação

O fluxo de cotação é contínuo e dividido em etapas de alimentação de dados, comunicação externa e validação sistêmica.

### 3.1. Inclusão de Produtos

A primeira etapa consiste em definir o escopo da cotação, listando os produtos desejados. 
O sistema permite duas abordagens:
1. **Inclusão Manual:** O usuário digita o código ou a descrição do item e a quantidade desejada.
2. **Importação Inteligente:** Utilização da ferramenta de `[[Sugestão de Compra]]`.

> [!tip] Dica de Automação
> A ferramenta de **Sugestão de Compra** pode analisar o histórico de vendas (ex: últimos 3 meses), cruzar com o estoque mínimo e calcular margens, importando em lote todos os produtos que necessitam de reposição para dentro da cotação em um único clique.

### 3.2. Vinculação de Fornecedores

Após a definição da lista de produtos, o usuário deve incluir os parceiros comerciais que participarão da concorrência. É possível lançar propostas internamente (manualmente) caso o fornecedor passe os valores por telefone, mas o fluxo sistêmico ideal envolve a comunicação e automação via planilhas.

### 3.3. Geração e Envio de Planilhas

Com produtos e fornecedores definidos, o sistema consolida os dados e prepara a comunicação.

1. Clique no botão **Gerar Planilha**.
2. O sistema criará arquivos em Excel individuais para cada fornecedor salvo no diretório configurado.
3. Utilize a função **Enviar Planilha** para disparar o arquivo via **E-mail** ou **WhatsApp** diretamente da interface do ERP.
4. O status de envio é atualizado na interface visual (marcando como enviado).

### 3.4. Retorno e Importação de Dados

O fornecedor receberá o arquivo, o preencherá com os valores de proposta e o devolverá para a empresa. A arquitetura da planilha enviada possui regras estritas de proteção e edição.

> [!warning] Ponto Crítico de Falha (Estrutura da Planilha)
> A planilha enviada possui células bloqueadas estruturalmente e células de edição liberadas (identificadas pela cor rosê, exclusivas para Preço, Prazo de Entrega, Prazo de Pagamento e Observações). **O fornecedor não pode adicionar ou excluir colunas/linhas**, pois qualquer quebra de estrutura corromperá o *parser* de importação do sistema, gerando erro de leitura.

Ao receber o retorno do fornecedor:
1. Salve a planilha preenchida recebida.
2. No sistema, selecione o fornecedor correspondente.
3. Clique em **Importar** e aponte para o arquivo devolvido.
4. O sistema lerá e preencherá automaticamente as propostas e valores para os respectivos produtos.

**Indicadores Visuais de Proposta (Interface):**
* ⚪ **Bolinha Cinza:** Indica que o produto possui uma ou mais propostas lançadas, mas ainda não tem um vencedor definido.
* 🔵 **Bolinha Azul:** Indica que o produto já possui uma proposta vencedora apurada.

### 3.5. Apuração de Vencedores

Com todas as propostas importadas, a guia **Vencedores** é utilizada para cruzar os dados analiticamente.

O usuário aplica um filtro global (ex: selecionando o critério *Menor Preço*). O *engine* do sistema varre as propostas da cotação e atribui o status de vencedor (Bolinha Azul) para o fornecedor que obteve a melhor métrica competitiva em cada item individualmente.

**Exceções e Ajustes Manuais:**
* É possível forçar a vitória de um fornecedor específico. O usuário seleciona o fornecedor na tela de apuração e confirma, ignorando temporariamente a métrica de preço em virtude de fatores externos (ex: confiabilidade, necessidade de entrega imediata).
* Produtos deixados em branco (sem proposta) por determinados fornecedores são ignorados pelo algoritmo de comparação.

---

## Finalização e Integração

Após a conferência e decisão dos vencedores item a item, o processo de cotação deve ser encerrado para dar andamento logístico.

1. Clique no botão **Finalizar**.
2. O sistema executará uma rotina de quebra e agrupamento por fornecedor (*split and group*).
3. Serão gerados automaticamente documentos consolidados no módulo de `[[Pedido de Compra]]`.

> [!info] Regra de Negócio de Finalização
> Se três fornecedores diferentes venceram partes fracionadas de uma mesma cotação, o sistema não gera um único documento misto. A arquitetura processa o resultado e gera **três Pedidos de Compra distintos**, vinculados aos seus respectivos CNPJs e contendo estritamente os produtos e condições em que cada um foi vitorioso.
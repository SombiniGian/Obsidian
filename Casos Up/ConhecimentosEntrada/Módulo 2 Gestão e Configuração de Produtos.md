O módulo de produtos estrutura o core operacional e fiscal do sistema, suportando configurações multiempresa e regras de negócio específicas para diferentes verticais de varejo, indústria e food service.

---

## 1. Arquitetura do Cadastro e Multiempresa

O cadastro de itens foi projetado para atuar em instâncias únicas ou de múltiplas filiais que compartilham a mesma base de dados.
*   **Visibilidade Multiempresa:** É possível associar um produto a uma empresa específica ou deixá-lo com o campo empresa "em branco", tornando-o visível globalmente para todas as instâncias operacionais.
*   **Tabelas de Preços por Empresa:** O sistema permite definir tabelas de precificação distintas para o mesmo produto, dependendo da filial que está efetuando a venda.
*   **Descrições de Integração:** Há campos distintos para a **Descrição** interna do ERP e a **Descrição Resumida**, otimizada para integrações com e-commerce e catálogos virtuais.

---

## 2. Controle de Estoque Dual

A arquitetura do ERP separa as lógicas de armazenagem e trânsito fiscal através de dois controles paralelos:
*   **Estoque Inventariado (Físico):** Refere-se à contagem real de itens presentes nas gôndolas, prateleiras e depósitos da empresa.
*   **Estoque Contábil (De Papel):** Reflete a movimentação gerada estritamente pela emissão de documentos fiscais eletrônicos. Permite ajustes logísticos em notas fiscais de devolução de compra operando separadamente do giro físico.

---

## 3. Conversão de Unidades de Medida

O controle dimensional e quantitativo exige que o produto principal seja sempre cadastrado com a **menor unidade possível para venda e controle de estoque** (ex: unidade, lata, metro).
*   **Fatores de Multiplicação/Divisão:** É possível cadastrar infinitas conversões na aba secundária (ex: *Caixa com 12*, *Fardo com 48*), informando o fator de conversão de estoque.
*   **Bloqueio Operacional:** Na conversão, parametriza-se se aquela unidade específica está disponível para uso na venda, apenas para compra, ou ambas. Exemplo: um material de construção pode forçar a venda exclusiva de caixas fechadas, ignorando a fração.

---

## 4. Engenharia de Produtos: Composições e Desmembramentos

Para setores de transformação, alimentação e açougues, o sistema gerencia transformações de insumos em tempo real:
*   **Ficha Técnica (Produtos Produzidos):** Estrutura lógica de produção onde o produto final (ex: hambúrguer, camisa) consome insumos diretos (pão, tecido, botões) do estoque. O sistema pode processar a baixa automática de insumos no fechamento da venda ou via geração de Ordem de Produção (OP).
*   **Produtos Desmembráveis:** Processo reverso. Utilizado quando um macro-produto de entrada gera submúltiplos para venda. Exemplo: A nota fiscal de entrada registra uma carcaça de boi, e a rotina de produção converte o peso total em percentuais predefinidos de cortes específicos (picanha, alcatra) repassando os custos.

---

## 5. Rastreabilidade: Lotes, Validades e Quarentena

Módulo essencial para indústrias, comércio de eletrônicos e manipulação de químicos:
*   **Controle de Lote na Entrada/Saída:** Exige o apontamento (manual ou via bipe) do lote ou código de serialização (ex: número de IMEI de celulares) no ato do recebimento do XML e no momento do faturamento no PDV.
*   **Status de Quarentena:** Bloqueia temporariamente um insumo recém-recebido, impedindo seu consumo na fábrica/cozinha até que uma análise laboratorial libere o lote no sistema.

---

## 6. Inteligência de Vendas e Setores de Impressão

*   **Produtos Similares:** Ferramenta de *cross-selling* e substituição de itens (comum em autopeças). O relacionamento de similaridade no banco de dados gera uma teia automática: ao amarrar a peça "A" à peça "B", e a "B" à "C", o sistema auto-vincula a "C" à "A". O PDV sugere as alternativas automaticamente na ruptura de estoque.
*   **Configuração de Restaurante:** Alterar o tipo de produto para "Restaurante" injeta componentes específicos na interface:
    *   **Complementos:** Gestão de acréscimos com custo adicional ou retiradas de ingredientes.
    *   **Sabores:** Tratamento de fracionamento de preços (ex: Pizza 1/2 a 1/2 cobrando pela média ou maior valor).
    *   **Roteamento de Produção:** Vincula o produto a um **Setor** (Bar, Cozinha Quente). Os itens do mesmo pedido são desmembrados nas impressoras corretas (priorizando a impressora vinculada ao Vendedor/Garçom, se existir).

---

## 7. Particularidades Fiscais e Código Fiscal (SPED)

*   **Identificador Fiscal:** O campo **Código Fiscal** não deve ser confundido com a chave primária (ID) ou código de barras. Ele é a `String` transmitida na tag `<cProd>` do XML da NF-e.
*   **Atenção Crítica em Migrações de Dados:** Alterar este código indevidamente ou utilizar IDs sequenciais durante a troca de um sistema antigo pelo novo gera inconsistência grave no Bloco K e no inventário do SPED. O fisco interpretará como omissão de estoque antigo e entrada não documentada de itens novos.
*   **Regras Específicas:** Tipos como **Armas de Fogo**, **Veículos** e **Medicamentos** forçam a abertura de abas exclusivas. Remédios exigem a inserção do número de registro da ANVISA e obrigatoriedade de receituário vinculado ao CPF do comprador (cenário rotineiro em Pet Shops).
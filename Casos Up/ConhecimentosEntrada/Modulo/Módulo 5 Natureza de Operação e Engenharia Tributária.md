A **Natureza de Operação** é a entidade central que orquestra o comportamento fiscal, financeiro e logístico de todas as movimentações do ERP (vendas, compras, devoluções e transferências).

---

## 1. Comportamento Base da Operação

Cada Natureza de Operação define regras binárias e condicionais que impactam diretamente os módulos paralelos do sistema:

*   **Movimentação de Estoque:** Define se a operação exige o incremento ou o abatimento de saldos de estoque (físico ou contábil).
*   **Geração Financeira:** Determina se o processamento da movimentação irá gerar títulos no **Contas a Receber** (saídas) ou **Contas a Pagar** (entradas).
*   **Acionamento de Ordem de Produção (OP):** Permite configurar se a conclusão de uma venda específica deve automatizar a baixa de insumos vinculados à ficha técnica do produto acabado.
*   **Base de Precificação:** Define a origem de valor da transação (ex: usar *Preço de Venda* para faturamento padrão ou *Preço de Custo* para emissão de notas fiscais de devolução).

---

## 2. Automação e Conversão Tributária (Regras Fiscais)

O sistema dispensa a criação de inúmeros "Grupos Tributários" para cenários comuns, utilizando a própria Natureza de Operação para injetar exceções e conversões de *tags* fiscais no momento da emissão da Nota Fiscal Eletrônica (NF-e).

### 2.1. Substituição Dinâmica de Regras Fiscais
Com base no tipo de cliente (ex: Consumidor Final) ou destino da mercadoria (UF), o sistema pode aplicar conversores lógicos automáticos:
*   **Conversão de CSOSN:** Um produto cadastrado nativamente com `CSOSN 101` (que permite crédito de ICMS) pode ser convertido em tempo real para `CSOSN 102` (sem permissão de crédito) se a Natureza de Operação reconhecer que a venda destina-se a um consumidor final.
*   **Mapeamento de CST / CFOP:** É possível parametrizar a troca exata de códigos dependendo da origem. *Exemplo:* Se a operação envolver um produto de origem Nacional (0) e a CST original for 60, o sistema substitui o CFOP de saída para 5.405.

### 2.2. Tratamento de Entradas (Conversão de XML de Terceiros)
A aba **Outras Entradas** gerencia a conversão de parâmetros ao importar notas fiscais de fornecedores de diferentes regimes tributários:
*   **Adequação de Regime:** Se a empresa operadora (Simples Nacional) importar um XML de uma indústria (Lucro Real/Presumido) que utiliza CST (ex: CST 00), o sistema efetua o *de-para* automático no banco de dados, convertendo para a nomenclatura equivalente do CSOSN. Isso garante a integridade do inventário fiscal.
*   **Zerar Tributos:** Funcionalidade na aba *Avançado* que permite zerar alíquotas e bases de cálculo de PIS, COFINS e ICMS durante a importação, caso a escrituração contábil e a parametrização do SPED da empresa assim exijam.

---

## 3. Parametrização e Filtros de Interface

A Natureza de Operação também atua como filtro de restrição nas telas operacionais do sistema:

*   **Tipos de Produto Autorizados:** Permite bloquear quais categorias de itens podem ser faturados sob determinada natureza. *Exemplo:* Uma operação de "Venda de Mercadoria" pode ser parametrizada para exibir apenas itens marcados com a flag *Produto para Revenda*, ocultando insumos e bens do ativo imobilizado da tela do operador de caixa.
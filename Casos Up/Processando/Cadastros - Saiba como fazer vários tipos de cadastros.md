---
id: CASO-001
link: https://www.youtube.com/watch?v=WHJUlS48MaM
setor: Desenvolvimento, Suporte, Treinamento
modulo: Cadastros Gerais
tags:
  - erp
  - cadastros
  - regras-de-negocio
  - gerenciamento-de-estoque
  - faturamento
data_criacao: 2026-06-24
---

# Documentação Técnica de Cadastros e Configurações de Sistema

Esta documentação provê uma análise profunda das diretrizes de negócio, regras de validação e parametrizações operacionais baseadas no funcionamento dos módulos de cadastro do ERP. Ela serve como guia técnico para as equipes de [[Suporte Interno]], [[Desenvolvimento]] e implantação do sistema.

---

## Sumário
1. [[#1. Cadastro de Pessoas (Clientes, Vendedores e Fornecedores)]]
2. [[#2. Gestão de Veículos e Manutenção]]
3. [[#3. Cadastro de Produtos e Gestão de Estoque]]
4. [[#4. Parametrização Financeira e Formas de Pagamento]]
5. [[#5. Tabelas de Preço Dinâmicas]]
6. [[#6. Naturezas de Operação e Segurança (Liberações)]]

---

## 1. Cadastro de Pessoas (Clientes, Vendedores e Fornecedores)

O sistema centraliza o cadastro de entidades (Pessoas) permitindo a atribuição de múltiplos perfis à mesma entidade dentro do banco de dados, otimizando o relacionamento comercial.

### Regras de Negócio e Comportamento
* **Multi-Perfil:** Uma única pessoa cadastrada pode acumular as funções de **Cliente**, **Vendedor** e/ou **Fornecedor** simultaneamente. Ao atualizar e salvar os marcadores de perfil na interface, o registro passa a ser indexado dinamicamente nas respectivas telas de consulta filtradas.
* **Legenda Visual de Status:** Para facilitar a gestão visual nas listagens, o sistema adota cores baseadas no status de ativação:
  * <font color="blue">**Azul**</font>: Registro com status normal / ativo.
  * <font color="red">**Vermelho**</font>: Registro inativo.
* **Grupo de Clientes:** Permite o agrupamento de entidades para fins de segmentação comercial e aplicação de políticas de descontos em lote.

> [!tip] Otimização de Registro
> Caso uma pessoa cadastrada inicialmente apenas como **Vendedor** também realize compras na empresa, não há necessidade de duplicar o cadastro. Basta acessar a ficha cadastral existente, marcar a flag **Cliente**, clicar no botão **Salvar** e atualizar a listagem correspondente.

---

## 2. Gestão de Veículos e Manutenção

Módulo dedicado ao controle de frota, acoplado ao gerenciamento logístico de cargas e ordens de serviço internas.

### Fluxos e Rastreabilidade
* **Controle de Manutenções:** Registra o histórico completo de intervenções (ex: trocas de óleo, reparos mecânicos) associando valores financeiros e especificações técnicas.
* **Logística de Cargas:** Rastreia o histórico de carregamentos e Notas Fiscais transportadas pelo veículo.
* **Rastreabilidade por Auditoria:** Todas as modificações críticas feitas nas fichas de veículos (como alteração nos valores gastos em manutenções) são interceptadas pelo módulo de [[Auditoria do Sistema]]. O sistema grava automaticamente o estado anterior do dado, o novo valor, a data/hora e o usuário responsável pela modificação.

---

## 3. Cadastro de Produtos e Gestão de Estoque

O cadastro de produtos possui uma arquitetura robusta voltada ao cálculo automático de margens, alertas de custos e múltiplos identificadores.

### Estrutura do Markup e Alerta de Margem de Lucro
O cálculo de rentabilidade do produto é balizado por parametrizações globais de Markup definidas nas configurações da empresa. O sistema monitora a relação entre o **Custo de Entrada** e o **Preço de Venda** aplicando uma sinalização visual baseada em intervalos percentuais:

| Faixa de Margem (Markup) | Sinalização Visual (Cor da Linha/Filtro) | Significado Operacional |
| :--- | :--- | :--- |
| **Abaixo do Mínimo Estipulado** | <font color="red">Vermelho</font> | **Alerta Crítico:** O custo do produto subiu e a margem atual está abaixo do limite aceitável. Exige reajuste imediato do preço de venda. |
| **Faixa Intermediária** | <font color="yellow">Amarelo</font> | **Alerta de Atenção:** Margem aceitável, porém em zona de compressão de lucro. |
| **Acima da Meta Máxima** | <font color="green">Verde</font> | **Status Ideal:** Margem de lucro saudável conforme as diretrizes da empresa. |

> [!warning] Ponto Crítico: Entrada de Notas Fiscais
> No momento da importação ou digitação da nota de entrada, caso o sistema identifique um aumento no custo do produto que rompa o limite mínimo do Markup cadastrado, o item ficará imediatamente marcado em **Vermelho**. O operador do estoque/compras deve recalcular o preço de venda na própria tela para restabelecer a saúde financeira da operação antes de liberar o lote para venda.

### Atributos Técnicos do Produto
* **Códigos de Barra Múltiplos:** Um produto pode possuir vários códigos de barras vinculados ao seu registro (ex: código da embalagem individual e código da caixa master). No entanto, obrigatoriamente um deles deve ser assinalado como o **Principal** para exibição em relatórios padrão.
* **Flexibilidade de Código Interno:** O sistema gera um ID sequencial automático, mas permite que o usuário sobrescreva o campo **Código** com uma string personalizada. O sistema aceita a duplicidade de códigos personalizados; quando um código duplicado é inserido na tela de vendas, o sistema interrompe o fluxo e abre uma tela de seleção contendo todos os produtos associados àquela identificação para escolha manual do operador.
* **Tipos de Produto:**
  * *Revenda (Normal):* Produtos convencionais de estoque.
  * *Balança:* Produtos precificados por peso, integrados a leitores de etiquetas pesáveis.
  * *Composição (Produto Acabado):* Ativa a aba de Engenharia de Produto/Ficha Técnica, onde são vinculadas todas as matérias-primas que compõem o item e que sofrerão baixa automática no estoque no momento da produção.
* **Segmentação Logística:** Cadastro estruturado por **Grupo**, **Subgrupo**, **Marca**, **Localização Física no Depósito**, **Metragem Cúbica** e **Peso**.
* **Regras Comerciais Específicas:** Configuração de percentual de comissão diferenciado por item (sobrepondo a comissão padrão do vendedor), definição de aplicação de descontos automáticos e integração com dispositivos móveis (força de vendas via tablets).
* **Visões de Estoque:**
  * *Estoque Real/Gerencial:* Registra a movimentação física total de entradas e saídas de mercadorias.
  * *Estoque Fiscal:* Computa apenas as movimentações lastreadas estritamente por emissão ou recebimento de Notas Fiscais Eletrônicas.

---

## 4. Parametrização Financeira e Formas de Pagamento

A configuração financeira mapeia como cada transação afetará a contabilidade e a Tesouraria da empresa.

### Tipos de Documento e Regras de Movimentação de Caixa
No cadastro de **Tipos de Documento/Formas de Pagamento**, determina-se o destino do fluxo financeiro e os comportamentos automáticos de tela do ERP:
* **Dinheiro (Espécie):** Configurado para realizar lançamentos e conciliações diretas na **Conta Caixa**. Pode ser parametrizado para atuar tanto em fluxos de Recebimentos quanto de Pagamentos.
* **Cheque:** Vinculado à gestão de *Cheques Recebidos*. Quando uma venda é concluída utilizando este tipo de documento, o sistema interrompe a liquidação automática e abre obrigatoriamente um pop-up para a digitação de metadados do cheque (Agência, Banco, Conta, Emitente e Bom Para).
* **Depósito Bancário:** Direciona a movimentação de fundos em tempo real para a **Conta Bancária** selecionada, ignorando o fluxo de caixa interno de balcão.

> [!info] Plano de Contas
> Toda forma de pagamento e tipo de documento deve estar devidamente associado ao [[Plano de Contas Contábil]] da empresa para garantir a correta classificação das receitas e despesas nos demonstrativos de resultados.

---

## 5. Tabelas de Preço Dinâmicas

O sistema oferece dois modelos de aplicação de regras de preço por meio do módulo de **Tabelas de Preço**:

1. **Acréscimo ou Desconto Linear (Lote):** Permite configurar uma porcentagem fixa (ex: +10% de acréscimo ou -5% de desconto) que incidirá automaticamente sobre o preço de venda base de **todos** os produtos que entrarem em um pedido associado a essa tabela.
2. **Exceção / Preço Fixo por Item:** Dentro da mesma tabela configurada com percentual linear, o gestor pode registrar produtos específicos para operarem como exceção. Nesses itens selecionados, o sistema ignora a regra percentual do lote e passa a praticar o valor monetário exato predefinido para a tabela.

---

## 6. Naturezas de Operação e Segurança (Liberações)

### Natureza de Operação (CFOP/Regras Fiscais)
As naturezas de operação (Venda, Compra, Brinde, Devolução) delimitam o comportamento fiscal, financeiro e de estoque do documento de saída/entrada. Suas diretrizes incluem:
* Ativação/Desativação da movimentação automática de estoque.
* Geração ou não de parcelas no Contas a Receber/Pagar (financeiro).
* Vinculação da matriz de tributação de ICMS/ST parametrizada por Estado de destino.

### Segurança de Alçada e Liberação de Crédito
O sistema implementa uma camada rígida de controle de acessos baseada em perfis de usuário e permissões administrativas para contingenciar riscos operacionais.

* **Bloqueio Automático por Inadimplência:** Se um cliente possuir pendências financeiras vencidas no módulo de Contas a Receber, ao tentar abrir uma nova venda, o sistema altera o status do pedido para **Bloqueado** (sinalizado com um ícone de cadeado na interface).
* **Comportamento do Sistema no Bloqueio:** Com o status travado, o sistema impede terminantemente ações de **Faturamento**, inclusão do pedido em **Planilhas de Carga** ou prosseguimento logístico. O pedido permanecerá estagnado em modo de visualização restrita.
* **Fluxo de Desbloqueio:** A liberação só poderá ser efetuada mediante a intervenção física de um usuário supervisor, que deve acionar o botão de liberação na interface e autenticar a operação digitando sua **Senha de Liberação**.

> [!warning] Validação de Crédito
> Jamais altere o status de um pedido bloqueado manualmente no banco de dados. O fluxo correto exige a validação das pendências com o cliente e a inserção da senha do perfil de usuário autorizado diretamente no ERP, registrando o log de auditoria da concessão de crédito de exceção.


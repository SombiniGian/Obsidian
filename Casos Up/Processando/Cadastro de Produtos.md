---
id: [CASO-166]
link: https://www.youtube.com/watch?v=20SR89LnkR4&t=448s
setor: [Suporte, Implementação, Cadastros]
modulo: [Cadastros / Produtos]
tags: [cadastro-de-produtos, estoque, tributacao, lotes, tipos-de-produto, cashback]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Cadastro de Produtos]]
2. [[#Configurações Globais do Módulo (Engrenagem)]]
3. [[#Parametrização Básica e Comercial]]
4. [[#Controle Avançado de Lotes e Quarentena]]
5. [[#Tributação e Documentos Fiscais]]
6. [[#Comportamento Dinâmico por Tipo de Produto]]
7. [[#Pontos Críticos e Validações]]

# Visão Geral do Cadastro de Produtos
O **Cadastro de Produtos** é o núcleo de operações do ERP, ditando o comportamento de compras, vendas, produção e integrações com hardwares externos (balanças e maquininhas). O módulo é altamente expansível: a interface adapta-se dinamicamente com base no "Tipo de Produto" selecionado (ex: Medicamento, Combustível, Restaurante), exibindo apenas os campos e exigências fiscais pertinentes àquele segmento.

# Configurações Globais do Módulo (Engrenagem)
Antes de iniciar o cadastro de itens, o administrador (apenas usuários com este nível de permissão visualizam o ícone da engrenagem) deve definir as regras estruturais da tela.

### Estoque e Códigos
*   **Mostrar Estoque por Empresa:** Se ativo, a grade principal exibirá o saldo físico do item fragmentado por CNPJ (caso o cliente possua múltiplas filiais na mesma base). Se inativo, exibe apenas o saldo da loja logada no momento.
*   **Geração de Código:** Define se o operador digitará manualmente a chave primária do produto (ID) ou se o sistema aplicará um incremento automático (Auto-increment).

### Travas Fiscais (Validação)
*   **Validar Dados Fiscais:** Trava de segurança crucial. Se ativa, o sistema impede o salvamento de qualquer produto que esteja com o NCM, CST ou CSOSN em branco.
    *   *Dica de Implantação:* Em cenários de frente de caixa informal (ex: barzinho sem emissão de NFC-e), essa opção pode ser desmarcada para agilizar o lançamento de cardápios apenas com nome e preço. Para varejo fiscal, **deve permanecer sempre ativa**.
*   **Código Fiscal (SPED/Sintegra):** Estabelece o paralelismo entre o código interno do sistema e o código que será enviado no XML para a SEFAZ. Se a empresa realizar migração de software, o código fiscal legado deve ser preenchido rigorosamente nesta aba para não duplicar o inventário no fisco.

# Parametrização Básica e Comercial

*   **Venda por Valor Total (Cálculo Inverso):** Ao invés de o operador bipar o item e digitar `1,5 Kg`, ele seleciona o produto e digita `R$ 30,00`. O sistema realiza a divisão pelo preço unitário e preenche a quantidade exata automaticamente (muito utilizado em açougues e padarias).
*   **Venda de Área/Volume:** Ativa campos de `Altura`, `Largura` e `Comprimento` na tela do [[PDV]] para cálculo automatizado de Metro Quadrado (M²) ou Metro Cúbico (M³).
*   **Vasilhame/Devolução:** Funcionalidade para depósitos de bebidas e gás. Ao vender um `Botijão de Gás 13Kg (Cheio)`, o sistema dá saída neste item e processa automaticamente uma **entrada** paralela no produto oculto configurado como `Vasilhame 13Kg (Vazio)`.
*   **Múltiplos Códigos de Barras:** Um único produto (ex: Detergente) pode possuir dezenas de códigos EAN cadastrados (quando a indústria muda a embalagem ou quando se compra de fornecedores diferentes), mantendo um único registro de saldo no sistema.

# Controle Avançado de Lotes e Quarentena
A aba de Lotes atende às normativas da ANVISA e indústrias de transformação.

*   **Rastreabilidade de Movimento:** O administrador define se a indicação do lote será obrigatória na **Entrada** (compra), na **Saída** (venda) ou em ambos.
    *   *Exemplo Prático (Assistência Técnica):* A loja compra 10 iPhones e anota os 10 IMEIs (como lotes) na entrada. Na saída, seleciona qual IMEI específico foi vendido, garantindo rastreio para garantias futuras.
*   **Quarentena de Produção:** Se o produto for derivado de uma [[Ordem de Produção]] (ex: queijo artesanal ou produto químico), é possível configurar um prazo (ex: 20 dias). O sistema bloqueia a visualização e venda do lote resultante no PDV até que o prazo de maturação seja atingido.

# Tributação e Documentos Fiscais
Localizada na aba "Documentos Fiscais", esta é a área de maior sensibilidade jurídica do ERP.
*   Deve conter o **NCM**, **CST/CSOSN** e **Origem** da mercadoria.
*   Para empresas do Simples Nacional, o preenchimento costuma ser estático. Para empresas do Lucro Real/Presumido, a complexidade aumenta. 
*   **Exceção de Regras Interestaduais:** Se o produto possuir tributações diferentes baseadas no estado (UF) de destino, a regra unitária do cadastro deve ser ignorada em favor do uso da rotina de **Grupo Tributário**, que sobrepõe os dados desta aba através de uma matriz fiscal hierárquica.

# Comportamento Dinâmico por Tipo de Produto

O campo principal "Tipo de Produto" altera radicalmente as abas disponíveis na interface:

1.  **Restaurante:** Habilita a aba para vínculo de **Complementos**, **Modos de Preparo** e **Opcionais** (ex: Ponto da carne, Adicionar Bacon).
2.  **Balança (Check-out ou Etiquetadora):** Abre a aba de carga de balança, exigindo o "Código de Balança" (geralmente de 4 a 6 dígitos) que será lido pelo maquinário Toledo/Filizola. Habilita também campos de informação nutricional se o sistema gerar etiquetas.
3.  **Combustíveis/Gás:** Habilita campos regulatórios obrigatórios para a SEFAZ, como o **Código ANP** e percentuais de mistura de gás.
4.  **Kits / Cestas Básicas:** Permite vincular produtos subjacentes. A grande diferença para o restaurante é que, ao emitir a NF-e, o sistema **desmembra a cesta**, exibindo linha a linha no XML (Arroz, Feijão, etc.) para tributação correta, enquanto na tela de venda exibe apenas "Cesta Básica".
5.  **Desmembramento (Produção Inversa):** Específico para açougues de grande porte. Cadastra-se o item "Boi/Carcaça" e mapeia-se o rendimento percentual de cortes (ex: 10% Picanha, 20% Costela). Ao dar entrada em 100Kg de Carcaça, o sistema destrincha automaticamente o saldo para os produtos filhos na proporção da ficha técnica.
6.  **Medicamentos:** Habilita obrigatoriamente as tags do **Código da ANVISA** e número do lote/validade da indústria farmacêutica, sem os quais a transmissão fiscal será rejeitada pela SEFAZ.

# Pontos Críticos e Validações

> [!warning] Alteração de Código Fiscal com Estoque Ativo
> Se um produto já está sendo comercializado e transmitido à SEFAZ (ex: código fiscal `100`), e a empresa decide alterar seu código interno para `1000`, a alteração no ERP deve ser precedida de uma notificação ao contador. O fisco interpretará como se o estoque do produto `100` estivesse paralisado e o produto `1000` tivesse surgido do nada. O contador precisará lançar um evento fiscal de ajuste/correção de estoque no SPED.

> [!tip] Cashback (Híbrido)
> A configuração de Cashback pode operar em duas frentes cruzadas. A [[Natureza de Operação]] pode ditar um cashback global (ex: 1% para a venda inteira). Contudo, se um produto específico tiver preenchido em sua aba comercial um cashback de 5%, o sistema respeitará a individualidade do item (somando 5% deste item + 1% dos demais) no saldo de crédito do cliente.
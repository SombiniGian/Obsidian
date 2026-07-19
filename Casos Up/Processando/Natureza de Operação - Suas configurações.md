---
id: [CASO-167]
link: https://www.youtube.com/watch?v=hR6qMHhVtH4&t=102s
setor: [Suporte, Implementação, Fiscal]
modulo: [Cadastros / Natureza de Operação]
tags: [natureza-de-operacao, cfop, regras-fiscais, faturamento, estoque]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Natureza de Operação]]
2. [[#Parametrização Básica (Estoque, Financeiro e Modelos)]]
3. [[#Configurações Avançadas e Impostos]]
4. [[#Configurações Estruturais e Travas de Segurança]]
5. [[#Mapeamento Inteligente de CFOPs]]
6. [[#Pontos Críticos e Regras de Negócio]]

# Visão Geral da Natureza de Operação
A **Natureza de Operação** é considerada a "alma" do sistema ERP. É o motor de regras que orquestra o comportamento interno de cada movimentação realizada, seja uma venda, compra, devolução, remessa ou transferência. É através desta parametrização que o sistema entende se uma ação deve deduzir o estoque, gerar boletos no financeiro ou acionar a emissão de documentos fiscais eletrônicos como [[NF-e]] ou [[NFC-e]].

# Parametrização Básica (Estoque, Financeiro e Modelos)
Ao criar um novo registro em **Cadastros > Naturezas de Operação**, as seguintes diretrizes primárias devem ser definidas:

*   **Modelo de Documento Fiscal:** Define qual infraestrutura tributária será acionada no encerramento da operação.
    *   `55` = Nota Fiscal Eletrônica (NF-e).
    *   `65` = Nota Fiscal de Consumidor (NFC-e).
*   **Movimenta Estoque:** Sinaliza se os produtos listados devem gerar saída/entrada patrimonial no ato do faturamento.
*   **Gera Financeiro:** 
    *   Se **marcado**, o sistema obrigará o usuário a passar pela tela de recebimento/pagamento (selecionar espécie, parcelamento) e alimentará as tabelas de contas a receber ou pagar.
    *   Se **desmarcado**, o sistema avança o faturamento sem gerar obrigações financeiras (útil para simples remessas ou doações).
*   **Local de Estoque:** Como o sistema UP não gerencia estoque por item fracionado na tela de venda, é na Natureza de Operação que se define de qual almoxarifado global a operação deduzirá (ex: `Depósito Loja 1`).
*   **Mensagem Fiscal Padrão:** Permite atrelar um texto genérico (ex: "Validade da Proposta: 15 dias" ou leis fiscais) que será forçado e impresso no campo de observações adicionais de todos os documentos gerados com esta natureza.

# Configurações Avançadas e Impostos
A aba "Avançado" engloba dezenas de gatilhos automáticos para personalizar fluxos contábeis e industriais específicos:

*   **Zerar Base de Cálculo (PIS/COFINS):** Utilizado em operações de remessa ou devoluções onde o imposto não deve ser re-tributado, forçando o cálculo a R$ 0,00 no XML.
*   **Cálculo Prévio no Pedido de Venda:** Se ativo em operações de atacado/indústria, o sistema realiza a matemática de impostos e tributos já na fase de orçamento/pedido, permitindo ao lojista visualizar a margem real e o valor bruto antes mesmo de acionar o botão de emitir NF-e.
*   **Geração Automática de Ordem de Produção (OP):** Direcionada a indústrias e padarias. Ao finalizar uma venda com uma natureza de operação de produto manufaturado (ex: Venda de Pão), o sistema dispara em background uma [[Ordem de Produção]], consumindo a matéria-prima (farinha, ovos) da ficha técnica e abatendo do estoque industrial, evitando a necessidade de baixa manual.

# Configurações Estruturais e Travas de Segurança

### Travas de Valores e Identificação
*   **Valor Máximo da Operação:** Determina um teto financeiro para o uso da natureza. Muito utilizado para limitar a emissão de NFC-e (ex: R$ 900,00 ou R$ 10.000,00 dependendo da UF). Ao estourar o limite, o sistema bloqueia a gravação e exige que o operador altere a natureza para uma emissão de NF-e (Modelo 55).
*   **Valor Máximo sem Identificar o Consumidor:** Trava legal que exige a inserção do CPF/CNPJ do cliente caso o cupom ultrapasse determinado limite financeiro.

### Cashback Global
A natureza de operação atua como a régua global do módulo de fidelidade. Caso a operação gere retorno ao cliente, define-se o percentual (ex: `1%`) aqui. Se um produto específico na venda possuir uma regra própria de cashback no seu cadastro unitário, o sistema priorizará a regra daquele item, calculando o cashback fracionado linha a linha e consolidando o crédito no final.

# Mapeamento Inteligente de CFOPs
O CFOP (Código Fiscal de Operações e Prestações) dita a legalidade do trânsito da mercadoria perante o fisco. Para empresas do Simples Nacional ou varejos de bairro, as regras são mapeadas diretamente na aba **CFOP**.

> [!tip] Mapeamento Relacional CFOP
> O sistema não obriga a criação de uma Natureza de Venda separada para cada tipo de produto tributário. O operador cadastra uma única Natureza "Venda de Mercadorias" e adiciona uma matriz de "De -> Para" baseada no produto:
> *   Se Produto Acabado (`Origem 0`, `CSOSN 101`) -> O sistema injeta o CFOP `5.101`.
> *   Se Produto de Revenda (`CSOSN 500`) -> O sistema injeta o CFOP `5.405`.
>
> Se uma regra específica não for mapeada na grade ou a matriz falhar, o motor utilizará os campos de **CFOP Padrão** (interno e externo) parametrizados na capa do cadastro como contingência.

# Pontos Críticos e Regras de Negócio

> [!warning] Estoque Duplo em Notas Fiscais de Compra (XML)
> A configuração **"Movimentar Estoque Gerencial/Real e Contábil"** deve ser mantida **obrigatoriamente ativa** nas Naturezas de Operação designadas para **Entrada de Compras**.
> 
> *   **Motivo:** Em vendas convencionais, o pedido abate o gerencial e a NF-e abate o fiscal (dois tempos). No recebimento de mercadorias, a importação direta do XML via SEFAZ funde essas etapas em uma única ação. Se a opção não estiver marcada, a nota fiscal injetará os itens no saldo fiscal, mas deixará os produtos em falta no estoque físico da loja para a venda no balcão, quebrando a logística do cliente.

> [!info] Exceção de Tributação Interestadual
> Embora as regras de CFOP configuradas dentro da Natureza de Operação atendam perfeitamente vendas internas de pequenos e médios varejos, operações de atacado com saída interestadual que exigem substituição tributária complexa ou mudança de alíquotas por fronteira não devem depender dessa tela. Para cenários fiscais elásticos, deve-se adotar o recurso avançado de [[Grupo Tributário]].
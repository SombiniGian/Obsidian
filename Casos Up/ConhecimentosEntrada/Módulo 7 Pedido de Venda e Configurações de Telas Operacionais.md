Este módulo detalha a arquitetura do **Pedido de Venda** e as múltiplas interfaces de frente de loja (PDV) disponíveis no sistema. O ecossistema foi desenhado para se adaptar a diferentes verticais de negócio (varejo, indústria, food service) através de parametrizações por estação de trabalho.

---

## 1. Regras de Configuração e Parametrização por Estação

A tela de configurações do Pedido de Venda é o painel de controle que dita as regras de negócio de faturamento.

* **Configuração Local (Estação de Trabalho):** Todo parâmetro que possui um **asterisco (*)** na frente de sua nomenclatura indica que a regra é salva *por estação* (no registro da máquina local), e não globalmente no banco de dados.
    * *Exemplo Prático:* O administrador pode configurar o computador do caixa frontal para abrir diretamente o **PDV Super** (rápido para supermercado), enquanto a máquina do escritório comercial abre a tela **Pedido** (mais detalhada) por padrão.
* **Bloqueios e Restrições de Venda:**
    * **Bloqueio de Pendências Financeiras:** Se ativado, o sistema impede o fechamento de novas vendas a prazo/faturadas para clientes que possuam títulos vencidos no "Contas a Receber".
    * **Bloqueio de Estoque Negativo:** Impede a venda de itens sem saldo físico/contábil suficiente.
    * **Alertas Dinâmicos:** O sistema pode exibir alertas em tempo real se o cliente selecionado possuir outros pedidos abertos ou pendentes, evitando duplicidade.

---

## 2. Automação de Comportamento Comercial

* **Obrigatoriedades Configuráveis:** A gerência pode forçar o operador a informar o Vendedor, a Natureza de Operação, ou exigir a inserção de Senha para concessão de descontos e cancelamentos.
* **Transição de Natureza para Pessoa Jurídica (PJ):** O sistema possui um gatilho automático que altera a Natureza de Operação nativa caso o operador selecione um cliente cadastrado como PJ. Isso garante que a emissão não saia como NFC-e (Cupom) caso a legislação local exija NF-e (Modelo 55) para contribuintes.
* **Mapeamento de Observações:** Há um parâmetro para espelhar automaticamente a "Observação do Produto" (texto configurado no cadastro de estoque) direto na "Observação do Item" no ato da venda.

---

## 3. Interfaces Operacionais (Telas de Venda)

O sistema disponibiliza múltiplas interfaces gráficas para atender a operações com diferentes ritmos e necessidades de dados.

### 3.1. Tela Pedido (Modo Escritório / Indústria)

* Interface mais rígida e completa de todas.
* Projetada para backoffice, televendas ou indústrias que exigem o preenchimento de múltiplos dados logísticos e comerciais (transportadora, lote do produto, classificação de transporte, etc.) no ato do orçamento.

### 3.2. Tela Balcão (Pré-Venda e Varejo Tradicional)

* Tela de alta produtividade, otimizada para uso com teclado.
* **Gestão de Orçamentos:** Pressionando `Alt + O`, a tela altera seu status para "Orçamento", desabilitando o botão de finalização financeira e permitindo salvar a cotação em status "Aberto".
* **Cliente Não Registrado (Ctrl + P):** Funcionalidade essencial para lojas de material de construção ou papelarias. Permite iniciar o pedido, digitar apenas o nome do cliente no cabeçalho sem obrigatoriedade de cadastro completo, salvar e enviar o cliente fisicamente ao caixa apenas para liquidação e emissão fiscal.

### 3.3. Tela Touch (Food Service / Restaurantes)

* Desenhada especificamente para monitores sensíveis ao toque (touchscreen).
* Elimina a dependência de teclado/mouse. Os itens são organizados visualmente por painéis de Grupos e Subgrupos.
* Ideal para lançamento rápido de comandas e consumo em mesas.

### 3.4. Novo PDV e PDV Super (Frente de Caixa e Supermercados)

* **Customização Extrema:** Esta interface permite arrastar os elementos da tela, alterar a ordem dos botões, modificar cores e trocar as teclas de atalho (atalhos dinâmicos).
* **PDV Super:** Versão "enxuta" do PDV moderno. Possui menos funcionalidades complementares visíveis na tela para focar estritamente na velocidade de *scan* (leitura de código de barras) e recebimento rápido de pagamento, fundamental para filas de supermercado.

---

## 4. Teclas de Atalho e Acessibilidade

O sistema provê "mapas de atalhos" acessíveis dentro das telas.

* No modelo tradicional (Tela Balcão), o operador pode consultar os comandos mapeados pressionando `Alt + A` (ex: `Ctrl + Q` para alterar a quantidade de um item já lançado).
* No Novo PDV, as teclas de atalho podem ser totalmente remapeadas através do menu da engrenagem (`Configurações > Personalizar`), permitindo adaptar o software aos vícios de uso de sistemas concorrentes anteriores, minimizando a curva de aprendizado do operador.
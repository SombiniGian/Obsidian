---
id: [CASO-165]
link: https://www.youtube.com/watch?v=uZ1yzSYDewU&t=1s
setor: [Suporte, Implementação, Cadastros]
modulo: [Cadastros / Pessoas]
tags: [cadastro-de-pessoas, cliente, vendedor, comissao, regime-tributario, aplicativo-mobile]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Tabela Única de Pessoas]]
2. [[#Estrutura Básica e Integração de Dados]]
3. [[#Perfil Cliente: Parametrização e Regras Fiscais]]
4. [[#Contratos, Mensalistas e Modalidades]]
5. [[#Perfil Vendedor / Garçom e App Mobile]]
6. [[#Pontos Críticos e Validações]]

# Visão Geral da Tabela Única de Pessoas
O sistema adota uma arquitetura de **Cadastro Único (Tabela Única)** para a gestão de entidades. Diferente de sistemas legados que mantêm tabelas separadas para clientes, fornecedores e vendedores, no ERP UP Sistemas a entidade base é apenas "Pessoa". A atribuição de papéis (Cliente, Fornecedor, Vendedor, Colaborador) ocorre por meio da ativação de *flags* (caixas de seleção) no rodapé do cadastro.

> [!info] Multi-Papel da Entidade
> Uma mesma pessoa/CNPJ pode ser, simultaneamente, seu Cliente e seu Fornecedor. Ao marcar ambas as flags, o sistema evita a duplicidade de cadastros e bloqueia a inserção de dois registros com o mesmo CNPJ, unificando o controle financeiro na aba de contas a pagar e receber.

Ao marcar um papel no rodapé, o sistema habilita automaticamente as abas superiores correspondentes contendo os parâmetros específicos daquela função (ex: aba `Cliente` ou aba `Vendedor`).

# Estrutura Básica e Integração de Dados
A interface principal do cadastro abrange funcionalidades de ganho de produtividade e histórico:

*   **Consulta à Receita Federal:** Através do botão da lupa ao lado do campo do CNPJ, o sistema realiza uma chamada de API nos servidores do governo, retornando de forma automática a Razão Social, endereço, bairro, CEP e Inscrições Estaduais, mitigando erros de digitação.
*   **Abas Globais:** Independentemente do papel, todo cadastro possui a aba `Endereços` (suportando múltiplos locais de entrega), a aba `Financeiro` (exibindo saldos em aberto e movimentações de crédito), além de abas para o `Plano de Contas`, fotos e registro de auditoria.

# Perfil Cliente: Parametrização e Regras Fiscais
Ao habilitar o papel de **Cliente**, a aba homônima se torna visível, agrupando os parâmetros comerciais que ditarão o comportamento do módulo de [[Vendas / Pedidos]]:

*   **Vínculos Padrão:** É possível amarrar uma "Tabela de Preço", "Forma de Pagamento" e "Vendedor" como padrão para o cliente. Quando um novo pedido for aberto e o cliente for selecionado, o sistema puxará essas regras automaticamente.
*   **Limite de Crédito:** Permite travar o faturamento a prazo.
*   **Vínculo com Vendedor Externo:** Trava essencial para privacidade de carteira. Se um cliente for vinculado ao `Vendedor A`, quando este vendedor sincronizar o [[Mobile / Força de Vendas]], ele fará o download exclusivo dos seus próprios clientes, ocultando a carteira do `Vendedor B`.

### O Peso do Regime Tributário no Cadastro
A configuração do campo **Regime Tributário** (Simples Nacional, Lucro Presumido, Lucro Real, MEI) dentro do cadastro do cliente é fundamental para o sucesso das emissões fiscais em empresas submetidas ao regime de lucro normal ou atacadistas.

> [!warning] Ponto Crítico de Tributação
> O motor fiscal do sistema UP, conhecido como [[Grupo Tributário]], toma decisões dinâmicas baseadas neste campo. O sistema pode ser instruído a calcular e aplicar o CFOP e ICMS X se o cliente que está comprando for do estado de São Paulo E for do Simples Nacional, ou aplicar a regra Y caso o mesmo cliente seja uma Indústria do Lucro Presumido. Portanto, o preenchimento incorreto deste regime fará com que o sistema calcule os impostos da NF-e na alíquota errada.

*   **Configurações de Isenção/Adição:** Pode-se configurar para que o sistema não calcule IPI ou não integre a base de cálculo do ICMS especificamente para as operações daquele cliente, sobrepondo as regras globais dos produtos.

# Contratos, Mensalistas e Modalidades
Para empresas prestadoras de serviço, escolas ou clubes, a aba de clientes oferece soluções de automação de faturamento:

*   **Mensalista:** Utilizado para serviços contínuos sem fim predeterminado (ex: mensalidade de suporte de software). Informa-se o valor recorrente e o dia de vencimento. Uma rotina global chamada "Controle de Cobranças" fará a varredura e gerará os boletos em massa mensalmente para todos os marcados com a flag.
*   **Modalidade:** Utilizado para contratos com prazo determinado. Gera um carnê linear de parcelas (ex: 12 parcelas) projetadas de uma única vez no contas a receber na data do acordo.
*   **Controle de Associados:** Habilita a geração de código de barras ou numeração de matrícula. O sistema permite o cadastro de Pessoas com a flag `Dependente`, vinculadas ao cadastro do Associado titular.

# Perfil Vendedor / Garçom e App Mobile
Ao ativar a flag **Vendedor**, o sistema abre a interface de controle do usuário para os ecossistemas de comissionamento e aplicativos móveis.

*   **Credenciais de Acesso Remoto:** Contém o Login e a Senha que o funcionário utilizará para acessar o aplicativo móvel.
*   **Tipo de Usuário App:** Determina a interface do celular:
    *   `Vendedor`: Libera o menu de Força de Vendas (Pedidos, clientes, catálogo).
    *   `Garçom`: Modifica radicalmente o layout do app, habilitando o módulo de [[Restaurante / Mesas e Comandas]], limitando o fluxo à adição de itens em mesas ativas.
*   **Direitos do App:** Permite liberar ou bloquear a capacidade do usuário emitir Nota Fiscal Eletrônica diretamente pelo celular, faturar pedidos no encerramento ou forçar o sistema no retaguarda a imprimir a comanda automaticamente na cozinha assim que o pedido for transmitido via app.
*   **Controle de Modelos de Impressão:** Se o Vendedor atuar de forma externa e utilizar uma mini-impressora bluetooth (ex: 58mm ou 80mm) de fabricante ou layout distinto, é possível configurar caminhos de arquivos FastReport (`.frx`) individualizados e restritos ao cadastro daquele vendedor.

# Pontos Críticos e Validações

> [!danger] Multi-Empresa e Vínculos de Vendedores
> Em bases de dados que processam o controle de faturamento centralizado de Múltiplos CNPJs, se a aba do vendedor NÃO tiver o campo "Empresa" explicitamente amarrado, o funcionário conseguirá trafegar e faturar dados de todas as filiais. O administrador deve obrigatoriamente restringir o vínculo corporativo do vendedor para preservar o isolamento operacional de cada unidade de negócio.
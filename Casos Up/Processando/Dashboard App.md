---
id:
  - CASO-131
link: https://www.youtube.com/watch?v=0xjb81vmN0s&t=12s
setor:
  - Suporte
  - Desenvolvimento
  - Implementação
modulo:
  - Mobile / Painel de Dashboards Estendidos
tags:
  - android
  - dashboard
  - relatorios
  - sql
  - permissões
  - graficos
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Módulo de Dashboards]]
2. [[#Origem dos Dados: Gerador de Telas Personalizadas]]
3. [[#Controle de Hierarquia e Permissões de Acesso]]
4. [[#Modelagem Visual e Tipos de Gráficos Disponíveis]]
5. [[#Mecanismo de Filtros Dinâmicos e Persistência de Padrão]]
6. [[#Arquitetura de Cache Local e Operação Offline]]
7. [[#Customização de Preferências e Organização de Painéis]]
8. [[#Regras de Negócio e Pontos Críticos de Falha]]

# Visão Geral do Módulo de Dashboards
O módulo de **Painel de Dashboards Estendidos** fornece a gestores, diretores e vendedores externos a capacidade de analisar indicadores de desempenho, faturamento e metas em tempo real por meio de dispositivos móveis Android. Seguindo a filosofia estrutural do ERP, este ecossistema se destaca por ser totalmente personalizável em tempo de execução, permitindo que a própria revenda crie, altere ou exclua indicadores por meio de queries estruturadas na retaguarda Windows, com sincronização automática para as frentes móveis.

# Origem dos Dados: Gerador de Telas Personalizadas
As informações renderizadas no smartphone não possuem layouts rígidos no código-fonte do aplicativo móvel. Toda a inteligência de dados é derivada do **Gerador de Telas Personalizadas** localizado no retaguarda Windows (caminho: **Configurações > Telas Personalizadas**), uma ferramenta que compartilha o mesmo motor do gerador de relatórios do sistema.

### Requisitos de Exportação da Query:
*   Para que uma análise estruturada seja integrada ao aplicativo, o desenvolvedor ou técnico da revenda deve redigir a consulta SQL e marcar obrigatoriamente a flag **Exportar para o App** na ficha técnica do relatório.
*   **Capacidade de Variáveis:** O interpretador de queries suporta a extração e consolidação linear de até 5 valores quantitativos simultâneos por linha de instrução (ex: é possível plotar em uma única query o *Valor Total de Pedidos*, *Valor Efetivamente Faturado* e o *Valor de Comissão Gerada* de um mesmo mês competência).

# Controle de Hierarquia e Permissões de Acesso
A segurança de dados proíbe que operadores operacionais acessem o faturamento consolidado da empresa. Para gerenciar as chaves de acesso no [[Mobile / Servidor Força de Vendas]]:

1.  Acesse o cadastro de **Usuários** na retaguarda Windows e selecione o perfil do funcionário.
2.  Navegue até o bloco de **Permissões** e localize a árvore de **Telas Personalizadas**.
3.  Marque exclusivamente os painéis que o colaborador poderá inspecionar.
4.  **Vinculação Mandatória:** No cadastro do Usuário, certifique-se de preencher o campo **Vendedor Relacionado** (ex: associar o Usuário 2 ao Vendedor 2). 

> [!danger] Erro Crítico de Quebra de Vínculo de Handshake
> Caso o técnico realize o provisionamento de permissões nas tabelas de relatórios, mas esqueça de amarrar o ID do Vendedor ao Usuário no ERP, o aplicativo Android interceptará o conflito no momento em que o usuário clicar em **Atualizar Dash** e abortará o carregamento exibindo o alerta de exceção: `Nenhum usuário vinculado ao vendedor. Não é possível acessar telas personalizadas`.

# Modelagem Visual e Tipos de Gráficos Disponíveis
O aplicativo móvel renderiza os dados em duas camadas visuais síncronas: uma representação gráfica superior e um detalhamento analítico em formato de lista indexada na base inferior. O operador pode alternar dinamicamente entre 6 famílias de gráficos em tempo de execução:

| Família de Gráfico | Comportamento e Regra de Renderização Visual |
| :--- | :--- |
| `Donut` / `Pizza` / `Rosas` | **Regra dos 10 Primeiros:** O motor gráfico agrupa e renderiza de forma visual apenas os **10 primeiros registros** retornados pela query SQL. Essa trava de design impede a poluição visual do gráfico de setores em telas pequenas. Contudo, as linhas subsequentes (ex: 100 itens) continuam listadas integralmente na tabela logo abaixo do gráfico. |
| `Colunas` / `Barras` / `Linhas` | Suportam a amostragem de dados complexos com paginação lateral, permitindo a comparação de múltiplos valores simultâneos (até 5 variáveis) por período competência. |

# Mecanismo de Filtros Dinâmicos e Persistência de Padrão
Sempre que a query SQL parametrizada no retaguarda exigir argumentos de entrada (como escopo de períodos ou restrição de carteiras), o aplicativo Android ativa de forma automática o botão de **Filtro** no canto superior direito da tela do dashboard.

*   **Variáveis Elegíveis de Entrada:** O sistema processa nativamente 4 modalidades de filtros estruturados: `Período` (Datas), `Cliente`, `Vendedor` e `Empresa`.
*   **Persistência de Fallback:** Para eliminar a necessidade de o gestor parametrizar as datas (ex: selecionar os últimos 300 dias) a cada inicialização de tela, o usuário pode definir os parâmetros e clicar na opção **Salvar Filtro como Padrão**. O ERP local grava o estado e passa a adotá-lo como carregamento inicial estável para aquele relatório específico.

# Arquitetura de Cache Local e Operação Offline
O sistema foi projetado para preservar a usabilidade do gestor em trânsito ou em ambientes com restrição de sinal de internet.

*   **Persistência em Cache:** Assim que o smartphone realiza a consulta síncrona a um dashboard pela primeira vez, o aplicativo salva o dataset em um banco de dados SQLite local na memória interna do aparelho.
*   **Funcionamento Offline:** Caso o [[Mobile / Servidor Força de Vendas]] sofra uma queda de energia ou o smartphone fique sem conectividade, os painéis que já foram consultados anteriormente continuarão abrindo e renderizando os gráficos normalmente. A interface exibirá a string de controle: `Última atualização: [Dia da Semana], [Data] às [Hora]`.
*   **Invalidação de Cache:** Para forçar o aplicativo a expurgar o banco local e buscar novos dados atualizados na retaguarda, o usuário deve clicar explicitamente no botão de **Sincronizar/Atualizar Dados** interno daquele gráfico.

# Customização de Preferências e Organização de Painéis
O gerenciamento da fila de relatórios suporta customizações por gestos diretos na tela de listagem de dashboards:

*   **Definição de Painel Home (Favorito):** Ao abrir o menu de buscas, o usuário pode **Arrastar para a Direita** sobre o relatório desejado para ativá-lo com o status de **Tornar Principal**. O registro receberá um destaque verde e, em todos os logins futuros, o aplicativo abrirá este painel como tela inicial padrão.
*   **Descarte de Visões:** O operador pode **Arrastar para a Esquerda** sobre um indicador para comandar a ação de **Excluir**, removendo o widget da sua grade móvel de visualização sem deletá-lo do servidor de retaguarda.
*   **Tipos de Login e Atalhos Rápidos:** Para diretores cujo foco seja unicamente o monitoramento analítico da corporação, o cadastro do vendedor pode ser parametrizado com o Perfil = `Dashboard`. Ao realizar o login no app, o sistema pula o catálogo de vendas e abre diretamente a interface gráfica de indicadores. Para vendedores mistos, o acesso ocorre por meio do menu lateral flutuante ou pelo botão de atalho presente no dashboard tradicional de metas de [[Vendas / Pedidos]].

# Regras de Negócio e Pontos Críticos de Falha

> [!warning] Otimização de Performance e Timeout de Queries Complexas
> Como o acionamento do botão de atualização de dados força o servidor de retaguarda a executar a query SQL diretamente no banco de dados [[Banco de Dados / Firebird]], queries mal indexadas ou sem travas de data (ex: tentar somar o faturamento histórico de 10 anos de uma grande corporação sem paginação) travarão o serviço de retaguarda por Timeout. O aplicativo Android reportará falha de comunicação e interromperá a renderização. Certifique-se de aplicar cláusulas `WHERE` associadas aos filtros de período móvel na retaguarda.
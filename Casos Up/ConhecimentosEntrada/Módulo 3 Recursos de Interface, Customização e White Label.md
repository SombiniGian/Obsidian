Este módulo detalha as ferramentas de personalização da interface gráfica do ERP, permitindo adaptar o sistema às regras de negócio específicas do cliente e aplicar o modelo de licenciamento White Label.

---

## 1. Configuração Dinâmica de Grids e Filtros

As tabelas de exibição de dados (*grids*) em todo o sistema suportam um alto nível de personalização por usuário, gerenciado através do menu de contexto (botão direito do mouse).

*   **Organização de Colunas:** Permite adicionar, remover e reordenar as colunas visíveis. É possível ajustar a largura e o tamanho da fonte para acessibilidade visual.
*   **Persistência de Layout:** O layout customizado pode ser salvo e vinculado ao perfil do usuário ativo, bloqueando modificações acidentais através do painel de permissões.
*   **Gerenciamento de Filtros (*Salvar Filtros*):** Permite fixar ("martelar") uma regra de filtro no cabeçalho da grid associada a um operador.
    *   *Exemplo de Caso de Uso:* Configurar a grid de movimentação para exibir estritamente "Vendas em Aberto do Dia de Hoje" para um caixa específico.
*   **Exportação Nativa:** Funções embutidas na estrutura da grid permitem exportar o dataset visualizado diretamente para Microsoft Excel, Word ou disparar a impressão via WhatsApp/e-mail.

---

## 2. Campos Extras (Campos Personalizados)

O recurso de Campos Extras atua como uma camada de extensibilidade de dados, mitigando a necessidade de alterações estruturais rígidas (DDL) no banco de dados Firebird.

*   **Disponibilidade Global:** Acessível via menu inferior em praticamente todas as telas modulares (Pessoas, Produtos, Ordem de Serviço, Contas a Pagar/Receber).
*   **Implementação:** O usuário administrador cria variáveis de formulário sob demanda. Os campos gerados são injetados na interface de cadastro na aba "Dados / Campos Personalizados".
*   **Consumo de Dados:** A informação persistida nesses campos não é meramente decorativa; ela se integra ao dicionário de dados e pode ser consumida pelo motor do **Gerador de Relatórios** (*FastReport*) para composição de documentos impressos customizados.

---

## 3. Arquitetura White Label e Tradução Textual

A estrutura de software foi projetada para *rebranding* total, garantindo que o distribuidor/revenda de software aplique sua própria marca no Retaguarda (Delphi), App Mobile (Flutter) e módulos web.

*   **Customização de Identidade Visual:** Substituição sistemática de logomarcas, aplicação de paletas de cores específicas da revenda e supressão de módulos ou menus não comercializados em determinados planos de assinatura.
*   **Motor de Tradução/Renomeação de Interface:**
    *   Todas as *strings* de tela são isoladas da camada de código compilado, armazenadas em arquivos de texto editáveis no diretório raiz da aplicação.
    *   Uma ferramenta de *overlay* embutida na tela ativa mapeia e permite editar o texto dos botões e painéis.
    *   *Exemplo Prático:* Renomear o label nativo `Logradouro` para `Endereço` ou `Rua`, adaptando a interface ao dialeto ou preferência do cliente final.
*   **Deploy Personalizado (Inno Setup):** Automação do instalador do Windows. A revenda pode compilar o pacote de instalação embutindo a identidade visual e o banco de dados previamente parametrizado, acelerando o laboratório de implantação.
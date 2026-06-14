Este módulo detalha o funcionamento da ferramenta de **Campos Extras (Campos Personalizados)** do ERP Código UP, uma funcionalidade projetada para permitir a extensão do banco de dados em tempo de execução (_Runtime_), eliminando a necessidade de solicitar novas implementações à equipe de desenvolvimento de software `[00:00:24]`.

### 1. Arquitetura e Tipagem de Dados dos Campos Extras `[00:01:06]`

A criação de um novo campo exige a definição prévia de sua estrutura de dados para garantir a integridade do banco de dados Firebird. O ERP disponibiliza as seguintes tipagens nativas `[00:01:06]`:

- **Texto Normal:** Campo alfanumérico padrão para inserção de strings curtas `[00:01:15]`.
    
- **Memo:** Caixa de texto expandida (Blob Text) para o armazenamento de observações longas ou textos com quebras de linha `[00:01:15]`.
    
- **Inteiro:** Campo numérico para valores sem casas decimais (ex: contadores, códigos externos) `[00:01:23]`.
    
- **Numérico / Decimal:** Suporta a definição customizada de precisão e escala (ex: definir tamanho total de 15 caracteres com 6 casas decimais, ideal para pesos, medidas ou índices complexos) `[00:01:23]`.
    
- **Data:** Campo formatado para controle de calendários e timestamps `[00:01:31]`.
    
- **Combobox (Lista de Seleção):** Permite predefinir uma lista restrita de valores aceitáveis (ex: cadastrar opções como "Opção A", "Opção B"). O usuário final escolhe o dado através de um menu suspenso, padronizando a entrada `[00:01:31]`.
    

#### Máscaras de Entrada de Dados `[00:02:34]`

Para campos de texto que exigem um formato rígido, o sistema permite injetar **máscaras de validação** (ex: criar um campo "CPF Teste" associado a uma máscara que força a digitação padronizada com pontos e hífen), otimizando a qualidade do cadastro `[00:02:40]`.

### 2. Comportamento e Herança nas Telas do Sistema `[00:03:09]`

Uma vez configurado, o campo extra é injetado automaticamente em duas camadas principais da interface do ERP:

- **Integração Automática nas Grids de Consulta `[00:03:09]`:** O novo campo passa a figurar imediatamente como uma coluna na grade de pesquisa rápida da entidade (ex: tela de localização de pessoas). Isso permite que os dados extras sejam ordenados, agrupados, filtrados ou exportados para o Excel exatamente como os campos nativos do software `[00:03:09]`.
    
- **Habilitação da Aba de Customizados `[00:03:33]`:** Nos formulários de edição (ex: ficha do cliente ou do produto), o ERP identifica a existência de extensões e habilita dinamicamente a aba **"Campos Personalizados"**, concentrando ali as novas variáveis `[00:03:41]`.
    

### 3. Designer de Interface em Tempo de Execução `[00:04:26]`

O grande diferencial da ferramenta é o seu motor de estilização visual baseado em _Drag-and-Drop_ (arrastar e soltar), permitindo que técnicos de suporte ou administradores redesenhem o layout do formulário sem digitar linhas de código `[00:04:26]`.

- **Agrupamento e Setorização (Grupos Visuais) `[00:04:58]`:** É possível criar contêineres e caixas de agrupamento para categorizar os campos extras, organizando-os de forma vertical ou horizontal na tela `[00:05:31]`.
    
- **Geração de Sub-Abas Customizadas `[00:05:39]`:** O designer permite converter grupos de campos extras em abas secundárias dentro da própria área de personalização, otimizando o espaço da tela `[00:05:39]`.
    
- **Manipulação de Propriedades Visuais `[00:05:57]`:** Através do menu de contexto (botão direito do mouse), o operador pode gerenciar o comportamento visual dos componentes: ocultar rótulos (labels), remover bordas, definir propriedades de expansão elástica e travas de dimensionamento `[00:06:02]`.
    

### 4. Persistência de Layout e Tratamento de Exceções `[00:06:25]`

As modificações visuais realizadas no designer de tela precisam ser salvas para entrar em produção na empresa `[00:06:25]`.

- **Salvamento do Layout:** O ERP grava o esquema visual criado. Toda vez que qualquer usuário abrir aquela tela, o formulário será renderizado conforme a nova estrutura `[00:06:25]`.
    
- **Tratamento de Campos Ocultos (Campos Órfãos) `[00:06:32]`:** Se um novo campo extra for criado _após_ o administrador já ter salvado um layout customizado, esse campo não aparecerá automaticamente no formulário `[00:06:38]`. O ERP isola o novo campo em uma barra lateral de ferramentas (janela de customização) `[00:06:44]`. Para exibi-lo, o operador deve reabrir o designer, capturar o campo na lista de "não posicionados" e arrastá-lo para o local desejado da tela `[00:07:02]`.
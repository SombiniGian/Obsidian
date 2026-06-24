  

---

id: CASO-002

link: https://www.youtube.com/watch?v=2Qvk8hKJW20

setor: Suporte, Desenvolvimento, Implantação

modulo: Core do Sistema (Grids, Auditoria e Cadastros Base)

tags:

  - customizacao-grids

  - auditoria-sistema

  - cadastro-unificado

  - layouts-dinamicos

  - gerador-relatorios

data_criacao: "{ date }":

---

  

# Personalização Avançada de Grids, Layouts e Logs de Auditoria

  

Este documento técnico detalha as diretrizes de funcionamento do **Grid Genérico do Sistema**, os mecanismos nativos de **Auditoria de Dados** e a arquitetura do **Cadastro Unificado de Pessoas** da plataforma [[Código UP Sistemas]]. O objetivo desta documentação é capacitar equipes de suporte, implantação e desenvolvimento a explorar os recursos de customização em tempo de execução, eliminando a necessidade de manutenções no código-fonte para geração de relatórios e análises fiscais ou comerciais básicas.

  

---

  

## Sumário

1. [[#1. Cadastro Unificado de Pessoas (Arquitetura Conceitual)]]

2. [[#2. Mecanismo Nativo de Auditoria (Logs de Modificação)]]

3. [[#3. Customização Avançada e Manipulação de Grids]]

4. [[#4. Mecanismo de Layouts Dinâmicos e Relatórios Ad-Hoc]]

5. [[#5. Exportação de Dados e Integrações Externas]]

  

---

  

## 1. Cadastro Unificado de Pessoas (Arquitetura Conceitual)

  

A plataforma utiliza o conceito de **Entidade Unificada** no cadastro de pessoas. Diferente de arquiteturas legadas que segregam fisicamente tabelas de clientes, fornecedores e funcionários, o sistema centraliza os dados estruturais em um único registro e gerencia os papéis através de flags booleanas de perfil.

  

### Fluxo de Interface e Comportamento Dinâmico

Ao marcar ou desmarcar os perfis de atuação na interface (ex: **Cliente**, **Fornecedor**, **Vendedor**, **Transportador**), o sistema renderiza dinamicamente as abas específicas contendo as regras de negócio de cada módulo:

* **Aba Cliente:** Parâmetros de limites de crédito, tabela de preço padrão, região comercial e forma de pagamento preferencial.

* **Aba Fornecedor:** Dados fiscais para emissão de NFe de entrada, prazos de entrega e condições comerciais de compra.

* **Aba Vendedor:** Definição de percentuais de comissão, metas e vinculação a carteiras de clientes.

  

> [!info] Vantagem Arquitetural e Integridade Financeira

> Essa unificação elimina a redundância de dados. Se um indivíduo atua simultaneamente como **Vendedor** interno e **Cliente** (realizando compras na empresa), o sistema utiliza a mesma chave primária (`ID`). Isso permite que o módulo [[Financeiro]] consolide o fluxo de caixa, exibindo os lançamentos de **Contas a Receber** (vendas) e **Contas a Pagar** (comissões) sob a mesma entidade, mantendo o histórico unificado.

  

---

  

## 2. Mecanismo Nativo de Auditoria (Logs de Modificação)

  

O sistema possui um microsserviço transacional de auditoria que captura qualquer instrução de `INSERT` ou `UPDATE` nas tabelas do banco de dados. Este recurso é padronizado e está presente em todas as telas operacionais, incluindo o cadastro de produtos, pessoas, pedidos e lançamentos financeiros.

  

### Funcionamento do Log de Alterações

Diferente de logs tradicionais que registram apenas a última modificação ou o estado final do registro, a auditoria armazena o histórico histórico delta de cada campo alterado.

  

Ao acessar a aba **Auditoria** de qualquer registro (como em **Pessoas** ou **Produtos**), o sistema exibe um grid histórico contendo:

1. **Data e Hora exata** do evento.

2. **Usuário responsável** pela transação (vinculado ao login de autenticação).

3. **Detalhamento do Delta (Antes vs. Depois):** Ao expandir o registro através do nó de expansão (**"+"**), o sistema exibe o nome do campo modificado, o valor original (antigo) e o novo valor gravado.

  

#### Exemplo Prático de Log de Auditoria em Produtos

Se o preço de um item for modificado, o log registrará a mutação exatamente como no modelo lógico abaixo:

  

```json

{

  "tabela": "PRODUTOS",

  "id_registro": 1042,

  "usuario": "suporte_tecnico",

  "data_alteracao": "2026-06-24T09:15:32-03:00",

  "modificacoes": [

    {

      "campo": "PRECO_CUSTO",

      "valor_antigo": "0.00",

      "valor_novo": "10.00"

    },

    {

      "campo": "PRECO_VENDA",

      "valor_antigo": "0.00",

      "valor_novo": "20.50"

    }

  ]

}

  

```

  

> [!warning] Ponto Crítico de Fallback e Validação Humana

> Operadores frequentemente alteram preços, limpam campos de endereços ou modificam pedidos e alegam falha de sistema. A consulta à aba de auditoria deve ser o **primeiro passo do analista de suporte** para rastrear manipulações indevidas. O sistema impede a sobrescrita do histórico, garantindo a rastreabilidade integral e a segurança jurídica das transações da empresa.

  

---

  

## 3. Customização Avançada e Manipulação de Grids

  

Todos os grids de consulta da plataforma compartilham um comportamento padrão herdado de uma classe base de interface. O usuário final tem autonomia total para reorganizar a disposição das colunas sem demandar customizações de desenvolvimento.

  

### Recursos de Manipulação Direta na Interface

  

* **Pesquisa Global Omnibox:** O campo de pesquisa localizado no topo de cada grid realiza varreduras em **todas as colunas visíveis simultaneamente** (texto parcial, códigos, números ou cidades), aplicando filtros em tempo real à medida que o operador digita.

* **Reordenamento por Drag and Drop:** É possível redefinir a ordem de visualização das colunas clicando sobre o cabeçalho do campo e arrastando-o horizontalmente para a nova posição (ex: mover a coluna **Cidade** para ficar ao lado da **Razão Social**).

* **Dimensionamento de Colunas:** O operador pode ajustar a largura das colunas manualmente ou clicar com o **botão direito do mouse** sobre o cabeçalho e acionar as funções de **"Melhor ajuste"** (para a coluna selecionada) ou **"Melhor ajuste para todas as colunas"**, otimizando a legibilidade.

  

### Agrupamento Dinâmico e Sumarizações (Group By)

  

Para realizar análises rápidas, a interface disponibiliza uma barra superior de agrupamento ("Caixa de Agrupamento").

  

1. Arraste qualquer cabeçalho de coluna (ex: **Cidade** ou **Grupo de Produtos**) para a área de agrupamento localizada logo acima da grade.

2. O grid reestruturará os registros em um modelo de árvore hierárquica. O usuário pode gerenciar a visualização utilizando os botões de contexto **Expandir todos os agrupamentos** ou **Fechar todos os agrupamentos**.

3. **Sumarizações em Rodapé (Agregações):** Clicando com o **botão direito no rodapé** das seções agrupadas, o sistema permite habilitar funções matemáticas automatizadas. É possível aplicar operações como `COUNT` (**Contar registros**), `SUM` (**Somar totais**), `AVERAGE` (**Média**) ou valores máximos e mínimos.

  

> [!tip] Exemplo de Aplicação Prática

> Ao agrupar o grid de Clientes por **Cidade** e ativar a função **Contar cidades** no rodapé do grupo, o operador obtém um censo instantâneo da distribuição da sua carteira comercial diretamente na tela de consulta, exibindo, por exemplo, que existem 3 clientes em Ubá, 2 em Tocantins e 1 em Juiz de Fora.

  

---

  

## 4. Mecanismo de Layouts Dinâmicos e Relatórios Ad-Hoc

  

O sistema permite consolidar as modificações feitas no grid (filtros, ordenações, colunas ocultas e agrupamentos) em um formato persistente chamado **Layout**. Este recurso atua como um gerador de relatórios simplificado para o usuário final, eliminando a dependência do setor de desenvolvimento.

  

### Criação e Configuração de um Novo Layout

  

Para instanciar uma nova estrutura de visualização, utilize as ações do painel lateral ou menu de contexto:

  

1. Clique em **Incluir** na tela de gerenciamento de layouts da grade.

2. Preencha o **Título do Layout** (ex: `Clientes por Cidade` ou `Tabela de Preço Reduzida`).

3. Configure os metadados visuais através das seguintes tags e diretrizes:

* **Nome da Empresa no Relatório:** Utilize a tag coringa `#` (ou strings parametrizadas como `[Nome Fantasia]`) para injetar dinamicamente a razão social da empresa logada no cabeçalho.

* **Orientação da Página:** Defina entre os modos **Retrato** (vertical, indicado para poucas colunas) ou **Paisagem** (horizontal, ideal para grids com muitos dados fiscais ou financeiros).

* **Estilização Visual:** Altere propriedades de tamanho da fonte, aplicação de **Negrito**, cores de fundo para os cabeçalhos das colunas e definição se a grade impressa manterá o comportamento zebrado/colorido do sistema.

  
  
  

```

[Interface de Configuração de Grids]

  ├── Botão Direito no Cabeçalho -> Ocultar/Exibir Campos (Seletor de Colunas)

  ├── Ajustar colunas desejadas para exibição

  └── Painel de Layouts -> Clicar em "Salvar a Grade"

  

```

  

### Escopo e Permissões de Layout

  

Ao salvar um layout customizado, o criador pode definir o nível de compartilhamento do arquivo:

  

* **Layout Privado:** Visível e editável exclusivamente pelo usuário que o desenvolveu.

* **Layout Público (Visível para todos os usuários):** Fica disponível para uso de toda a corporação. No entanto, o sistema aplica uma regra rígida de proteção: **outros usuários podem consumir o layout, mas não possuem permissão para alterá-lo ou sobrescrevê-lo**. Apenas o proprietário original pode realizar modificações na estrutura salva.

  

> [!warning] Validação de Layouts com Excesso de Colunas

> Ao gerar relatórios impressos a partir de layouts com muitas colunas ativas, o texto sofrerá esmagamento ou truncamento se a orientação estiver em modo **Retrato**. Como boa prática, oriente o usuário a acessar o seletor de colunas, desmarcar os campos irrelevantes para aquela análise, aplicar o **Melhor ajuste** e salvar o layout dedicado para impressão.

  

---

  

## 5. Exportação de Dados e Integrações Externas

  

Caso o operador necessite de manipulações matemáticas complexas, dashboards gráficos avançados ou cruzamento com planilhas de terceiros, a plataforma provê uma rota de integração nativa com ferramentas de BI e suítes de escritório.

  

### Fluxo de Exportação para Planilhas Eletrônicas

  

1. Configure o grid com os filtros e colunas necessários para a análise.

2. Acesse o menu **Opções** do grid ou utilize o clique secundário e selecione a opção **Exportar para Excel**.

3. O sistema gerará o arquivo formatado em tempo de execução e invocará a instância local do Microsoft Excel ou componente equivalente de forma automatizada.

  

> [!tip] Preservação de Estrutura no Excel

> O motor de exportação do sistema preserva a estrutura exata montada na interface do usuário. Se o grid estiver agrupado por cidades com totalizadores ativados no momento do clique, o arquivo `.xlsx` resultante será aberto no Excel respeitando os agrupamentos e as quebras de linha nativas, economizando tempo de retrabalho com formatação.

  

```

http://googleusercontent.com/youtube_content/1

  

```
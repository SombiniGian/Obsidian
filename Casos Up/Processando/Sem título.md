Markdown

````
---
id: CASO-002
link: https://www.youtube.com/watch?v=2Qvk8hKJW20
setor: Suporte, Treinamento, Desenvolvimento
modulo: Configurações Básicas
tags: [customizacao-grids, auditoria-sistema, cadastros-unificados, layouts, relatorios]
data_criacao: 2026-06-23
---

# Configurações Básicas — Personalização de Grids, Layouts e Auditoria

## Sumário
1. [[#1. Conceito de Cadastro Unificado de Pessoas]]
2. [[#2. Módulo de Auditoria Nativa (Log de Alterações)]]
3. [[#3. Customização Avançada de Grids (Grades de Dados)]]
4. [[#4. Criação e Gerenciamento de Layouts Customizados]]
5. [[#5. Geração de Relatórios e Exportação Ad-Hoc]]

---

## 1. Conceito de Cadastro Unificado de Pessoas

O sistema utiliza um modelo de arquitetura de dados centralizado para o registro de entidades. Em vez de segregar fisicamente indivíduos ou empresas em tabelas e telas distintas (como tabelas separadas para Clientes, Fornecedores ou Vendedores), o ecossistema emprega o conceito de **Cadastro Unificado de Pessoas**.

### Funcionamento Técnico
* Ao registrar ou editar uma entidade no módulo de **Pessoas**, o operador define os papéis que aquela pessoa desempenha no ecossistema através de sinalizadores (*checkboxes*).
* Uma única entidade pode ser marcada simultaneamente como **Cliente**, **Fornecedor**, **Vendedor** e/ou **Transportador**.
* A interface reage dinamicamente à seleção dos papéis, injetando abas de dados específicas em tempo de execução:
    * Ao marcar **Cliente**, liberam-se campos de região, tabelas de preço padrão e formas de pagamento preferenciais.
    * Ao marcar **Fornecedor**, abrem-se parâmetros de condições de compra e dados fiscais específicos de suprimentos.

> [!info] Vantagem Arquitetural
> Este modelo elimina a redundância de dados no banco, mitigando inconsistências de histórico financeiro. Se um **Vendedor** realizar uma compra na empresa, ele não precisa de um novo cadastro: basta ativá-lo como **Cliente**. Suas movimentações de contas a receber e comissões permanecerão vinculadas ao mesmo identificador único corporativo.

---

## 2. Módulo de Auditoria Nativa (Log de Alterações)

O sistema possui um subsistema de rastreabilidade e **Auditoria** que monitora operações de modificação de dados. Esta rotina não é exclusiva de um módulo; ela funciona de forma padronizada em todas as telas transacionais e cadastrais da aplicação, incluindo [[Cadastro de Produtos]], [[Cadastro de Pessoas]], [[Módulo Financeiro]] e [[Pedidos de Venda]].

### Mecanismo de Funcionamento e Rastreamento
Diferente de sistemas que apenas guardam a data e o último usuário que modificou o registro (sobreescrevendo o histórico), este módulo armazena incrementalmente o estado anterior e o novo estado de cada campo alterado.

Ao acessar a aba **Auditoria** de qualquer registro, o sistema apresenta um grid histórico contendo:
1. **Data e Hora** exata da modificação.
2. **Usuário** responsável pela ação (ex: `suporte`).
3. **Estrutura de Diferença (Diff):** Ao expandir o nó do log (clicando no ícone **+**), o sistema detalha os campos alterados:

```json
{
  "campo_alterado": {
    "nome_fantasia": {
      "antes": "Diego",
      "depois": "Diego 123"
    },
    "telefone_celular": {
      "antes": null,
      "depois": "(32) 99999-9999"
    },
    "preco_custo": {
      "antes": 0.00,
      "depois": 10.00
    }
  }
}
````

> [!warning] Pontos Críticos e Validação
> 
> - **Rastreabilidade de Erros:** O módulo impede a perda de informações decorrentes de erros operacionais (ex: quando um usuário apaga acidentalmente o conteúdo de um campo). O histórico permite reaver o dado anterior consultando a auditoria.
>     
> - **Auditoria de Preços e Pedidos:** Alterações drásticas em tabelas de preços ou exclusões de itens de pedidos ficam registradas de forma indelével, permitindo que a gerência identifique desvios de margem de lucro ou alterações não autorizadas.
>     

## 3. Customização Avançada de Grids (Grades de Dados)

A interface do sistema renderiza as consultas iniciais sempre no formato de grids de dados dinâmicos. Esses grids oferecem recursos avançados de manipulação em tempo de execução pelo próprio usuário, sem necessidade de customização via código fonte.

### Recursos de Manipulação do Grid

- **Pesquisa Global Omnibox:** A barra de pesquisa localizada no topo do grid realiza varreduras em todas as colunas visíveis simultaneamente. Se o usuário digitar um termo, o sistema filtra registros que contenham o argumento seja na coluna de Nome, Cidade, CPF ou Código Interno.
    
- **Redimensionamento e Reordenamento Drag-and-Drop:** As colunas do grid podem ser arrastadas para redefinir a ordem de leitura. O tamanho das colunas pode ser ajustado manualmente ou otimizado clicando com o botão direito e selecionando **Melhor Ajuste** (ou **Melhor Ajuste para Todas as Colunas**).
    
- **Agrupamento Dinâmico (Group By):** É possível arrastar qualquer cabeçalho de coluna para a zona de agrupamento superior. O grid imediatamente colapsa os registros em grupos estruturados (ex: agrupar clientes por **Cidade** ou produtos por **Grupo de Estoque**).
    
- **Funções de Agregação no Rodapé (Footers):** Clicando com o botão direito na barra de rodapé das colunas de agrupamento, o sistema permite injetar funções matemáticas ou estatísticas.
    
    - A opção **Contar** permite obter a quantidade exata de registros contidos em cada nó agrupado (ex: contar quantos clientes existem ativos por cidade).
        

## 4. Criação e Gerenciamento de Layouts Customizados

Para evitar que o usuário perca suas parametrizações de colunas, ordenações e agrupamentos ao fechar a tela, o sistema disponibiliza o recurso de **Salvar Grade** e gerenciamento de **Layouts**.

### Fluxo de Configuração de Layout

1. O operador ajusta o grid com as colunas desejadas, remove os campos desnecessários e define os agrupamentos e totalizadores de rodapé.
    
2. Acessa-se a opção de layout e clica-se em **Incluir** para dar um nome à visão (ex: `Pessoas por Cidades`, `Visualização Simples`).
    
3. O sistema memoriza o estado exato dos componentes visuais.
    

```
[Tela de Cadastro] ➔ [Configurar Grid/Filtros] ➔ [Salvar Grade / Criar Layout] ➔ [Definir Permissão de Leitura]
```

### Propriedades de Customização do Layout

Ao criar ou editar as propriedades de um Layout, abre-se uma interface de parametrização avançada:

- **Título customizado:** Permite o uso de tags dinâmicas como `#nome_fantasia` no cabeçalho do relatório gerado.
    
- **Formatação Visual:** Configuração de quebra de página por grupo, definição de fontes (tamanho, estilo negrito) para títulos e cores de fundo específicas para diferenciar as seções do grid.
    
- **Orientação de Página:** Configuração prévia para impressão em modo **Retrato** ou **Paisagem**, além do ajuste automático de estiramento das colunas para caber na página do relatório.
    

> [!tip] Permissões e Distribuição de Layouts
> 
> Ao salvar um layout, o criador pode marcar a opção **Visível para todos os usuários**. Isso faz com que a visão fique disponível para toda a empresa, contudo, o sistema implementa uma trava de segurança: **apenas o usuário criador possui permissão para alterar ou salvar modificações estruturais neste layout**, protegendo a padronização operacional.

## 5. Geração de Relatórios e Exportação Ad-Hoc

O motor de grids do sistema funciona como um **gerador de relatórios dinâmico**. Qualquer configuração visual estabelecida no grid (filtros, agrupamentos, ordenação e contadores) pode ser convertida instantaneamente em um documento oficial ou planilha eletrônica.

### Processo de Saída de Dados

- **Impressão Direta:** Ao clicar em **Imprimir**, o sistema processa a árvore de dados ativa no grid e gera um relatório formatado de acordo com as regras de design definidas no Layout selecionado.
    
    - Se o grid estiver agrupado por cidade e com os nós expandidos, o relatório sairá hierarquizado, exibindo os sub-totais de registros por grupo e o rodapé estatístico perfeitamente alinhado.
        
- **Exportação para Planilhas (Excel):** O sistema possui integração nativa de exportação. Ao selecionar a opção de exportar para planilha, o sistema converte a estrutura do grid em formato de linhas e colunas compatível com o Microsoft Excel, preservando a integridade dos dados e as separações de campos sem quebras de strings.
    

> [!warning] Otimização de Impressão
> 
> Caso o relatório gerado apresente colunas cortadas ou layout poluído, a causa raiz geralmente é o excesso de colunas ativas no grid em modo Retrato. Para mitigar isso, acesse o seletor de colunas do grid, desmarque os campos secundários, execute o comando **Melhor Ajuste** e salve a grade antes de realizar uma nova tentativa de impressão.

```
http://googleusercontent.com/youtube_content/1
```

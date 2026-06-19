Este vídeo detalha o funcionamento e a arquitetura de customização do **Novo Frente de Caixa (PDV)** do ERP Código UP. O módulo foi reprojetado para oferecer flexibilidade estética e operacional diretamente em tempo de execução (_Runtime_), permitindo adaptar a interface à identidade de cada cliente ou modelo de negócio (mercados, distribuidoras, varejo) sem a necessidade de novas linhas de código.

### 1. Inicialização e Seleção de Interface `[00:00:17]`

Para ativar o novo ambiente de vendas, o integrador ou administrador do sistema deve acessar o painel de propriedades do terminal e alterar o tipo de tela padrão para a opção **"PDV Novo"** `[00:00:24]`. A partir dessa definição, toda inicialização do Frente de Caixa carregará o novo motor gráfico personalizável `[00:00:36]`.

### 2. Painel de Estilização e Identidade Visual `[00:01:04]`

Quando acessado por um usuário com privilégios de **Administrador**, o PDV exibe um botão flutuante de configurações estéticas `[00:01:04]`. Esse painel gerencia os seguintes elementos de interface:

- **Controle de Redimensionamento Dinâmico `[00:01:04]`:** Permite definir alturas e larguras fixas em pixels para o formulário ou forçar a inicialização em modo maximizado, otimizando a exibição para ambientes com múltiplos monitores ou telas touch screen `[00:01:13]`.
    
- **Injeção de Backgrounds Customizados `[00:01:26]`:** Suporte para carregamento de imagens de fundo personalizadas (ex: logotipo da empresa do cliente ou campanhas sazonais de marketing) no painel principal do caixa `[00:04:25]`.
    
- **Tipografia e Paleta de Cores `[00:01:37]`:** Controle granular de fontes (família, tamanho e peso) e cores dos textos, permitindo aplicar realces visuais (como efeitos de brilho/neon) nos campos de totalizadores de venda para facilitar a leitura pelo operador `[00:01:46]`.
    

### 3. Matriz de Atalhos e Alçadas por Usuário `[00:02:18]`

O motor de funções do PDV separa a lógica de execução das teclas de atalho físicas do teclado, permitindo emular o comportamento de sistemas legados aos quais os operadores já estão habituados `[00:02:36]`.

- **Mapeamento de Teclas Flexível `[00:02:18]`:** Todas as funções vitais do caixa (ex: dar desconto, cancelar item, fechar venda) podem ter seus atalhos modificados livremente (ex: redefinir a concessão de desconto para a tecla `F1` ou qualquer outra combinação) `[00:02:45]`.
    
- **Segurança Baseada em Perfil (Flags de Senha) `[00:02:50]`:** O administrador pode definir individualmente se uma função exige ou não a digitação de uma senha de liberação de supervisor, associando essa regra ao perfil do usuário logado `[00:02:50]`.
    

### 4. Engenharia de Distribuição de Layouts (Importação/Exportação) `[00:02:57]`

Para otimizar o tempo de implantação em clientes com múltiplos PDVs ou replicar padrões homologados pelo suporte técnico, o sistema introduz um motor de serialização de layouts baseado em arquivos de configuração externos `[00:04:14]`.

A estrutura completa de uma estação de trabalho é composta por **4 arquivos de configuração independentes** `[00:09:55]`:

1. **Arquivo de Teclas de Atalho:** Contém o mapa de funções e teclas físicas `[00:10:03]`.
    
2. **Arquivo de Propriedades Globais:** Armazena dimensões da tela, fontes, paleta de cores e caminhos de imagens `[00:09:55]`.
    
3. **Arquivo do Layout Principal (Tela de Vendas):** Determina a posição e visibilidade dos blocos da janela principal do PDV `[00:10:15]`.
    
4. **Arquivo do Layout de Fechamento (Tela de Finalização):** Armazena a disposição dos componentes do painel de recebimento `[00:10:15]`.
    

O técnico pode configurar o PDV ideal em laboratório, acionar a função **"Exportar Arquivo"** `[00:03:09]` e, no ambiente de produção do cliente, utilizar o comando **"Importar Arquivo"** `[00:03:15]` para carregar instantaneamente toda a identidade visual e os atalhos parametrizados `[00:03:54]`.

### 5. Designer Visual por Arrastar e Soltar (Drag-and-Drop) `[00:05:29]`

Tanto a tela de vendas quanto a de fechamento utilizam um componente de design em tempo de execução, permitindo reorganizar os blocos de dados de forma visual `[00:05:29]`.

- **Limpeza de Poluição Visual (Ocultação de Componentes) `[00:05:38]`:** Campos irrelevantes para determinados modelos de negócio podem ser removidos da interface apenas arrastando-os para fora do formulário (ex: se o estabelecimento não exige identificação de vendedor por item ou não aplica rotinas de descontos/acréscimos no balcão, esses campos podem ser movidos para a área oculta) `[00:05:46]`, `[00:09:01]`.
    
- **Repositioning e Ancoragem `[00:06:00]`:** Elementos como o grid de itens, o painel de exibição de venda em andamento ou os dados do cliente podem ser movidos para o topo, rodapé ou laterais da tela, adaptando-se a monitores verticais ou layouts específicos `[00:06:09]`.
    
- **Mecanismos de Segurança de Layout:** * _Desfazer Alterações Recentes:_ Permite retroceder passos caso um reposicionamento saia incorreto durante a edição `[00:06:59]`.
    
    - _Restaurar Padrão do Sistema:_ Comando de emergência que apaga as customizações locais e força o PDV a renderizar o layout original de fábrica do ERP Código UP `[00:07:06]`.
        

### 6. Customização da Tela de Finalização de Venda (`S9`) `[00:07:15]`

Ao pressionar o atalho de fechamento (padrão `S9`), o ERP abre o painel de liquidação financeira da venda, que também possui sua própria camada de design independente `[00:07:20]`.

- **Alinhamento dos Blocos de Recebimento `[00:07:37]`:** O operador pode modificar a disposição dos contêineres de formas de pagamento. Através das propriedades do grupo visual, é possível alternar a direção de exibição dos botões de pagamento entre **Horizontal** ou **Vertical** `[00:08:31]`, adaptando o fechamento para telas de diferentes resoluções.
    
- **Retenção de Troco na Tela `[00:09:21]`:** Configuração de comportamento que mantém os dados de troco em destaque na tela após o encerramento da venda, permitindo que o operador visualize o valor com calma antes de retornar automaticamente para o estado de "Caixa Livre" para a próxima operação `[00:09:27]`
ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link  https://www.youtube.com/watch?v=eZLAMLHAm2k
Este módulo detalha as diretrizes operacionais, a parametrização técnica no gerador de relatórios e as regras de permissão da ferramenta de **Controle de Impressões Personalizadas por Tela** no ERP Código UP `[00:00:00]`. O recurso foi desenvolvido para dar total autonomia às revendas técnicas e administradores para criarem e vincularem múltiplos layouts de impressão (como fichas, recibos ou relatórios gerenciais) a qualquer ecrã do sistema `[00:00:21]`, `[00:02:54]`.

### 1. Conceito e Onipresença do Controle de Impressões `[00:00:21]`

Anteriormente, os formatos de impressão de documentos eram engessados ou limitados por ecrã. Com esta atualização, o menu **"Controle de Impressões"** passa a estar disponível de forma transversal em todas as interfaces do ERP `[00:00:21]`, `[00:01:24]`:

- **Flexibilidade por Contexto:** O utilizador pode associar impressões customizadas ao cadastro de clientes (ex: uma ficha cadastral com foto), cadastro de fornecedores, produtos, pedidos de venda, notas fiscais ou ordens de serviço (OS) `[00:00:45]`, `[00:01:01]`.
    
- **Centralização de Modelos:** Uma única tela permite listar, incluir e gerir quais relatórios desenhados na retaguarda estarão disponíveis para o operador quando este acionar o comando de impressão na tela ativa `[00:01:36]`.
    

### 2. Vinculação em Lote e Restrição por Perfil de Usuário `[00:01:36]`

A inclusão de modelos de impressão no painel segue uma lógica hierárquica e de segurança `[00:01:36]`:

- **Múltiplos Documentos no Mesmo Clique:** O sistema permite associar mais do que um relatório à mesma tela (ex: configurar os modelos "Entrada de OS" e "Saída de OS" simultaneamente) `[00:01:46]`, `[00:02:01]`. Ao carregar no botão "Imprimir", o ERP processa e abre as janelas de visualização de todos os relatórios vinculados de uma só vez `[00:02:15]`.
    
- **Controlo de Acesso Nativo:** Durante o vínculo do relatório, o administrador pode definir uma flag de segurança para que **apenas um determinado utilizador ou perfil tenha permissão para emitir aquela impressão** `[00:01:54]`. Isso permite ocultar dados sensíveis (como relatórios de saída que exibem margens de lucro e valores financeiros) de operadores de nível básico, exibindo para estes apenas layouts operacionais sem preços `[00:02:34]`, `[00:02:43]`.
    

### 3. Integração Técnica via Parâmetro ID no Gerador `[00:03:02]`

Para que o ERP Código UP consiga filtrar e imprimir estritamente os dados do registo que está selecionado no ecrã (seja um cliente específico ou uma OS ativa), a revenda técnica deve configurar uma amarração de variáveis no _Gerador de Relatórios_ `[00:03:02]`, `[00:03:11]`:

```
+------------------------------------------------------------------------+
|                     LOGICA DE CAPTURA DO PARÂMETRO ID                  |
+------------------------------------------------------------------------+
|                                                                        |
|  [Operador seleciona um Registro] ──► [Clica no Botão Imprimir]        |
|                                                     │                  |
|                                                     ▼                  |
|  [ERP injeta a variável global de forma nativa: "id"]                  |
|                                                     │                  |
|                                                     ▼                  |
|  [Gerador de Relatórios captura o parâmetro exacto: "id"]               |
|                                                     │                  |
|                                                     ▼                  |
|  [Executa a Query SQL filtrada apenas por aquele ID específico]        |
|  (Ex: Filtra apenas o Cliente ID ou a Ordem de Serviço ID do ecrã)    |
|                          [00:03:29] - [00:03:48]                       |
+------------------------------------------------------------------------+
```

- **Passagem Automática de Variável:** O motor do ERP foi programado para, no momento do disparo da impressão, injetar de forma 100% automatizada a chave primária do registo do ecrã para dentro do ambiente de relatórios `[00:03:48]`.
    
- **Configuração da Query:** No painel de propriedades do relatório, a revenda deve criar e declarar o parâmetro com a nomenclatura exata de **`id`** (em letras minúsculas) `[00:03:29]`, `[00:03:39]`. Ao fazer esta declaração, o gerador de relatórios captura o código enviado pela tela do ERP e processa a consulta SQL isolando apenas as informações daquela linha específica `[00:03:58]`, `[00:04:07]`.
    

ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: [Assista ao vídeo no YouTube](https://www.youtube.com/watch?v=p5XTDAnIiro).
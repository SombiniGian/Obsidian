---
id: [CASO-001]
link: https://www.youtube.com/watch?v=2Dch3z1og-8
setor: Desenvolvimento, Suporte, Operações
modulo: Inventário, Aplicativo de Vendas, Retaguarda
tags: [inventario, app, contagem-estoque, mobile, retaguarda, sincronizacao]
data_criacao: {{date}}
---

## Sumário
1. [[#Visão Geral da Arquitetura]]
2. [[#Pré-requisitos e Dependências]]
3. [[#Fluxo Operacional de Contagem]]
    - [[#3.1. Configuração na Retaguarda (Backoffice)]]
    - [[#3.2. Operação no Aplicativo Mobile]]
    - [[#3.3. Fechamento e Sincronização]]
4. [[#Mecanismos de Inserção no App]]
5. [[#Regras de Negócio Críticas]]

## Visão Geral da Arquitetura

O módulo de **Inventário de Estoque** foi projetado para descentralizar e agilizar a contagem de produtos dentro de um estabelecimento. Ele utiliza o aplicativo de vendas mobile padrão para permitir que múltiplos usuários (ou colaboradores) realizem contagens simultâneas pelas gôndolas ou depósitos. Estas contagens parciais são enviadas e consolidadas de forma automática no sistema de **[[Retaguarda]]**.

> [!info] Objetivo Principal
> Eliminar a necessidade de hardware dedicado ou planilhas de papel, permitindo que as equipes enviem lotes de contagem diretamente do celular. O servidor de retaguarda atua como agregador inteligente das remessas.

## Pré-requisitos e Dependências

Para que o aplicativo consiga transmitir os lotes de estoque aferidos para o servidor, a rotina de recebimento deve estar ativada na retaguarda.

> [!warning] Validação de Envio
> O aplicativo bloqueia a sincronização e retorna a mensagem de erro **"Nenhum inventário em digitação encontrado"** caso não exista um documento de inventário previamente criado e com o status específico de preenchimento em aberto no sistema base. A operação deve ser preparada pela gestão antes que a contagem inicie.

## Fluxo Operacional de Contagem

### 3.1. Configuração na Retaguarda (Backoffice)

A criação do espelho do inventário deve ser gerida pelo administrador ou gerente (usuário com permissões adequadas), visto que define parâmetros gerenciais críticos do estoque.

1. Acesse o módulo correspondente na interface de retaguarda.
2. Clique no botão de **Incluir** novo registro.
3. Configure os parâmetros principais, como a seleção da filial/empresa e os tipos de controle.
4. Salve o documento, garantindo que o status esteja explicitamente sinalizado como **Digitando** (ou equivalente para operação em andamento).
5. O corpo de itens do documento pode permanecer vazio, já que será preenchido dinamicamente pelos envios mobile.

### 3.2. Operação no Aplicativo Mobile

O acesso ao módulo no aplicativo é feito por meio da opção **Inventário de Estoque** no menu principal.

1. Inicialize um escopo clicando em **Novo Inventário** no app.
2. A aplicação fará a sugestão da empresa padrão do banco de dados local.
3. Realize os apontamentos de produto e quantidade usando os variados [[#Mecanismos de Inserção no App]].
4. Concluída a contagem daquele corredor ou setor, selecione **Salvar Inventário**.
5. Retorne à listagem de tarefas locais, localize o pacote recém-salvo, faça o gesto de arrastar para o lado **direito** e pressione **Enviar**.

> [!tip] Dica de Navegação e Gestão de Lotes
> Na tela de listagem de pacotes, um deslize para a **esquerda** sobre o registro revela o botão **Excluir**, útil para descartar contagens equivocadas localmente. O deslize para a **direita** revela o fluxo de **Envio**.

### 3.3. Fechamento e Sincronização

Após os sucessivos envios da equipe no chão de loja, a gerência retoma a operação no computador base para analisar e processar os dados recebidos.

1. No painel de retaguarda, abra o documento que se manteve com o status **Digitando**.
2. Na aba de visualização principal, a listagem de produtos mostrará a consolidação agrupada das quantidades.
3. Acesse a aba específica denominada **Contagem pelo App**. Esta área garante a rastreabilidade completa e exibe logs em nível de lote, permitindo identificar:
   - Qual colaborador fez o apontamento.
   - Quais as métricas exatas submetidas naquela transação específica.
4. Após as validações de divergência, modifique o status global do inventário de **Digitando** para **Ativo**.
5. Clique em **Gravar**. Este gatilho efetua de forma imediata o bloqueio de novos recebimentos e dispara a rotina no banco de dados para ajustar o estoque gerencial.

## Mecanismos de Inserção no App

A inserção de itens é construída de maneira idêntica à de um módulo de Pedidos de Venda, garantindo familiaridade e curva de aprendizado nula. Existem três lógicas operacionais de cômputo:

* **Modo Swipe (Deslize de Tela):** Para itens de baixo volume ou visualização sequencial rápida. Arrastar a célula do produto para o lado força o incremento de `+1` unidade no contador da interface, sucessivamente.
* **Modo Acesso Direto (Clique na Linha):** Tocar num produto que já consta na grade altera o painel para um cenário analítico com duas ramificações de ação de entrada:
    * **Somar:** O usuário digita uma fração a ser adicionada. Ex: Haviam `6` itens contados, inserindo `10` na ferramenta 'somar', a listagem é atualizada para `16`.
    * **Sobrescrever:** O usuário insere o novo número real do agrupamento físico, substituindo a totalização anterior.
* **Modo Leitor de Cód. Barras:** Ação contínua focada no tempo de resposta, onde cada acerto no decodificador EAN/QR invoca o prompt numérico para input da quantidade.

## Regras de Negócio Críticas

* **Comportamento de Agregação por Acúmulo:** Diferentes usuários submetendo dados do mesmo Produto (SKU) em envios paralelos não geram linhas repetidas no inventário principal, e sim o somatório automático matemático no agrupador correspondente, desde que mirem o mesmo inventário aberto (mesma empresa receptora). Exemplo: o envio de 5 unidades pelo Terminal A e 10 unidades pelo Terminal B será renderizado como 15 no relatório geral da retaguarda, divididos apenas no rastreio da guia de lote.
* **Trava de Controle Temporal:** No exato momento em que o status sistêmico é comutado para **Ativo** na retaguarda, o encerramento sistêmico é concluído e todas as apis de recepção para o caso em questão são bloqueadas. Aparelhos no campo que não sincronizaram a tempo estarão impossibilitados de transmitir até que um novo ID de inventário master seja gerado.

```json
// Mockup Lógico de Payload - Estrutura submetida via App ao Servidor
{
  "controle_remoto": {
    "empresa_destino_id": 1,
    "vendedor_usuario_id": "cod_operador_01",
    "timestamp_envio": "2026-07-18T14:30:00Z"
  },
  "conteudo_lote": [
    {
      "produto_sku_id": "10510",
      "quantidade_consolidada": 15,
      "origem_leitura": "manual"
    },
    {
      "produto_sku_id": "8024",
      "quantidade_consolidada": 20,
      "origem_leitura": "barcode"
    }
  ]
}
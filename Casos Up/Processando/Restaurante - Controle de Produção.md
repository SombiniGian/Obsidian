---
id: CASO-042
link: https://www.youtube.com/watch?v=GE2KXOK7k60&t=3s
setor: Suporte
modulo: Controle de Restaurante
tags:
  - restaurante
  - controle-producao
  - kds
  - configuracao-sistema
data_criacao: 2026-06-24
---

# Controle de Produção de Cozinha (KDS)

Este documento descreve as diretrizes operacionais, fluxos de interface e requisitos de retaguarda para o funcionamento do módulo de Controle de Produção em Cozinhas de Restaurantes, baseado na aplicação de tela de produção (estilo KDS - Kitchen Display System) da UP Sistemas.

## Sumário
- [[#Visão Geral do Sistema]]
- [[#Fluxo de Estados da Produção]]
- [[#Configuração na Retaguarda]]
- [[#Simulação de Operação Integrada]]
- [[#Pontos Críticos e Validações]]

---

## Visão Geral do Sistema

O módulo de controle de produção foi desenvolvido para operar de forma descentralizada nas áreas de preparação (cozinha, copa, bar), eliminando a dependência de comandas em papel e otimizando o tempo de resposta do estabelecimento.

> [!info] Compatibilidade de Hardware
> A interface do Mapa de Produção é responsiva e adaptável, podendo ser executada em sistemas **Windows** ou **Android**. É homologada para uso em monitores convencionais (com navegação via mouse), telas touchscreen (KDS dedicados) ou tablets industriais alocados nas praças de produção.

---

## Fluxo de Estados da Produção

A tela principal do Mapa de Produção organiza as ordens de serviço de forma cronológica através de cards identificados pelo número da comanda/mesa e o item solicitado. O ciclo de vida de um item em produção possui três estados distintos sinalizados visualmente:

[Fundo Preto: Pendente] -> Clique -> [Fundo Verde: Pronto] -> Clique -> [Removido da Tela: Entregue]

1. Item Pendente (A Produzir) * **Comportamento:** O item entra no mapa com o card em **fundo preto**. * **Operação:** Representa que o pedido foi registrado no terminal de vendas (POS ou aplicativo móvel), mas a preparação ainda não foi concluída. * **Exibição de Detalhes:** Ao efetuar um clique sobre o card em fundo preto, o sistema abre a tela **Finalizar Produto**, onde são exibidos os campos detalhados: * **Modo de Preparo** (Ex: Bem passado, sem cebola, queimado). * **Acrescentar/Adicionais** (Ex: Adicionar banana, adicionar feijão). * **Observações textuais** livres inseridas pelo atendente. 
2. Item Pronto (Preparado) * **Comportamento:** Após conferir as especificações na tela detalhada, o operador da cozinha clica no botão **Concluir**. O sistema exibe um modal de confirmação: *"Confirma Produção de Produto?"*. Ao selecionar **Sim**, o fundo do card altera automaticamente para **verde** e o card se desloca para a base da tela. * **Significado:** Sinaliza à equipe de garçons/cumins que o item está pronto no balcão de expedição.
3. Item Entregue (Finalizado) * **Comportamento:** O responsável pela entrega ao cliente final (ou o próprio garçom) clica sobre o card verde. Na tela detalhada, clica em **Concluir** e confirma a operação. * **Resultado:** O item é totalmente removido da listagem do Mapa de Produção e o sistema registra internamente o status do produto como "Entregue". 
--- ## Configuração na Retaguarda Para que um item inserido em uma venda seja direcionado automaticamente para o Mapa de Produção, é mandatório realizar a parametrização do cadastro de produtos no ERP retaguarda. ### Caminho de Interface No menu superior do sistema comercial, acesse: **Cadastros** > **Produtos** > localize o item desejado e clique em **Alterar**. ### Configurações Necessárias 
4. Na aba **Dados Principais**, localize o campo **Tipo de Produto** e defina-o obrigatoriamente como `RESTAURANTE`. 
5. No painel superior direito da ficha de modificação do produto, marque a flag **Controlar Status Prepara** para `SIM`. 
6. *(Opcional)* Na aba **Modos de Preparo**, vincule os modificadores e adicionais permitidos para aquele item específico. > [!warning] Validação de Cadastro > Se a flag **Controlar Status Prepara** estiver definida como `NÃO` ou se o tipo de produto não for condizente com a categoria de produção, o item será ignorado pelo servidor de fila e nunca aparecerá no monitor da cozinha, impossibilitando o controle de KDS. --- ## Simulação de Operação Integrada O fluxo completo abaixo demonstra a interoperabilidade entre a aplicação móvel de atendimento e o terminal de produção da cozinha:
[App Força de Vendas] --(Envio via API REST)--> [Servidor de Comandas] --> [Mapa de Produção (KDS)]

O atendente abre a mesa correspondente no aplicativo móvel de vendas. 
2. Seleciona o item parametrizado (Ex: *Cerveja Imperio Gold GRF 210ML* ou um prato de cozinha). 
3. No campo **Observação**, insere o texto instrucional (Ex: *"Teste com as revendas"*). 
4. Ao clicar em **Confirmar** e enviar o pedido, a requisição passa pelo Servidor de Comandas (Servidor REST ativo na rede local) e o card aparece instantaneamente no monitor da cozinha com o número da mesa e as observações vinculadas. 

 Pontos Críticos e Validações > [!warning] Estabilidade do Servidor REST > O sincronismo em tempo real entre os terminais de venda e o painel de produção depende diretamente do status do componente **Servidor Comanda**. Certifique-se de que o painel do servidor exibe o status **ATIVO** e que o endereço IP local e a porta estejam corretamente mapeados nas estações de trabalho. | Sintoma de Falha | Causa Provável | Ação Corretiva | | :--- | :--- | :--- | | Itens de comanda não aparecem no painel da cozinha. | Cadastro incorreto do produto ou flag de controle desmarcada. | Verificar se o tipo de produto é `RESTAURANTE` e se a opção **Controlar Status Prepara** está configurada como `SIM`. | | Lentidão ou falha de comunicação nos cliques de conclusão. | Instabilidade na rede local ou queda do serviço de banco de dados Firebird. | Validar a conectividade de rede do terminal KDS com o servidor e checar o status do processo do banco de dados. | | Perda de observações de itens modificados. | Versão desatualizada da API de integração do aplicativo. | Atualizar os pacotes do servidor REST da UP Sistemas para garantir a leitura correta das tags de observações XML/JSON do pedido. |
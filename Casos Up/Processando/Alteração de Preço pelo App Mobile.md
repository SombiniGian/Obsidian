---
id:
  - CASO-138
link: https://www.youtube.com/watch?v=Js6IxkbboKw
setor:
  - Suporte
  - Implementação
  - Operacional
modulo:
  - Mobile / Alteração de Preço
tags:
  - android
  - alteracao-em-massa
  - precificacao
  - conversao-de-unidade
  - retaguarda
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Alteração de Preço Mobile]]
2. [[#Fluxo de Criação de Lote de Alteração]]
3. [[#Impacto em Módulos Relacionados: Conversão de Unidades]]
4. [[#Mecânica de Sincronização (Envio ao Retaguarda)]]
5. [[#Regras de Negócio e Pontos Críticos de Falha]]

# Visão Geral da Alteração de Preço Mobile
O módulo de **Alteração de Preço pelo Aplicativo** permite que gerentes, encarregados de gôndola ou inventariantes atualizem as tabelas de preços de venda diretamente no pátio da loja utilizando dispositivos Android. Esta rotina elimina a necessidade de o operador anotar os códigos fisicamente ou deslocar-se até um computador de retaguarda Windows, funcionando através da geração de lotes de modificações locais que operam de forma assíncrona até o comando de persistência final no banco de dados.

# Fluxo de Criação de Lote de Alteração
A inclusão de novos valores no dispositivo segue um fluxo linear e preventivo semelhante ao inventário de estoque:

1. No menu principal do aplicativo móvel, toque na opção **Alteração de Preços**.
2. Clique no botão de adição (**Incluir**) para abrir um novo lote de alteração.
3. Utilize a barra de pesquisa ou o leitor de código de barras para localizar os itens desejados.
4. Ao tocar sobre o produto (ex: `Coca-Cola`), a interface renderizará o nome do item e o campo **Preço Atual** bloqueado para leitura.
5. Insira o valor desejado no campo de input de preço de venda (ex: alterar de `R$ 15,00` para `R$ 16,00`) e clique em **Salvar**.
6. O item é adicionado à listagem de rascunho com o status de lote `Em Digitação`.

# Impacto em Módulos Relacionados: Conversão de Unidades
O comportamento do aplicativo difere substancialmente ao interceptar produtos parametrizados com a rotina de [[Cadastros / Produtos > Conversão de Unidades]] (ex: produtos vendidos em Unidade e em Caixa). Ao selecionar um item indexado com fatores de conversão, a interface desdobra-se em duas regras comerciais de precificação:

### 1. Conversão por Fator Multiplicador Líquido (Preço de Venda Zerado)
Aplica-se a embalagens cujo preço acompanha de forma exata e linear a flutuação da unidade mestre.
*   **Regra de Negócio:** No ERP UP Sistemas, essa conversão possui o valor unitário de venda gravado como `R$ 0,00` no cadastro real, instruindo o banco a calcular o subtotal com base na fórmula `Preço de Venda Pai * Fator de Conversão`.
*   **Comportamento no App:** Ao tentar alterar o valor desta linha de forma direta pelo aplicativo, o sistema **bloqueia o input** e proíbe a edição isolada. Quando o usuário altera o preço da unidade principal (ex: altera de `R$ 17,63` para `R$ 18,00`), o motor do aplicativo calcula o reflexo em tempo de execução, ajustando o lote (ex: a caixa com fator 10 muda automaticamente para `R$ 180,00`).

### 2. Conversão com Preço de Venda Independente (Preço Fixo)
Aplica-se a combos ou caixas fechadas que possuem precificação promocional ou diferenciada da soma de suas frações unitárias.
*   **Comportamento no App:** O aplicativo libera o campo de input para edição direta. O usuário pode alterar o preço da unidade mestre and, na mesma tela, definir que a caixa com 5 unidades custará `R$ 30,00`, ignorando o cálculo fracionado.

# Mecânica de Sincronização (Envio ao Retaguarda)
Os valores alterados na tela do dispositivo Android não são gravados imediatamente na base de dados de produção enquanto o lote mantiver o status `Em Digitação`. Para selar a precificação, deve-se realizar o comando de transmissão:

1. Na listagem de lotes de alteração de preços do aplicativo, identifique o lote ativo.
2. O sistema adota comandos baseados em gestos (*Gestures de Arrasto*):
   *   **Arrastar para a Esquerda:** Invoca a ação de **Excluir** para abortar o lote e descartar as alterações.
   *   **Arrastar para a Direita:** Invoca a ação de **Enviar**.
3. Ao arrastar para a direita, o sistema dispara a validação: `Tem certeza que deseja enviar para o servidor?`. Clique em **Sim**.
4. O aplicativo consome as APIs do [[Mobile / Servidor Força de Vendas]] e injeta as atualizações na base Firebird. Ao atualizar a tela de listagem de produtos da retaguarda Windows, os novos preços estarão consolidados e disponíveis para os caixas do [[PDV]].

# Regras de Negócio e Pontos Críticos de Falha

> [!warning] Latência de Sincronização e Repressão de Carga de Balanças
> Após a confirmação de envio do lote via aplicativo e atualização instantânea no banco de dados do retaguarda, o encarregado deve se atentar à propagação periférica. Se o estabelecimento comercial utilizar balanças integradas de açougue ou padaria (Toledo/Filizola), a atualização de preços na base do ERP **não força** a carga automática para os hardwares. O suporte ou gerência deve comandar manualmente a exportação do arquivo de carga de balanças no retaguarda para atualizar as etiquetas físicas do pátio, evitando divergências no check-out.

> [!danger] Concorrência de Digitação e Sobrescrita de Lotes Ativos
> Como a ferramenta opera por lotes estáticos em modo assíncrono, se o `Operador A` abrir um lote no smartphone para alterar o produto X para R$ 16,00 e, no mesmo intervalo de tempo, o gerente alterar o mesmo produto X para R$ 17,00 diretamente na retaguarda Windows, o ERP aceitará o comando do retaguarda. Contudo, assim que o `Operador A` comandar o envio do seu lote móvel, a API processará a requisição e **sobrescreverá** o valor para R$ 16,00 sem emitir alertas de colisão. Evite a manutenção simultânea de preços por múltiplas estações.
---
id: CASO-209
link: https://www.youtube.com/watch?v=TxpXXFsQ770
setor:
  - Suporte
  - Implementação
  - Operacional
modulo:
  - Portaria e Controle de Ingressos
tags:
  - controle-de-acesso
  - comandas
  - portaria
  - ingressos
  - pdv
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Módulo]]
2. [[#Configurações de Parâmetros Globais]]
3. [[#Fluxo de Portaria: Entrada de Clientes]]
4. [[#Fluxo de Caixa: Consumo e Cobrança]]
5. [[#Fluxo de Portaria: Conferência de Saída]]
6. [[#Regras de Validação e Pontos de Falha]]

# Visão Geral do Módulo
O módulo de **Portaria e Controle de Ingressos** gerencia o fluxo de acesso do público a estabelecimentos. O sistema suporta cenários com venda antecipada de ingressos (validação de bilhetes impressos ou digitais) e cenários com cobrança na saída vinculada ao consumo. A integração nativa com o submódulo de **Controle de Comandas** permite automatizar o lançamento de taxas de entrada ou produtos "ingresso" no momento exato do acesso, agilizando o trabalho dos porteiros e caixas e mitigando fraudes ou evasões.

# Configurações de Parâmetros Globais
Antes de iniciar a operação na portaria, o administrador deve acessar a tela de **Configuração de Ingressos** na retaguarda do sistema para definir as seguintes regras de negócio:

### Identificação do Cliente
Define qual chave primária de pesquisa será utilizada para buscar ou iniciar o cadastro do cliente na portaria:
*   **Telefone** (Padrão)
*   **RG**
*   **CPF**

### Campos Obrigatórios no Cadastro Rápido
Determina quais informações o sistema exigirá para salvar o perfil de um cliente novo na entrada:
*   **Endereço**
*   **Telefone**
*   **RG / CPF**

### Modelos de Cobrança de Ingresso na Saída
Para estabelecimentos que não vendem ingressos antecipados e optam por cobrar o acesso junto com o consumo gerado no local, existem duas modalidades de configuração:
1.  **Incluir o valor do ingresso no acréscimo:** O valor da entrada (ex: R$ 10,00) é embutido diretamente como um acréscimo financeiro geral no fechamento do pedido/comanda.
2.  **Incluir um produto ingresso na comanda:** O sistema realiza o lançamento automático de um item pré-cadastrado na base de dados (ex: Código do Produto: `Ingresso Couvert / Entrada`) dentro da comanda informada assim que o operador valida o acesso.

# Fluxo de Portaria: Entrada de Clientes
Na entrada do evento, o operador trabalha com a tela dedicada de **Portaria** ativa. Esta interface pode ser configurada para ser executada em modo exclusivo (sem dar acesso ao restante do sistema de retaguarda ou [[PDV]]) para garantir a segurança da operação.

### Passos para Liberação de Entrada:
1.  O operador clica em **Novo Ingresso**.
2.  Informa o dado de identificação configurado (ex: digita o número do **Telefone**).
3.  Se o cliente já existir na base, seus dados são preenchidos. Caso contrário, os campos obrigatórios (como endereço e RG) devem ser preenchidos para salvar o cadastro rápido.
4.  O sistema solicita a associação do acesso a um dispositivo físico de controle: o operador digita ou bipa o número da **Comanda** que será entregue ao cliente.
5.  Ao clicar em **Gravar**, o sistema registra o vínculo do ingresso com a comanda e exibe a mensagem de sucesso `Ingresso Concluído`. Se a modalidade de cobrança por produto estiver ativa, o item ingresso é enviado para a comanda em segundo plano.

# Fluxo de Caixa: Consumo e Cobrança
Com a comanda em mãos, o cliente consome normalmente no estabelecimento. Todas as bebidas, alimentos ou serviços são lançados no número de sua comanda pelas telas de atendimento ou pelo [[PDV]].

### Fechamento e Quitação:
1.  Ao se dirigir ao caixa para encerrar sua permanência, o operador abre o número da comanda do cliente no módulo de **Vendas**.
2.  O sistema exibe a lista de produtos consumidos agregada ao valor do ingresso (seja listado como o item produto `Ingresso` ou embutido no campo **Acréscimo** do pedido).
3.  O operador realiza o recebimento dos valores utilizando as formas de pagamento disponíveis (Dinheiro, Cartão, PIX).
4.  Após a confirmação do pagamento, a comanda muda seu status interno de `Em Aberto` para `Finalizado`.

# Fluxo de Portaria: Conferência de Saída
Ao tentar deixar o estabelecimento, o cliente apresenta sua comanda física na portaria de saída. O operador utiliza a mesma tela de **Portaria** para validar a liberação.

### Mecânica de Validação de Saída:
1.  O operador posiciona o cursor no campo de conferência e digita ou realiza a leitura com leitor de código de barras do número da comanda.
2.  A validação ocorre imediatamente e a interface responde de forma visual e textual:

> [!tip] Liberação Autorizada (Alerta Verde)
> Se a comanda foi devidamente paga no caixa, a tela exibe a mensagem em destaque verde: **`Saída liberada! Não existe pendência.`** O sistema limpa o campo de forma imediata e automática, deixando o cursor pronto para a leitura da próxima comanda sem a necessidade de cliques adicionais do operador.

> [!warning] Bloqueio de Saída (Alerta Vermelho)
> Se o cliente se dirigir à saída sem passar pelo caixa, a tela exibe em destaque vermelho a mensagem: **`Saída Não Autorizada. Comanda não finalizada.`** O sistema abre uma janela auxiliar listando os itens em aberto daquela comanda para que o porteiro oriente o cliente a retornar ao caixa.

# Regras de Validação e Pontos de Falha

### Tentativa de Duplicidade de Ingresso (Prevenção de Fraudes)
Caso um cliente tente reutilizar um ingresso físico/digital clonado ou que já passou pelo processo de entrada, o sistema bloqueia o registro:
*   Ao bipar o código na entrada, o sistema consulta a tabela de acessos ativos e recusa o registro se o código do bilhete já constar como "Utilizado" ou "Dentro do Evento". 
*   A tela exibe um aviso de erro crítico informando que o ingresso já deu entrada no estabelecimento, impedindo a geração de uma nova comanda para o mesmo bilhete.

### Comanda Não Localizada
Se o operador digitar um número de comanda inexistente ou não cadastrado no lote ativo do sistema, a interface emitirá o aviso de **Comanda não localizada**, exigindo a correção do dígito ou a substituição do cartão físico.
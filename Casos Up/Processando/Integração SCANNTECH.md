---
id: [CASO-170]
link: https://www.youtube.com/watch?v=_K0AtMU6S3w&t=67s
setor: [Suporte, Implementação, Operacional]
modulo: [Integração Scanntech]
tags: [scanntech, integracao-api, clube-de-promocoes, envio-de-vendas, webhook, pdv]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Integração Scanntech]]
2. [[#Pré-requisitos e Autenticação Inicial]]
3. [[#Parametrização da Camada de Comunicação (URLs e Credenciais)]]
4. [[#Configuração de Gatilhos de Envio (Vendas, Fechamento e Reenvio)]]
5. [[#Sincronização de Promoções e Aceite Obrigatório no Portal]]
6. [[#Auditoria, Logs e Tratamento de Exceções]]
7. [[#Regras de Negócio e Pontos Críticos de Falha]]

# Visão Geral da Integração Scanntech
A integração **Scanntech** conecta o sistema de retaguarda e PDVs da empresa ao hub de promoções e inteligência de mercado da Scanntech. O módulo integrador atua como um serviço (daemon) executado preferencialmente no servidor, sendo responsável por consumir as APIs da Scanntech para fazer o download de campanhas promocionais, bem como transmitir em lote as vendas realizadas e o fechamento diário do caixa para fins de auditoria e reembolso de descontos.

# Pré-requisitos e Autenticação Inicial
O integrador Scanntech funciona como uma aplicação satélite. No primeiro acesso, o sistema exigirá a identificação do operador.

1.  Execute o integrador Scanntech.
2.  Na tela de login, insira as credenciais de um usuário válido previamente cadastrado na retaguarda do ERP.
3.  **Dica de Automação:** Recomenda-se utilizar o login do usuário **Administrador**. Após autenticar, navegue até a tela de configurações e marque a opção **Iniciar Automaticamente**. Isso criará um cache de credenciais, impedindo que o serviço fique travado na tela de login caso o servidor Windows seja reiniciado durante a madrugada.

# Parametrização da Camada de Comunicação (URLs e Credenciais)
As chaves de acesso e os caminhos dos Webhooks são fornecidos de forma exclusiva pelo time de implantação da Scanntech.

1. Acesse o botão **Configuração** no integrador.
2. Preencha os campos obrigatórios baseados no manual fornecido pela Scanntech:
   * **Usuário / Senha:** Credenciais da API da Scanntech.
   * **Empresa / Local:** Códigos numéricos que identificam o CNPJ e a filial específica.
   * **URL 1, URL 2, URL 3:** Endereços (Endpoints) da API.

> [!info] Mecanismo de Redundância (Failover de URLs)
> A exigência de preenchimento de três URLs distintas atua como uma contingência arquitetural. Caso os servidores primários da Scanntech sofram oscilações e a **URL 1** retorne erro de *timeout*, o integrador da UP Sistemas chaveia automaticamente a transmissão do lote para a **URL 2**, garantindo a entrega contínua dos cupons.

# Configuração de Gatilhos de Envio (Vendas, Fechamento e Reenvio)
A transmissão dos dados transacionais do PDV não exige interferência humana, sendo orquestrada por *timers* de background configuráveis na mesma tela.

*   **Caixa:** Por padrão, preenche-se com o valor `1`.
*   **Intervalo para envio das vendas (segundos):** Tempo de espera entre os lotes. Padrão recomendado: `30 segundos`.
*   **Quantidade de vendas por lote:** Volume máximo de cupons por transmissão. Padrão recomendado: `50 vendas`.
*   **Horário de envio dos Fechamentos Pendentes:** Horário fixo em que o sistema consolida as transações do dia anterior e envia o resumo fiscal exigido pela Scanntech. Padrão: `09:00`.
*   **Consultas de Solicitação de Reenvio:** A Scanntech pode solicitar ativamente (via API) a retransmissão de dados que não foram processados adequadamente. O sistema realiza verificações de pendências duas vezes ao dia. Padrões: `09:00` (Consulta 1) e `15:00` (Consulta 2).

> [!tip] Envio Manual de Contingência
> Caso o valor do "Intervalo para envio das vendas" seja ajustado para `0` (zero), a inteligência de envio automático será inativada. As vendas ficarão represadas no banco de dados e só serão transmitidas quando o operador clicar manualmente nos botões do painel lateral (ex: **Enviar lote de vendas** ou **Enviar um fechamento**).

# Sincronização de Promoções e Aceite Obrigatório no Portal
Uma das funcionalidades centrais da integração é aplicar descontos automaticamente no PDV financiados pelas indústrias parceiras da Scanntech.

### Comportamento da Sincronização de Promoções
1. O integrador varre a API e faz o download da lista de novas campanhas promocionais.
2. As campanhas são gravadas na retaguarda no caminho: **Cadastro > Outros > Produtos > Promoções**.
3. **Status Inicial (Pendente - Verde):** Ao serem inseridas no ERP, as promoções ficam com o status pendente e **não são aplicadas no PDV**. O motor da UP Sistemas não possui um *endpoint* autorizado para realizar o aceite das regras comerciais de forma nativa.

### Fluxo Obrigatório de Liberação (Portal Scanntech)
Para que a promoção entre em vigor, o gestor do supermercado deve realizar a liberação no ecossistema da Scanntech:
1. Acesse o **Portal Web do Clube de Promoções Scanntech** via navegador.
2. Identifique a campanha listada e clique em **Aceitar Promoção**.
3. Aguarde o tempo de processamento. A mudança de status (de pendente para ativa) no ERP ocorrerá na próxima varredura de sincronização do integrador.

> [!warning] Latência de Propagação (Delay de 30 minutos)
> Mesmo após o aceite no portal web da Scanntech, a estrutura deles exige um tempo de processamento interno para liberar a flag nas APIs. A atualização no integrador e a efetivação no PDV podem demorar até **30 minutos** para acontecer. Não reenvie cargas manuais ou acione o suporte técnico durante este intervalo.

# Auditoria, Logs e Tratamento de Exceções
Para auditar a estabilidade e a volumetria de dados trocados com as indústrias, o integrador possui abas de monitoramento avançado.

*   **Histórico de Envios:** Lista cronológica de todas as requisições (Vendas, Fechamentos, Sincronização de Promoções).
*   **Inspeção de Payload (JSON):** Caso uma transmissão retorne um status de falha, o operador pode clicar em **Envio e Resposta** na lateral da grade. O painel exibirá o código bruto do JSON enviado pelo ERP e a string do erro devolvida pelos servidores da Scanntech, facilitando o diagnóstico técnico.
*   **Integrações de Vendas:** Grade que separa e exibe os cupons que já foram confirmados e os que permanecem represados (`Pendentes`).
*   **Relatório Específico Scanntech:** O módulo conta com um relatório formatado estruturalmente sob as diretrizes de compliance visual da Scanntech para homologação e auditoria contábil.

# Regras de Negócio e Pontos Críticos de Falha

> [!danger] Perda de Identificação de Estação (Múltiplos Integradores)
> A arquitetura da integração demanda que exista preferencialmente **apenas uma instância** do integrador rodando na infraestrutura do cliente, geralmente instalada no PC servidor de retaguarda. Se houver a necessidade técnica de espalhar instâncias do integrador por múltiplos caixas físicos, o campo **Caixa** na aba de configurações deve ser numerado de forma distinta (ex: Caixa 1, Caixa 2) em cada máquina, para evitar colisão e duplicidade de envio de lotes de vendas para a mesma API.
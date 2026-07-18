---
id: CASO-014
link: https://www.youtube.com/watch?v=ScQyFTO2PDA
setor: Suporte
modulo: Licenciamento e Faturamento
tags: [pix, automacao, cobranca, pdv-pay, licenciamento, erp, revenda]
data_criacao: 2026-07-18
---

## Sumário
- [[#Visão Geral]]
- [[#Pré-requisitos e Configurações]]
  - [[#1. Conta PSP (PDV Pay)]]
  - [[#2. Configuração no Painel da Revenda]]
  - [[#3. Configuração no Cadastro do Cliente]]
- [[#Regras de Negócio e Comportamento]]
- [[#Fluxos de Execução]]
  - [[#Cenário 1: Licença Expirada (Bloqueio Total)]]
  - [[#Cenário 2: Renovação Antecipada (Manual)]]
  - [[#Cenário 3: Avisos Prévios e Prompt de Vencimento]]
- [[#Gestão Financeira e Baixa Bancária]]

## Visão Geral
A funcionalidade de **Cobrança Automatizada** permite que os clientes finais da revenda realizem o pagamento de suas mensalidades diretamente pela interface do sistema de retaguarda, utilizando uma integração via PIX com o [[PDV Pay]] (provedor PSP). O objetivo principal da *feature* é reduzir a fricção no processo de cobrança do *software*, eliminando a necessidade de emissão de boletos, contato ativo de cobrança e o processamento manual de arquivos de retorno bancário. A renovação de acesso ao *software* ocorre de forma instantânea (*machine-to-machine*) após a liquidação do pagamento.

## Pré-requisitos e Configurações

Para que o módulo de automação financeira atue de forma integrada com a validação da licença de uso local, as credenciais e as chaves de integração devem ser devidamente cadastradas nos respectivos painéis.

### 1. Conta PSP (PDV Pay)
> [!info] Integração e Gateway
> É obrigatório que a revenda possua uma conta ativa no ecossistema do [[PDV Pay]]. Esta plataforma gerencia as transações, processa os *webhooks* e gerencia as liquidações.

O acesso aos dados da API (chaves de integração) ocorre no portal do PSP:
1. Acesse o painel web do PDV Pay.
2. Navegue pelo caminho **Configurações** > **Meus Dados**.
3. Copie as chaves criptográficas necessárias:
   - `Token` de autenticação da revenda.
   - `Secret Key` para assinatura das requisições.
   - `Chave PIX` de recebimento principal.

### 2. Configuração no Painel da Revenda
As chaves obtidas devem ser registradas no painel de gestão central da *software house*/revenda para orquestrar as requisições geradas pelas pontas (terminais dos clientes):
1. Acesse o **Painel / Controle** central.
2. Navegue para o módulo **Cadastro de Revendas**.
3. Insira o `Token`, `Secret Key` e a `Chave PIX` da sua empresa.

### 3. Configuração no Cadastro do Cliente
A cobrança só é disparada se o *flag* de autorização de faturamento estiver habilitado de forma individual (por *tenant*/cliente):
1. Acesse a aba **Cadastro do Cliente**.
2. Defina o valor financeiro da licença no campo **Valor** (ex: `150.00`).
3. Habilite a automação setando o campo **Realizar cobrança** como `S` (Sim).

Exemplo estrutural do estado de configuração de um cliente para viabilizar o fluxo:

```json
{
  "client_id": "999888",
  "licensing": {
    "expiration_date": "2026-02-10",
    "status": "active"
  },
  "billing_config": {
    "monthly_value": 150.00,
    "auto_charge": "S",
    "psp_integration": "pdv-pay"
  }
}


> [!warning] Atenção: Supressão da Cobrança
> Se a revenda optar por não cobrar um cliente via sistema (ex: acordos verbais ou contratos de pagamento anualizados), deve-se manter a flag **Realizar cobrança** configurada como `N`. Com isso, a aplicação não gerará a requisição ao PSP e apenas renderizará o modal tradicional bloqueando o acesso e pedindo contato com o suporte.

## Regras de Negócio e Comportamento

* **Renovação Automática**: A confirmação de transação (*callback* ou *polling*) injeta imediatamente o período referencial de um mês (30 dias) ao ciclo de vida da licença vigente, liberando acesso ao sistema instantaneamente.
* **Cálculo de Juros e Multa**: Pagamentos processados após o vencimento (quando o sistema já se encontra na tela de bloqueio total) embute, por padrão, as taxas de juros moratórios e multas configurados no painel. Pagamentos antecipados isentam o cliente de encargos.
* **Degradação Visual e Alertas**: O sistema utiliza codificação de cores para alertar o cliente sobre o vencimento próximo. A lógica aplicada no cabeçalho/interface da aplicação é:
* `Vencimento <= 5 dias`: Alerta visual e de rodapé na cor **Laranja**.
* `Vencimento <= 2 dias`: Alerta visual na cor **Vermelha** e ativação de prompt no ato da inicialização do software.



## Fluxos de Execução

### Cenário 1: Licença Expirada (Bloqueio Total)

Este fluxo ocorre quando o ciclo de licenciamento esgota (data atual > data de validade):

1. A inicialização da aplicação é interceptada e uma tela impeditiva é exibida: *"A licença expirou dia DD/MM. Deseja gerar uma cobrança PIX para renovar o acesso?"*
2. Se a ação no botão **Não** for acionada, a rotina aborta e a aplicação é finalizada abruptamente.
3. Se a ação no botão **Sim** for acionada, o sistema submete uma requisição de cobrança à API, retornando e renderizando o QR Code PIX em tela, já computando os acréscimos por atraso.
4. O *client* submete o pagamento, o *socket* ou rotina de monitoramento acusa o evento de baixa e exibe: *"Pagamento finalizado e atualizando sistema"*.
5. A licença local atualiza seu token de validade e desvia a navegação para a tela principal de retaguarda.

> [!tip] Cancelamento de Operação (Interrupção)
> Durante a exibição do QR Code, o cliente dispõe do botão **Cancelar**. Esta ação aplica a lógica de *fallback*, notificando: *"Pagamento não efetuado. Contato com o fornecedor do sistema"* e impede o acesso.

### Cenário 2: Renovação Antecipada (Manual)

Fluxo proativo do usuário, prevenindo o bloqueio:

1. Com o sistema em operação, o cliente acessa a rotina administrativa e clica em **Pagar licença**.
2. A aplicação gera um *payload* de faturamento isento de juros/multa.
3. O QR Code é exposto na modal.
4. Concluída a leitura e liquidação, a validade se acumula (+1 mês com base na data original).

### Cenário 3: Avisos Prévios e Prompt de Vencimento

Fluxo de indução de pagamento baseado em D-2 (dois dias para expirar):

1. Na abertura do sistema, um *pop-up* intercepta a rotina de *login*: *"Faltam X dias para o sistema expirar. Deseja gerar uma nova cobrança PIX para renovação?"*
2. Se acionar **Não**, o sistema avança para a área de trabalho normal, contudo, aplica estado de interface vermelho.
3. Se acionar **Sim**, a aplicação desencadeia a geração do PIX antecipado, com as mesmas condições do Cenário 2.

## Gestão Financeira e Baixa Bancária

Toda a auditoria, conciliação e transbordo financeiro é processado no painel da instituição de pagamento:

* **Painel Centralizado**: No [[PDV Pay]], é possível monitorar a saúde financeira da carteira de clientes, acompanhando extratos completos das automações geradas.
* **Ações de Reparo**: Em casos de falhas sistêmicas ou pagamentos duplicados, a revenda pode efetuar a devolução (*refund*) integral do PIX no próprio painel.
* **Saques (Cash-out)**: Transferência dos recebíveis liquidados para a conta bancária da própria *software house*.
* **Oportunidade de Receita (Sub-adquirente)**: A mesma estrutura técnica de PSP suporta que a própria revenda cadastre os usuários de seu software (lojas, comércios) na plataforma. Ao ativar os recebimentos por PIX no *checkout* do PDV dessas lojas, a revenda arrecada *split* percentual ou *fee* de centavos por transação, criando uma vertical de monetização adicional baseada em TPV (*Total Payment Volume*).
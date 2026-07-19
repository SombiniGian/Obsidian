---
id:
  - CASO-203
link: https://www.youtube.com/watch?v=wYhb3-lqLKU
setor:
  - Suporte
  - Operacional
  - Logística
modulo:
  - Expedição / Controle de Cargas
tags:
  - multi-empresa
  - controle-de-cargas
  - faturamento
  - cubagem
  - roteirizacao
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Carga Multi-Empresa]]
2. [[#Seleção Expresso de Empresa Logada]]
3. [[#Montagem e Validação da Capacidade de Carga]]
4. [[#Faturamento e Restrições de Segurança]]
5. [[#Regras de Negócio e Pontos Críticos]]

# Visão Geral da Carga Multi-Empresa
O recurso de **Carga Multi-Empresa** permite que o setor de logística unifique a roteirização e a expedição de mercadorias pertencentes a diferentes filiais ou CNPJs do grupo econômico em uma única unidade de transporte (mesmo caminhão/veículo). Essa arquitetura centraliza a gestão de frotas, otimiza o espaço físico dos veículos e gera economia de combustível. As cargas passam a ser globais, ficando visíveis independentemente de qual empresa o usuário esteja conectado no momento.

# Seleção Expresso de Empresa Logada
Para agilizar o fluxo operacional de conferência e alteração de documentos sem a necessidade de realizar o processo completo de *Logoff* e redigitação de credenciais, o sistema conta com a funcionalidade de alternância expressa de contexto.

1. O operador pode acessar a rotina clicando no botão **Trocar Empresa** ou utilizando a tecla de atalho **ALT + L**.
2. A janela auxiliar listará as empresas liberadas para o usuário.
3. Ao selecionar a nova filial, o sistema atualiza o contexto de dados mantendo o mesmo usuário logado anteriormente, realizando a troca de ambiente em segundo plano.

# Montagem e Validação da Capacidade de Carga
Ao criar ou editar uma carga unificada, o sistema permite a inserção de pedidos de vendas originados em múltiplas empresas. A interface de montagem disponibiliza um campo de busca avançada por **CEP** para facilitar a consolidação de rotas geográficas.

### Indicadores de Progresso e Cubagem
Para auxiliar o operador, a tela exibe duas barras de progresso que medem em tempo real a ocupação física da unidade de transporte baseada nas configurações do veículo selecionado:
*   **Capacidade de Volumetria (M³):** Exibe o limite de cubagem suportado (ex: `10 metros cúbicos`).
*   **Capacidade de Peso (Kg):** Exibe o limite de peso de arrasto suportado (ex: `10 Kg`).

```json
{
  "validacao_capacidade_veiculo": {
    "carga_id": 482,
    "veiculo_placa": "ABC1234",
    "limites": {
      "metragem_cubica_max": 10.0,
      "metragem_cubica_atual": 12.0,
      "peso_max_kg": 10.0,
      "peso_atual_kg": 8.5
    },
    "status_alerta": {
      "excesso_cubagem": true,
      "excesso_peso": false
    }
  }
}

>[!warning] Alerta Visível de Excesso de Capacidade Quando os pedidos adicionados superam o limite físico cadastrado no veículo (conforme o payload acima, onde a cubagem atingiu 12M³ para um limite de 10M³), o sistema altera a cor da barra de progresso para **vermelho**, indicando visualmente o estouro.

No momento da gravação, uma janela pop-up emitirá a mensagem de advertência notificando que os limites foram extrapolados. O operador pode optar por ignorar o aviso clicando em **Sim** para continuar e salvar a carga mesmo com excesso, transferindo a decisão para o nível gerencial.
>

# Faturamento e Restrições de Segurança

Embora a visualização e a montagem da carga sejam globais e unificadas, o isolamento fiscal por empresa permanece estrito por questões de segurança e integridade de dados.

### Alteração de Pedidos

- O operador só conseguirá clicar em **Alterar** e modificar as propriedades de um pedido se estiver logado exatamente na empresa detentora daquele documento.
    
- Caso tente alterar um pedido de outra filial sem alternar o contexto de login, o sistema retornará um erro de permissão bloqueando a ação.
    

### Processo de Faturamento (Geração de Nota Fiscal e Financeiro)

A rotina de **Faturamento** realiza a quebra automática dos lotes por empresa.

1. O usuário aciona o comando para faturar.
    
2. O sistema processa e emite os documentos e o [[Financeiro / Contas a Receber]] apenas dos pedidos pertencentes à empresa em que o usuário está atualmente conectado.
    
3. Para os pedidos das demais empresas presentes na mesma carga, o faturamento será recusado com a mensagem de que não é possível faturar documentos fora do contexto logado. O operador deverá utilizar o comando **ALT + L**, migrar para a próxima filial e repetir a operação de faturamento para o lote restante.
    

# Regras de Negócio e Pontos Críticos

> [!info] Isolamento de Abas de Saída e Notas Fiscais Dentro do painel da carga, as abas complementares (como as de **Notas Fiscais** e documentos de **Evoluções**) são filtradas dinamicamente. Elas exibirão exclusivamente as informações e chaves eletrônicas correspondentes à empresa selecionada no login atual, ocultando os dados fiscais das demais filiais para evitar cruzamentos indevidos de relatórios.

> [!danger] Quebra de Sequência no Faturamento em Lote Como o faturamento de uma carga multi-empresa exige que o operador mude de filial no meio do processo, esquecer de efetuar a troca de contexto via **ALT + L** fará com que parte das mercadorias saia para a rota sem a emissão do documento fiscal de transporte correspondente, gerando riscos de apreensão de carga em barreiras fiscais. Certifique-se de que todas as quebras de lote foram faturadas antes de liberar o veículo.
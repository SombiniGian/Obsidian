
id: [CASO-XXX]
link: https://www.youtube.com/?hl=pt&gl=BR&app=desktop
setor: [Setor de aplicação, ex: Suporte, Desenvolvimento]
modulo: [Módulo do sistema]
tags: [tag1, tag2, tag3]
data_criacao: 2026-06-23


# Configuração e Operação do Módulo de Ordem de Serviço (OS)

Este documento descreve detalhadamente o ecossistema e as regras de negócio integradas ao módulo de **Ordem de Serviço (OS)** do sistema [[Código UP Sistemas]]. O objetivo é orientar a parametrização inicial, o gerenciamento de estados da OS e os fluxos financeiros e operacionais relacionados.

---

## Sumário
1. [[#1. Estrutura de Cadastros e Parâmetros Base]]
2. [[#2. Configurações Globais do Usuário / Administrador]]
3. [[#3. Ciclo de Vida e Fluxo de Execução da OS]]
4. [[#4. Lançamento de Itens e Gestão de Comissões]]
5. [[#5. Faturamento e Fechamento Financeiro]]

---

## 1. Estrutura de Cadastros e Parâmetros Base

A base de sustentação do módulo de Ordem de Serviço depende do alinhamento lógico entre três tabelas principais. A flexibilidade do sistema permite atender desde oficinas mecânicas até assistências de TI ou telefonia celular.

### 1.1 Tipos de Equipamentos
Determina o escopo de atuação do serviço da empresa e define quais características técnicas serão exigidas em tela.
* **Campos Customizáveis:** Permite configurar rótulos e propriedades específicas para cada segmento (ex: se o tipo for *Veículo*, ativa-se campos para Placa, Modelo e Chassi; se for *Celular*, preenche-se Modelo, IMEI e Operadora).
* **Vínculo com o Cliente:** O sistema permite parametrizar se o equipamento fica atrelado em definitivo a um cliente específico (como um automóvel que sempre pertence ao mesmo proprietário) ou se é livre de vínculo fixo.

### 1.2 Equipamentos
Consiste na unidade física que receberá a manutenção. 
* O sistema permite trabalhar de duas formas: utilizando um registro pré-cadastrado no banco de dados para rastreabilidade histórica completa ou aceitando uma digitação livre no ato da abertura da OS.

### 1.3 Situações (Status)
As situações ditam as etapas que a OS irá percorrer dentro da empresa (ex: *Aguardando Manutenção*, *Em Trabalho*, *Aguardando Peça*, *Finalizada*, *Cancelada*).
* **Diferencial de Controle Visual:** É possível definir cores específicas para cada situação para facilitar a triagem na grade geral.
* **Vínculo com Impressão/Relatórios:** Cada situação pode ser associada a um layout do **Gerador de Relatórios**. Quando a OS assume determinado status, o sistema chama o modelo de impressão específico (ex: ao entrar em "Faturada", imprime-se o termo de saída e entrega de equipamento).

---

## 2. Configurações Globais do Usuário / Administrador

Para acelerar o processo operacional e mitigar erros humanos, o usuário administrador deve parametrizar os comportamentos automáticos do sistema através do painel de configurações.

```

[Painel Administrativo da OS]

│

├── Natureza da Operação (Padrão para emissão fiscal)

├── Classificação de Urgência (Ex: Urgente, Prazo Normal)

├── Impressão Padrão (Fallback de layout)

└── Regras de Negócio e Validações Estritas

```

### Regras de Negócio Importantes:
* **Obrigar Cadastrar Equipamento:** Quando ativo, impede o preenchimento por texto livre. O operador deve selecionar um registro previamente validado. 
* **Obrigar Cadastrar Defeito:** Força o preenchimento do campo de triagem inicial de defeito/sintoma relatado pelo cliente.
* **Imprimir Automaticamente:** Se habilitado, no momento exato em que a OS muda de situação, o sistema dispara a impressão física ou visualização do relatório associado, sem requerer o clique manual no botão **Imprimir**.
* **Abrir Situação ao Incluir OS:** Faz com que, ao clicar no botão de nova OS, o sistema exiba imediatamente uma janela de pré-configuração de estado, exigindo a definição do status inicial, técnico responsável e observações de entrada.

> [!warning] Atenção à Padronização
> Permitir a digitação livre do equipamento e do defeito agiliza o processo inicial, porém compromete a qualidade estatística posterior. Erros de digitação, espaços extras ou nomenclaturas diferentes impossibilitam a extração de relatórios consolidados sobre quais equipamentos ou defeitos são mais recorrentes na base.

---

## 3. Ciclo de Vida e Fluxo de Execução da OS

O fluxo operacional padrão de uma Ordem de Serviço segue as seguintes etapas integradas:

1. **Abertura/Entrada:** O operador aciona a inclusão. Se a flag *Abrir Situação ao Incluir OS* estiver ativa, define-se o status inicial (ex: *Aguardando Triagem*). Associa-se o **Cliente**, o **Equipamento** e insere-se o relato do defeito.
2. **Distribuição Técnico:** Através do painel de transição de situações, altera-se o estado da OS para *Em Trabalho* (ou equivalente) e vincula-se o **Técnico Responsável**. O sistema grava o histórico completo dessas mudanças no rodapé da consulta.
3. **Execução e Atualização:** Conforme o diagnóstico evolui, observações técnicas internas são inseridas sem alterar os dados de entrada fornecidos pelo cliente.

```

```
   [Abertura da OS] ──> Define Cliente / Equipamento / Defeito
          │
          ▼
   [Distribuição]   ──> Altera Situação para "Em Trabalho" + Associa Técnico
          │
          ▼
   [Execução]       ──> Lançamento de Peças, Serviços e Históricos
          │
          ▼
   [Faturamento]    ──> Baixa no Estoque + Geração de Títulos Financeiros
```

```

> [!tip] Automação de Datas
> Vincule a situação final de entrega (ex: *Entregue ao Cliente*) ao parâmetro de **Situação da Entrega** nas configurações globais. Ao fazer isso, assim que a OS migrar para este status, o sistema preencherá de forma automatizada o campo **Data da Entrega**, registrando o encerramento do ciclo físico do produto.

---

## 4. Lançamento de Itens e Gestão de Comissões

A composição financeira da OS é dividida entre peças (produtos) e mão de obra (serviços).

* **Lançamento de Itens:** Na aba de itens, inserem-se os insumos utilizados. Cada item adicionado dá baixa física no estoque se configurado para tal.
* **Comissionamento por Item:** O sistema permite determinar as comissões individualmente por linha de lançamento. É possível associar um técnico ou vendedor diferente para cada peça ou serviço adicionado.
* **Rastreabilidade e Auditoria:** No painel inferior da OS, o sistema gera uma linha do tempo detalhando cada alteração de status, o horário da mudança, o usuário responsável pela transição e as anotações geradas em cada etapa.

---

## 5. Faturamento e Fechamento Financeiro

Uma ordem de serviço em andamento ou finalizada não gera impactos financeiros diretos no caixa ou contas a receber até que o processo de **Faturamento** ocorra.

### Mecânica do Faturamento:
1. Com a OS com todos os itens e valores consolidados, o operador clica no botão **Faturar** (ou aciona o fluxo de pagamento na tela).
2. O sistema exibe a interface padrão de fechamento (similar ao módulo de [[Pedido de Venda]]), onde são definidas as condições de pagamento (à vista, parcelado, boleto, cartão).
3. Após salvar as condições, o fluxo executa as seguintes rotinas em segundo plano:
   * **Fluxo Financeiro:** Os títulos são lançados no módulo de *Contas a Receber* ou o valor é creditado diretamente no *Fluxo de Caixa*.
   * **Fluxo de Estoque:** Consolidação definitiva da saída das peças aplicadas.
   * **Atualização de Status:** A OS assume automaticamente a situação padrão configurada para o pós-faturamento (ex: *Faturada*).

> [!info] Impressão Pós-Faturamento
> Caso a opção de impressão automática esteja ativa para o status *Faturada*, a tela com a autorização de saída do equipamento e o sumário de valores para assinatura do cliente será gerada em tela logo após a confirmação do pagamento.
```

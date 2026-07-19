---
id: CASO-213
link: https://www.youtube.com/watch?v=7b7aCBHshUg
setor: Suporte / Implantação
modulo: Hotelaria / Controle de Hospedagem
tags:
  - hotelaria
  - reserva
  - checkout
  - quartos
  - faturamento
data_criacao: 2026-07-18
---

## Sumário
1. [[#Ativação do Módulo Oculto]]
2. [[#Estrutura de Cadastros e Regras de Negócio]]
3. [[#Controle de Reservas e Check-in]]
4. [[#Lançamento de Consumo e Gestão de Hóspedes]]
5. [[#Fluxo de Check-out e Faturamento Técnico]]
6. [[#Pontos de Falha e Validações Críticas]]

---

## Ativação do Módulo Oculto

O **Módulo de Hotelaria e Controle de Hospedagem** do Oxystem é um recurso específico ocultado por padrão no sistema para simplificar a interface de clientes de outros ramos (como autopeças ou varejo geral). 

### Processo de Liberação da Interface:
1. Em qualquer menu ou aba superior do sistema, clique com o **Botão Direito**.
2. No menu de contexto exibido, localize as opções de módulos disponíveis.
3. Marque a caixa de seleção do módulo **Hotel**.
4. Desmarque o módulo **Restaurante** caso queira isolar as operações e evitar poluição visual de comandas e mesas na rotina de hospedagem.

> [!info] Informação
> A separação física dos menus garante maior performance de tela e foco operacional para o recepcionista do estabelecimento hoteleiro ou motel.

---

## Estrutura de Cadastros e Regras de Negócio

Antes de iniciar as reservas, o sistema exige o preenchimento encadeado de três cadastros estruturais para precificação automática.

### 1. Tipo de Apartamento
* **Objetivo**: Classificação técnica e agrupamento dos quartos (ex: Luxo, Suíte Master, Standard).
* **Impacto**: Não define valores diretamente, mas serve como agrupador para a extração de relatórios gerenciais e estatísticas de ocupação futuras.

### 2. Tipo de Hospedagem
* **Objetivo**: Determinar a unidade de tempo da cobrança.
* **Parametrização**: O sistema aceita a configuração do período base em **Dias (Diária)**, **Horas** ou **Minutos** (essencial para operação de motéis com cobranças fracionadas de 30 em 30 minutos, por exemplo).
* **Flexibilidade**: Permite criar variações para o mesmo quarto, como "Diária com Café da Manhã" e "Diária sem Café da Manhã".

### 3. Apartamentos (Quartos)
Permite associar o quarto físico à sua respectiva precificação e regras de tolerância.
* **Vínculos Múltiplos**: O mesmo apartamento (ex: Quarto 101) pode ter múltiplos valores associados de acordo com o tipo de hospedagem, quantidade de pessoas ou adicionais.
* **Regra de Hora Excedente/Multa**: Definição do valor cobrado por fração ou hora que ultrapassar o horário limite do check-out. Se o check-out expirar, o sistema calcula, por exemplo, R$ 10,00 ou R$ 20,00 para cada hora excedente de forma automática no fechamento.

---

## Controle de Reservas e Check-in

A tela de **Controle de Reservas** funciona como um grid visual ou matriz de ocupação dividida por dias e apartamentos.
[Quarto Disponível (Grid em Branco)]
│ 
▼ [Clique no Dia Desejado]
│ 
▼ [Inserir Cliente / Nome / Dias / Salvar] ──► (Gera Status: Reservado) 
│ 
▼ [Ação: Registrar Check-in] ──────────► (Gera Status: Ocupado)

Processo de Ocupação Direta (Balcão/Walk-in): 1. Quando um hóspede chega sem reserva prévia, o operador seleciona o quarto livre diretamente na matriz do dia atual. 2. Clique no botão **Check-in** localizado na parte inferior da tela. 3. O sistema captura o horário do relógio do servidor de forma automatizada para preencher o campo de entrada oficial, vincula o cliente e altera a cor do quarto no painel para **Ocupado**. --- ## Lançamento de Consumo e Gestão de Hóspedes Com o quarto no status **Ocupado**, o sistema abre sub-abas de gerenciamento interno que refletem diretamente na conta final do cliente. ### Lançamento de Produtos: * Os lançamentos utilizam a mesma interface consolidada do módulo de PDV/Vendas do sistema. * O operador informa o número do apartamento (ex: `2`), busca o produto comercializado (ex: água mineral) e clica em **Salvar**. O item é imputado de forma instantânea no extrato interno daquela hospedagem. ### Ficha de Hóspedes e Veículos: * Permite anexar múltiplos hóspedes ao mesmo apartamento, controlando horários individuais de entrada e saída de acompanhantes. * Armazena dados de segurança como a placa do veículo do cliente. * **Impressão de Ficha**: O botão de impressão gera o modelo de cartão de hospedagem ou ficha de balcão regulamentar para coleta da assinatura física do cliente no momento da entrada. --- ## Fluxo de Check-out e Faturamento Técnico No momento da saída do hóspede, o operador seleciona o quarto ocupado no grid e clica no botão **Check-out**. ### Composição Automática da Tela de Fechamento: * **Valor de Hospedagem**: Calculado com base nas diárias ou períodos transcorridos desde o check-in. * **Valor de Consumo**: Totalizador de todos os produtos lançados para o quarto durante a estadia. * **Campo de Multa/Excedente**: Caso o horário atual do sistema ultrapasse o limite de tolerância parametrizado no cadastro do apartamento, o grid exibirá o acréscimo calculado automaticamente no topo da tela. ### Finalização Financeira e Fiscal: * O recebimento segue o padrão de faturamento de vendas (múltiplas formas de pagamento: dinheiro, cartão, etc.). * Ao **Finalizar**, se o estabelecimento estiver integrado aos módulos fiscais regulamentados, o sistema realiza o disparo automático para emissão do Cupom Fiscal Eletrônico ou da Nota Fiscal de Serviço Eletrônica (NFS-e) direto da manutenção de saída. --- ## Pontos de Falha e Validações Críticas 
> [!warning] Atenção: Riscos de Operação e Travamentos Fiscais > * **Bloqueio de Parâmetro de Multa**: Se os valores de hora excedente não forem devidamente delimitados no cadastro de cada apartamento, o sistema ignorará o atraso do check-out, gerando prejuízo financeiro por subfaturamento de horas. > * **Duplicidade de Reservas**: O grid visual impede que dois clientes ocupem o mesmo slot de apartamento no mesmo dia, porém o operador deve se atentar ao horário de transição de check-out/check-in em locais com alta rotatividade (motéis) para evitar sobreposição de estadias. > * **Rejeição de NFS-e**: Se o cadastro do cliente não possuir CPF/CNPJ válido ou se o código do serviço municipal de hotelaria não estiver configurado nos parâmetros fiscais do sistema, o check-out será concluído no financeiro, mas a nota fiscal correspondente ficará travada na fila de transmissão com erro de validação.


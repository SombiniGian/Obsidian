---
id: [HOTEL-001]
link: https://www.youtube.com/watch?v=au0WvoEDTB0
setor: Suporte e Desenvolvimento
modulo: Hotelaria
tags: [hotelaria, hospedagem, reservas, controle-de-apartamentos, pms]
data_criacao: 2026-07-18
---

## Sumário
- [1. Visão Geral do Módulo](#1-visão-geral-do-módulo)
- [2. Cadastros Estruturais](#2-cadastros-estruturais)
  - [2.1. Tipo de Apartamento](#21-tipo-de-apartamento)
  - [2.2. Tipo de Hospedagem](#22-tipo-de-hospedagem)
  - [2.3. Cadastro de Apartamentos](#23-cadastro-de-apartamentos)
- [3. Controle de Reservas](#3-controle-de-reservas)
  - [3.1. Visão de Calendário e Status](#31-visão-de-calendário-e-status)
  - [3.2. Fluxo de Inclusão de Reserva](#32-fluxo-de-inclusão-de-reserva)
- [4. Estrutura de Dados (Referência API)](#4-estrutura-de-dados-referência-api)

---

## 1. Visão Geral do Módulo

O módulo de **Hotelaria** é desenhado para o gerenciamento de propriedades baseadas em ocupação por tempo, atendendo não apenas hotéis, mas também motéis e estacionamentos rotativos. A arquitetura do módulo é dividida em configurações de base (cadastros) e operacionais (reservas e histórico de hospedagens), acessíveis através da aba **Hotel** no menu principal do sistema.

A lógica de negócio central baseia-se na vinculação de `[[Apartamentos]]` a múltiplos `[[Tipos de Hospedagem]]`, permitindo uma precificação dinâmica baseada no período de ocupação e serviços atrelados.

---

## 2. Cadastros Estruturais

A parametrização do módulo exige o preenchimento de três cadastros fundamentais localizados no caminho **Hotel > Cadastros**.

### 2.1. Tipo de Apartamento
Localizado em **Hotel > Cadastros > Tipo Apartamentos**.
Trata-se de uma classificação puramente categórica estrutural (ex: *Luxo*, *Comum*). Serve para agrupar e filtrar as unidades no mapa de reservas, facilitando a alocação do hóspede de acordo com o padrão exigido.

### 2.2. Tipo de Hospedagem
Localizado em **Hotel > Cadastros > Tipo Hospedagem**.
Define a métrica de tempo e a regra de cobrança base para a estadia. 

*   **Períodos suportados:** Dias, Horas ou Minutos.
*   **Aplicações comuns:** 
    *   Diária padrão (Dias = 1).
    *   Locação rotativa/Motel (Horas = 3).
    *   Pacotes promocionais (Dias = 3).
    *   Variações de serviço (Diária com Café da Manhã).

> [!info] Horário de Check-in / Check-out
> Para o tipo "Diárias", o sistema habilita os campos de hora inicial e final (ex: Entrada às 12:00 e Saída às 13:00 do dia seguinte), estabelecendo o ciclo de 24 horas lógicas para o cálculo financeiro da estadia.

### 2.3. Cadastro de Apartamentos
Localizado em **Hotel > Cadastros > Apartamentos**.
É a entidade principal onde as regras de negócio se cruzam. O apartamento é instanciado com os seguintes atributos vitais:

1.  **Dados Principais:** Número do AP, Descrição (ex: *AP Oriental*), e vínculo com o `[[Tipo de Apartamento]]`.
2.  **Hospedagem Padrão:** Define o comportamento *default* de faturamento ao selecionar a unidade na tela de reservas. Inclui o **Valor** da hospedagem.
3.  **Regra de Multa (Overstay):** O sistema possui um motor de tolerância e multas automatizado.
    *   **Como funciona:** Caso a data/hora de saída registrada na `[[Hospedagem]]` ultrapasse o limite, o sistema engatilha a cobrança adicional.
    *   **Configuração:** Define-se o gatilho de tempo (ex: a cada 5 horas) e o valor a ser acrescido (ex: R$ 10,00). Pode ser fracionado em horas ou minutos.

> [!warning] Atenção: Múltiplos Tipos de Hospedagem por Unidade
> A aba **Valores** dentro do cadastro do apartamento é um ponto crítico de flexibilidade. Embora o apartamento possua uma hospedagem padrão (ex: *Diária* a R$ 50,00), nesta aba é possível adicionar precificações alternativas (ex: *3 Horas* a R$ 10,00 com multa de R$ 5,00/hora excedente). Isso impede a necessidade de duplicar cadastros de apartamentos físicos para atender fluxos operacionais de motelaria ou promoções.

---

## 3. Controle de Reservas

Localizado em **Hotel > Controle de Reservas**.
Painel operacional (PMS) para gerenciamento de alocações futuras e visualização de disponibilidade.

### 3.1. Visão de Calendário e Status
A interface é composta por um calendário à esquerda para seleção rápida de datas e um *grid* central que exibe as unidades.
A regra de validação visual obedece dois estados distintos e paralelos:
*   **Situação Atual:** O estado da unidade neste exato momento (ex: *Ocupado*, provindo de uma hospedagem em andamento).
*   **Status da Grade (Reserva):** O estado da unidade para a **data selecionada no calendário**. É possível que o AP 101 esteja *Ocupado* hoje, mas no calendário conste como *Livre* ou *Reservado* para o dia 10.

### 3.2. Fluxo de Inclusão de Reserva
Para alocar um apartamento:
1. Navegue até a data desejada no calendário lateral.
2. Clique no botão **Incluir** (ou utilize o atalho de teclado mapeado).
3. Na janela de Hospedagem, informe o **Apartamento** (ex: *102*). O sistema efetuará o preenchimento automático do `[[Tipo de Hospedagem]]` e seu valor base, respeitando a configuração padrão da unidade.
4. **Substituição de Regra (Opcional):** Se o cliente desejar uma modalidade diferente (ex: *Diária com Café*), altere o campo **Tipo Hospedagem**. O sistema recalculará a tarifa baseada nos atributos da aba **Valores** daquele apartamento.
5. Preencha os metadados da reserva: **Cliente**, **Quem Reservou**, **Telefone Reserva**.
6. Defina a métrica temporal: **Data Chegada / Hora Chegada** e **Data Saida / Hora Saida**.
7. Clique em **Salvar**. A unidade passará a exibir o ícone indicativo de status **Reservado** na grade da data correspondente.

> [!tip] Dica de Fluxo
> Se a base de apartamentos for grande, digite o número do AP diretamente no campo "Apartamento" durante a reserva em vez de buscar no modal de lupa. O gatilho de perda de foco (OnBlur) já carrega as parametrizações padrão da unidade instantaneamente.

---

## 4. Estrutura de Dados (Referência API)

Para integrações e entendimento do banco de dados, a estrutura gerada pelo formulário de reserva reflete o seguinte modelo de payload JSON:

```json
{
  "reserva": {
    "apartamento_id": 102,
    "cliente_id": 21,
    "tipo_hospedagem_id": 7, 
    "quem_reservou": "Julio",
    "telefone_reserva": "32999999999",
    "previsao_chegada": "2026-07-09T20:00:00",
    "previsao_saida": "2026-07-10T12:00:00",
    "status": "RESERVADO"
  }
}
```

*Nota: O `tipo_hospedagem_id` pode variar do padrão estabelecido no cadastro principal do apartamento, refletindo a negociação feita no momento do contato (Upsell).*
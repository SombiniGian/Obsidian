---
id:
  - CASO-134
link: https://www.youtube.com/watch?v=owotxmsJVW8
setor:
  - Suporte
  - Implementação
  - Operacional
modulo:
  - Mobile / Terminal de Auto Pagamento
tags:
  - autoatendimento
  - totem
  - restaurante
  - comanda
  - tef
  - portaria
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Terminal de Auto Pagamento (Totem)]]
2. [[#Mecanismo de Segurança e Modo Kiosk (Kiosk Mode)]]
3. [[#Interface Inicial e Captura de Comandas (Métodos de Input)]]
4. [[#Processamento Financeiro e Integrações TEF / Pix]]
5. [[#Validação de Fluxo de Portaria Pós-Pagamento]]
6. [[#Regras de Negócio e Pontos Críticos de Falha]]

# Visão Geral do Terminal de Auto Pagamento (Totem)
O módulo de **Terminal de Auto Pagamento (Autopagamento)** é uma extensão nativa do ecossistema [[Mobile / Aplicativo Garçom]] desenvolvida para operar em estruturas de Totens de Autoatendimento. O seu propósito principal é mitigar filas em caixas de estabelecimentos comerciais (como restaurantes, bares, casas noturnas e eventos), conferindo ao consumidor final autonomia para consultar o extrato de consumo de sua comanda física, processar o pagamento eletrônico via [[Periféricos / TEF / Pix]] e obter a autorização automatizada para liberação na roleta de saída do estabelecimento.

# Mecanismo de Segurança e Modo Kiosk (Kiosk Mode)
Uma vez que o aplicativo é direcionado para a operação de autoatendimento, o sistema ativa uma barreira rígida de isolamento de processos (Modo Kiosk) para impedir que o cliente final manipule o sistema operacional Android/Windows ou acesse rotinas administrativas.

*   **Ativação:** O técnico ou supervisor acessa o menu lateral e clica em **Autopagamento**.
*   **Bloqueio de Saída:** Ao entrar nesta interface, o botão físico ou virtual de "Voltar" é neutralizado. A aplicação oculta os menus de navegação do garçom.
*   **Proteção por Credenciais:** Qualquer tentativa de retornar à tela anterior, fechar o sistema ou acessar o painel de sincronização de dados exigirá a digitação imediata da senha master do usuário administrador da revenda.
*   **Protetor de Tela Comercial (Modo Standby):** Enquanto nenhum cliente estiver interagindo com o totem, a tela permanece executando um carrosel cíclico de imagens promocionais e propagandas. Esses ativos de mídia digital são gerenciados e herdados diretamente das configurações de publicidade atreladas ao cadastro do vendedor no retaguarda.

# Interface Inicial e Captura de Comandas (Métodos de Input)
Para iniciar a jornada de pagamento, o consumidor toca na tela e depara-se com até três métodos alternativos para identificação de sua conta no banco de dados Firebird:
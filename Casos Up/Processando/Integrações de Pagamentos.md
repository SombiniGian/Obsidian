---
id:
  - CASO-132
link: https://www.youtube.com/watch?v=5TH97Tf5-_s&pp=0gcJCUwLAYcqIYzv
setor:
  - Suporte
  - Implementação
  - E-commerce
modulo:
  - Configurações / Integrações de Pagamentos
tags:
  - pix
  - api-pagamentos
  - webhook
  - e-commerce
  - pdv-pix
  - gateway
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Integração de Pagamentos]]
2. [[#Passo a Passo da Parametrização no Painel do Cliente]]
3. [[#Mecânica de Sincronização Síncrona e Resiliência (Webhooks)]]
4. [[#Exibição de Gateways no Checkout do E-commerce]]
5. [[#Pontos Críticos e Regras de Negócio]]

# Visão Geral da Integração de Pagamentos
O módulo de **Integrações de Pagamentos** gerencia o fluxo de transações eletrônicas do ecossistema de [[E-commerce / Loja Virtual]], com foco na automação de recebimentos via Pix. A rotina estabelece uma ponte de comunicação direta via API entre a loja virtual e o gateway de pagamento (PDV Pix), permitindo a geração dinâmica de chaves do tipo Copy and Paste (Copia e Cola) ou QR Codes no fechamento do carrinho. A inteligência do módulo processa a baixa automática do pedido, eliminando a conferência manual de extratos bancários pelo lojista.

# Passo a Passo da Parametrização no Painel do Cliente
A conexão do ambiente virtual do cliente com os servidores de processamento financeiro exige a captação de tokens de autenticação criptografados:

1. Acesse o painel administrativo da plataforma financeira do cliente (**PDV Pix**).
2. Localize e copie as duas chaves de barramento de segurança: `Secret Key` (Chave Secreta) e o `Token`.
3. No ERP/Retaguarda de gerenciamento do E-commerce, acesse o menu de **Configurações de Pagamento**.
4. Cole rigorosamente os hashes nos campos correspondentes: **Secret Key** e **Token**.
5. Realize a associação de vínculos: amarre a integração ao respectivo tipo de documento contábil/financeiro utilizado na empresa para conciliações automáticas de tesouraria.

# Mecânica de Sincronização Síncrona e Resiliência (Webhooks)
A segurança operacional do fluxo de pagamentos depende da correta parametrização das rotinas de escuta e notificação reversa (*Webhooks / Callbacks*).
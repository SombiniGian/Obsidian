## Índice
1. [Gestão de Boletos Bancários](#1-gestão-de-boletos-bancários)
2. [Integração Bancária (CNAB e API)](#2-integração-bancária-cnab-e-api)
3. [Captura e Operações de TEF e PIX](#3-captura-e-operações-de-tef-e-pix)
4. [Gestão e Conciliação de Cartões de Crédito](#4-gestão-e-conciliação-de-cartões-de-crédito)

---

## 1. Gestão de Boletos Bancários

O sistema permite a geração nativa de boletos bancários atrelados aos recebimentos, eliminando a necessidade de redigitação em portais bancários.

* **Geração Flexível:** O boleto pode ser gerado no ato da venda (PDV), na emissão da Nota Fiscal, ou a partir da tela de "Contas a Receber" para títulos que ficaram em aberto.
* **Configuração de Conta:** Exige o preenchimento preciso dos dados da conta bancária (número do banco, agência, conta e endereço) e a ativação da *flag* **"Emitir Boletos"** nas configurações do sistema.

## 2. Integração Bancária (CNAB e API)

A comunicação com as instituições financeiras (PSP - Provedor de Serviços de Pagamento) pode ser realizada de duas formas distintas, garantindo compatibilidade com os principais bancos (ex: Banco do Brasil, Bradesco).

* **Integração Tradicional (Arquivos):** Geração e leitura manual de arquivos de remessa e retorno padrão CNAB para processamento em lote.
* **Integração via API (Webservice):** Conexão direta e síncrona com o banco.
  * Permite enviar remessas e processar retornos de pagamentos diretamente pela interface do sistema, sem a necessidade de baixar e enviar arquivos físicos (*upload/download*).
  * Exige configurações específicas de chaves e *tokens* fornecidos pelo banco.

## 3. Captura e Operações de TEF e PIX

O módulo financeiro centraliza as transações capturadas eletronicamente na frente de caixa, integrando cartões, carteiras digitais e PIX.

* **Cobrança TEF:** Tela de movimentação dedicada que exibe todas as transações de TEF processadas. Permite auditar, finalizar cobranças pendentes ou realizar cancelamentos sistêmicos integrados com a maquininha.
* **Recebimentos via PIX:** 
  * Integração para exibição de **QR Code** direto na tela do PDV (via TEF ou PSP configurado).
  * *Pagamento de Licença (Revenda):* Há uma integração específica de PIX no painel para que clientes finais paguem a mensalidade da licença do software, com liberação e renovação automática dos dias de uso.

## 4. Gestão e Conciliação de Cartões de Crédito

A gestão de recebíveis de cartões foi projetada para lidar tanto com lojas que exigem auditoria rigorosa quanto com aquelas que preferem um fluxo simplificado.

* **Comportamento de Baixa (Tipo de Documento):**
  * **Baixa Automática:** Se configurado "sem baixa administradora", a venda no cartão cai automaticamente como "faturada" (paga) no caixa. Ideal para clientes que não fazem conciliação bancária.
  * **Lançamento em Aberto:** Se desmarcado, as transações caem "em aberto" no sistema, aguardando a compensação real da adquirente (ex: D+1, D+30).
* **Borderô e Conciliação de Cartão:**
  * **Configuração de Arquivo:** O sistema permite customizar o layout de leitura de arquivos disponibilizados pelas administradoras (Visa, Master, Elo), bem como parametrizar as taxas descontadas.
  * **Importação e Baixa:** O analista importa o extrato da adquirente, e o sistema realiza o cruzamento e a conciliação das parcelas pendentes com o arquivo.
  * **Conciliadores API:** Há suporte nativo a ferramentas terceirizadas de conciliação automática via API (ex: integração com conciliador da *Elgin*).
* **Recálculo de Taxas:** Ferramenta que permite corrigir e recalcular as taxas administrativas do cartão de forma retroativa para títulos já lançados.
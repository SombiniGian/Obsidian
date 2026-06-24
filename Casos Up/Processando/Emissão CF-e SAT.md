---
id: CASO-003
link: https://www.youtube.com/watch?v=elcnR9FsFyY
setor: Suporte, Comercial, Faturamento
modulo: Emissão de Documentos Fiscais
tags:
  - sat
  - cfe
  - emissao-fiscal
  - pdv
  - cancelamento
data_criacao: 2026-06-24
---

# Documentação Técnica: Processo de Emissão e Cancelamento de CF-e SAT

Esta documentação detalha os fluxos operacionais e as regras de negócio para a emissão e o cancelamento do Cupom Fiscal Eletrônico ([[CF-e-SAT]]) através do sistema de Frente de Caixa ([[PDV]]), cobrindo os comportamentos do software tanto em modo local quanto utilizando o servidor concentrador.

---

## Sumário
1. [[#1. Modelo de Documento e Configuração de Natureza]]
2. [[#2. Regra de Negócio: Ciclo de Numeração do SAT]]
3. [[#3. Fluxo de Venda e Emissão no PDV]]
4. [[#4. Validação Visual de Conectividade do Módulo]]
5. [[#5. Fluxo de Cancelamento de Cupom]]

---

## 1. Modelo de Documento e Configuração de Natureza

Para que o sistema realize a emissão de cupons eletrônicos corretos na rotina de faturamento, o preenchimento e a classificação do documento fiscal devem seguir o padrão exigido pelo fisco do estado de São Paulo.

* **Modelo do Documento:** O sistema adota o **Modelo 59** para a identificação do CF-e SAT.
* **Parametrização:** Antes de realizar a primeira venda, é obrigatório cadastrar uma **Natureza de Operação** configurada especificamente com o Modelo 59 ativo para processar a saída de mercadorias via cupom.

---

## 2. Regra de Negócio: Ciclo de Numeração do SAT

A arquitetura do SAT difere estruturalmente do modelo de emissão da Nota Fiscal Eletrônica ([[NF-e]]) ou Nota Fiscal de Consumidor Eletrônica ([[NFC-e]]).

[Fluxo NF-e / NFC-e] 
ERP (Gera XML + Define Numeração) ------> SEFAZ (Valida e Autoriza)

[Fluxo CF-e SAT] 
ERP (Envia dados de venda limpos) ------> HARDWARE SAT (Gera XML + Assina + Define Número)

---### Comportamento de Atribuição de Números * **Controle Centralizado no Hardware:** O ERP monta e envia um lote contendo apenas os dados comerciais da venda (itens, valores, pagamentos). O hardware físico do SAT processa as informações, gera o arquivo XML definitivo, assina digitalmente e **atribui a numeração** correspondente ao cupom. * **Inexistência de Inutilização:** Diferente de outros modelos fiscais, no ecossistema SAT não existe a rotina de "Inutilização de Numeração" ou problemas com "Pulo de Faixa". Como o próprio hardware gerencia o contador interno sequencial, o risco de quebras de sequência numérica por falhas de software é nulo. 
--- ## 3. Fluxo de Venda e Emissão no PDV O processo de faturamento foi projetado para ser ágil e síncrono, operando em segundos a partir do fechamento do caixa. ### Fluxo de Execução Técnica 
1. O operador do PDV inicia a venda e realiza a inserção dos itens através do leitor de código de barras ou busca direta. 
2. É acionada a finalização da venda informando as **Formas de Pagamento** (ex: Dinheiro, Cartão). 
3. Ao **Gravar e Transmitir**, o ERP processa o comando em segundo plano: - *Cenário Local:* O ERP invoca a DLL local que se comunica diretamente via USB com o aparelho conectado na máquina. - *Cenário Servidor:* O ERP despacha a requisição via TCP/IP para a aplicação concentradora externa (`Servidor SAT`), que gerencia a fila e envia as informações para o hardware compartilhado.
4. O equipamento valida, armazena, consome o payload e devolve o status positivo com o XML assinado. 
5. O sistema captura o retorno e executa instantaneamente o comando de **Impressão do Extrato do Cupom SAT** na impressora não fiscal previamente vinculada. 
--- ## 4. Validação Visual de Conectividade do Módulo O módulo do PDV possui um indicador visual dinâmico localizado na parte superior da tela de vendas para que o operador acompanhe a saúde da conexão com o fisco antes de fechar a venda. 
---### Monitoramento de Status * **Status "Servidor em Operação":** Exibido em tempo real quando o sistema detecta que o concentrador de rede (`Servidor SAT`) está ativo e pronto para receber requisições de transmissão de cupons das estações escravas. * **Chaveamento Rápido:** A interface disponibiliza um botão de atalho rápido para o menu de configurações técnicas, permitindo ao suporte técnico chavear o modo de comunicação de *Servidor* para *Local* diretamente pela tela de vendas caso ocorram problemas de infraestrutura de rede no cliente. 
--- ## 5. Fluxo de Cancelamento de Cupom O cancelamento de um cupom emitido via SAT possui limitações legais severas que são espelhadas em regras de validação rígidas dentro do ERP.

---### Regras de Validação e Operação * **Prazo Limite Legal:** Um cupom fiscal gerado via SAT só pode ser cancelado em um período máximo de **até 30 minutos** após a sua emissão. Passado este período, o hardware rejeita a operação e o cancelamento deve ser feito por meios administrativos extracontáveis na SEFAZ. * **Justificativa Obrigatória:** Ao comandar a exclusão/cancelamento do pedido na tela do histórico de cupons emitidos, o ERP bloqueia a tela e exige a inserção de uma **Justificativa de Cancelamento** para fins de auditoria no banco de dados. * **Processamento:** O ERP aciona a função de cancelamento da DLL/Servidor passando o ID do cupom original. O emulador/equipamento SAT processa a reversão, estorna a operação fiscal e gera o extrato físico de cancelamento, disparado automaticamente para a impressora. 
> [!warning] Estorno de Estoque e Financeiro > O cancelamento efetuado com sucesso no módulo SAT realiza automaticamente o estorno físico das mercadorias de volta ao estoque gerencial do ERP e deleta os lançamentos gerados no Fluxo de Caixa vinculados àquele documento, evitando faturamento duplicado ou inconsistências de inventário.


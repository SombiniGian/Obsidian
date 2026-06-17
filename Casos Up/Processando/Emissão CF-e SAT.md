Este módulo demonstra o fluxo operacional de **Emissão de Cupões Fiscais Eletrónicos (CF-e SAT)** no ERP Código UP, abordando desde a configuração da natureza de operação até à gestão de cancelamentos `[00:00:00]`. Ao contrário das notas fiscais tradicionais (NF-e/NFC-e), o sistema SAT destaca-se pela alta velocidade de resposta e pela gestão delegada ao hardware `[00:00:31]`.

### 1. Preparação da Natureza de Operação `[00:00:09]`

Para que o sistema consiga processar o cupão, é necessário garantir que a natureza da operação esteja parametrizada com o modelo fiscal correto:

- **Modelo 59:** No cadastro de natureza de operação, deve selecionar-se especificamente o **Modelo 59 (SAT)** `[00:00:20]`.
    
- **Diferença de Fluxo:** Diferente da NF-e ou NFC-e, onde o ERP gere a numeração e a autorização junto aos servidores do Sefaz, no SAT, o sistema apenas envia um XML reduzido para o equipamento `[00:00:41]`. É o próprio hardware SAT que processa a validação, gera o número do cupão e retorna os dados fiscais finais ao ERP `[00:00:51]`. Por isso, não há controlo de numeração (salto de números) na retaguarda do ERP para este modelo `[00:01:05]`.
    

### 2. Modos de Transmissão (Local vs. Servidor) `[00:01:31]`

O ERP permite alternar dinamicamente entre os modos de comunicação para adaptar-se a diferentes infraestruturas de rede:

- **Modo Local:** O ERP comunica diretamente com a DLL do equipamento instalado na mesma estação de trabalho `[00:01:31]`, `[00:03:53]`. A transmissão é extremamente ágil `[00:02:01]`.
    
- **Modo Servidor:** Quando o equipamento SAT está fisicamente noutra máquina da rede, o ERP direciona os comandos para o "Servidor SAT" (aplicação _background_), que faz a ponte com o hardware `[00:02:31]`, `[00:03:10]`.
    

### 3. Fluxo de Emissão em Ponto de Venda (PDV) `[00:03:23]`

O processo de venda segue um fluxo simplificado para agilizar o atendimento ao cliente:

1. **Identificação do Modo:** No ecrã de vendas, um indicador visual mostra se o sistema está a comunicar via "Servidor" ou "Local" `[00:03:44]`.
    
2. **Lançamento e Pagamento:** O operador adiciona os itens e seleciona a forma de pagamento (ex: dinheiro) `[00:04:10]`, `[00:04:49]`.
    
3. **Transmissão e Impressão:** Ao gravar o pedido, o ERP transmite o XML para o SAT, que retorna a validação em milissegundos. A impressão do cupão ocorre automaticamente conforme o modelo de impressora configurado na retaguarda do sistema `[00:04:49]`, `[00:05:03]`.
    

### 4. Gestão de Cancelamentos `[00:06:38]`

Caso seja necessário anular uma operação fiscal já emitida:

- **Cancelamento Direto:** O utilizador acede ao histórico de vendas, seleciona o cupão desejado e clica em cancelar `[00:06:38]`.
    
- **Justificativa:** O sistema pode solicitar (opcionalmente) um motivo para o cancelamento, que é registado para fins de auditoria interna `[00:06:46]`.
    
- **Confirmação via Hardware:** O ERP envia o comando de cancelamento ao equipamento SAT. O emulador (ou hardware real) processa a anulação e atualiza o estado fiscal do cupão imediatamente no sistema `[00:06:58]`.
    

ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: [Assista ao vídeo no YouTube](https://www.youtube.com/watch?v=elcnR9FsFyY&t=53s).
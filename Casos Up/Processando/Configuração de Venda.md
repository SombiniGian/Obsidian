Este vídeo detalha as configurações e parametrizações críticas necessárias no ERP Código UP para a emissão de **NFC-e (Nota Fiscal de Consumidor Eletrónica)**. O processo envolve a correta sincronização entre a natureza de operação, o plano de contas financeiro e as regras de segurança do ponto de venda `[00:00:00]`.

### 1. Preparação da Natureza de Operação `[00:00:18]`

A emissão da NFC-e depende de uma configuração precisa da "Natureza de Operação":

- **Modelo 65:** No cadastro de naturezas de operação, é obrigatório selecionar o **Modelo 65** para NFC-e `[00:01:06]`, `[00:01:15]`.
    
- **Configurações Fiscais:** A finalidade da nota deve estar definida como "Normal", e a indicação de presença do comprador deve ser "Presencial" (ou "Presencial fora do estabelecimento") `[00:01:27]`, `[00:01:37]`.
    
- **Vinculação Financeira:** É essencial apontar o plano de contas e as contas de movimento corretas para que, ao finalizar a venda, o financeiro seja atualizado automaticamente `[00:01:45]`, `[00:02:02]`.
    

### 2. Configurações Financeiras e Formas de Pagamento `[00:02:27]`

Para que as formas de pagamento (dinheiro, cartão, etc.) apareçam no PDV e sejam validadas pela NFC-e:

- **Flags no Cadastro:** No ecrã de "Tipos de Documentos", as formas de pagamento pretendidas devem ter a opção **"Usa no PDV/NFC-e"** marcada `[00:02:27]`, `[00:02:37]`.
    
- **Consumidor Final:** O sistema utiliza um cadastro padrão de "Consumidor Final" para agilizar as vendas que não exigem a identificação do cliente no momento da emissão `[00:03:37]`, `[00:03:46]`.
    

### 3. Parametrização do Ponto de Venda (PDV) `[00:04:01]`

Na aba de configurações do PDV, definem-se as regras de negócio e a interface:

- **Tipo de Tela:** Deve ser configurado como **"Balcão"** (específico para NFC-e) em vez de "Pedido" (mais comum para indústrias/distribuidoras) `[00:04:10]`, `[00:04:44]`.
    
- **Segurança e Senhas de Liberação:** O sistema permite exigir uma senha de supervisor para:
    
    - Aplicar descontos `[00:08:29]`.
        
    - Alterar o valor unitário de um produto `[00:08:42]`.
        
    - Cancelar vendas ou excluir itens `[00:08:29]`.
        
    - Alterar a tabela de preços `[00:08:35]`.
        
- **Gestão de Caixas:** É recomendado vincular cada estação de trabalho a um "Caixa" específico para que a movimentação financeira reflita a realidade de cada terminal de vendas `[00:06:47]`, `[00:07:05]`.
    

### 4. Fluxo de Venda e Operação `[00:10:19]`

- **Interface:** O layout do PDV é flexível, permitindo ocultar ou exibir informações como cabeçalhos e totais `[00:10:30]`.
    
- **Gestão de Pedidos em Aberto:** O sistema permite salvar uma venda em aberto (estacionar o pedido) para retomar o atendimento posteriormente, facilitando o fluxo de loja `[00:10:50]`.
    
- **Comunicação Fiscal:** Após inserir os itens e as formas de pagamento, o sistema envia o XML para a Sefaz. O retorno positivo finaliza o cupão e imprime o DANFE NFC-e automaticamente `[00:14:01]`.
    

ℹ️ **Nota de Apoio:** A correta configuração das senhas de liberação (`suporte123` é o padrão) é vital para a segurança. Recomendamos que, após a instalação, altere estas credenciais. Para mais detalhes sobre a transmissão fiscal e resolução de erros, poderá aceder à continuação deste tutorial no canal ou visualizar o vídeo completo: [Assista ao vídeo no YouTube](https://www.youtube.com/watch?v=jSPyG3JarvA).
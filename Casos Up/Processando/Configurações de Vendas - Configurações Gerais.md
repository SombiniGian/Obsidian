---
id: [CASO-169]
link: https://www.youtube.com/watch?v=TQTc8uw_4TI&t=15s
setor: [Suporte, Implementação, Operacional]
modulo: [Vendas / Configurações Gerais]
tags: [configuracoes-de-vendas, pdv, perfil-de-tela, balanca, tef, bloqueios]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral das Configurações de Vendas]]
2. [[#Seleção do Tipo de Tela (Perfil de Interface)]]
3. [[#Parametrização de Dados Principais e Regras de Negócio]]
4. [[#Configurações Específicas de PDV e Contingência Fisco]]
5. [[#Integrações de Hardware (Balanças, Catracas e TEF)]]
6. [[#Pontos Críticos e Dicas de Implantação]]

# Visão Geral das Configurações de Vendas
O painel de **Configurações de Vendas** é o coração da parametrização operacional do ERP. Ele define o comportamento, as travas de segurança e a interface visual que o usuário final utilizará no momento do faturamento. Por ser um sistema altamente personalizável, o analista de implantação deve configurar estas regras *antes* de iniciar a operação no cliente, garantindo que o sistema obedeça às diretrizes comerciais, fiscais e logísticas da empresa.

Para acessar o painel, navegue até a listagem de **Pedidos de Venda** e clique no ícone da engrenagem (Configurações).

# Seleção do Tipo de Tela (Perfil de Interface)
A primeira e mais impactante configuração é o **Tipo de Tela**. O sistema permite adaptar o layout da rotina de vendas de acordo com o segmento do cliente final.

*   **Pedido (Indústria / Atacado):** Interface legada e densa. Exibe múltiplos campos simultâneos (comprador, vendedor, transportadora, placa do veículo, etc.). Ideal para distribuidoras e fábricas que necessitam de um detalhamento exaustivo no ato da venda.
*   **Balcão (Orçamento / Pré-venda):** Focada no operador e não no consumidor. Possui forte apelo em uso de teclado e atalhos rápidos para alteração de preços e tabelas. Muito utilizada em autopeças e lojas de materiais de construção onde o cliente está de costas para o monitor.
*   **Touch Screen:** Desenhada para monitores sensíveis ao toque. Obrigatória para o segmento de [[Restaurante / Mesas e Comandas]], pois habilita a gestão visual de complementos, montagem de pratos e pontos de preparo.
*   **PDV e PDV Super:** Telas modernas com apelo visual de varejo. São projetadas para ficarem de frente para o consumidor (Check-out de supermercados e lojas), permitindo personalização de cores, logomarcas e fontes.
*   **Autoatendimento:** Derivada da tela Touch, é utilizada em totens (kiosks). Bloqueia atalhos administrativos e guia o cliente final pelo fluxo de escolha de produtos e pagamento (via TEF ou Pix) sem intervenção de um funcionário.

# Parametrização de Dados Principais e Regras de Negócio
A aba "Dados Principais" concentra os bloqueios e os gatilhos automáticos do sistema.

### Regras de Estoque
*   **Bloquear vendas sem estoque:** Se ativado, o sistema impede a inclusão do item no carrinho se o saldo for menor ou igual a zero, evitando faturamento a descoberto.
*   **Alerta Contábil / Estoque Mínimo:** Se o bloqueio rígido não for desejado, o sistema pode apenas emitir um *warning* na tela avisando que o item atingiu o estoque de segurança, mas permitindo que a venda seja concluída (estoque negativo).

### Recálculo e Alteração de Cliente
*   **Ao alterar cliente (Buscar novos dados?):** Quando o operador inicia uma venda genérica e, no meio do processo, identifica o cliente (`Cliente B`), o sistema precisa saber como tratar os itens já lançados. Pode-se configurar para que ele busque automaticamente a *Tabela de Preço* e *Forma de Pagamento* do `Cliente B` e recalcule os valores do carrinho imediatamente, ou configurar para que mantenha os preços originais lançados.

### Gestão de Lotes (FIFO vs. Vencimento)
Se o cliente controla estoque por lote/validade, a baixa automática no momento da venda deve ser parametrizada:
*   **Por Vencimento (FEFO):** O sistema dá saída automática no lote que expira primeiro.
*   **Por Entrada (FIFO):** O sistema dá saída no lote que foi comprado/cadastrado há mais tempo no sistema.

# Configurações Específicas de PDV e Contingência Fisco
Na aba "PDV", o comportamento do terminal de check-out e as regras de impressão são moldados.

### Configurações de Estação (Máquina Local)
> [!info] Variáveis de Estação (Sinalizadas com Asterisco `*`)
> Configurações que possuem um asterisco ao lado do nome significam que são salvas no banco de dados vinculadas à máquina física atual (Estação de Trabalho). Isso permite que o Caixa 1 use a **Série Fiscal 1**, enquanto o Caixa 2 usa a **Série Fiscal 2**, mesmo compartilhando o mesmo painel de configurações gerais.

*   **Conta Caixa:** Define qual conta do [[Plano de Contas]] ou tesouraria receberá o dinheiro daquela estação específica (Ex: `Caixa 01 - Frente de Loja`).

### Tratamento de Offline / Contingência NFC-e
*   **Timeout de Comunicação (SEFAZ):** Tempo em segundos que o PDV aguardará a resposta da SEFAZ na emissão da nota. Se a internet falhar e o tempo estourar, o sistema entra automaticamente em **Modo de Contingência Offline**.
*   **Retorno ao Online:** Configuração de "tentativas". O sistema pode ser parametrizado para, a cada *X* minutos ou *Y* vendas, tentar pingar a SEFAZ novamente. Se a internet voltar, ele sai do modo offline sozinho, evitando que o lojista esqueça o sistema em contingência por dias.

# Integrações de Hardware (Balanças, Catracas e TEF)

### Balanças (Check-out vs. Etiqueta)
*   **Balança de Check-out:** Configuração da comunicação serial (COM) para a balança acoplada no caixa (ex: Toledo, Filizola). O operador coloca o produto, e o sistema lê o peso ao vivo.
*   **Balança Etiquetadora (Açougue/Padaria):** Configuração da máscara de leitura. O sistema aprende como extrair o peso ou valor total de dentro do código de barras impresso nos bastidores pela etiquetadora.

### TEF (Transferência Eletrônica de Fundos)
A aba TEF permite chavear a integradora de cartões que será chamada pelo faturamento:
*   Opções nativas incluem *Tef Dial*, *SiTef*, *PayGo*, *MultiCard*, entre outras.
*   Após homologar a solução, o sistema orquestrará as chamadas, imprimindo as vias do cartão diretamente no fechamento do cupom.

### Catracas de Acesso (Comandas)
Para padarias e casas noturnas, o sistema integra com catracas (coletoras de entrada e bloqueadoras de saída).
*   Ao entrar, a catraca lê a comanda e abre o consumo. No caixa, o sistema atrela o pagamento. Se o cliente tentar sair e inserir a comanda na catraca de saída sem ter quitado o débito no PDV, o hardware manterá a roleta travada.

# Pontos Críticos e Dicas de Implantação

> [!warning] Faturamento com Restrição Financeira
> Na aba Principal, a flag **Bloquear Pendência Financeira (Dias)** é uma trava crucial de proteção ao crédito. Se configurada (ex: `10` dias), o sistema impedirá o faturamento de qualquer novo pedido a prazo para um cliente que possua títulos vencidos há mais de 10 dias no [[Financeiro / Contas a Receber]].

> [!tip] Criação de Base Padrão (Laboratório)
> Como o painel conta com dezenas de marcações sensíveis, a melhor prática de engenharia é criar uma **Base de Dados Padrão (Modelo)**. O suporte realiza a configuração refinada de todas as regras (trocos, descontos, alertas) no laboratório. Ao fechar um novo contrato, o técnico apenas restaura esse banco de dados modelo no cliente e altera a razão social e CNPJ, mitigando o risco de esquecer gatilhos vitais na implantação do zero.


---
id: [CASO-001]
link: https://www.youtube.com/watch?v=JClmTdw6YM0
setor: Financeiro
modulo: Integrações Bancárias e PSP
tags: [pix, boleto-pix, psp, pdvp, financeiro, automacao, meios-de-pagamento]
data_criacao: {{date}}
---

## Sumário

1. [[#Visão Geral do Módulo]]
2. [[#Configurações de PSP (Provedor de Serviços de Pagamento)]]
3. [[#Parametrização de Tipo de Documento]]
4. [[#Fluxo de Operação e Emissão (PDV e Pedidos)]]
5. [[#Gestão Financeira e Baixa de Títulos]]
6. [[#Emissão em Lote (Borderô de Cobrança)]]
7. [[#Regras de Negócio e Vantagens Comerciais]]

---

## Visão Geral do Módulo

A funcionalidade de **[[PIX Cobrança]]** (também conhecida como Boleto PIX) permite a emissão de cobranças a prazo utilizando o ecossistema do PIX, substituindo os boletos bancários tradicionais. A solução elimina a necessidade de troca de arquivos de remessa/retorno (CNAB) com bancos, possuindo conciliação automatizada via API, e melhora o fluxo de caixa através da compensação instantânea.

O sistema divide a funcionalidade em dois conceitos operacionais:
*   **[[PIX Imediato]]**: Voltado para recebimento no ato da venda (ex: balcão, checkout).
*   **[[PIX Vencimento]]**: Voltado para vendas a prazo, comportando-se estruturalmente como um boleto, suportando parcelamentos e acréscimos.

---

## Configurações de PSP (Provedor de Serviços de Pagamento)

A parametrização base dita as regras financeiras da transação e como o sistema deve interagir com as APIs do integrador.

**Caminho:** Acesso ao cadastro de **PSP** > aba **Configurações**.

*   **Configuração de Taxas:** Permite definir a taxa de transação cobrada pelo integrador. Para o integrador **[[PDVP]]**, esta taxa é um valor fixo. Para outros PSPs, é possível configurar o percentual de desconto. Esta taxa já é provisionada para o desconto no lançamento financeiro.
*   **Configuração de Acréscimos:** Assim como nos boletos tradicionais, é possível configurar regras ativas para **Juros**, **Multa** e **Desconto** por antecipação.
*   **Dias de Validade (Após Vencimento):** Define o limite em dias em que o QR Code permanecerá ativo para pagamento após a data de vencimento. Passado este prazo, o próprio PSP cancela a cobrança automaticamente.
*   **Meios de Distribuição:**
    *   **Impressão:** O layout do PIX utiliza o gerador de relatórios do sistema, permitindo personalização total (tamanho, bobina térmica ou A4).
    *   **WhatsApp:** Habilita o disparo da cobrança (código Copia e Cola / Imagem) diretamente para o cliente, exigindo que o serviço interno de mensageria (Servidor de WhatsApp) esteja em execução.
    *   **E-mail:** Envio do link e detalhes da cobrança para a base cadastral do cliente.

> [!warning] Atenção à Compatibilidade de API
> Atualmente, a modalidade de **PIX Vencimento** (com agendamento, juros e multas) é uma funcionalidade estritamente suportada quando o provedor configurado for o **[[PDVP]]**. Outros provedores podem estar limitados apenas à emissão do PIX Imediato.

---

## Parametrização de Tipo de Documento

Para garantir a integridade dos relatórios e do fluxo de caixa, as cobranças PIX exigem validações estritas no fechamento da operação.

**Caminho:** Cadastro de **Tipos de Documento**.

Ao configurar um Tipo de Documento sinalizando a obrigatoriedade do uso do ecossistema PIX (seja ele imediato ou vencimento), o sistema passará a exigir:
1.  **Vínculo de Movimentação PIX:** É mandatório informar a operação contábil correspondente (Imediato ou Vencimento).
2.  **Conta Bancária de Destino:** O sistema trava a operação caso a conta bancária de liquidação não esteja mapeada e vinculada ao respectivo PSP no cadastro do documento.
3.  **Herança de Regras de Prazo:** O Tipo de Documento transfere integralmente suas regras nativas (quantidade de parcelas, intervalos em dias e permissão de alteração de parcelamento) para o PIX Vencimento, reaproveitando a lógica de vendas a prazo.

---

## Fluxo de Operação e Emissão (PDV e Pedidos)

O comportamento da interface se adapta dinamicamente dependendo da modalidade da cobrança escolhida no momento do faturamento (seja no Balcão ou via Pedido de Venda).

### 1. PIX Imediato
Ao selecionar esta forma de pagamento, o sistema renderiza a modal com:
*   **QR Code Dinâmico:** Gerado em tempo real com o valor exato.
*   **Botão WhatsApp:** Abre um teclado virtual para inserção rápida do número do cliente e disparo da cobrança.
*   **Botão Copia e Cola:** Copia a string de payload para área de transferência.
*   **Mecanismo de Fechamento Automático:** O sistema entra em estado de *polling* (escuta). Assim que o cliente processa o pagamento no aplicativo do banco, o sistema reconhece o retorno do webhook instantaneamente, finaliza a venda e fecha a tela sem necessidade de interação humana.

> [!tip] Dica de Homologação
> Se o PSP estiver configurado em "Ambiente de Teste", a interface exibirá um botão exclusivo chamado **Simular Pagamento**, permitindo homologar o fluxo de baixa automática sem efetuar transações reais.

### 2. PIX Vencimento (Boleto PIX)
Comporta-se funcionalmente como um crediário. Ao selecionar o pagamento a prazo:
*   Abre-se a tela de gestão de parcelamento (herdando do Tipo de Documento a divisão de parcelas e as datas projetadas).
*   Ao concluir, uma janela de consolidação exibe todas as faturas geradas, oferecendo as opções de imprimir o carnê/boletos, disparar via WhatsApp ou enviar por E-mail em massa.

> [!warning] Validação Crítica de Cadastro
> É impossível gerar um PIX Vencimento para o "Consumidor Final". A API do Banco Central e do PSP exige um sacado formalmente identificado. **Obrigatoriamente**, o cliente vinculado à venda deve possuir um cadastro completo contendo Cidade e Documento Válido (**CPF ou CNPJ**).

---

## Gestão Financeira e Baixa de Títulos

A maior vantagem arquitetural da substituição de Boletos por [[PIX Cobrança]] ocorre no backoffice financeiro.

**Caminho:** Módulo **Financeiro** > **Cobranças**.

*   **Identidade Visual:** A listagem global recebeu iconografia específica, permitindo ao usuário distinguir visualmente Cartões, Boletos e títulos transacionados em PIX.
*   **Comportamento dos Títulos:**
    *   **PIX Imediato:** Como a liquidação ocorre em tempo de execução, estes títulos já chegam no módulo Financeiro com o status "Baixado" (exceto em casos de falha de energia durante o QR Code, onde a transação morre precocemente).
    *   **PIX Vencimento:** Chegam com o status "Em Aberto", aguardando a liquidação futura pelo sacado.
*   **Conciliação Automatizada (Fim do CNAB):**
    Para registrar as baixas, o operador **não** necessita fazer download/upload de arquivos `.rem` ou `.ret` no site do banco.
    1.  O usuário clica no botão **Baixar**.
    2.  Informa a data de recebimento e clica em **Pesquisar**.
    3.  O sistema consome a API do PSP de forma massiva e lista todos os títulos liquidados naquele intervalo.
    4.  Com um clique em **Processar**, todas as faturas recebem baixa no ERP de forma atômica e instantânea.

---

## Emissão em Lote (Borderô de Cobrança)

A funcionalidade atende modelos de negócio de recorrência (mensalidades, clubes de assinatura, serviços de provedores).

**Caminho:** **Financeiro** > **[[Borderô de Cobrança]]**.

1.  O operador filtra os clientes mensalistas em lote.
2.  Clica em **Gerar**. Onde antes existia apenas a opção "Emitir Boletos", agora a interface disponibiliza o botão **PIX**.
3.  O sistema exige o Tipo de Documento de recebimento, permite a inclusão de uma mensagem customizada na instrução e gera todas as cobranças em massa.
4.  No grid final, selecionam-se os títulos emitidos, permitindo disparar os links por E-mail ou WhatsApp (utilizando os contatos da ficha cadastral) de uma única vez.

---

## Regras de Negócio e Vantagens Comerciais

O modelo do PIX Cobrança viabiliza uma nova linha de receita recorrente para o distribuidor/revenda de software, baseada em arbitragem de tarifas.

> [!info] Oportunidade de Monetização
> Ao contrário do sistema bancário tradicional — que frequentemente tarifa a empresa no ato da *emissão* ou *registro* do boleto (independente de ser pago ou não) — o gateway de PIX normalmente possui tarifas na casa dos centavos e **somente sobre títulos liquidados**.

**Exemplo Prático de Arbitragem:**
1.  **Custo Atual do Cliente:** Paga ao banco tradicional `R$ 2,00` por boleto emitido.
2.  **Custo da Revenda de Software (PSP):** A revenda paga ao provedor (ex: PDVP) `R$ 1,00` (ou menos) apenas sobre o título liquidado.
3.  **Proposta de Valor:** A revenda repassa a tecnologia para o cliente final cobrando uma tarifa de `R$ 1,50`.
4.  **Resultado Econômico:**
    *   **Para o Cliente Final:** Redução de R$ 0,50 no custo por título, isenção de tarifa sobre emissão não liquidada, compensação financeira imediata (o dinheiro cai em tempo real) e eliminação da burocracia de manipular arquivos de remessa.
    *   **Para a Revenda:** Lucro líquido passivo de `R$ 0,50` por cada transação efetuada dentro da base de clientes, criando receita contínua integrada ao próprio ERP.
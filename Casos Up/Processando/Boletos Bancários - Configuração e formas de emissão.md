---
id: CASO-021-022
link:
  - https://www.youtube.com/watch?v=2EDlh07da_g
  - https://www.youtube.com/watch?v=8j3AqG6P2Hg
setor: Suporte, Faturamento, Financeiro
modulo: Pedidos, Cadastros e Contas a Receber
tags:
  - boleto-bancario
  - faturamento
  - formas-de-pagamento
  - contas-a-receber
  - remessa-bancaria
  - upsystem
data_criacao: 2026-06-24
---

# Manual de Configuração e Emissão de Boletos Bancários

Este documento técnico descreve de ponta a ponta a parametrização do módulo de boletos, o fluxo de emissão (avulsa ou via faturamento de pedidos), as regras de negócio de desacoplamento de títulos e a gestão de arquivos de remessa no sistema [[UpSystem]].

---

## Sumário

1. [[#1. Parâmetros e Cadastros Iniciais]]
2. [[#2. Fluxos de Emissão de Boletos]]
3. [[#3. Arquitetura de Vinculação e Regras de Negócio]]
4. [[#4. Gestão de Arquivos de Remessa]]
5. [[#5. Pontos Críticos e Resolução de Problemas]]

---

## 1. Parâmetros e Cadastros Iniciais

Para que o sistema esteja apto a gerar boletos bancários, três cadastros básicos precisam estar devidamente relacionados.

### A. Tipo de Documento

- Deve existir um cadastro de Tipo de Documento específico para a operação (ex: **Boleto Bancário**).
- A flag **"Movimentar boletos bancários"** deve estar obrigatoriamente marcada.
- _Diretriz:_ O usuário pode optar por criar um único tipo genérico para todos os bancos ou criar um tipo para cada instituição (ex: _Boleto Sicoob_, _Boleto Banco do Brasil_) conforme sua preferência de organização.

### B. Conta Bancária / Conta Caixa

No cadastro de contas de tipo "Bancária", o sistema habilita os campos de agência, conta, número do banco e titularidade. Após o preenchimento dos dados básicos, abre-se a aba **Configurações para Boletos Bancários**, onde devem ser informados:

- Carteira, convênio e Layout de transmissão (ex: CNAB 400).
- Agência/Código do cedente e regras de juros, multa ou dias para protesto.
- Caminho de rede/diretório local para gravação dos arquivos de **Remessa** e leitura de **Retorno**.
- Logotipos e caminhos dos arquivos físicos de impressão do boleto.

### C. Formas de Pagamento

- Identifique a forma de pagamento comercial (ex: _Boleto 30 dias_).
- Vincule o tipo de documento configurado para boletos e a **Conta Bancária** que receberá os fundos.
- Defina as regras de parcelamento padrão (ex: 2 parcelas com intervalo de 30 dias) e possíveis descontos comerciais na nota fiscal.

---

## 2. Fluxos de Emissão de Boletos

O sistema permite a geração de boletos por dois caminhos operacionais distintos:

### Fluxo A: Emissão a partir do Faturamento de Pedidos

1. Acesse o **Pedido de Venda** e selecione a Forma de Pagamento atrelada ao boleto bancário.
2. Na aba financeira, o lançamento inicial constará como um débito normal aberto.
3. Ao clicar no botão **Emitir Boleto** e confirmar a caixa de diálogo, o sistema processará as parcelas, aplicará as taxas/juros da carteira e **faturará o pedido automaticamente**.

### Fluxo B: Emissão Avulsa (Contas a Receber)

1. Acesse **Financeiro > Recebimentos** e lance um título manual (utilizando duplicata ou crédito, já que opções de boleto não aparecem em lançamentos avulsos de entrada).
2. Selecione o título gerado, acesse o menu **Opções** e clique em **Gerar Boleto**.
3. O sistema solicitará a conta bancária emitente. Ao confirmar, o tipo de documento do título original é convertido e indexado ao novo boleto.

---

## 3. Arquitetura de Vinculação e Regras de Negócio

A regra de integridade do ERP baseia-se no **desacoplamento total** entre o título financeiro e o documento de cobrança.

- **Bloqueio de Alteração:** Um título financeiro associado a um boleto ativo não pode ter seus dados (como vencimento ou valor) alterados diretamente, pois o boleto pode já estar em posse do cliente ou registrado no banco.
- **Persistência do Débito:** O boleto é apenas o meio de cobrança. Se o boleto for cancelado no sistema, o título financeiro (a dívida do cliente) **não é extinto**; ele apenas perde o vínculo com o boleto e retorna ao status de "débito normal", permitindo receber via cheque, dinheiro ou ser reemitido em outra carteira bancária.

---

## 4. Gestão de Arquivos de Remessa

A transmissão dos boletos gerados para registro no banco ocorre na tela de **Movimentações Financeiras > Boletos Bancários > Remessa**.

1. **Filtragem:** O operador seleciona a conta bancária desejada. O sistema filtra e exibe estritamente os boletos pendentes daquele banco.
2. **Geração:** Seleciona-se os títulos e clica-se em **Gerar Arquivo**. O lote será salvo na pasta parametrizada na conta caixa.
3. **Controle de Lotes:** O painel de remessas mantém o histórico de arquivos gerados:
   - **Cancelar Remessa:** Se o lote foi gerado com erros de configuração ou falta de dados, a remessa pode ser cancelada _antes_ do envio. Todos os boletos internos voltam ao status "Em Aberto".
   - **Confirmar Envio:** Uma vez enviado o arquivo ao banco (via van ou internet banking), o usuário deve clicar em "Confirmar Envio". Isso trava o lote contra cancelamentos acidentais e muda o status dos boletos para **"Enviado ao Banco"**.

---

## 5. Pontos Críticos e Resolução de Problemas

> [!warning] Cancelamento de Boletos pós-Remessa
> Se um boleto precisar ser cancelado **depois** que a remessa já foi gerada e enviada ao banco, a operação de cancelamento no sistema deve ser feita normalmente. O ERP identificará que o título já foi transmitido e gerará automaticamente uma **instrução de baixa/cancelamento** no próximo arquivo de remessa para que o banco invalide o título do lado deles. Se o cancelamento ocorrer **antes** da geração da remessa, o boleto é descartado sem ônus de tarifas bancárias de registro.

### Matriz de Status do Boleto

| Status no Painel         | Significado Operacional                                      | Permite Cancelamento?         | Próxima Ação Esperada                   |
| :----------------------- | :----------------------------------------------------------- | :---------------------------- | :-------------------------------------- |
| **Em Aberto**            | Boleto gerado no sistema, pendente de registro.              | Sim (Livre)                   | Incluir em um lote de Remessa.          |
| **Enviado ao Banco**     | Arquivo de remessa gerado e confirmado pelo usuário.         | Sim (Gera instrução de baixa) | Aguardar leitura do arquivo de Retorno. |
| **Baixado / Descontado** | Cliente efetuou o pagamento e o banco confirmou o crédito.   | Não (Requer estorno)          | Conciliação e arquivamento.             |
| **Cancelado**            | Documento invalidado. O título original voltou a ser débito. | Não se aplica                 | Liquidar por outro meio ou reemitir.    |

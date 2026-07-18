---
id: PIX-001
link: https://www.youtube.com/watch?v=VzSDwaiqJlQ
setor: Financeiro
modulo: Integração PIX
tags: [pix, psp, automacao, pdv, banco-do-brasil, pdvp]
data_criacao: 2026-07-18
---

# Integração Direta de Cobrança via PIX (PSP)

## Sumário
- [[#Visão Geral e Benefícios]]
- [[#Provedores Homologados (PSPs)]]
- [[#Fluxo de Configuração]]
	- [[#1. Cadastro do Provedor de Pagamento]]
	- [[#2. Parametrização do Tipo de Documento]]
- [[#Fluxo de Execução e Rotinas]]
	- [[#Faturamento no PDV]]
	- [[#Baixa de Contas a Receber]]
- [[#Gestão e Monitoramento de Cobranças]]
- [[#Roadmap e Futuras Implementações]]

---

## Visão Geral e Benefícios

A integração direta de PIX com Provedores de Serviço de Pagamento (PSP) elimina a obrigatoriedade do uso de TEF (Transferência Eletrônica de Fundos) para emissão de PIX dinâmico no sistema. Anteriormente, o fluxo exigia a contratação de uma plataforma TEF e o uso de um pinpad para exibir ou imprimir o QR Code. Com a nova arquitetura, o sistema se comunica **diretamente com as APIs dos bancos e carteiras digitais**, reduzindo custos operacionais e intermediários na transação.

> [!info] O que é um PSP?
> Um PSP (Provedor de Serviços de Pagamento) é a entidade responsável por processar as transações financeiras. A integração direta via API permite que o software receba os *callbacks* (notificações de pagamento) em tempo real, agilizando o processo de checkout.

---

## Provedores Homologados (PSPs)

O sistema foi arquitetado para suportar múltiplos provedores de forma dinâmica. Alguns bancos exigem configurações complexas (como geração e vínculo de certificados digitais), enquanto outros possuem integrações baseadas apenas em chaves de acesso.

Atualmente, os seguintes provedores estão testados, homologados e **100% operacionais**:
- **Banco do Brasil**: Integração simplificada, baseada no preenchimento de credenciais.
- **PDVP**: Provedor parceiro oficial.

> [!warning] Atenção: Homologação de Novos Bancos (ex: Itaú, Bradesco)
> A lista de PSPs no sistema contém provedores que ainda não foram plenamente validados por falta de ambiente de homologação. Caso um cliente necessite utilizar um banco não certificado, será necessário solicitar as credenciais reais do cliente para que a equipe técnica realize a parametrização e os testes antes de liberar o PSP para uso em ambiente de produção.

---

## Fluxo de Configuração

Para que a geração do PIX ocorra perfeitamente no [[PDV]] e na retaguarda, duas etapas de parametrização são obrigatórias.

### 1. Cadastro do Provedor de Pagamento
Caminho: **Financeiro** > **PIX Controles** > **Provedor de Pagamentos**

Nesta tela, cadastra-se o motor de comunicação com o banco escolhido:
1. Adicione os dados do recebedor (Nome da conta, Chave PIX, Dados bancários).
2. Configure as credenciais fornecidas pelo banco (Client ID, Secret, etc.).
3. Defina o campo **Ambiente** (certifique-se de alterar de **Testes** para **Produção** quando for iniciar a operação real).
4. *Opcional*: A tela possui endpoints de teste (ex: gerar cobrança imediata, consultar cobrança). Isso permite validar se a comunicação com o banco está operante antes de disponibilizá-la no PDV.

### 2. Parametrização do Tipo de Documento
Caminho: **Cadastros** > **Tipo de Documento**

Esta etapa vincula uma forma de pagamento do sistema ao motor de PSP configurado.
1. Crie ou edite o tipo de documento destinado ao PIX.
2. Marque a *flag* **PIX**.
3. É **obrigatório** marcar a opção **Movimentar Conta Bancária** e selecionar a conta correspondente. Se isso não for feito, o sistema bloqueará a operação, pois a liquidação financeira deve ocorrer de forma automática.
4. Na aba **Configurações de Venda**, selecione o PSP que aquele documento irá acionar (ex: *Pix Banco do Brasil*).

> [!tip] Dica: Roteamento Inteligente por PSP
> É possível definir um **Valor Mínimo** e **Valor Máximo** no Tipo de Documento. Isso permite criar estratégias financeiras (ex: valores baixos vão para o banco X que não cobra taxa, enquanto valores mais altos vão para o banco Y). O sistema bloqueará a transação se o valor da venda estiver fora das regras estabelecidas para o PSP selecionado.

---

## Fluxo de Execução e Rotinas

### Faturamento no PDV
O processo de caixa foi desenhado para ser fluido e sem interação desnecessária do operador:
1. Na tela de finalização, o operador seleciona o **Tipo de Documento** configurado para PIX.
2. O sistema abre automaticamente uma *modal* renderizando o **QR Code** na tela, entrando em estado de escuta (aguardando o pagamento).
3. O cliente realiza a leitura pelo aplicativo bancário.
4. Ao receber o *webhook* do PSP confirmando o recebimento, o sistema finaliza a venda **automaticamente**, liberando o caixa.

**Ações disponíveis na Modal de Pagamento:**
- **Copiar**: Gera a *string* do "PIX Copia e Cola" para envio rápido.
- **Cancelar**: Permite ao operador abortar a escuta do pagamento caso o cliente desista ou queira alterar a forma de pagamento.
- *(Funcionalidades previstas para o layout)*: Botão para enviar o QR Code por e-mail ou disparar diretamente pelo servidor do módulo [[WhatsApp]] integrado.

### Baixa de Contas a Receber
O mesmo componente desenvolvido para o caixa está disponível na retaguarda financeira.
1. Acesse o módulo **Contas a Receber**.
2. Selecione um título em aberto e clique no botão **Pagar**.
3. Ao selecionar o pagamento via PIX, a tela de geração do QR Code será exibida, efetuando a baixa automática do título e sua respectiva movimentação bancária assim que o cliente liquidar a cobrança.

---

## Gestão e Monitoramento de Cobranças

Caminho: **Financeiro** > **PIX Cobranças**

Todas as requisições geradas pelo sistema possuem rastreabilidade. Esta tela atua como um painel de conciliação, listando a origem (venda ou título), a movimentação bancária vinculada e o status da operação:
- **Aberta**: O QR Code foi gerado, mas o pagamento ainda não foi efetuado.
- **Paga**: A liquidação foi confirmada pelo banco.
- **Cancelada**: Operação abortada manualmente pelo operador de caixa.
- **Cancelada pelo PSP**: O banco rejeitou a transação ou o tempo do QR Code expirou.
- **Devolvido**: Houve estorno do valor.

> [!warning] Atenção: Tratamento de Quedas (Recuperação de Status)
> Caso haja uma interrupção crítica (ex: queda de energia) exatamente após o cliente pagar, o *webhook* pode não ser processado, mantendo a cobrança como **Aberta** localmente. Nesse cenário, o operador deve localizar a cobrança na tela de gestão e acionar a consulta manual. O sistema irá requisitar o status real na API do banco e questionar se o usuário deseja atualizar o *status* local do software, efetuando a baixa com segurança.

---

## Roadmap e Futuras Implementações

A arquitetura do novo motor de PIX viabiliza os seguintes recursos (em fase de planejamento/desenvolvimento):

1. **Mensalidades e Renovação de Licença (B2B)**: 
   Inclusão de um recurso na interface do usuário (lojista) para gerar o pagamento da própria mensalidade do software via PIX, dispensando a emissão manual de boletos. O sistema também exibirá o QR Code ativamente em telas de aviso de bloqueio por inadimplência.
2. **Cobrança por Vencimento (Substituto do Boleto)**: 
   Geração de PIX com data de validade futura. Isso integrará diretamente com o módulo de Contas a Receber, operando como um boleto registrado digital.
3. **Integração com Ecossistema Mobile**:
   - **Força de Vendas (Pronta Entrega)**: Geração do QR Code no aplicativo do vendedor para recebimento imediato no ato da entrega da mercadoria.
   - **Aplicativo de Restaurantes**: Permissão para que garçons exibam o QR Code em seus *smartphones* ou *tablets* diretamente na mesa, agilizando o fluxo do restaurante sem a necessidade de deslocamento ao caixa físico.
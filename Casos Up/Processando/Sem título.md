
---
id: CASO-043
link: https://www.youtube.com/watch?v=pTcujjfK-l0
setor: Suporte, Desenvolvimento
modulo: Frente de Caixa / PDV (NFC-e)
tags: [pdf, nfc-e, contingência, faturamento, regras-de-negocio]
data_criacao: 2026-06-23

---

# Fluxo de Venda no PDV e Transmissão de NFC-e

## 1. Introdução e Visão Geral
Este documento descreve as regras de negócio, o fluxo operacional de vendas no Ponto de Venda (PDV) e os processos de contingência na transmissão da [[Nota Fiscal de Consumidor Eletrônica (NFC-e)]]. O entendimento central do sistema baseia-se na segregação de duas entidades independentes: o **Pedido/Venda** e a **Nota Fiscal**.

> [!info] Conceito Chave: Independência de Entidades
> A venda e a nota fiscal são tratadas como registros distintos no banco de dados. Uma venda concluída com sucesso gera o gatilho para a emissão de uma nota fiscal, porém falhas na autorização da nota fiscal não estornam automaticamente a venda. Uma única venda pode possuir múltiplos históricos de tentativas ou documentos fiscais atrelados (como em casos de cancelamento e reemissão).

---

## 2. Sumário
- [[#1. Introdução e Visão Geral]]
- [[#3. Regras de Negócio e Validações]]
- [[#4. Fluxo de Operação Padrão (Caminho Feliz)]]
- [[#5. Tratamento de Erros e Contingência de Transmissão]]
- [[#6. Desfazimento e Cancelamento de Faturamento]]

---

## 3. Regras de Negócio e Validações

O sistema possui travas de integridade para garantir o cumprimento da legislação fiscal e evitar rejeições da Secretaria da Fazenda (SEFAZ).

### 3.1 Venda a Prazo para Consumidor Final
* **Regra:** Não é permitido realizar vendas com modalidade de pagamento a prazo (geração de duplicatas/contas a receber) utilizando o cadastro genérico de "Consumidor Final".
* **Comportamento Esperado:** Caso o operador tente finalizar um pedido sem identificação com uma forma de pagamento a prazo, o sistema exibirá um bloqueio em tela.

> [!warning] Validação de Crédito
> Para vendas a prazo, torna-se obrigatória a identificação nominal do cliente por meio de seu cadastro (CPF/CNPJ). Caso contrário, a operação financeira não pode ser provisionada em aberto.

---

## 4. Fluxo de Operação Padrão (Caminho Feliz)

O fluxo a seguir demonstra a emissão contínua e automatizada sob condições ideais de comunicação com os servidores da SEFAZ:

```

[Iniciar Venda] ➔ [Inserir Itens] ➔ [Pressionar F5 (Finalizar)] ➔ [Selecionar Dinheiro] ➔ [Confirmar] ➔ [Transmissão Automática] ➔ [Impressão do DANFE]

```

1. Na tela principal do PDV, insira os produtos na lista de itens utilizando o leitor de código de barras ou a busca manual.
2. Utilize os atalhos de gerenciamento (como a alteração de preço ou inserção de descontos, sujeitos à liberação por senha de supervisor se configurado).
3. Pressione a tecla de atalho correspondente para **Finalizar a Venda** (ex: **F5** ou **F12**, variando conforme layout).
4. Informe o meio de pagamento (ex: **Dinheiro**).
5. Digite o valor pago pelo cliente para que o sistema calcule e exiba o valor do troco na tela.
6. Pressione **Confirmar**.
7. O sistema processa o fechamento financeiro e executa a transmissão assíncrona da NFC-e em segundo plano.
8. Após o retorno positivo de autorização da SEFAZ, a tela de visualização ou a impressão direta do arquivo do DANFE (Documento Auxiliar da NFC-e) é disparada conforme as configurações locais de impressão do terminal.

---

## 5. Tratamento de Erros e Contingência de Transmissão

### 5.1 Desencadeamento de Falhas
Quando ocorre um erro na validação do arquivo XML ou na comunicação com o webservice da SEFAZ (por exemplo, parâmetros incorretos como o *Identificador de Presença* inválido), o sistema bloqueia a conclusão fiscal da venda e adota a seguinte postura:

1. Uma mensagem contendo a rejeição oficial da SEFAZ ou o erro interno do componente de transmissão é exibida na tela.
2. Ao clicar em **OK**, o PDV abre imediatamente e de forma automática a tela de edição e gerenciamento de **Nota Fiscal**.

### 5.2 Correção de Parâmetros Fiscais
Com a tela de Nota Fiscal aberta, o operador ou a equipe de suporte pode intervir no documento sem a necessidade de refazer a venda:

* É possível navegar pelas abas da nota para inspecionar os **Itens**, dados de **Identificação** e **Totais**.
* Caso a falha seja cadastral (como o tipo de atendimento ou ausência de dados do cliente), realiza-se a correção diretamente no campo divergente.
* Após a retificação, clique no botão **Salvar Nota**.
* O sistema efetuará uma nova tentativa de validação, geração do XML e transmissão para a SEFAZ.

```

+-------------------------------------------------------------+

| Erro na Transmissão (Rejeição SEFAZ / Parâmetro Inválido) |

+-------------------------------------------------------------+

│

▼

+-------------------------------------------------------------+

| Abertura Automática da Tela de Manutenção de Nota Fiscal |

+-------------------------------------------------------------+

│

▼

[ Correção dos dados / Campos ]

│

▼

+-------------------------------------------------------------+

| Botão "Salvar Nota" ➔ Nova tentativa de Envio |

+-------------------------------------------------------------+

```

> [!tip] Análise de Rejeições Recorrentes
> Se o erro persistir devido a problemas estruturais ou duplicidade de numeração (comum em ambientes de homologação ou troca de base de dados), o operador pode fechar a tela de tratamento de notas. A venda ficará gravada no sistema como concluída, porém com a nota fiscal associada sob o status de **Sem Confirmação** (Pendente), permitindo o tratamento posterior pela retaguarda.

---

## 6. Desfazimento e Cancelamento de Faturamento

Caso uma venda apresente erros críticos na nota fiscal que impeçam a sua emissão correta e seja necessário reiniciar o atendimento ao cliente, deve-se estornar o status financeiro da operação.

### 6.1 Processo de Cancelamento de Faturamento
1. Acesse a tela de gerenciamento de vendas/pedidos do terminal.
2. Localize o registro da venda associada à nota rejeitada ou travada.
3. Clique no botão ou utilize a opção **Cancelar Faturamento** (não confundir com Cancelar Pedido).
4. O sistema exibirá o seguinte alerta de validação:
   > *"Pedido possui vínculo com nota fiscal e não será excluída. Tem certeza que deseja cancelar o faturamento?"*
5. Clique em **Sim** para confirmar e digite a senha do supervisor se for solicitado pelo sistema.

### 6.2 Comportamento do Sistema após o Estorno
* **Status do Pedido:** O pedido retorna do estado "Faturado" para o estado **Em Aberto**, ficando disponível na tela para edição, exclusão de itens ou nova tentativa de fechamento.
* **Status da Nota Fiscal:** A nota fiscal vinculada originalmente se torna uma entidade órfã rejeitada/cancelada, garantindo que o número fiscal correspondente possa ser tratado isoladamente (ou inutilizado), enquanto o pedido ganha a liberdade para gerar uma nova numeração sequencial de NFC-e ao ser refaturado.
```
---
id: CASO-023
link: https://www.youtube.com/?hl=pt&gl=BR&app=desktop
setor: Faturamento, Logística, Financeiro
modulo: Cargas e Distribuição
tags:
  - montagem-de-carga
  - faturamento-em-lote
  - nfe
  - romaneio
  - acerto-motorista
  - upsystem
data_criacao: 2026-06-24
---

# Fluxo de Montagem, Faturamento e Acerto de Cargas

Este documento descreve as diretrizes operacionais para o ciclo completo de gerenciamento de cargas no sistema [[UpSystem]]. O módulo foi projetado para centralizar as operações de distribuição de mercadorias, unificando a montagem de romaneios, o faturamento em lote de notas fiscais eletrônicas, a impressão massiva de boletos bancários e o controle financeiro de acerto com motoristas.

---

## Sumário
1. [[#1. Pré-requisitos e Cadastros Base]]
2. [[#2. Processo de Montagem de Carga]]
3. [[#3. Faturamento em Lote e Transmissão de NF-e]]
4. [[#4. Emissão Massiva de Boletos da Carga]]
5. [[#5. Retorno de Viagem e Acerto com o Motorista]]
6. [[#6. Regras de Validação e Pontos de Falha]]

---

## 1. Pré-requisitos e Cadastros Base

Para que a roteirização e os cálculos de cubagem operem com precisão dentro do módulo de cargas, é indispensável a correta parametrização dos cadastros adjacentes:

* **Cadastro de Produtos:** Deve conter os campos de peso líquido, peso bruto e cubagem (metragem cúbica) preenchidos. A ausência desses dados impede o sistema de calcular a capacidade ocupada do caminhão.
* **Cadastro de Veículos:** Cadastro da frota logística indicando a capacidade máxima em peso e a metragem cúbica limite suportada pelo baú.
* **Integração Força de Vendas:** Os pedidos de venda entram no sistema como pendentes, geralmente originados via sincronização de tablets ou smartphones da equipe de campo, aguardando a consolidação logística.

---

## 2. Processo de Montagem de Carga

A montagem agrupa os pedidos com base na estratégia de entrega (região, rotas ou canais de venda).

1. Acesse o menu **Movimentações > Cargas**.
2. Clique em **Incluir** para abrir uma nova carga e informe uma **Descrição** que sirva de identificação (ex: *Rota Zona da Mata*).
3. Selecione o **Transportador** e o **Veículo** responsável.
4. Para associar os documentos de venda, clique no botão de pesquisa de pedidos.
5. Utilize os filtros avançados por **Região**, **Vendedor**, **Cidade** ou **Data de Emissão** para isolar a carteira pendente.
6. Selecione os registros desejados e adicione-os à carga.

> [!tip] Roteirização Manual por Ordenação de Entrega
> Dentro do painel da carga, o operador pode utilizar as setas de ordenação da grade de pedidos para sequenciar as entregas. Mover um pedido para cima ou para baixo altera diretamente a ordem de impressão das notas e do **Romaneio de Entrega**, facilitando a logística do motorista na desidratação do caminhão (carregamento inverso).

---

## 3. Faturamento em Lote e Transmissão de NF-e

Uma vez consolidada a carga, o processo de faturamento permite emitir e validar os documentos fiscais em lote.

1. No painel de cargas, selecione a carga criada e acione a rotina de **Faturamento**.
2. O sistema listará todos os pedidos anexados. A navegação sequencial entre os pedidos permite visualizar notas internas e observações inseridas pelos vendedores.
3. Utilize o atalho **F5** para processar o faturamento individualizado revisando o conteúdo ou selecione em lote para transmissão massiva.
4. Configure as opções de transmissão:
   - **Envio Automático de Nota Fiscal:** Transmite o arquivo XML diretamente para a [[SEFAZ]].
   - **Envio Automático de E-mail:** Envia o documento fiscal eletrônico e o arquivo XML para o e-mail do cliente cadastrado.
5. Clique em **Transmitir Notas** para iniciar a comunicação assíncrona com o fisco.

---

## 4. Emissão Massiva de Boletos da Carga

O grande ganho operacional do módulo é a possibilidade de gerar os boletos bancários de todos os pedidos integrantes da carga de forma simultânea.

* O sistema faz a leitura interna das [[Formas de Pagamento]] associadas a cada pedido (ex: *Boleto Sicoob*, *Boleto Banco do Brasil*).
* Ao acionar a opção **Imprimir Todos os Boletos da Carga**, a rotina realiza uma ordenação inteligente por instituição financeira.
* O sistema agrupa e realiza a chamada de impressão primeiro para os títulos de um determinado banco (ex: Banco do Brasil) e, na sequência, inicia os da próxima instituição (ex: Sicoob), evitando gargalos ou mistura de layouts.

---

## 5. Retorno de Viagem e Acerto com o Motorista

Após a conclusão das entregas, o veículo retorna para a empresa e o operador realiza a rotina de encerramento da carga na aba **Acerto**.

1. **Dados de Viagem:** Insira as informações de quilometragem de saída, quilometragem de chegada e data de retorno. Com base no cadastro do veículo, o sistema calcula a média de consumo de combustível.
2. **Despesas de Viagem:** Registre os gastos ocorridos no trajeto, como combustíveis, pedágios, alimentação ou manutenção emergencial.
3. **Conferência de Valores por Meio de Pagamento:** O sistema apresenta um relatório com o somatório dos títulos agrupados por tipo de recebimento.

> [!info] Exemplo Prático de Agrupamento de Acerto
> Para uma carga com valor total de R$ 10.000,00, o painel exibe:
> - **Boleto:** R$ 5.000,00 (O operador confere os canhotos assinados e boletos entregues).
> - **Cheque:** R$ 3.000,00 (O motorista deve entregar R$ 3.000,00 em folhas de cheque físicas).
> - **Dinheiro:** R$ 2.000,00 (O motorista deve realizar a entrega da espécie em espécie no caixa).

4. **Fechamento Financeiro:** O sistema deduz as despesas gerais do valor líquido da carga e exibe o indicador de lucratividade real da viagem. Caso o motorista tenha saído com adiantamento, o sistema calcula o saldo de devolução ou reembolso.

---

## 6. Regras de Validação e Pontos de Falha

Abaixo estão listadas as principais travas do sistema para evitar faturamentos incorretos.

### Crítica de Estoque Negativo
> [!warning] Alerta de Estoque
> Durante a montagem da carga, se um pedido contiver itens cuja quantidade solicitada seja maior do que o saldo físico real no inventário, o sistema destacará a linha do pedido na cor **Vermelha**. Trata-se de um indicativo visual crítico para que o faturista verifique se há faturamento de saldo fictício que cause rejeição ou erro de estoque na operação.

### Rejeições Fiscais da SEFAZ
> [!warning] Dependência de Autorização para Geração de Boletos
> Se uma Nota Fiscal for rejeitada pela [[SEFAZ]] durante a transmissão em lote (ex: erro de *Duplicidade de NF-e com diferença na chave de acesso*), o sistema interromperá a geração do boleto bancário correspondente àquele pedido específico.
> 
> **Motivo:** O sistema possui uma trava de segurança que impede a emissão de documentos de cobrança bancária vinculados a notas fiscais sem autorização de uso ativa.
> 
> **Solução:** O operador deve estornar o faturamento daquele pedido rejeitado, corrigir a inconsistência tributária ou de numeração, faturar novamente para gerar uma nova chave de acesso válida e, após a autorização da nota, processar a impressão do boleto remanescente de forma avulsa ou pelo painel da carga.
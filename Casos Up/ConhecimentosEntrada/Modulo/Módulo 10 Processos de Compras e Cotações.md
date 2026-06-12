Este módulo gerencia a cadeia de suprimentos (Supply Chain) da empresa, abrangendo desde o planejamento e cotação de insumos/mercadorias até a geração do pedido formal e o recebimento junto aos fornecedores.

---

## 1. Pedido de Compra e Sugestão de Reposição

O módulo de Pedido de Compra suporta tanto a digitação manual de itens quanto a automação da reposição de estoque baseada em regras de negócio.

* **Sugestão de Compra Inteligente:** O operador não precisa identificar manualmente o que está faltando. O sistema possui uma ferramenta de importação de itens com filtros estratégicos:
    * **Abaixo do Mínimo:** Traz todos os produtos que atingiram o limite mínimo de segurança configurado no cadastro.
    * **Estoque Negativo:** Puxa itens que sofreram ruptura e venderam no negativo.
    * **Atender até a Capacidade Máxima:** O sistema calcula a diferença entre o saldo atual e o "estoque ideal", sugerindo a quantidade exata para encher a gôndola/depósito.
* **Filtro por Fornecedor:** Ao utilizar a sugestão inteligente, o sistema respeita o fornecedor selecionado no cabeçalho, importando apenas os itens que estão vinculados àquele fabricante/distribuidor no banco de dados.
* **Comunicação e Recebimento:**
    * A partir do menu lateral (engrenagem), o pedido pode ser enviado diretamente para o e-mail do fornecedor com um layout de impressão customizado.
    * O sistema permite o **Recebimento Parcial ou Total** do pedido, mantendo o controle de saldo pendente de entrega.
* **Trava de Integridade Fiscal/Compliance:** Nas configurações gerais, é possível parametrizar a **obrigatoriedade de um Pedido de Compra prévio** para permitir a entrada de uma Nota Fiscal (XML). Essa trava impede compras não autorizadas e garante a conferência cega no recebimento.

---

## 2. Cotação de Compra (Bidding Process)

A ferramenta de cotação formaliza a busca pelas melhores condições comerciais antes do fechamento de um pedido de suprimentos.

* **Configuração da Planilha de Cotação:** O gestor de compras define a data limite de resposta e os itens necessitados.
* **Critérios de Avaliação:** A cotação pode ser parametrizada para priorizar:
    * **Melhor Preço:** Foco financeiro em redução de custos.
    * **Melhor Prazo:** Foco logístico em recebimento rápido.
* **Análise Comparativa:** A cotação é enviada simultaneamente para múltiplos fornecedores. Quando as respostas retornam, o operador alimenta os dados no sistema. O motor de cálculo analisa as planilhas lado a lado e sinaliza automaticamente o vencedor (ex: O Fornecedor A tem o melhor preço, mas o Fornecedor B atende o prazo exigido).
* **Conversão em Pedido:** Após a tomada de decisão, a cotação vencedora é convertida com um único clique em um Pedido de Compra oficial, sem necessidade de redigitar os itens ou valores acordados.
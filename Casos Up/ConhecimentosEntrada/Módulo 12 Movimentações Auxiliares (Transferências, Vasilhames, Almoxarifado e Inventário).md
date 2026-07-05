Este módulo documenta as operações complementares de controle de suprimentos, gestão de ativos de giro (vasilhames), consumo interno e auditoria física, além da sincronização de dados de precificação com os terminais de venda.

---

## 1. Transferência de Estoque

A rotina de transferência garante a integridade do rastreio de mercadorias que mudam de localidade física ou de CNPJ dentro da mesma infraestrutura.

* **Topologia de Transferência:** Suporta dois cenários principais:
    * **Multiempresa:** Transferência entre diferentes filiais (CNPJs distintos), utilizando parâmetros de Preço de Custo, Venda ou Compra.
    * **Múltiplos Depósitos:** Movimentação interna na mesma filial (ex: do "Depósito Central" para o "Estoque de Loja/Gôndola").
* **Ações Vinculadas:** Durante a transferência, é possível automatizar a geração de fila de impressão para **Etiquetas de Gôndola**, inserindo observações específicas e garantindo que o novo local de armazenamento receba a precificação visual atualizada.
* **Rastreio de Lote:** A transferência obriga e respeita a rastreabilidade, exigindo o apontamento dos lotes que estão sendo deslocados.

---

## 2. Devolução de Vasilhames (Logística Reversa de Embalagens)

Módulo específico para distribuidores de gás, água mineral e bebidas que trabalham com retenção e troca de embalagens retornáveis.

* **Configuração Base:** O comportamento é ativado no cadastro do produto (flag de "Possui Vasilhame").
* **Fluxo de Recolhimento:**
    * **Recolhimento Futuro:** Gera um título de devolução de vasilhame "em aberto".
    * **Recolhimento Imediato (Troca):** A venda do produto cheio (ex: Botijão de Gás) processa sistemicamente, e de forma invisível, a entrada simultânea de um item vazio (vasilhame) no estoque, equalizando o inventário físico em tempo real.

---

## 3. Gestão de Almoxarifado (Consumo Interno)

Destinado ao controle de requisições de materiais para uso interno dos setores da empresa, evitando a baixa manual descontrolada de estoque.

* **Solicitação de Estoque:** Setores criam requisições formais informando os itens necessários.
* **Atendimento Fracionado:** O administrador do almoxarifado pode alterar o status da solicitação para "Atendida" ou "Atendida Parcialmente" (ex: solicitou 5 peças, liberou 2), controlando o saldo pendente.
* **Emissão de Nota Fiscal de Consumo:** O sistema permite selecionar as requisições "Atendidas" e gerar, em lote, as Notas Fiscais de saída (CFOP de Consumo Interno/Perda), garantindo a baixa contábil legal da mercadoria.

---

## 4. Inventário e Conferência de Estoque

Processos de auditoria para garantir que o saldo do banco de dados (Estoque Contábil/Sistema) reflita o saldo do mundo real (Estoque Físico).

* **Conferência de Pedidos (Expedição):** Etapa de validação logística. O pedido faturado passa por uma tela de conferência (bipagem) antes da liberação para transporte, garantindo que o volume físico separado corresponde ao pedido exato.
* **Inventário Anual/Periódico:**
    * O inventário pode ser digitado via retaguarda ou executado de forma dinâmica utilizando o aplicativo **Mobile** (coletor de dados).
    * O sistema processa a contagem e permite definir se a divergência deve apenas gerar um relatório gerencial ou aplicar a alteração forçada do estoque no banco de dados.
    * Integração nativa para exportação do saldo inventariado para os arquivos de escrituração da contabilidade.

---

## 5. Outras Movimentações e Ajustes Avulsos

* **Movimentos Personalizados:** Criação de tipos de movimentos customizados (Entradas/Saídas) para justificar quebras, bonificações, doações ou ajustes não ligados a uma nota fiscal de fornecedor ou venda padrão.
* **Lastro Fiscal:** Toda movimentação avulsa permite o acionamento direto do motor fiscal para emissão da nota fiscal correspondente de saída/entrada.

---

## 6. Sincronização e Decisão de Preços (PDV)

O sistema possui uma arquitetura de dados unificada, reduzindo o *delay* (latência) de propagação de preços.

* **Alteração Direta:** Mudanças de preço efetuadas na entrada da nota fiscal ou na tela de "Precificação de Produtos" atualizam diretamente a tabela principal e/ou o cadastro do produto.
* **Sincronização com Terminais:** A arquitetura padrão disponibiliza o novo preço instantaneamente para operação de venda. Para cenários de **PDV Offline**, a rotina do serviço local deve estar configurada para sincronizar o pacote de preços de forma constante, garantindo que a frente de caixa pratique a decisão de preço mais recente do retaguarda.
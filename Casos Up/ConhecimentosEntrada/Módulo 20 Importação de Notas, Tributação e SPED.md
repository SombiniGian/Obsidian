Este módulo consolida as operações de recebimento fiscal, integração de dados de entrada, auditoria de tributos e a geração de obrigações acessórias, garantindo que a entrada de mercadorias seja escriturada de forma automatizada e correta.

---

## 1. Importação de Documentos (Entradas)

O sistema centraliza todas as notas fiscais de entrada na tela **Documentos Fiscais Recebidos**.

* **Importação via XML:** O processo mais eficiente é a importação direta do arquivo XML do fornecedor. Ao incluir um novo documento, o sistema processa o arquivo e tenta vincular automaticamente:
    * **Produtos:** O vínculo é feito através de descrições, código de barras (EAN) ou código do fornecedor. O sistema aprende o relacionamento, evitando que o operador precise realizar o vínculo manual em compras futuras.
    * **Financeiro:** O sistema extrai as parcelas de pagamento do XML e as insere automaticamente no Contas a Pagar.
    * **Custos:** Permite a precificação imediata (ver seção abaixo).
* **Manifesto do Destinatário:** Ferramenta obrigatória para garantir o controle fiscal das compras. O sistema consulta diretamente a Sefaz para baixar notas emitidas contra o CNPJ da empresa. 
    * O operador pode realizar a consulta, manifestar (Ciência/Confirmação) e realizar o download dos XMLs em lote, mantendo a contabilidade sempre atualizada.

---

## 2. Precificação e Composição de Custos

O ERP permite que a precificação seja realizada no ato da entrada, antes mesmo do produto ser movido para a gôndola.

* **Precificação Individual ou Massiva:** Na aba *Custos* da entrada de nota, é possível selecionar todos os itens e aplicar um *Markup* (margem de lucro) padrão, ou realizar o ajuste manual item por item.
* **Composição de Preço:** Ferramenta avançada que calcula o preço de venda considerando impostos, margem de contribuição e despesas acessórias.
* **Atualização Automática:** Ao salvar as alterações de preço na nota de entrada, o sistema dispara a atualização imediata no cadastro do produto (se configurado), garantindo que a frente de caixa (PDV) pratique o preço mais recente.
* **Etiquetagem (Gôndola):** Com os produtos precificados, o operador pode enviá-los diretamente para o módulo de impressão de etiquetas, agilizando a organização da loja.

---

## 3. Gestão Tributária (Regras de Exceção)

Para evitar erros recorrentes, o sistema permite a automação das regras tributárias:

* **Conversão de CST/CSOSN:** O sistema possui uma tabela interna com centenas de tipos de conversão (ex: CST 500 para CSOSN 500). Isso corrige erros comuns de fornecedores que emitem notas com tributação incompatível ao regime tributário do cliente.
* **Manter Dados do Produto:** Nas configurações da empresa, pode-se optar por "Manter dados do produto na XML". Isso força o sistema a respeitar a tributação informada pelo fornecedor na nota de entrada, facilitando o cadastro de itens novos.
* **Recálculo de Tributação:** Caso um erro fiscal seja identificado após a importação, o botão "Recalcular Tributação" reprocessa todos os itens da nota com base nas regras atuais cadastradas no Grupo Tributário ou no Produto, corrigindo cálculos de ICMS-ST, PIS e COFINS sem precisar refazer o lançamento.

---

## 4. Escrituração e SPED (Obrigações Acessórias)

O fechamento fiscal é automatizado através da geração de registros padronizados para a contabilidade.

* **SPED Fiscal (EFD ICMS/IPI) e Contribuições:** O sistema gera os blocos necessários conforme a legislação vigente. 
    * **Registro C170:** O sistema gera especificamente este registro para contadores que precisam validar itens dentro de arquivos estruturados, contornando erros comuns de estrutura encontrados em validadores padrão.
    * **Unificação (Matriz/Filial):** O módulo possui um unificador para empresas que possuem matriz e filiais. Ele consolida os arquivos de forma que a contabilidade receba um único conjunto de dados coerente.
* **Plano de Contas SPED:** Configuração básica onde se vinculam as naturezas de operações e tipos de documentos às contas contábeis equivalentes. Uma vez configurado, o sistema automatiza o preenchimento dos registros do SPED mensalmente.
* **Gerador de Relatórios (GNRE):** Para impostos específicos (DIFAL/ST) que exigem pagamento antecipado, o sistema emite a guia de recolhimento diretamente, permitindo a exportação ou impressão antes da movimentação da carga.
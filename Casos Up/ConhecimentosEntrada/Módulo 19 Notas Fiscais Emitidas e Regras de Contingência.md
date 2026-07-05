Este módulo documenta o painel de gerenciamento das Notas Fiscais Eletrônicas (NF-e) e Notas Fiscais de Consumidor (NFC-e), detalhando as rotinas de auditoria, correção e contingência operacional.

---

## 1. Gestão e Auditoria de Emissões

O painel de **Notas Fiscais Emitidas** é a central de controle de todas as saídas fiscais. O sistema mantém um histórico rigoroso de cada documento, permitindo operações em lote ou individuais.

* **Reclassificação de Natureza:** Caso uma nota tenha sido emitida com natureza errada (ex: Venda com CFOP de Remessa), o sistema permite realizar o cancelamento (dentro do prazo legal) ou o refaturamento referenciando o documento anterior.
* **Recálculo e Correção em Massa:**
    * **Cenário de Rejeição:** Se o contador identificar um erro estrutural em notas já emitidas ou pendentes (ex: alíquota de ICMS incorreta), o operador pode selecionar o lote de notas, realizar a correção no cadastro de produto (ou grupo tributário), e solicitar o **"Recalcular Tributação"**. O motor do sistema reprocessa os cálculos de PIS, COFINS e ICMS de todas as notas selecionadas simultaneamente.
* **Nota Referenciada:** Ferramenta indispensável para operações de devolução ou retificação. O operador seleciona documentos anteriores, e o sistema gera uma nova nota fiscal que "puxa" a chave de acesso e os dados fiscais das notas citadas, mantendo a rastreabilidade fiscal completa.

---

## 2. Gestão de Notas Pendentes e Rejeitadas

A tela de **Notas Fiscais Pendentes** é o ambiente de diagnóstico para erros de comunicação com a Sefaz.

* **Fluxo de Resolução:** Quando a Sefaz rejeita um XML, o erro retornado é exibido no log. O operador pode:
    1. **Resolver Pendências:** Ajustar os dados diretamente na nota (ou via cadastro de produto) e clicar em **Retransmitir**.
    2. **Inutilização de Numeração:** Caso haja um salto na numeração (ex: nota 50 foi pulada e o sistema está tentando a 52), o sistema permite selecionar a faixa de números saltados e enviá-los como "Inutilizados" para a Sefaz, regularizando o sequencial.
* **Atualização de Status:** Em situações de instabilidade na internet ou nos servidores da Receita, onde o sistema não recebeu o "Recibo" ou a "Autorização", o botão **Atualizar Status** consulta diretamente o webservice da Sefaz para confirmar se a nota foi autorizada, rejeitada ou denegada, sincronizando o status local com o real do governo.

---

## 3. Contingência e PDV Offline (NFC-e)

Para garantir que o ponto de venda nunca pare (especialmente em redes de supermercados), o sistema gerencia regimes de contingência.

* **Modo Offline:** Quando o sistema detecta indisponibilidade do webservice da Sefaz ou falha na internet local, ele alterna automaticamente para o modo de contingência. As vendas continuam sendo processadas localmente.
* **Transmissão em Lote:** Assim que a conexão é restabelecida, o sistema detecta as notas emitidas offline e dispara a transmissão em massa para a Sefaz, normalizando a situação fiscal.
* **Identificação de Rejeições por Produto:** Em caso de erro de validação (ex: "NCM Inválido" no item 3), o sistema aponta exatamente a linha e o item do XML que causou o problema, permitindo que o suporte técnico atue cirurgicamente sobre o produto sem necessidade de analisar o XML inteiro ou navegar em todo o cadastro.
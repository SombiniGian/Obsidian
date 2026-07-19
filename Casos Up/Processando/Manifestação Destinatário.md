---
id:
  - CASO-202
link: https://www.youtube.com/watch?v=W6o5S9XL994
setor:
  - Suporte
  - Faturamento
  - Fiscal
modulo:
  - Fiscal / Manifestação do Destinatário
tags:
  - manifestacao-destinatario
  - nfe
  - sefaz
  - xml
  - download-xml
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Manifestação do Destinatário]]
2. [[#Instabilidade e Regras de Consumo da SEFAZ]]
3. [[#Mudança Estrutural na Aplicação]]
4. [[#Mecânica de Download do XML Completo]]
5. [[#Recursos de Produtividade: Emissão em Lote e Auditoria]]
6. [[#Pontos Críticos e Diagnósticos de Erros]]

# Visão Geral da Manifestação do Destinatário
O módulo de **Manifestação do Destinatário** permite à empresa identificar e gerenciar todas as Notas Fiscais Eletrônicas (NF-e) emitidas contra o seu CNPJ por fornecedores em todo o território nacional. Através deste painel, o operador realiza eventos fiscais obrigatórios, como a **Ciência da Emissão**, confirmando o conhecimento da operação e permitindo a posterior captura dos arquivos XML para a escrituração e [[Entrada de Estoque]].

# Instabilidade e Regras de Consumo da SEFAZ
A Secretaria da Fazenda (SEFAZ) adota políticas rígidas baseadas no Manual de Boas Práticas para coibir o uso indevido e abusivo de seus servidores de consulta de documentos fiscais.

> [!warning] Bloqueio por Consumo Indevido (Uso de Robôs)
> Provedores ou sistemas que executam requisições em loops contínuos (automações robóticas de consulta) sobrecarregam a infraestrutura governamental. Como medida de contingência, a SEFAZ bloqueia temporariamente as requisições de download e consulta originadas pelo CNPJ ou IP infrator por um intervalo de até **uma hora**. Sintomas como a mensagem `Serviço paralisado sem previsão` indicam o acionamento dessas travas de segurança do fisco.

# Mudança Estrutural na Aplicação
Diante do cenário de bloqueios do fisco e pelo entendimento da SEFAZ de que o envio do XML é uma obrigação comercial direta do fornecedor e não da infraestrutura do governo, o sistema UP Sistemas sofreu uma reengenharia:

*   **Remoção do Botão de Download Direto:** O botão dedicado a forçar o download foi eliminado da interface. Tecnicamente, esse comando apenas submetia a chave de acesso isolada a uma busca na SEFAZ, o que gerava alto índice de rejeição por consumo indevido.
*   **Consulta por NSU (Número Sequencial Único):** O sistema passou a adotar estritamente a varredura cronológica linear baseada no último NSU retornado. O NSU é um indexador controlado pela SEFAZ que ordena cada evento ou nota gerada para o CNPJ de forma incremental.

# Mecânica de Download do XML Completo
A liberação e o download do XML estruturado de uma NF-e (contendo a lista detalhada de itens, impostos e valores) estão diretamente condicionados à realização de um evento de manifestação pelo destinatário.

### Estados do XML no Fluxo de Consulta:
1.  **Sem Manifestação (Resumo da NF-e):** Quando a nota é gerada pelo fornecedor e capturada inicialmente na fila de NSU do sistema, a SEFAZ disponibiliza apenas um lote resumido de dados. Esse layout inicial carece de dados cruciais, inviabilizando a rotina automatizada de entrada de notas.
2.  **Com Manifestação (XML Completo):** Quando o operador seleciona o registro e executa o evento de **Ciência da Emissão**, a SEFAZ processa o vínculo. No servidor do governo, o documento muda de status e é reindexado na fila de distribuição sob um novo NSU incremental subsequente.

> [!tip] Fluxo Correto para Captura do XML Completo
> Ao executar o comando **Ciência da Emissão**, aguarde alguns instantes e realize uma nova varredura utilizando a opção de consulta baseada no **Último NSU**. Como a nota ganhou uma nova posição na fila após o evento de ciência, o sistema capturará a resposta atualizada contendo o arquivo XML completo com todos os itens.

# Recursos de Produtividade: Emissão em Lote e Auditoria

### Manifestação em Lote
Para otimizar o tempo operacional em rotinas com grande volume de documentos fiscais recebidos:
1.  Na grade principal do módulo, selecione múltiplos registros utilizando as caixas de seleção.
2.  Escolha o tipo de evento desejado (ex: **Ciência da Emissão**).
3.  Clique em **Enviar**. O sistema transmitirá em segundo plano as manifestações de todos os documentos marcados em uma única chamada de lote para a SEFAZ.

### Indicador Visual de Consistência
A grade de monitoramento inclui uma coluna dedicada denominada **XML Completo**. Esta coluna permite uma auditoria visual rápida: o operador consegue identificar de imediato quais notas fiscais já possuem a estrutura rica de dados salva no banco local (liberadas para faturamento/entrada) e quais ainda dependem do fluxo de manifestação e repesca por NSU.

# Pontos Críticos e Diagnósticos de Erros

### Log de Erros Fiscais
Caso ocorram falhas durante o envio do lote de manifestações, o sistema exibe o retorno detalhado da SEFAZ no painel inferior da tela (**Log de Erros**).

```json
{
  "rejeicao_sefaz_manifestacao": {
    "codigo_status": 578,
    "motivo": "Rejeição: A assinatura do MDF-e/NF-e difere do padrão ou o CNPJ do certificado digital não condiz com o emitente/destinatário do documento.",
    "acao_corretiva": "Verificar se o certificado digital A1/A3 selecionado no sistema pertence exatamente ao mesmo CNPJ da filial logada."
  }
}
´´´´


[!danger] Validação de Titularidade do Certificado O principal motivo de falha na manifestação em lote ocorre quando a grade exibe notas destinadas a filiais com CNPJs diferentes da empresa selecionada no contexto do login atual. Ao tentar assinar o evento, a SEFAZ recusará a operação emitindo erro de titularidade, conforme detalhado no payload acima. Certifique-se de filtrar e manifestar os documentos correspondentes estritamente ao certificado digital configurado no ambiente logado.
---
id: [CASO-160]
link: https://www.youtube.com/watch?v=ZvmiEbYt9kY
setor: [Suporte, Implementação, Fiscal]
modulo: [Cadastros / Empresa]
tags: [configuracao-empresa, mensageria-fiscal, automacao-nfe, xml-entrada, contingencia]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral das Configurações de Empresa]]
2. [[#Parametrização do Motor de E-mails do Sistema]]
3. [[#Automação de Tratamento de Contingências e Pendências (Fisco)]]
4. [[#Mecânica de Retransmissão com Data Atrasada]]
5. [[#Regras de Negócio de Notas de Consumidor (NFC-e)]]
6. [[#Ajustes Fiscais e Vínculos na Importação de XML de Entrada]]
7. [[#Pontos Críticos e Regras de Segurança]]

# Visão Geral das Configurações de Empresa
O preenchimento refinado da aba **Outras** e da aba **Configurações Extras** dentro do **Cadastro da Empresa** é uma etapa crítica e mandatória durante o processo de implantação do ERP. Essas diretrizes determinam o comportamento global do motor de mensageria fiscal, ditando como o sistema resolverá furos de numeração, notas presas em processamento, amarrações de XML de fornecedores e contingências da [[NF-e]] e [[NFC-e]].

# Parametrização do Motor de E-mails do Sistema
A seção superior do painel gerencia a conta de saída do protocolo SMTP para disparos automáticos.
*   **Finalidade Principal:** Envio de arquivos fiscais XML e PDFs da NF-e/NFC-e gerados para os clientes.
*   **Escopo de Hierarquia:** Este e-mail atua como o endereço padrão global do sistema. Caso uma rotina não encontre um e-mail específico configurado, ela herdará as credenciais desta tela.

> [!info] Exceção de Regra de Herança (Boletos)
> O motor de envio de boletos bancários ignora a parametrização de e-mail desta aba. O fluxo financeiro de cobrança herda as configurações de e-mail SMTP diretamente do cadastro individualizado da **Conta Bancária** do emitente.

# Automação de Tratamento de Contingências e Pendências (Fisco)
O quadrante de "Pendências da Nota Fiscal" configura rotinas de background acionadas de forma automática sempre que o operador realiza o boot ou efetua o logoff do sistema (**Abrir e Sair do Sistema**).

*   **Alertar/Transmitir:** Monitora e tenta resolver notas que ficaram travadas com status de pendência de retorno na SEFAZ.

### Flags de Resolução Automatizada (Ao Sair do Sistema):
*   **Atualizar status, cancelar ou inutilizar as substituídas:** Trata o cenário onde uma nota sofreu falha de comunicação com a SEFAZ (Timeout), forçando o caixa a emitir uma segunda nota em contingência offline (com numeração subsequente). Ao rodar a rotina, o ERP consulta o status da primeira nota de envio com falha no banco do fisco. Se ela tiver sido autorizada, o sistema cancela a nota emitida em contingência. Se ela não constar na base da SEFAZ, o ERP comanda a inutilização da numeração antiga de forma síncrona.
*   **Transmitir todas as offline:** Envia em lote todos os cupons NFC-e gerados em contingência local que ainda não foram integrados ao banco de dados estadual.
*   **Inutilizar as numerações não encontradas:** Varre as sequências numéricas emitidas nos últimos **3 a 4 dias** (janela de segurança recomendada). Caso identifique furos cronológicos (ex: pulou da nota 10 para a 12), o sistema dispara automaticamente uma requisição de inutilização para o número fantasma (nota 11), blindando a empresa contra autuações por quebra de sequência fiscal.

# Mecânica de Retransmissão com Data Atrasada
Quando uma nota fiscal fica retida localmente e precisa ser retransmitida após a virada do dia, o manual de boas práticas do CONFAZ determina que o número antigo deve ser inutilizado, gerando-se uma nova numeração adequada à cronologia atual. Contudo, o sistema oferece duas alternativas de comportamento para se adequar às exigências de diferentes contabilidades:

*   **Método Padrão (Legal):** Inutiliza a numeração atrasada e despacha a nota sob uma nova numeração e data/hora atualizadas.
*   **Métoto de Atualização de Data (Aproveitar Número):** Ativada por solicitação de contadores através da flag **Aproveitar o mesmo número para transmitir a nota**. 
    *   *Comportamento:* O sistema reaproveita o número retido, alterando apenas a tag de Data/Hora de emissão para o momento atual.

> [!warning] Risco Fiscal de Inversão Cronológica
> A ativação da flag de aproveitamento de número pode fazer com que a nota número 10 exiba no XML a data de emissão de 10:00h e a nota número 11 (transmitida sem erros anteriormente) conste com o horário de 09:00h. Essa inversão cronológica viola as boas práticas da Receita Federal e pode gerar notificações fiscais eletrônicas. Ative o recurso apenas sob autorização expressa da contabilidade do cliente.

# Regras de Negócio de Notas de Consumidor (NFC-e)

*   **Permitir emissão de NFC-e para contribuinte do ICMS:** Por definição legal, vendas para pessoas jurídicas com Inscrição Estadual ativa (Contribuintes) exigem a emissão de NF-e (Modelo 55). Caso o lojista atue no varejo e precise forçar a emissão de NFC-e (Modelo 65) para uma PJ, esta flag deve estar ativa. O sistema alterará a tag da IE do destinatário para `Isento` no XML, burlando a rejeição em UFs que aceitam essa exceção jurídica.
*   **Ação ao cancelar Nota Fiscal:** Define o comportamento relacional do ERP ao invalidar um documento:
    1. *Não fazer nada com o pedido.*
    2. *Cancelar apenas o faturamento (retorna o pedido para o status "Em Aberto" para nova edição).*
    3. *Cancelar o faturamento e o pedido simultaneamente.*

# Ajustes Fiscais e Vínculos na Importação de XML de Entrada
Na aba **Configurações Extras**, parametrizam-se os critérios que o sistema adotará ao processar a importação de notas fiscais de compra via arquivo `.xml` do fornecedor:

*   **Chaves de Vínculo de Produto:** Determina quais atributos o motor de busca utilizará para tentar amarrar o item do fornecedor a um produto já cadastrado na base local, evitando duplicidades. Pode-se ativar ou isolar a validação por: *Descrição exata do item*, *Código de Barras (EAN)* ou *Histórico de Vendas anteriores do Fornecedor*.
*   **Atualizar NCM/CST pelo Fornecedor:** Se marcado, o ERP sobrescreve os dados fiscais do seu cadastro de produtos com as informações contidas no XML do fornecedor. Se desmarcado, preserva a inteligência fiscal cadastrada localmente, mitigando o risco de importar erros de digitação cometidos pelo emitente da nota.

# Pontos Críticos e Regras de Segurança

> [!danger] Trava de Divergência de Substituição Tributária (CST/CSOSN)
> A flag **"Manter o CST/CSOSN original do XML de Entrada"** deve ser avaliada com critério. Se uma indústria vende um produto para uma distribuidora, o XML virá preenchido com foco em "Saída de Indústria". Se o sistema importar o código de forma literal para a tela de compras sem processar a conversão para a realidade fiscal da empresa (ex: converter para uso e consumo ou revenda varejista), os relatórios de apuração do crédito de ICMS e o cálculo do preço de custo médio do produto serão gerados com inconsistências severas.

> [!info] Destaque de Crédito do Simples Nacional
> No campo **Alíquota de Crédito do ICMS**, insira o percentual de partilha da receita do Simples Nacional da empresa. Esse valor alimentará automaticamente o bloco de informações complementares das notas fiscais de saída, habilitando indústrias e clientes do Lucro Real a aproveitarem o crédito fiscal de ICMS assegurado por lei.
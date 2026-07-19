---
id: CASO-215
link: https://www.youtube.com/watch?v=Xnfll-GhduI
setor: Suporte
modulo: Faturamento / CT-e
tags: [cte, xml, nfe, importacao, mdfe]
data_criacao: 2026-07-18
---

# Emissão Automatizada de CT-e através da Importação de XML de NF-e

Este guia orienta na execução do processo de geração em lote de Conhecimentos de Transporte Eletrônicos (**CT-e**) a partir dos arquivos XML de Notas Fiscais Eletrônicas (**NF-e**), detalhando as regras de negócio de tomada de frete, movimentação de arquivos e geração de vínculos para o Manifesto Eletrônico de Documentos Fiscais (**MDF-e**).

## Sumário
- [[#Pré-requisitos e Estrutura de Diretórios]]
- [[#Fluxo de Importação e Regras de Negócio]]
- [[#Gerenciamento de Arquivos e Automação de Cadastros]]
- [[#Transmissão do CT-e e Integração com MDF-e]]

---

## Pré-requisitos e Estrutura de Diretórios

Para que o processo de importação em lote funcione corretamente, o ambiente operacional deve seguir regras específicas de organização de arquivos.

1. **Diretório de Entrada:** Deve ser mantida uma pasta dedicada para o recebimento dos arquivos das notas fiscais dos clientes. No exemplo, utiliza-se a pasta `src` localizada na raiz do sistema, embora qualquer diretório acessível na rede possa ser mapeado.
2. **Parametrização da Transportadora:** A empresa emitente deve estar previamente configurada com o número do **RNTRC** ativo no cadastro corporativo para evitar rejeições imediatas da SEFAZ durante a validação da tag do transportador.

---

## Fluxo de Importação e Regras de Negócio

O processo de geração elimina a necessidade de digitação manual de itens, remetentes e destinatários ao extrair os dados estruturais da NF-e.

### Passo a Passo para Importação
1. Acesse o módulo de preenchimento de conhecimentos de transporte.
2. Na tela principal de listagem, clique no botão de seta posicionado ao lado do comando de inclusão e selecione a opção **Importar XML**.
3. O sistema exibirá a tela de parametrização da importação. Selecione a **Natureza de Operação** fiscal correspondente à prestação de serviço de transporte.
4. No campo de definição do **Tomador do Serviço**, determine a regra de negócio com base nas opções:
   - **Remetente da Nota**
   - **Destinatário da Nota**
   - **De acordo com a Nota Fiscal:** O sistema analisa a tag correspondente à modalidade do frete (CIF/FOB). Se o frete for por conta do emitente, o remetente será definido como tomador; se for por conta do destinatário, o papel de tomador é atribuído ao recebedor.
5. Defina o método de precificação. O sistema possibilita aplicar uma **porcentagem de cobrança** calculada sobre o valor total da nota fiscal importada ou a inserção manual de valores negociados diretamente na grade de cada CT-e gerado em caso de frete fixo.
6. Clique em **Espelhar Pasta** para listar em tela todas as chaves de acesso e notas contidas no diretório configurado. É possível filtrar e marcar documentos específicos ou utilizar a seleção global de registros.
7. Clique em **Confirmar** para consolidar a criação dos CT-es com o status inicial "Em Aberto".

---

## Gerenciamento de Arquivos e Automação de Cadastros

O sistema possui uma rotina automatizada de tratamento de arquivos para mitigar falhas operacionais e duplicidade de lançamentos.

> [!info] Mecanismo de Controle de Arquivos (Gatilho de Sucesso)
> Assim que a importação de uma NF-e é concluída com sucesso, o sistema cria automaticamente um subdiretório chamado `processados` dentro da pasta de origem e move os arquivos XML consumidos para este local. Isso garante que, em consultas ou espelhamentos subsequentes, apenas novas notas pendentes de processamento sejam listadas na interface.

> [!tip] Recuperação de XMLs
> Caso seja necessário reprocessar uma nota fiscal cuja importação precise ser refeita, basta acessar fisicamente o diretório `processados`, recortar o arquivo XML desejado e colá-lo novamente na raiz da pasta de entrada (`src`).

### Auto-cadastro de Clientes
Se os CNPJs ou CPFs do remetente e do destinatário extraídos do XML da NF-e não constarem no banco de dados do [[ERP]], o sistema realiza a abertura do registro e o **cadastro automático de clientes** de maneira transparente, populando os campos de endereço, nome e identificadores fiscais sem interromper o fluxo do caixa ou do suporte.

---

## Transmissão do CT-e e Integração com MDF-e

### Transmissão em Lote
* Com os conhecimentos gerados em tela sob a situação "Em Aberto", marque as caixas de seleção dos documentos que deseja enviar.
* Clique no botão de seta adjacente à emissão e clique em **Transmitir Selecionados**. 

> [!warning] Validação de Chave de Certificado
> A transmissão exige correspondência exata entre o CNPJ do certificado digital configurado no painel fiscal e o CNPJ da transportadora configurada como emitente do documento, sob risco de falha de validação de assinatura.

### Vinculação com o MDF-e
Após a transmissão bem-sucedida, os documentos assumem o status de "Transmitidos" e ficam elegíveis para compor o Manifesto Eletrônico:

1. Acesse o módulo de [[MDF-e]] e clique em **Incluir**.
2. Os dados padrões do emitente e do motorista/veículo serão carregados da base interna.
3. Utilize a função **Importar por Filtro** para buscar os CT-es autorizados. O sistema filtrará os conhecimentos emitidos e permitirá a amarração em lote das chaves ao manifesto de carga para encerramento e emissão do DAMDFE.
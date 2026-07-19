---
id:
  - CASO-204
link: https://www.youtube.com/watch?v=ZyRyXdCvpKs
setor:
  - Suporte
  - Operacional
  - Faturamento
modulo:
  - Fiscal / MDF-e
tags:
  - mdfe
  - manifesto-de-carga
  - cte
  - integracao-fiscal
  - transporte
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do MDF-e]]
2. [[#Importação e Vínculo de Documentos Fiscais]]
3. [[#Parametrização de Rotas e Percurso]]
4. [[#Informações de Carga, Veículo e Condutor]]
5. [[#Configuração de Seguro Obrigatório]]
6. [[#Emissão e Pontos Críticos de Falha]]

# Visão Geral do MDF-e
O **MDF-e (Manifesto Eletrônico de Documentos Fiscais)** é um documento digital de emissão obrigatória para empresas transportadoras ou emitentes de mercadorias que realizam o transporte interestadual ou intermunicipal de cargas. Ele tem como finalidade agrupar e vincular as informações dos documentos fiscais originários (como o [[CT-e]] ou NF-e) à unidade de transporte correspondente, agilizando a fiscalização nos postos fiscais de fronteira.

# Importação e Vínculo de Documentos Fiscais
O fluxo de preenchimento do manifesto inicia-se de forma automatizada através do reaproveitamento dos dados de fretes previamente autorizados.

1. Acesse o módulo de emissão de **MDF-e** e clique em **Incluir**.
2. Clique no botão **Importar** para abrir a janela auxiliar de busca.
3. Utilize os filtros de data ou cliente para **Filtrar os CT-es** ou notas fiscais geradas no sistema.
4. Na listagem retornada, selecione o documento desejado. O sistema permite a seleção múltipla de registros caso o veículo transporte cargas consolidadas de diferentes remetentes/destinatários.
5. Clique em **Confirmar** para carregar os vínculos na grade.

# Parametrização de Rotas e Percurso
Após a importação dos documentos fiscais originários, o motor de regras do sistema realiza a leitura dos endereços do emitente e do destinatário para preencher os dados logísticos de viagem.

*   **Município de Início do Carregamento:** Preenchido de forma automática com base na cidade de origem indicada no documento importado.
*   **Município de Fim do Carregamento (Descarregamento):** Preenchido de forma automática com base na cidade de destino da entrega.

> [!warning] Configuração Obrigatória de Percurso Intermediário
> Em viagens interestaduais, caso o veículo precise transitar por unidades federativas intermediárias antes de alcançar o estado de destino, o operador deve informar manualmente a tabela de **Estados de Percurso**. A omissão dos estados de trânsito na grade gerará rejeição imediata da Secretaria da Fazenda (SEFAZ) durante o envio.

# Informações de Carga, Veículo e Condutor

### Classificação de Carga
Na aba de dados do modal rodoviário, o operador deve preencher o campo **NCM** informando a codificação fiscal correspondente ao produto principal ou de maior relevância que compõe o volume transportado.

### Unidade de Tração e Condução
1. Selecione o **Veículo** cadastrado na frota (placa, UF, tipo de rodado e tipo de carroceria).
2. No campo **Condutor**, selecione o motorista responsável pelo transporte.
3. Clique no botão **Incluir** para anexar o motorista ao manifesto. O sistema aceita a inclusão de mais de um condutor nos casos de revezamento em viagens de longa distância.

# Configuração de Seguro Obrigatório
O MDF-e exige o detalhamento das regras de gerenciamento de risco e seguro da carga transportada.

1. Acesse a aba ou bloco destinado à **Seguradora**. O sistema carrega a seguradora padrão configurada nos parâmetros globais da empresa, mas permite a alteração manual para outro parceiro se necessário.
2. Informe o **Número de Averbação** gerado no portal ou sistema da companhia de seguros após a comunicação prévia da viagem.
3. Clique em **Incluir** para salvar a linha da apólice no corpo do manifesto.

> [!info] Exigência da Averbação
> O número de averbação é um campo com validação estrutural pela SEFAZ. Lançar sequências de caracteres genéricas ou incorretas pode invalidar o seguro gerando passivos jurídicos e retenção da carga em barreiras de fiscalização rodoviária.

# Emissão e Pontos Críticos de Falha
Com todas as abas devidamente preenchidas e com as contrapartidas de documentos, veículos, motoristas e seguros inseridas na grade:

1. Clique no botão **Salvar** na barra de ferramentas inferior para validar a consistência local dos dados e persistir o manifesto eletrônico com o status `Em Aberto`.
2. Em seguida, clique em **Transmitir** para disparar o XML gerado aos servidores da SEFAZ.

> [!danger] Validação de Bloqueio por Manifesto em Aberto
> O veículo e o motorista vinculados a um MDF-e ficam retidos virtualmente na SEFAZ a partir do momento de sua autorização de uso. Se o operador tentar emitir um novo manifesto para o mesmo veículo sem efetuar o encerramento do MDF-e anterior no destino final, o sistema retornará a rejeição: *Existe MDF-e não encerrado para esta data/veículo*. Certifique-se sempre de executar a rotina de encerramento ao término de cada entrega.
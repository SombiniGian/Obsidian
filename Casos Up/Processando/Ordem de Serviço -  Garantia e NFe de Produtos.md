---
id: [CASO-058]
link: https://www.youtube.com/watch?v=LtdMeLDREgc
setor: [Suporte, Faturamento, Oficina]
modulo: [Ordem de Serviço]
tags:
  - ordem-servico
  - nf-e
  - garantia-terceiros
  - faturamento-os
data_criacao: 2026-06-24
---

# Ordem de Serviço: Parametrização, Garantias e Emissão de NF-e de Produtos

Esta documentação técnica detalha as melhorias estruturais implementadas no módulo de **Ordem de Serviço (OS)**, cobrando a integração com a emissão de Notas Fiscais Eletrônicas (NF-e) para os insumos e peças aplicadas, a gestão de garantias próprias e de terceiros (fabricantes/garantidores) e o controle fotográfico de vistorias de entrada e saída.

---

## Sumário
1. [[#Configuração Global do Módulo de OS]]
2. [[#Gestão de Garantias (Própria vs. Terceiros)]]
3. [[#Fluxo de Vistoria por Registro Fotográfico]]
4. [[#Fluxo de Execução e Faturamento da OS]]
5. [[#Roteamento Fiscal e Emissão de NF-e de Peças]]
6. [[#Pontos Críticos e Validações]]

---

## Configuração Global do Módulo de OS

Para habilitar a automação de faturamento e os novos campos de rastreabilidade de garantias, o analista deve parametrizar as regras de fallback e comportamento do sistema.

* **Caminho de Acesso:** Menu **Configurações** -> Parâmetros do módulo **Ordem de Serviço**.

### Campos e Flags de Controle:
* **Natureza de Operação dos Produtos:** Associa a [[Natureza de Operação]] padrão (ex: `5.949` ou `5.102`) que será herdada na NF-e para os itens aplicados na OS.
* **Selecionar Natureza de Operação ao Faturar:** Flag que, quando ativa, força o sistema a abrir uma tela de seleção de natureza de operação no momento exato do faturamento, permitindo ao operador alterar o fluxo tributário sob demanda.
* **Garantia de Terceiros como Padrão:** Flag que pré-ativa o bloco de controle de integridade para marcas e fabricantes conveniados.
* **Abrir Tela de Nota Fiscal após Faturar:** Quando ativa, assim que a OS recebe a instrução de fechamento financeiro, o ERP inicializa automaticamente a tela de transmissão de NF-e, agilizando o despacho fiscal.

---

## Gestão de Garantias (Própria vs. Terceiros)

O sistema segrega a responsabilidade financeira e os prazos legais de cobertura dos serviços e peças aplicadas em duas modalidades:

### 1. Garantia Própria (Interna)
É a cobertura concedida diretamente pelo estabelecimento prestador (ex: mecânica, assistência técnica). O prazo (ex: 30 dias) é inserido na ficha da OS e o custo de um eventual retrabalho é absorvido internamente.

### 2. Garantia de Terceiros / Fabricante
Cenário aplicável quando o reparo é executado em um item cuja cobertura é de responsabilidade do fabricante ou de uma seguradora (ex: um celular Samsung levado à assistência autorizada).

> [!info] Mecanismo de Herança Financeira
> Ao ativar a flag de garantia de terceiros, o sistema exibe dinamicamente a aba **Garantia** no cabeçalho da OS. Nesta aba, o operador associa o **Garantidor** (o cadastro da marca/fabricante). No fechamento da OS, o contas a receber (fluxo financeiro) **não será gerado para o cliente tomador do serviço**, mas sim transferido automaticamente para o cadastro do terceiro garantidor, que arcará com o reembolso dos insumos.

---

## Fluxo de Vistoria por Registro Fotográfico

Como medida de segurança jurídica e auditoria de sinistros, o sistema conta com uma central de armazenamento de imagens integrada ao corpo da OS.

* **Caminho de Acesso:** Aba **Fotos** no formulário interno da OS.

### Modos de Captura:
1. **Importação Local:** O usuário clica com o **Botão Direito** na grade e aciona o comando **Carregar Foto**, escolhendo arquivos salvos em diretórios locais do Windows.
2. **Captura Direta (Webcam):** Caso a estação de trabalho possua uma câmera ou webcam homologada e conectada, o sistema ativa o dispositivo de vídeo nativamente, capturando a foto e salvando-a diretamente no banco de dados vinculada àquela OS.

> [!tip] Casos de Uso Recomendados
> É uma boa prática registrar no mínimo duas imagens do objeto ou veículo em manutenção: uma no ato do recebimento (comprovando o estado físico de entrada e avarias preexistentes) e outra no ato da entrega (comprovando a resolução do problema e integridade do bem).

---

## Fluxo de Execução e Faturamento da OS

A execução operacional da OS segue uma sequência rígida de processamento de dados e geração de documentos fiscais e financeiros:
┌─────────────────────────┐ ┌─────────────────────────┐ ┌─────────────────────────┐ │ 1. Abertura OS │ ───> │ 2. Fechamento e Fatura │ ───> │ 3. Processamento NF-e │ 
│ Coleta dados e imagens │ │ Separação de Financeiro │ │ Transmissão de Produtos │ └─────────────────────────┘ └─────────────────────────┘ └─────────────────────────┘

1. Clique em **Incluir** e preencha os dados do cliente, veículo/objeto e do técnico responsável. 
2. Insira as peças aplicadas e a mão de obra executada nas respectivas grades de controle. 
3. Ao concluir a manutenção, selecione o comando **Faturar**. 
4. O sistema processará as parcelas financeiras e aplicará a regra de divisão: **o financeiro de peças e o financeiro de serviços são gerados em registros apartados**, garantindo a conciliação nativa para as declarações municipais (prestação de serviço) e estaduais (circulação de mercadorias). 
--- ## Roteamento Fiscal e Emissão de NF-e de Peças Após a confirmação do faturamento e geração das duplicatas financeiras, o sistema invoca a rotina fiscal do Estado (SEFAZ). 
5. O sistema redireciona o usuário para a interface de **Nota Fiscal de Produtos (NF-e)** de forma automatizada (caso configurado). 
6. O documento fiscal é gerado carregando estritamente os produtos consumidos na Ordem de Serviço, estruturados de acordo com a natureza de operação parametrizada na [[#Configuração Global do Módulo de OS]]. 
7. O operador realiza a validação dos dados fiscais e aciona o comando **Transmitir** para autorizar o documento e imprimir o DANFE correspondente. --- ## Pontos Críticos e Validações

>[!warning] Validações Técnicas e Regras Tributárias > 1. **Divergência de Titularidade Financeira:** Ao utilizar a garantia de terceiros, certifique-se de validar se o cadastro do Fabricante/Garantidor possui dados fiscais válidos (CNPJ, Inscrição Estadual). Erros no cadastro do garantidor travarão a geração das duplicatas no módulo [[Contas a Receber]]. > 2. **Separação de Impostos Estaduais e Municipais:** Peças integram a competência do ICMS (Estado) e demandam NF-e. Mão de obra integra o ISSQN (Município) e demanda NFS-e. Tentar faturar serviços dentro da nota de produtos (NF-e) sem a devida configuração de Nota Conjugada (recurso raro e dependente de convênio municipal) gerará rejeição severa na SEFAZ.
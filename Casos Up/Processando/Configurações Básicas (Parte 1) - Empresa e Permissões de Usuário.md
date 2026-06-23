---
id: [CASO-001]
link: https://www.youtube.com/watch?v=Q0cCN1rgEOQ
setor: Suporte
modulo: Configurações Gerais
tags: [configuracao_inicial, empresas, permissoes, usuarios, perfis]
data_criacao: 2026-06-23
---
---
# Sumário
1. [[#Visão Geral da Interface]]
2. [[#Cadastro e Parametrização de Empresas]]
   2.1 [[#Dados Principais e Contabilidade]]
   2.2 [[#Documentos Eletrônicos (NF-e, MDF-e, CT-e)]]
   2.3 [[#Regras de Negócio e Estoque]]
   2.4 [[#Parâmetros de Vendas e Integração com Tablets]]
3. [[#Controle de Acesso e Permissões de Usuário]]
   3.1 [[#Configurações de Usuários por Empresa]]
   3.2 [[#Gerenciamento e Importação de Perfis de Usuário]]

---

# Visão Geral da Interface

O sistema opera sob o conceito de arquitetura **multi-empresa**, permitindo o gerenciamento e o controle centralizado de movimentações de múltiplos CNPJs a partir de uma única base de dados. 

A interface com o usuário utiliza uma estrutura de navegação em **Abas (Tabs)**. Ao abrir telas de consultas como **Pessoas** ou **Cidades**, cada visualização é mantida em uma aba persistente. O painel central **Home** atua como um gerenciador de sessões, exibindo a lista de janelas ativas e permitindo a alternância rápida ou o fechamento em lote dos módulos.

As telas de listagem seguem um padrão estrito de interação:
1. Exibição da grade de registros em formato de listagem de dados.
2. Seleção do registro desejado na grade.
3. Clique em **Alterar** ou **Visualizar** para abrir o formulário modal de edição do registro selecionado.

---

# Cadastro e Parametrização de Empresas

As diretrizes do comportamento do sistema dependem diretamente da correta configuração das propriedades de cada empresa cadastrada.

## Dados Principais e Contabilidade
Na aba de identificação da empresa, preenchem-se as informações cadastrais básicas, o endereço completo e o enquadramento operacional (Definição de **Matriz** ou **Filial** e tipo de atividade, como **Indústria** ou **Comércio**). 
Na sub-aba **Contabilidade**, realizam-se os vínculos com o contador responsável e especificam-se os caminhos de geração e exportação dos arquivos fiscais regulatórios, tais como [[SPED Fiscal]] e [[Sintegra]].

## Documentos Eletrônicos (NF-e, MDF-e, CT-e)
A parametrização de documentos fiscais eletrônicos engloba a Nota Fiscal Eletrônica (NF-e), o Manifesto Eletrônico de Documentos Fiscais (MDF-e) e o Conhecimento de Transporte Eletrônico (CT-e).

> [!warning] Ambiente de Operação
> Deve-se validar estritamente a chave do ambiente selecionado. A alternância entre o ambiente de **Homologação** (Testes) e **Produção** (Validade Jurídica) altera os endpoints de comunicação com a [[SEFAZ]].

A estrutura de configuração exige os seguintes parâmetros:
* **Certificado Digital:** Seleção do certificado digital de modelo A1 ou A3 instalado no sistema operacional da estação de trabalho, com a respectiva captura da chave/número de série.
* **Diretório de Comunicação:** Caminho local ou de rede para o armazenamento dos arquivos `.xml` gerados.
* **Diretório de Esquemas:** Localização física dos arquivos de validação estrutural (`.xsd`) da SEFAZ, indispensáveis para a consistência dos XMLs antes do envio.
* **Configurações de Layout:** Definições para a impressão do Documento Auxiliar da Nota Fiscal Eletrônica (DANFE), como expansão automática do logotipo.
* **Parâmetros de Conexão:** Definição do tempo máximo de espera (**Timeout**) para o retorno da resposta dos servidores da SEFAZ.

## Regras de Negócio e Estoque
No escopo de comportamento de retaguarda, o sistema expõe flags controladoras na ficha da empresa:
* **Controlar Estoque Depósito:** Ativa ou desativa a baixa automática e o controle físico de saldos por almoxarifado.
* **Validar Dados Fiscais dos Produtos no Cadastro:** Quando ativada, impede o salvamento de novos itens cujo cadastro apresente omissão de alíquotas ou inconsistência tributária.

> [!tip] Alimentação de Padrões Tributários
> Para agilizar a operação em empresas onde o mix de produtos partilha da mesma carga tributária, configure os campos padrão de **IPI**, **PIS** e **COFINS** diretamente nos parâmetros da empresa. Novos produtos herdados trarão estes campos preenchidos automaticamente, permitindo alteração manual se necessário.

### Análise Visual de Markup
O sistema oferece uma ferramenta de monitoramento visual do preço de venda baseado no percentual de margem adicionado ao custo (**Markup**):

| Margem Apurada | Classificação | Comportamento em Tela |
| :--- | :--- | :--- |
| Menor que 30% | Baixa (Atenção Crítica) | O campo de Markup no produto é exibido na cor **Vermelha** |
| Entre 30% e 40% | Razoável | O campo de Markup no produto é exibido na cor **Amarela** |
| Maior que 40% | Favorável | O campo de Markup no produto é exibido na cor **Verde** |

> [!info] Mecanismo do Markup
> Se o custo de um item sofrer reajuste via entrada de nota fiscal e o preço de venda não for atualizado proporcionalmente, o indicador visual mudará automaticamente de cor, alertando a gerência sobre a perda de rentabilidade.

## Parâmetros de Vendas e Integração com Tablets
Para as operações de força de vendas externas vinculadas a dispositivos móveis, determinam-se os limites operacionais do vendedor:
* **Desconto Máximo / Acréscimo Máximo:** Definição em percentual do limite que a aplicação externa aceitará sem exigir liberação gerencial.
* **Valor Mínimo do Pedido:** Trava de valor monetário mínimo para que o pedido consiga ser faturado e transmitido ao módulo de faturamento central.

---

# Controle de Acesso e Permissões de Usuário

O sistema implementa o controle de acesso baseado em funções e isolamento por empresa, garantindo que os usuários acessem somente os dados pertinentes às suas atribuições.

## Configurações de Usuários por Empresa
O cadastro de usuários permite a criação de credenciais de acesso individuais. A concessão de direitos de uso é granulada e vinculada à empresa em que o operador está autenticado:
1. O administrador seleciona o usuário e a empresa correspondente.
2. A árvore de permissões lista todos os módulos do sistema.
3. Para cada módulo (ex: Cidades, Clientes, Financeiro), é possível definir os seguintes níveis de acesso:
   * **Bloqueio Total:** O módulo é removido do menu do usuário. Caso ele tente acessar através de atalhos ou links adjacentes, o sistema ocultará o botão de carregamento.
   * **Acesso de Leitura (Visualização):** O usuário visualiza os registros na grade, mas os botões de ação interna de **Incluir**, **Alterar** ou **Excluir** ficam desabilitados no formulário.
   * **Acesso Total:** Permissão irrestrita para operações de inclusão, alteração e exclusão de dados.

## Gerenciamento e Importação de Perfis de Usuário
Para otimizar o processo de implantação e manutenção de novas contas de operadores, o sistema utiliza o conceito de **Perfis de Usuário** (Roles).

Em vez de parametrizar a árvore de direitos manualmente para cada funcionário, o administrador pode criar um perfil estruturado (como Administrador, Gerente Comercial, ou Operador Financeiro) com permissões pré-definidas.

### Fluxo de Aplicação de Perfil: 
[Criar Novo Usuário] ? [Selecionar Empresa do Vínculo] ? [Acionar Botão "Importar Perfil"] ? [Escolher Perfil (Ex: Financeiro)]
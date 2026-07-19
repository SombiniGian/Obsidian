---
id:
  - CASO-161
link: https://www.youtube.com/watch?v=ZswVaygjzq8
setor:
  - Suporte
  - Implementação
  - Comercial
modulo:
  - Configurações Gerais / Ativação de Licenças
tags:
  - ativação
  - licenciamento
  - painel-da-revenda
  - demonstração
  - contingência
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Ativação de Clientes]]
2. [[#Primeiro Acesso e Inicialização do Banco de Dados]]
3. [[#Modalidade 1: Ativação Definitiva de Novo Cliente]]
4. [[#Modalidade 2: Ativação em Modo Demonstração (Trial)]]
5. [[#Gestão de Status e Governança no Painel de Controle]]
6. [[#Pontos Críticos e Regras de Negócio]]

# Visão Geral da Ativação de Clientes
O processo de homologação e licenciamento de uma nova empresa no ERP ocorre de forma descentralizada. Logo após a conclusão da instalação física dos arquivos binários e do [[Banco de Dados / Firebird]], o técnico ou revendedor deve realizar o primeiro provisionamento da licença. Este fluxo dispensa a necessidade de cadastros prévios manuais em plataformas web: a ativação consome as APIs do ecossistema central, realiza o handshake de segurança e insere a nova conta diretamente no portfólio de gestão da revenda de forma automatizada.

# Primeiro Acesso e Inicialização do Banco de Dados
Ao executar o binário do ERP pela primeira vez após uma instalação limpa, o banco de dados encontra-se desprovido de registros corporativos ou parametrizações de filiais.

1.  Execute o arquivo principal do sistema (`.exe`).
2.  Na janela de autenticação inicial, insira as credenciais de fábrica do sistema:
    *   **Usuário:** `1`
    *   **Senha:** `1`
3.  **Gatilho de Verificação:** O motor interno detectará que o contador de empresas ativas é igual a zero. O sistema interromperá o fluxo de login e exibirá um pop-up com o alerta: *Não há nenhuma empresa cadastrada. Há a necessidade de fazer o cadastro da empresa.*

# Modalidade 1: Ativação Definitiva de Novo Cliente
Para clientes que efetuaram a compra do software e iniciarão o processo de implantação oficial, deve-se seguir o fluxo de pareamento com a carteira da revenda.

1.  Na tela de cadastro de empresa recém-aberta, preencha obrigatoriamente os dados estruturais básicos (Razão Social/Nome Fantasia, CNPJ ou CPF do proprietário, Endereço e Cidade, ex: `Muriaé`).
2.  Ao clicar em **Avançar / Salvar**, o sistema interceptará os dados e, constatando que o documento fiscal não possui licença associada nos servidores centrais, abrirá a **Tela de Identificação da Revenda**.
3.  No campo de autenticação, insira o **Usuário** e a **Senha** administrativos da sua própria revenda (as mesmas credenciais utilizadas para gerenciar o painel web parceiro).
4.  Clique em **Confirmar**. 
5.  **Comportamento do Sistema:** O ERP transmitirá as informações via Web Service. O servidor central criará o registro de licença, associará o cliente ao CNPJ da revenda e retornará a liberação criptografada para a máquina local. O software recarregará a interface, exibindo o dashboard administrativo e os menus completos de operação.

# Modalidade 2: Ativação em Modo Demonstração (Trial)
Caso o objetivo da instalação seja puramente a execução de testes locais pelo prospecto ou a demonstração de rotinas por parte do técnico em uma feira comercial, a revenda não deve gastar suas credenciais oficiais.

*   Na tela de inserção de credenciais da revenda, ignore os campos de texto e clique diretamente no botão **Demonstração**.
*   O sistema aplicará um token de liberação provisório com as seguintes restrições rígidas de conformidade:

| Atributo de Licença | Regra de Bloqueio em Modo Demonstração |
| :--- | :--- |
| **Prazo de Validade** | Expiração automática após **30 dias** corridos da data do clique. |
| **Teto de Registros** | Limite máximo de **10 registros por tabela/tela** do banco de dados. |
| **Bloqueio Operacional**| O sistema aceitará no máximo 10 produtos, 10 clientes e 10 notas emitidas, travando novos inputs após o teto. |

> [!warning] Política Comercial contra Trial Livre Prolongado
> O ERP adota uma postura rígida de proteção à propriedade intelectual e governança de dados. O modo demonstração serve unicamente para o cliente "sentir a interface" do balcão e conferir a estética visual. O sistema não dá suporte e proíbe a liberação de versões de avaliação sem limites para uso produtivo estendido, forçando a transição para o licenciamento definitivo caso a empresa decida operar.

# Gestão de Status e Governança no Painel de Controle
Após a ativação de um cliente (seja via credenciais ou modo definitivo), o registro correspondente surge em tempo real dentro do painel web corporativo da revenda. Para gerenciar a saúde financeira e operacional dos contratos, acesse o painel, vá em **Meus Clientes** e utilize a busca para localizar o cliente desejado. A plataforma suporta três estados de controle de licença:

### 1. Ativo (Em Operação)
O cliente utiliza todas as rotinas contratadas, consome os serviços de mensageria fiscal e gera faturamento regular de royalties/mensalidade para a revenda e para a central desenvolvedora.

### 2. Bloqueado (Alerta de Inadimplência)
Utilizado como ferramenta de cobrança extrajudicial para clientes com mensalidades ou boletos de suporte em atraso.
*   **Comportamento no Cliente:** Ao tentar abrir o ERP no terminal, o sistema exibe uma tela de bloqueio administrativo impedindo o faturamento ou consulta de dados.
*   **Regra Financeira da Revenda:** Enquanto o cliente permanecer sob o status de **Bloqueado**, ele continua listado no portfólio ativo da revenda. Portanto, a revenda continua arcando normalmente com os custos de manutenção daquela licença junto à central desenvolvedora.

### 3. Inativo (Rescisão de Contrato)
Utilizado em cenários de quebra definitiva de contrato, encerramento de atividades da empresa ou perda do cliente.
*   **Comportamento no Cliente:** O acesso ao banco de dados local é revogado em sua totalidade imediatamente.
*   **Regra Financeira da Revenda:** O sistema cessa imediatamente a cobrança de custos e taxas daquela licença específica contra o CNPJ da revenda. O registro do cliente é ocultado e expurgado da grade de gestão de clientes ativos.

# Pontos Críticos e Regras de Negócio

> [!danger] Custo Financeiro para Reativação de Clientes Inativos
> A alteração do status de um cliente para **Inativo** é uma ação administrativa definitiva de distrato. Caso o cliente mude de ideia após alguns meses e decida retornar para o sistema UP, a revenda não poderá simplesmente reverter a flag para "Ativo" no painel de controle de forma gratuita. O ecossistema do servidor central interpretará o retorno como um novo contrato de venda, exigindo o pagamento compulsório de uma **Taxa de Nova Licença** de ativação, idêntica ao custo de implantação de um cliente do zero.

> [!tip] Ajuste de Validade Retroativa e Prorrogações
> Através da interface web do painel da revenda, o gestor de suporte tem autonomia para alterar o campo **Data de Validade** de cada licença de forma individualizada. Este recurso é amplamente utilizado para conceder prazos adicionais de carência (ex: prorrogar por mais 5 dias) para clientes que estão com dificuldades no fluxo de caixa ou aguardando a compensação bancária de boletos de manutenção, evitando o bloqueio automático e inesperado das frentes de caixa no meio do expediente comercial.
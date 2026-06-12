
O sistema adota o paradigma de **Cadastro Centralizado de Entidades** (Single Entity Pattern), onde uma única linha de registro na tabela principal de pessoas (`PESSOA`) pode assumir múltiplos papéis operacionais e fiscais simultaneamente no ecossistema ERP. Esta abordagem elimina a redundância de dados, unifica o histórico financeiro e simplifica a integridade referencial do banco de dados Firebird.

---

## 1. Abas Dinâmicas e Relacionamentos Condicionais

A interface do sistema reage dinamicamente através de sinalizadores (*checkboxes*) que ativam ou ocultam componentes visuais e regras de validação em tempo de execução:

*   **Pessoa Física vs. Jurídica:** A alteração do tipo de pessoa modifica as máscaras de entrada (`CPF` ou `CNPJ`) e dispara rotinas de validação de dígitos verificadores. O sistema consome **três APIs redundantes de consulta de CNPJ** de forma assíncrona; se a API primária falhar por *timeout* ou limite de requisições, as secundárias são acionadas automaticamente para trazer os dados cadastrais da Receita Federal.
*   **Cliente:** Habilita parametrizações comerciais padrão para otimização do fluxo no Pedido de Venda. Permite amarrar uma Tabela de Preço padrão, uma Forma de Pago preferencial, uma Região Geográfica, um Vendedor e uma Transportadora fixa.
*   **Fornecedor:** Desbloqueia campos de qualificação fiscal para cruzamento de dados na importação de arquivos XML de Notas Fiscais de Entrada (NF-e).
*   **Vendedor:** Perfil crítico para a operação do ecossistema mobile. Transforma o registro da pessoa em uma credencial de acesso, liberando os campos de parametrização de comissões, vínculo a um caixa específico (Conta Caixa), permissões de concessão de descontos e amarração a impressoras de cupons.
*   **Transportador:** Registra dados logísticos e RNTRC para a emissão de documentos fiscais de transporte.
*   **Comprador (Intermediário):** Mapeamento de profissionais parceiros (ex: pedreiros, arquitetos, eletricistas). Esta entidade é vinculada à venda para fins de rastreabilidade e cálculo de comissões por indicação de negócios, modelo muito comum em lojas de varejo de construção civil.

---

## 2. Gestão Avançada de Endereços e Regras de Negócio Ocultas

O subcadastro de endereços funciona em uma relação `1:N` (uma pessoa para múltiplos endereços) com impacto direto na camada fiscal do software.

```

[Cadastro Centralizado: PESSOA]

│

├──► Endereço 1 (Faturamento / Sede) ──► CNPJ Base ──► Inscrição Estadual A

│

├──► Endereço 2 (Fazenda Alvorada) ──► CNPJ Base ──► Inscrição Estadual B

│

└──► Endereço 3 (Fazenda Progresso) ──► CNPJ Base ──► Inscrição Estadual C

```

### O Propósito da Razão Social por Endereço
Para atender cenários complexos como produtores rurais ou órgãos públicos, o sistema permite associar inscrições estaduais e **razões sociais distintas** a cada endereço cadastrado sob o mesmo registro base:
*   **Cenário Produtor Rural:** Um produtor rural possui o mesmo CPF/CNPJ base, mas detém diferentes inscrições estaduais vinculadas a diferentes propriedades (Fazendas). O operador do sistema seleciona o mesmo cliente e, no momento do pedido, escolhe o endereço da propriedade correta. O motor de emissão de NF-e altera dinamicamente as tags de Razão Social e Inscrição Estadual com base no endereço de entrega selecionado.
*   **Cenário Órgão Público:** Uma prefeitura municipal centraliza as compras em um único CNPJ, mas a entrega e o faturamento precisam discriminar secretarias ou escolas específicas (ex: "Secretaria de Educação - Escola Municipal X"). O campo de Razão Social no subcadastro de endereços substitui o nome principal na nota fiscal eletrônica modelo 55.

---

## 3. Camada de Comunicação Interna e Alertas

O sistema implementa regras automatizadas de comportamento que disparam gatilhos visuais baseados nas informações contidas nos cadastros de pessoas:

1.  **Mensagem de Alerta:** Campo de texto livre de alta prioridade. Toda vez que a entidade é selecionada em uma tela operacional (Pedido de Venda, Ordem de Serviço ou Nota Fiscal), o sistema interrompe o fluxo do usuário e exibe uma janela *pop-up* com o conteúdo configurado (ex: "Cliente com restrição de crédito", "Exige entrega agendada").
2.  **Observação da Nota Fiscal:** Conteúdo de texto focado em obrigações fiscais ou operacionais que deve constar no documento fiscal. As strings digitadas neste campo são injetadas automaticamente na tag de Informações Complementares da NF-e (`infCpl`).
3.  **Observação de Controle Interno:** Texto estrito para consumo da equipe interna da empresa, invisível em qualquer documento emitido para o cliente externo.

---

## 4. Histórico de Auditoria e Logs

As principais tabelas que compõem o módulo de pessoas possuem gatilhos de banco de dados (*triggers*) e classes na camada de aplicação que registram logs detalhados de auditoria:
*   Gravação automática do usuário responsável pela inserção, alteração ou exclusão do registro.
*   Registro da data e hora exata da transação.
*   Armazenamento do estado anterior e posterior dos dados em caso de alteração, permitindo o rastreamento completo de modificações em campos críticos como Limite de Crédito ou Regime Tributário.
Este módulo detalha o stack tecnológico do sistema, as ferramentas de integração com hardwares de pagamento e os processos de migração de dados e implantação em clientes.

---

## 1. Stack Tecnológico e Multiplataforma

O ecossistema do software é construído sobre uma arquitetura distribuída, utilizando tecnologias específicas para o retaguarda e terminais de venda.

*   **Retaguarda (ERP / Desktop):** Desenvolvido em **Delphi**, garantindo alta performance e estabilidade para as operações de backoffice administrativo e fiscal.
*   **Banco de Dados:** Utiliza **Firebird**, com suporte estrutural às versões mais recentes do motor relacional (ex: 5.0).
*   **Frente de Caixa e Mobile (POS):** Desenvolvido inteiramente em **Flutter**.
    *   *Vantagem Multiplataforma:* O código base em Flutter compila nativamente para **Android, iOS e Windows**. Isso elimina a necessidade de utilizar emuladores (ou subsistemas Android no Windows) para rodar o aplicativo de vendas e gestão de mesas em computadores desktop convencionais.

## 2. Integração com Terminais Inteligentes (Smart POS)

O aplicativo POS possui integração nativa e homologação com as principais adquirentes e hardwares do mercado (Smart POS / TEF embarcado), permitindo que a própria máquina de cartão funcione como o terminal de vendas independente.

*   **Hardwares e Adquirentes Homologados:**
    *   Clover
    *   Stone
    *   Bin
    *   Sicredi
    *   Caixa
    *   PagBank
    *   Rede
    *   Getnet
    *   Terminais de autoatendimento e totens (ex: linha Elgin).

## 3. Processos de Migração de Dados (Onboarding)

Para facilitar a transição de clientes operando em sistemas concorrentes, o software oferece vias estruturadas de importação de dados operacionais para o Firebird.

*   **Migrador Nativo via Excel:**
    *   A plataforma disponibiliza um conjunto de planilhas padronizadas compostas por rotinas de importação (abrangendo: Cadastros de Produtos, Clientes, Fornecedores, Contas a Pagar e Contas a Receber).
    *   Uma ferramenta migradora interna processa o arquivo `.xls`/`.csv` e executa a inserção estruturada no banco de dados.
*   **Migração Avançada via injeção SQL:**
    *   Para estruturas complexas e em nuvem, profissionais técnicos podem realizar a extração via comandos `SELECT` no banco de dados de origem e adaptar o *dataset* via injeção `SQL` bruta diretamente nas tabelas alvo do Firebird, otimizando o processo que seria manual.

## 4. Engenharia de Implantação e Deploy Customizado

O fluxo de *deploy* foi modelado para dar autonomia e escalabilidade para as operações de revendas de TI e implementadores independentes.

*   **Laboratório de Preparação:** O técnico pode instalar o banco de dados em sua própria máquina, parametrizar o CNPJ do cliente, importar os produtos e configurar as regras tributárias antes da ida a campo.
*   **Instalador Personalizado (Inno Setup):**
    *   Utilizando a ferramenta gratuita Inno Setup, a revenda compila um pacote de instalação próprio (conceito *White Label*).
    *   O banco de dados previamente preparado (do laboratório) e a identidade visual customizada são empacotados em um único arquivo executável (`.exe`). Ao rodar este pacote no cliente final, o sistema é descompactado pronto para operação imediata, reduzindo drasticamente o tempo técnico de implantação.
*   **Topologia Cloud vs. Local:**
    *   O sistema suporta a alocação do banco de dados em servidores Cloud (acessível via IPs públicos/VPNs), assemelhando-se a um SaaS nativo. No entanto, para evitar alta latência, a topologia recomendada para alta performance é o processamento local (Servidor/Cliente), utilizando ferramentas de acesso remoto para manutenção e suporte pela revenda.
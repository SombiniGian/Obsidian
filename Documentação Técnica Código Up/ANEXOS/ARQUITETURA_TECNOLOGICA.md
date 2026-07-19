---
id: DOCUP-046
setor: Documentação Técnica, Suporte, Implantação
modulo: Arquitetura
categoria: anexos
tags:
  - firebird
  - delphi
  - flutter
  - android
  - integracao
navegacao:
  - "[[00.1_SUMÁRIO_GERAL]]"
  - "[[00.2_GLOSSÁRIO_DE_TERMOS]]"
relacionados:
  - "[[03.2_FIREBIRD_INSTALACAO]]"
  - "[[03.4_CAMPOS_PERSONALIZADOS]]"
  - "[[03.16_APPS_ANDROID_FORCA_VENDAS_PDV]]"
  - "[[00.1_SUMÁRIO_GERAL]]"
aliases:
  - DOCUP-ARQUITETURA
  - Arquitetura Tecnológica
  - Stack Código Up
  - Delphi Firebird Flutter
resumo: "Visão da arquitetura tecnológica do Código Up (desktop, banco Firebird, mobile/Flutter e integrações)."
fontes:
  - tipo: video
    titulo: "Migração de dados - Migrador Excel"
    video_id: n8W6kmwZ6f8
    url: https://youtu.be/n8W6kmwZ6f8
  - tipo: video
    titulo: "Criar uma VPN para acessar APIs sem ter IP Público (ZeroTier)"
    video_id: OmAoied-4-8
    url: https://youtu.be/OmAoied-4-8
data_criacao: 2026-07-05
data_atualizacao: 2026-07-19
---

# Arquitetura Tecnológica, Integrações e Deploy

> **Escopo:** panorama técnico da stack e componentes do produto; complementar aos manuais operacionais.
>
> **Pré-requisitos:** [[00.1_SUMÁRIO_GERAL]]

> Documento de referência técnica sobre o stack do sistema Up, hardwares homologados e processos de migração e implantação. Voltado para o time técnico (Implantação, Suporte, Revenda).

## 1. Stack Tecnológico e Multiplataforma

O ecossistema do software é construído sobre uma arquitetura distribuída, utilizando tecnologias específicas para a retaguarda e terminais de venda.

* **Retaguarda (ERP / Desktop):** Desenvolvido em **Delphi**, garantindo alta performance e estabilidade para as operações de backoffice administrativo e fiscal.
* **Banco de Dados:** Utiliza **Firebird**, com suporte estrutural às versões mais recentes do motor relacional (ex: 5.0).
* **Frente de Caixa e Mobile (POS):** Desenvolvido inteiramente em **Flutter**.
    * *Vantagem Multiplataforma:* O código base em Flutter compila nativamente para **Android, iOS e Windows**. Isso elimina a necessidade de utilizar emuladores (ou subsistemas Android no Windows) para rodar o aplicativo de vendas e gestão de mesas em computadores desktop convencionais.

## 2. Integração com Terminais Inteligentes (Smart POS)

O aplicativo POS possui integração nativa e homologação com as principais adquirentes e hardwares do mercado (Smart POS / TEF embarcado), permitindo que a própria máquina de cartão funcione como o terminal de vendas independente.

* **Hardwares e Adquirentes Homologados:**
    * Clover
    * Stone
    * Bin
    * Sicredi
    * Caixa
    * PagBank
    * Rede
    * Getnet
    * Terminais de autoatendimento e totens (ex: linha Elgin e Clover).

## 3. Processos de Migração de Dados (Onboarding)

Para facilitar a transição de clientes operando em sistemas concorrentes, o software oferece vias estruturadas de importação de dados operacionais para o Firebird.

* **Migrador Nativo via Excel:**
    * A plataforma disponibiliza um conjunto de planilhas padronizadas compostas por rotinas de importação (abrangendo: Cadastros de Produtos, Clientes, Fornecedores, Contas a Pagar e Contas a Receber).
    * Uma ferramenta migradora interna processa o arquivo `.xls`/`.csv` e executa a inserção estruturada no banco de dados.
* **Migração Avançada via injeção SQL:**
    * Para estruturas complexas e em nuvem, profissionais técnicos podem realizar a extração via comandos `SELECT` no banco de dados de origem e adaptar o *dataset* via injeção `SQL` bruta diretamente nas tabelas alvo do Firebird, otimizando o processo que seria manual.

## 4. Engenharia de Implantação e Deploy Customizado

O fluxo de *deploy* foi modelado para dar autonomia e escalabilidade para as operações de revendas de TI e implementadores independentes.

* **Laboratório de Preparação:** O técnico pode instalar o banco de dados em sua própria máquina, parametrizar o CNPJ do cliente, importar os produtos e configurar as regras tributárias antes da ida a campo.
* **Instalador Personalizado (Inno Setup):**
    * Utilizando a ferramenta gratuita Inno Setup, a revenda compila um pacote de instalação próprio (conceito *White Label*).
    * O banco de dados previamente preparado (do laboratório) e a identidade visual customizada são empacotados em um único arquivo executável (`.exe`). Ao rodar este pacote no cliente final, o sistema é descompactado pronto para operação imediata, reduzindo drasticamente o tempo técnico de implantação.
* **Topologia Cloud vs. Local:**
    * O sistema suporta a alocação do banco de dados em servidores Cloud (acessível via IPs públicos/VPNs), assemelhando-se a um SaaS nativo. No entanto, para evitar alta latência, a topologia recomendada para alta performance é o processamento local (Servidor/Cliente), utilizando ferramentas de acesso remoto para manutenção e suporte pela revenda.

---

## Origem: vídeo — Migração de dados - Migrador Excel

> Fonte: [YouTube](https://youtu.be/n8W6kmwZ6f8) · arquivo: `Migração de dados - Migrador Excel.md` · video_id: `n8W6kmwZ6f8`

### Uso e planilhas

- Ferramenta **somente para carga inicial (Go-Live)** — não usar em base com movimento de NF/caixa.
- Pacote: executável + planilhas modelo (Produtos, Clientes, Fornecedores, Contas a Pagar, Contas a Receber).
- Produtos: ID inteiro; **Código Fiscal** legível à SEFAZ; EAN real; CST/CSOSN/NCM obrigatórios; tipo de produto.
- Financeiro: status `AB` ou `BX`; vínculo pessoa por ID ou CPF/CNPJ.
- Cadastro único de pessoas: colisão Cliente ID 1 vs Fornecedor ID 1 → vincular por CPF/CNPJ ou deslocar IDs de fornecedor (ex.: +10.000).

### Operação e pós-importação

1. Conectar (porta Firebird `3050` + caminho `.fdb`) → escolher empresa.
2. Ordem: Clientes/Fornecedores → Produtos → Contas a Receber/Pagar.
3. Colisão: substituir / atualizar só estoque / ignorar; IDs da planilha ou auto-incremento.
4. Após carga: ERP > **Ferramentas do Sistema > Controle de IDs > Atualizar IDs** (MAX nas generators; evita PK violation no próximo cadastro).

---

## Origem: vídeo — VPN ZeroTier para APIs sem IP público

> Fonte: [YouTube](https://youtu.be/OmAoied-4-8) · arquivo: `Criar uma VPN para acessar APIs sem ter IP Público (real) de forma simples e objetiva..md` · video_id: `OmAoied-4-8`

### Montagem

1. Portal `zerotier.com` → **Create a Network** (Network ID 16 caracteres).
2. Access Control **Private** (recomendado); IPv4 Auto-Assign com faixa de três blocos (ex.: `10.147.17.*`).
3. Instalar ZeroTier One no Windows do servidor → Join Network ID; autorizar interface de rede.
4. App ZeroTier One no Android/iOS → mesmo Network ID → no painel web, **Auth?** em Members + Short Name.
5. Acessar APIs pelo IP virtual: ex. Força de Vendas `http://10.x.x.x:8082`, Relatórios Online `http://10.x.x.x:8077`.
6. Firewall do Windows: liberar portas dos serviços para a sub-rede ZeroTier.
7. Serviço persiste IP virtual após reboot; elimina IP fixo, port forward e DDNS para o cenário de API móvel.

---

## Veja Também

- [[03.2_FIREBIRD_INSTALACAO]]
- [[03.4_CAMPOS_PERSONALIZADOS]]
- [[03.16_APPS_ANDROID_FORCA_VENDAS_PDV]]
- [[00.1_SUMÁRIO_GERAL]]

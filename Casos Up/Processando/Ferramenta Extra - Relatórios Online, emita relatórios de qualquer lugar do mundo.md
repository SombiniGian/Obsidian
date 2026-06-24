---
id: [CASO-054]
link: https://www.youtube.com/watch?v=Q8QsC_Y4Pp0
setor: [Suporte, Implantação, TI]
modulo: [Relatórios Online]
tags:
  - relatorio-web
  - configuracao-servidor
  - acesso-remoto
  - recursos-extras
data_criacao: 2026-06-24
---

# Ferramenta Extra: Configuração e Uso dos Relatórios Online

Este documento técnico detalha as diretrizes de implantação, infraestrutura e operação do módulo complementar **Relatórios Online**. Essa ferramenta web em tempo real foi desenvolvida para suprir a necessidade de gestores e proprietários que demandam o acompanhamento de indicadores financeiros e de vendas remotamente (via smartphone, tablet ou computador externo).

---

## Sumário
1. [[#Localização e Obtenção do Executável]]
2. [[#Arquitetura de Conexão e Implantação Técnica]]
3. [[#Configuração de Rede e Acesso Externo]]
4. [[#Módulos e Relatórios Disponíveis]]
5. [[#Modelos de Negócio para Revendas]]
6. [[#Pontos Críticos e Validações]]

---

## Localização e Obtenção do Executável

O utilitário não faz parte do instalador padrão do ERP, sendo classificado como uma ferramenta complementar voltada para canais autorizados.

* **Origem dos Arquivos:** Centralizado no **Painel da Revenda**.
* **Caminho de Download:** Menu **Downloads** -> subpasta **Extras**.

> [!info] Outros Recursos Extras
> A subpasta **Extras** concentra utilitários de integração e expansão do ecossistema, incluindo firmwares e utilitários de teclado analógico/gerencial Gertec, e módulos específicos para gestão de restaurantes self-service.

---

## Arquitetura de Conexão e Implantação Técnica

O serviço funciona como um microsservidor HTTP local que realiza consultas nativas e diretas à base de dados do ERP.

### Processo de Instalação Local:
1. Acesse o Painel da Revenda e baixe o binário compactado dos **Relatórios Online**.
2. Copie o arquivo executável obtido e cole-o obrigatoriamente dentro do diretório raiz de instalação do sistema principal (pasta onde reside o banco de dados/executável do ERP).
3. Execute o aplicativo correspondente. Ele rodará em segundo plano na barra de tarefas (próximo ao relógio do Windows), indicando que o servidor web interno está ativo.

---

## Configuração de Rede e Acesso Externo

Por padrão, a aplicação responde localmente através do protocolo HTTP utilizando uma porta TCP predefinida.

* **Porta Padrão de Fábrica:** `8077`.
* **URL de Teste Interno (Intranet):** `http://[IP_DO_SERVIDOR]:8077`.

> [!tip] Customização de Portas
> A porta padrão pode ser modificada em cenários onde haja conflito com outros serviços web (como IIS ou Apache). Caso seja necessário realizar a alteração, o suporte interno da Código UP disponibiliza o procedimento de edição do arquivo de configuração técnica da ferramenta.

### Requisitos para Acesso Global:
Para que o cliente final consiga monitorar a empresa a partir de redes externas (3G/4G/Wi-Fi externo):
1. É imperativo configurar uma regra de **Redirecionamento de Portas (Port Forwarding)** no roteador/modem da empresa, apontando a porta pública escolhida para o IP fixo da máquina servidora na porta `8077`.
2. Recomenda-se a utilização de um endereço de IP Público Estático ou a vinculação de um serviço de **DNS Dinâmico (DDNS)** (ex: No-IP, DynDNS) para contornar instabilidades de IPs dinâmicos fornecidos pelas operadoras de internet.

---

## Módulos e Relatórios Disponíveis

A interface gerada é totalmente responsiva, adaptando-se ergonomicamente ao formato de smartphones e tablets. Como a conexão com a base de dados ocorre de forma síncrona, todos os indicadores exibem dados em tempo real.

### Consultas Homologadas:
* **Análise de Vendas:** Visão macro e micro do faturamento diário/mensal.
* **Desempenho por Grupos de Produtos:** Segmentação do faturamento por categorias comerciais.
* **Financeiro Estrutural:** Acompanhamento dinâmico de Contas a Receber e Contas a Pagar.
* **Fechamentos de Caixa:** Detalhamento do histórico de caixas encerrados, permitindo auditar o faturamento segregado por meio de pagamento (Dinheiro, Cartão de Crédito/Débito, Pix, etc.).

> [!tip] Portabilidade de Dados
> A plataforma web permite a exportação nativa dos grids de dados e das tabelas geradas diretamente para o formato do **Microsoft Excel (.xlsx)**, facilitando auditorias e análises externas.

---

## Modelos de Negócio para Revendas

A Código UP fornece este módulo extra sob uma política comercial previsível para seus canais.

* **Custo da Revenda:** O módulo possui um custo fixo tabelado junto à desenvolvedora, independente do volume de relatórios ou acessos do cliente.
* **Margem de Lucro:** A revenda possui total autonomia para precificar, cobrar e faturar o cliente final de acordo com seu escopo de prestação de serviços (cobrança única de implantação ou acréscimo na mensalidade de suporte).

---

## Pontos Críticos e Validações

> [!warning] Riscos de Segurança e Conectividade
> 1. **Segurança de Rede:** Expor portas TCP diretamente na internet sem uma camada de proteção expõe o servidor local a varreduras maliciosas. É recomendado restringir as regras de firewall ou alterar a porta externa do modem para uma numeração alta e não óbvia.
> 2. **Servidor Desligado:** O painel online depende exclusivamente da execução do binário na máquina servidora. Se o servidor for desligado, reiniciar devido a atualizações do Windows, ou se o aplicativo for fechado acidentalmente pelo usuário, o link de acesso externo ficará indisponível. Recomenda-se configurar o executável para iniciar automaticamente com o logon do Windows.
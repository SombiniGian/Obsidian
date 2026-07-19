
---
id: [CASO-180]
link: https://www.youtube.com/watch?v=t25FevbSDCQ&t=4s
setor: [Suporte, Infraestrutura, Implementação]
modulo: [PDV / PDV Offline]
tags: [pdv-offline, replicação-de-dados, firebird, força-de-vendas, sincronização]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral e Conceito do PDV Offline]]
2. [[#Infraestrutura de Banco de Dados Local]]
3. [[#Mecanismo de Replicação Bidirecional]]
4. [[#Arquitetura de Comunicação via API]]
5. [[#Cenários Recomendações de Uso]]
6. [[#Pontos Críticos e Regras de Negócio]]

# Visão Geral e Conceito do PDV Offline
O **PDV Offline** é um ponto de venda autônomo projetado para garantir a continuidade da operação de vendas em cenários onde há queda de rede local, oscilação de internet ou indisponibilidade temporária do servidor principal (retaguarda). A ferramenta opera de forma descentralizada: cada terminal de venda possui uma estrutura completa independente, permitindo realizar registros de cupons, faturamentos, emissões e cadastros de novos clientes sem depender de conexões síncronas com o ecossistema central.

# Infraestrutura de Banco de Dados Local

> [!warning] Requisito de Instalação Tipo Servidor
> Diferente de uma estação de trabalho padrão que apenas aponta para o IP do servidor remoto, a máquina destinada ao PDV Offline deve ser obrigatoriamente instalada com as propriedades de um **Servidor Ativo**. 

Para viabilizar a autonomia de dados, os seguintes pré-requisitos de infraestrutura devem ser observados na máquina local:
*   **Instalação do SGBD:** Deve-se instalar o banco de dados [[Banco de Dados / Firebird]] completo, nas versões `3.0` ou `4.0` (32 ou 64 bits), seguindo os critérios de arquitetura do sistema operacional da máquina.
*   **Instância de Dados Própria:** O terminal recebe uma cópia local e estruturada do banco de dados, contendo as tabelas de produtos, preços, configurações fiscais e clientes sincronizados, permitindo que a aplicação viva isoladamente da rede interna.

# Mecanismo de Replicação Bidirecional
O fluxo de troca de informações entre os caixas locais e a retaguarda ocorre por meio de rotinas de replicação assíncronas.

```json
{
  "fluxo_replicacao_pdv_offline": {
    "origem_estacao_para_servidor": {
      "frequencia": "De tempo em tempo (conforme gatilho de conexão ativo)",
      "dados_enviados": ["Movimentações de Vendas", "Notas Fiscais Emitidas", "Novos Clientes Cadastrados no PDV"]
    },
    "origem_servidor_para_estacao": {
      "frequencia": "Abertura de dia, abertura de caixa ou gatilho manual do operador",
      "dados_recebidos": ["Atualizações de Preços", "Alterações de Cadastros de Produtos", "Novas Tabelas de Preços", "Modificações de Naturezas de Operação"]
    }
  }
}
````

### Otimização de Tráfego de Dados (Carga Incremental)

Para mitigar lentidões e evitar o consumo desnecessário de largura de banda, a sincronização do servidor para as estações opera no formato de **Carga Incremental (Dados Alterados)**.

- O sistema não realiza o download completo de toda a base a cada ciclo. Ele filtra e transfere exclusivamente os registros cujo carimbo de modificação seja superior à última sincronização (ex: se apenas um preço foi alterado no ERP, somente esse produto é enviado à estação).
    
- **Ação Manual Alternativa:** Caso o técnico ou o operador necessite realizar uma limpeza forçada na tabela local, a interface dispõe de um comando para forçar o download da base completa, sobrescrevendo os dados locais.
    

# Arquitetura de Comunicação via API

A ponte de integração entre o terminal offline e o banco de dados da retaguarda não utiliza conexões diretas via banco de dados (Direct String Connection). Em vez disso, o sistema reaproveita o ecossistema do **Servidor Força de Vendas** (a mesma API utilizada para a sincronização do [[Mobile / Força de Vendas]]).

- **Lado Servidor (Central):** O serviço da API do Força de Vendas permanece em escuta contínua no servidor central da empresa (ou em ambiente web).
    
- **Lado Cliente (PDV):** O módulo offline consome os endpoints da API para submeter o JSON de movimentações executadas localmente e requisitar pacotes com as novidades cadastradas no ERP.
    

# Cenários e Recomendações de Uso

A arquitetura do PDV Offline atende com eficiência a dois perfis específicos de negócios:

### 1. Operações Críticas Ininterruptas

Segmentos cujo faturamento no balcão não pode parar por instabilidades técnicas de infraestrutura local, tais como supermercados, hortifrutis, padarias e açougues. Se o cabo de rede romper ou o servidor principal queimar, os caixas continuam vendendo.

### 2. Redes de Lojas e Unidades Descentralizadas

Empresas que possuem múltiplas filiais de pequeno porte (ex: quiosques de shopping, lojas de roupas, franquias de acessórios) e optam por manter o banco de dados da retaguarda hospedado em nuvem (**Retaguarda Web/Cloud**). Cada filial opera de forma autônoma e offline localmente, enviando o faturamento para a matriz de forma assíncrona via internet, consolidando as informações em um único banco gerencial.

# Pontos Críticos e Regras de Negócio

> [!danger] Bloqueio de Cadastros Estruturais no Terminal
> 
> É expressamente proibido realizar o cadastro de novos **Produtos, Tabelas de Preços ou Naturezas de Operação** diretamente no terminal do PDV Offline. Toda e qualquer alteração de cunho mercadológico ou fiscal deve ser efetuada estritamente no software de retaguarda. Caso essa regra seja violada por alterações diretas em banco, os códigos internos perderão a integridade na replicação, gerando rejeições de chaves primárias duplicadas na API.

> [!tip] Registro de Clientes na Estação
> 
> Ao contrário dos produtos, o cadastro de **Novos Clientes** é liberado na tela do PDV Offline para não travar vendas que exijam CPF/CNPJ na nota. Esses novos registros são marcados com uma flag de contingência local e são enviados para o servidor central no ciclo de replicação subsequente, sendo integrados à base global da retaguarda.

```
http://googleusercontent.com/youtube_content/1
```
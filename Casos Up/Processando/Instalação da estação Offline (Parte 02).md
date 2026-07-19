
---
id: [CASO-179]
link: https://www.youtube.com/watch?v=_enM9gDSHDc&t=3s
setor: [Suporte, Infraestrutura, Implementação]
modulo: [PDV / PDV Offline]
tags: [pdv-offline, instalação-pdv, sincronização-inicial, replicação-incremental, firebird]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Processo de Instalação]]
2. [[#Mecânica e Regras da Carga Inicial de Dados]]
3. [[#Estratégia Avançada de Implantação em Lote]]
4. [[#Rotinas de Atualização Diária (Incremental vs. Total)]]
5. [[#Fluxo de Transmissão e Monitoramento de Contingência]]
6. [[#Regras de Negócio e Pontos Críticos de Falha]]

# Visão Geral do Processo de Instalação
A implantação do terminal [[PDV / PDV Offline]] requer uma metodologia específica de provisionamento de banco de dados para garantir o isolamento e a autonomia da estação de vendas. O processo de vinculação inicial estabelece uma assinatura digital única baseada no hardware da máquina, preparando o SGBD local para receber as tabelas estruturais de retaguarda.

### Fluxo de Ativação Padrão:
1. No software executado na estação local, acesse a tela de identificação.
2. Informe o **CNPJ** da empresa licitante.
3. Clique no botão **Habilitar Offline**. O sistema processará gatilhos internos e modificações estruturais diretamente nas tabelas nativas do banco local.
4. O sistema carrega a lista de PDVs cadastrados na retaguarda central. Selecione a **Estação** correspondente criada previamente para aquele terminal (ex: `Estação 4`).
5. A partir deste momento, o terminal encontra-se pareado e indexado na API de sincronização.

# Mecânica e Regras da Carga Inicial de Dados

> [!danger] Prática Proibida: Cópia Direta do Banco do Servidor
> É expressamente proibido realizar a cópia física do arquivo de banco de dados principal do servidor (`.fdb` da retaguarda) para tentar utilizá-lo como atalho na pasta do PDV Offline. Esta ação injeta registros redundantes e incompatíveis com a operação de balcão (notas fiscais antigas de outras filiais, históricos de vendas globais, tabelas de auditoria pesadas). Além de gerar lixo eletrônico no terminal, a quebra de integridade fará com que a API recuse a devolução de cupons, gerando falhas catastróficas de sincronização.

Como o banco de dados inicial do PDV nasce 100% vazio, a execução da **Primeira Carga de Dados** é um processo mandatório e inegociável.
*   **Comportamento do Sistema:** Como não há registro anterior no histórico local de sincronização, o sistema ignora travas de modificação e realiza a varredura total dos cadastros na retaguarda.
*   **Métrica de Volumetria (Exemplo Técnico):** Em bases complexas (contendo mais de 20.000 produtos/medicamentos, 5.000 cidades e 3.400 clientes), a carga inicial pode demandar cerca de **27 minutos** para ser concluída de forma íntegra. Em cenários simplificados (faixa de 1.000 itens), o tempo médio é reduzido para **2 minutos**.

# Estratégia Avançada de Implantação em Lote

Para otimizar o tempo de implantação em clientes com grande volume de caixas (ex: supermercados com 6 ou mais PDVs), o analista de suporte não deve realizar a carga de 27 minutos individualmente em cada máquina. Recomenda-se adotar a **Técnica de Clonagem de Base Limpa**:

```mermaid
graph TD
    A[Criar PDV Offline Vazio no Servidor] --> B[Executar Carga Inicial Completa]
    B --> C[Gerar Arquivo .FDB Limpo e Sincronizado]
    C --> D[Copiar o .FDB para os Caixas 01, 02, 03...]
    D --> E[Acessar Canal de Empresas de cada Caixa]
    E --> F[Executar Ação: Trocar Estação]
````

### Resolução de Conflito de Hardware (Serial de HD)

Ao colar o banco clonado e tentar abrir o PDV em outra máquina, a aplicação disparará um alerta de segurança informando que a estação não está configurada para o Serial de HD corrente. Para homologar o clone:

1. Acesse o menu interno por dentro da empresa logada.
    
2. Vá em **Configurações do Sistema > Trocar Estação**.
    
3. Selecione o respectivo número de identificação correto daquela máquina física. O sistema atualizará as chaves criptográficas locais e liberará o caixa para venda.
    

# Rotinas de Atualização Diária (Incremental vs. Total)

Após a consolidação da primeira carga, os ciclos subsequentes de atualização passam a utilizar inteligência de tráfego de dados para mitigar o consumo de hardware.

- **Filtro Padrão ("Dados Modificados"):** Mantido por padrão pelo sistema. Varre a API e faz o download estritamente das entidades que sofreram mutação na retaguarda (alteração de preço, alteração cadastral). Esse fluxo consome em média apenas **24 segundos** para ser concluído.
    
- **Filtro Alternativo ("Todos"):** Rebaixa a inteligência do sistema e força o download em massa de todas as tabelas novamente, incorrendo na lentidão do processo de carga inicial. Deve ser evitado em rotinas diárias.
    

> [!tip] Obrigatoriedade na Abertura do Caixa
> 
> Através do painel gerencial, o administrador pode ativar o parâmetro **Atualização Obrigatória por Dia**. Com esta flag ativa, no primeiro acesso do operador ao iniciar a jornada ou ao **Abrir um Novo Caixa**, o sistema bloqueia a tela de vendas e força a execução da rotina incremental de 24 segundos, garantindo que o operador trabalhe com os preços atualizados do dia.

# Fluxo de Transmissão e Monitoramento de Contingência

Toda movimentação comercial executada no PDV Offline gera registros em contingência local com tabelas limpas (sem histórico de lixo). O envio desses dados para a retaguarda ocorre de forma assíncrona, orquestrado por um _Timer_ de background configurável (ex: a cada **60 segundos**).

JSON

```
{
  "log_evento_sincronizacao_automatica": {
    "intervalo_varredura": "60s",
    "status_comunicacao": "Conexão com Servidor Força de Vendas Ativa",
    "lote_envio": {
      "pedidos_transmitidos": 2,
      "notas_fiscais_transmitidas": 1,
      "fechamentos_caixa_transmitidos": 0
    },
    "comportamento_servidor_central": "Absorve os registros do lote e disponibiliza as notas e cupons nas telas de faturamento do ERP em tempo real"
  }
}
```

O painel de monitoramento do PDV exibe o **Histórico de Envios**, permitindo ao usuário gerenciar graficamente o volume de cupons emitidos localmente que já foram integrados na retaguarda e auditar possíveis pendências.

# Regras de Negócio e Pontos Críticos de Falha

> [!warning] Erro de Duplicidade: Controle Único de Séries Fiscais
> 
> Um ponto crítico de falha na implantação de múltiplos PDVs Offline ocorre quando o técnico replica bancos ou configura terminais distintos utilizando a **mesma Série de Nota Fiscal / NFC-e**. No primeiro envio de lote, o Caixa 01 autorizará a nota número 10. Quando o Caixa 02 tentar emitir ou transmitir a sua nota número 10 sob a mesma série, a SEFAZ ou a API retornará o erro de **Duplicidade de Chave de Acesso**. É obrigatório que cada estação offline possua uma numeração de série exclusiva atribuída em seus parâmetros.

> [!warning] Restrição de Interface de Configurações
> 
> O input de endereço de servidor e ativação de CNPJ só é exibido na tela de configurações se o operador acessar a rotina **por dentro da empresa ativa**. Se a tela for invocada a partir dos menus externos do executável (com a base deslogada), o sistema exibirá apenas as opções básicas de atualização de cadastros, ocultando os campos estruturais de rede para proteção dos parâmetros de infraestrutura.

```
http://googleusercontent.com/youtube_content/1
```
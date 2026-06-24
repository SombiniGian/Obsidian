---
id: [CASO-056]
link: https://www.youtube.com/watch?v=maOauuYQAL8
setor: [Suporte, Implantação]
modulo: [Restaurante]
tags:
  - mapa-mesas
  - comandas
  - configuracao-totem
  - alertas-tempo
data_criacao: 2026-06-24
---

# Restaurante (Parte 1): Cadastro de Mesas, Comandas e Configuração do Mapa

Este documento técnico detalha os fundamentos de arquitetura e implantação do ecossistema de atendimento presencial do módulo de **Restaurante**. A ferramenta suporta a operação híbrida ou isolada através de mapas de mesas físicos, controle de comandas numeradas e integração de fluxos de delivery.

---

## Sumário
1. [[#Modelos de Trabalho Presencial]]
2. [[#Cadastro de Mesas em Lote]]
3. [[#Dimensionamento e Customização do Mapa de Mesas]]
4. [[#Temporizadores de Alerta e Status de Ociosidade]]
5. [[#Regras de Segurança e Autenticação de Operadores (Garçons)]]
6. [[#Pontos Críticos e Validações]]

---

## Modelos de Trabalho Presencial

O sistema adapta-se à infraestrutura logística do estabelecimento, disponibilizando duas metodologias principais para abertura e controle de contas:

* **Mapa de Mesas:** Focado em estabelecimentos com consumo local fixo em mesas numeradas. O garçom interage diretamente com o layout visual indicando o local físico do cliente.
* **Comandas Eletrônicas/Impressas:** Utiliza cartões numerados e individualizados. O sistema permite atrelar múltiplas comandas de consumo a uma única mesa física (ex: controle de contas separadas para indivíduos alocados na mesma mesa).

---

## Cadastro de Mesas em Lote

Para agilizar o processo de implantação técnica e evitar o *input* manual unitário de cada ponto de consumo, a ferramenta possui uma rotina de geração em massa.

* **Caminho de Acesso:** Menu **Cadastro** -> **Mesas**.

### Procedimento de Inclusão Rápida:
1. Caso a tabela esteja vazia, clique no botão auxiliar de **Geração Avançada / Opções**.
2. Informe o número do código inicial (ex: `51`) e o número do código final desejado (ex: `70`).
3. Confirme a operação. O sistema gerará de forma sequencial automática todos os registros no banco de dados.

> [!tip] Manutenção de Registros
> Na ficha individual da mesa, o analista pode atribuir uma descrição personalizada (ex: `Mesa 01 - Janela`), acrescentar letras de identificação no código ou **Inativar** o registro para que ele deixe de ocupar espaço visual no mapa caso a mesa seja removida fisicamente do salão.

---

## Dimensionamento e Customização do Mapa de Mesas

A interface do mapa de mesas é moldada através de parâmetros de enquadramento técnico para se adequar ao tamanho dos monitores locais (especialmente monitores *Touch Screen*).

* **Número Máximo de Linhas e Colunas:** Define a matriz de distribuição dos botões em tela, otimizando o enquadramento do grid.
* **Customização de Imagens de Status:** É possível carregar imagens bitmap distintas para representar visualmente uma **Mesa Vazia** (Livre) ou uma **Mesa Ocupada** (Consumindo).

> [!tip] Otimização de Performance Gráfica
> Por padrão técnico de homologação, recomenda-se manter o mapa **sem imagens de fundo nos botões** (utilizando apenas as cores de status sólidas nativas). Esta prática reduz o consumo de memória de vídeo da estação e melhora o enquadramento e aproveitamento de espaço útil do monitor.

---

## Temporizadores de Alerta e Status de Ociosidade

O mapa de mesas atua como um painel de monitoramento ativo do salão. O sistema executa um ciclo de varredura automática (ajustável no campo **Atualizar Mesas em X Segundos**) para reavaliar o tempo decorrido desde o último lançamento de item em cada ponto.

┌─────────────────────────┐ ┌─────────────────────────┐ ┌─────────────────────────┐ │ Normal (Verde) │ ───>            │ Ociosa (Amarelo) │ ───> │ Atenção (Vermelho) │
│ Consumo dentro do prazo│ │ Alerta de tempo atingido│ │ Sem consumo prolongado │ └─────────────────────────┘ └─────────────────────────┘ └─────────────────────────┘

* **Status Normal (Verde):** A mesa possui consumo ativo e a última inserção de item está dentro do tempo de tolerância padrão.
* **Status Ocioso (Marcador Amarelo):** Disparado quando o tempo configurado no parâmetro **Tempo de Alerta** é ultrapassado. Alerta visualmente a equipe que a mesa está sem novos pedidos, indicando oportunidade de abordagem pelo garçom.
* **Status Crítico (Marcador Vermelho):** Ativado ao atingir o limite estipulado no campo **Tempo de Atenção**. Indica ociosidade severa e prolongada, servindo de alerta para prevenir incidentes como evasão de clientes sem o devido acerto da conta.
* --- ## Regras de Segurança e Autenticação de Operadores (Garçons) Para garantir a auditoria de comissões e rastreabilidade de perdas, cada lançamento deve estar obrigatoriamente associado a um código de **Vendedor/Garçom**. A validação conta com duas topologias de configuração: 
* ---### Topologia A: Terminais de Uso Coletivo (Balcão / Totem Central) Em cenários onde múltiplos garçons utilizam o mesmo terminal físico para lançar pedidos, o parâmetro **Solicitar Código de Vendedor** deve estar ativo. 
1. O operador clica sobre a mesa desejada.
2. O sistema bloqueia a tela e exibe um teclado numérico virtual (*Touch*) exigindo a digitação do código do garçom antes de liberar o menu de produtos. 
3. O sistema abre o formulário de seleção, vincula o item àquele código e, após o salvamento, encerra a sessão para o próximo operador. 
* ---### Topologia B: Terminais de Uso Exclusivo (Micro-estação / PDA do Garçom) Caso o terminal seja operado estritamente por um único funcionário: 
1. No menu de **Cadastro de Usuários**, localize o login do operador correspondente. 
2. Vincule o respectivo código de vendedor diretamente ao perfil de usuário do sistema. 
3. Com este vínculo ativo, o sistema suprime a exigência do teclado numérico na abertura de mesas, herdando automaticamente o código do funcionário logado e agilizando o fluxo de trabalho. 
--- ## Pontos Críticos e Validações 
>[!warning] Validações Operacionais e Comportamento Automatizado > 1. **Gravação Automática por Abandono de Tela:** Para mitigar o risco de um operador deixar uma tela de venda de mesa aberta em um totem coletivo, impossibilitando o uso pelos demais funcionários, configure o tempo limite de ociosidade técnica da tela. Se a interface permanecer aberta sem interações pelo período determinado (ex: `10 segundos`), o sistema executará o comando de salvamento e fechamento de forma automática. > 2. **Instabilidade no Tempo de Atualização:** Configurar o temporizador de atualização do mapa de mesas com valores excessivamente baixos (ex: menos de `5 segundos`) em redes locais instáveis ou com conexões Wi-Fi deficientes pode sobrecarregar o banco de dados com requisições repetitivas, provocando lentidão nas telas de vendas dos terminais.


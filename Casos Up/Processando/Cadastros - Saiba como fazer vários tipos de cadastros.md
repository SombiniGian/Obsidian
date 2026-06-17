Este módulo detalha as diretrizes operacionais, a arquitetura de dados e as regras de negócio aplicadas à central de **Cadastros Gerais e Alertas do Sistema** no ERP Código UP. A ferramenta foi projetada para garantir a integridade da informação nas vertentes financeira, fiscal, logística e comercial da empresa `[00:00:25]`, `[00:05:05]`.

### 1. Centralização Cadastral de Pessoas e Agrupamentos `[00:00:25]`

A arquitetura do ERP Código UP adota o conceito de entidade unificada, eliminando a redundância de dados no banco de dados `[00:00:25]`:

- **Multi-Perfil no Mesmo Registo:** Uma mesma pessoa ou empresa cadastrada no sistema pode assumir múltiplos papéis simultâneos `[00:00:34]`. O operador pode marcar num único ecrã se a entidade é, ao mesmo tempo, **Cliente, Fornecedor e Vendedor** `[00:00:45]`. As listagens de pesquisa disponibilizam filtros rápidos para isolar os perfis quando necessário `[00:00:53]`.
    
- **Frota e Logística de Veículos:** O cadastro de veículos permite associar camiões e furgões à movimentação de cargas, servindo de base para o controlo de custos operacionais e histórico de manutenções preventivas (ex: controlo de quilometragem para trocas de óleo) `[00:01:31]`, `[00:01:52]`.
    
- **Sinalização Visual de Status:** As grades utilizam um padrão rígido de legendas coloridas para indicar a situação do registo `[00:02:36]`. Por exemplo, entidades ou produtos ativos assumem a cor azul, em promoção ficam em preto, e registos **inativos ou bloqueados assumem a cor vermelha** `[00:02:44]`, `[00:02:52]`.
    

### 2. Motor de Alerta de Margens e Inteligência de Custos (Markup) `[00:03:00]`

O módulo de produtos conta com uma matriz de alertas visuais para proteger a rentabilidade comercial do estabelecimento durante os processos de reposição de stock `[00:03:00]`:

```
+------------------------------------------------------------------------+
|                     ESQUEMA DE CORES DO ALERTA DE MARKUP               |
+------------------------------------------------------------------------+
|                                                                        |
|  [ Entrada de Nota ] ──► [ Aumento do Custo do Item ]                  |
|                                     │                                  |
|               ┌─────────────────────┼─────────────────────┐            |
|               ▼                     ▼                     ▼            |
|       Margem de Lucro:      Margem de Lucro:      Margem de Lucro:     |
|         ABAIXO DO MÍNIMO       DENTRO DO INTERVALO     ACIMA DO MÁXIMO |
|        (Custo Alto/Crítico)   (Alerta de Ajuste)   (Margem Segura)     |
|               │                     │                     │            |
|               ▼                     ▼                     ▼            |
|         SINAL VERMELHO        SINAL AMARELO         SINAL VERDE        |
|           [00:03:42]            [00:03:11]            [00:03:21]       |
+------------------------------------------------------------------------+
```

- **Gatilho de Entrada de Notas:** Quando o utilizador regista uma compra e o Web Service deteta que o preço de custo do fornecedor aumentou, o ERP cruza imediatamente o novo valor com as regras de **Markup** configuradas na empresa `[00:03:29]`, `[00:03:35]`.
    
- **Comportamento dos Alertas:** Se o Markup cair abaixo do limite crítico devido ao aumento do custo, o produto fica destacado a **vermelho** `[00:03:42]`. À medida que o operador reajusta o preço de venda, o indicador passa a **amarelo** (zona de transição e alerta) `[00:04:32]` e, finalmente, a **verde** ao atingir a margem ideal estipulada gerencialmente `[00:03:21]`. Isto garante que nenhum item seja vendido sem a margem de lucro corrigida `[00:04:50]`.
    

### 3. Ficha Técnica Avançada do Produto `[00:05:05]`

O cadastro de artigos reúne parâmetros específicos para atender a diversos modelos de negócio `[00:05:05]`:

- **Múltiplos Códigos de Barra:** O ERP suporta o vínculo de várias sequências numéricas (EAN) para o mesmo produto, exigindo apenas a marcação de um deles como o principal para fins de relatórios `[00:05:19]`.
    
- **Regras de Comissão Flexíveis:** É possível fixar uma percentagem de comissão direta no produto `[00:05:28]`. Esta regra sobrepõe-se à comissão padrão do vendedor, permitindo criar políticas de incentivo para produtos específicos `[00:05:38]`.
    
- **Tipo de Item e Engenharia de Composição:** Determina se o item é de revenda normal, produto de balança (peso) ou composto `[00:06:41]`. Na aba de **Composição**, o gestor cria a árvore de componentes (Matérias-Primas), ideal para a transformação industrial ou montagem de kits, realizando a baixa automática dos insumos no stock no momento da venda `[00:06:50]`.
    
- **Rastreabilidade de Estoque (Físico vs. Fiscal):** A aba de movimentação mapeia detalhadamente o histórico e o saldo do produto sob duas perspetivas: o stock **Real/Gerencial** (toda a entrada e saída interna) e o stock **Fiscal** (alimentado estritamente por emissão de Notas Fiscais) `[00:07:16]`, `[00:07:30]`.
    

### 4. Flexibilidade nas Tabelas de Preço Dinâmicas `[00:10:02]`

O sistema permite a criação de infinitas políticas comerciais através do ecrã de tabelas de preço `[00:10:02]`:

- **Ajuste Linear (Rápido):** O gestor pode criar uma tabela que aplica uma taxa percentual fixa (ex: acréscimo automático de 10% em todos os artigos do pedido) `[00:10:30]`.
    
- **Ajuste Cirúrgico (Exceção por Item):** O sistema permite abrir a tabela e digitar manualmente o preço de venda exato para itens específicos `[00:10:40]`. Nas linhas configuradas com preço manual, o ERP ignora a regra percentual geral e aplica o valor fixado, validando sempre se o preço de venda inserido não está abaixo do custo de reposição `[00:11:05]`.
    

### 5. Controlo Financeiro de Documentos e Segurança de Crédito `[00:08:47]`

A retaguarda financeira é gerida por regras rígidas de parametrização de tipos de documento e limites de crédito:

- **Automação por Tipo de Documento:** No cadastro de Formas de Pagamento e Documentos (Dinheiro, Cheque, Depósito), o sistema é configurado para determinar o comportamento do fluxo de caixa `[00:08:47]`. Ao selecionar "Cheque", por exemplo, o ERP abre obrigatoriamente a janela de custódia para inserção do número, banco e bom para do título `[00:09:16]`, `[00:09:24]`.
    
- **Bloqueio de Clientes Inadimplentes (Controlo por Senha):** O sistema permite parametrizar bloqueios automáticos baseados no perfil do cliente `[00:12:06]`. Se um cliente possuir pendências financeiras vencidas ou ultrapassar o limite de crédito, o registo assume o status de bloqueado (exibindo um ícone de cadeado) `[00:12:38]`, `[00:12:56]`. Nestas condições, o sistema impede a faturação e a inclusão do cliente em cargas logísticas até que um supervisor autorizado insira a sua senha de liberação `[00:13:37]`, `[00:13:47]`.
    

ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: [Assista ao vídeo no YouTube](https://www.youtube.com/watch?v=WHJUlS48MaM).
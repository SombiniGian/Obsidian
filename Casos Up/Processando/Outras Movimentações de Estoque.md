---
id: [CASO-053]
link: https://www.youtube.com/watch?v=lcF3vph1Mz4
setor: [Suporte, Logística, Estoque]
modulo: [Estoque]
tags:
  - outras-movimentacoes
  - ajuste-estoque
  - quebra-perda
  - troca-mercadoria
data_criacao: 2026-06-24
---

# Outras Movimentações de Estoque

Esta documentação técnica detalha o funcionamento da ferramenta de **Outras Movimentações de Estoque** introduzida a partir da versão 53.8. A rotina visa suprir cenários logísticos que não envolvem operações comerciais padrão de compra ou venda, tais como perdas de produção, quebras físicas, trocas de mercadorias ou consumos internos.

---

## Sumário
1. [[#Configuração dos Tipos de Movimentação]]
2. [[#Cálculo Automático por Porcentagem]]
3. [[#Fluxo de Lançamento de Movimentações]]
4. [[#Operações Complexas (Trocas de Produtos)]]
5. [[#Rastreabilidade e Impacto no Inventário]]
6. [[#Pontos Críticos e Validações]]

---

## Configuração dos Tipos de Movimentação

Antes de operacionalizar os ajustes no inventário, o sistema exige a parametrização dos motivos ou naturezas internas de ajuste. O cadastro é maleável e permite criar infinitos cenários conforme a regra de negócio da empresa.

* **Caminho de Acesso:** Menu **Cadastro de Produtos** -> **Outros Tipos de Movimentações**.

### Parâmetros por Tipo:
* **Descrição:** Nome que identifica o cenário (ex: `PERDA DE PRODUÇÃO`, `TROCA`, `AVARIA`).
* **Direção do Fluxo Padrão:** Define se a operação indica, por padrão, uma **Entrada** ou uma **Saída** de saldo.
* **Movimentação Principal:** Flag que determina qual tipo de movimentação será selecionado automaticamente pelo sistema como primeira opção ao abrir a tela de novos lançamentos.
* **Exigência de Pessoa:** Define se o preenchimento do cadastro do parceiro (fornecedor/cliente/funcionário) é obrigatório no ato da operação.
* **Porcentagem Atual (Fator de Cálculo):** Percentual pré-fixado aplicado diretamente sobre o volume total do saldo atual do produto no momento do lançamento.

---

## Cálculo Automático por Porcentagem

O sistema conta com um automatismo focado em indústrias ou empresas de fracionamento para agilizar o lançamento de perdas e quebras estatísticas de produção.

> [!info] Mecanismo de Funcionamento
> Se o tipo de movimentação configurado possuir o valor `10,00` no campo de porcentagem e o sentido padrão for **Saída**, ao selecionar um produto cujo estoque atual em sistema seja de 110 unidades, a aplicação calculará automaticamente a quantidade de `11` unidades para a baixa de inventário (`110 * 10% = 11`).

> [!tip] Flexibilização de Quantidade
> O cálculo gerado pelo percentual serve estritamente como uma sugestão automatizada para acelerar o processo. O operador do sistema retém autonomia total para alterar manualmente a quantidade sugerida no grid de itens antes de efetivar a gravação final do documento.

---

## Fluxo de Lançamento de Movimentações

O processo de input operacional das movimentações avulsas é centralizado e suporta a inserção de múltiplos itens sob o mesmo cabeçalho.

* **Caminho de Acesso:** Menu **Movimentação** -> **Outras Movimentações**.

### Passo a Passo Operacional:
1. Clique no botão **Incluir** para abrir o formulário de lançamento. O sistema preencherá de forma automatizada a **Data Atual** e carregará o tipo definido como **Movimentação Principal**.
2. Preencha o campo de **Observação** global, se necessário, para detalhar o motivo do ajuste.
3. No grid de itens, utilize o atalho **F2** para abrir a consulta rápida e selecionar o produto desejado.
4. O sistema carregará o sentido padrão e a quantidade (baseada na regra percentual ou valor unitário padrão).
5. Preencha a **Observação do Item** caso a justificativa mude de produto para produto dentro do mesmo lote.
6. Pressione as teclas de navegação ou clique em salvar para processar.

---

## Operações Complexas (Trocas de Produtos)

A arquitetura do módulo permite que um único documento de movimentação contenha naturezas e fluxos opostos simultaneamente (operações híbridas). O cenário mais comum para este uso é o processo de **Troca de Mercadorias**.

┌───────────────────────────────────────────────────────────────────┐ 
│ Documento Único de "Outra Movimentação" │ ├────────────────────────────────┬──────────────────────────────────┤ 
│ ITEM A: Produto Danificado │ Fluxo: SAÍDA (Ajuste/Descarte) │ ├────────────────────────────────┼──────────────────────────────────┤ 
│ ITEM B: Produto Novo Entregue │ Fluxo: ENTRADA (Retorno ao Esto) │ └────────────────────────────────┴──────────────────────────────────┘

> [!tip] Execução de Trocas > Para registrar uma troca interna, insira o item que está saindo do estabelecimento ou da área utilizável como uma **Saída** e insira o novo item correspondente na linha logo abaixo configurando o campo de fluxo manualmente como **Entrada**. Isso mantém a correlação do fato gerador em um único código de lançamento. 


> --- ## Rastreabilidade e Impacto no Inventário A gravação do registro realiza a consolidação imediata no banco de dados e afeta diretamente a ficha cárdex do produto. * **Auditoria de Operações:** O sistema armazena de forma permanente o valor financeiro do ajuste, a quantidade exata movimentada, a data/hora da gravação e a identificação do **Usuário** responsável pelo comando. * **Consulta de Extrato:** O histórico detalhado e o impacto dessas baixas ou acréscimos podem ser auditados acessando o módulo de [[Ficha Cárdex]] ou diretamente na aba de movimentações dentro da ficha cadastral do produto modificado.


 --- ## Pontos Críticos e Validações > 
>[!warning] Validações e Riscos Operacionais > 
  1. **Inversão de Fluxo Manual:** Ao realizar lançamentos híbridos (como trocas), certifique-se de que o campo que define a direção da movimentação (Entrada/Saída) foi ajustado devidamente em cada linha do grid. A falta de atenção nessa marcação gerará furos severos de inventário. 2. **Valoração do Ajuste:** O valor monetário atribuído à movimentação avulsa utilizará como base os parâmetros de custo definidos no sistema (geralmente Custo Médio ou Custo de Última Entrada). Divergências no cadastro de custo do produto irão distorcer os relatórios de perdas financeiras da empresa.
 
 







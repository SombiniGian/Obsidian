---
id: [CASO-168]
link: https://www.youtube.com/watch?v=n8W6kmwZ6f8&t=275s
setor: [Suporte, Implementação, Banco de Dados]
modulo: [Migração de Dados / Importador Excel]
tags: [migracao-de-dados, excel, importacao, controle-de-ids, firebird, implantacao]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Ferramenta de Migração]]
2. [[#Estrutura das Planilhas de Importação]]
    1. [[#Planilha de Produtos (Campos Críticos)]]
    2. [[#Planilhas de Clientes e Fornecedores]]
    3. [[#Planilhas Financeiras (Contas a Pagar / Receber)]]
3. [[#Operação da Ferramenta Importadora]]
4. [[#Rotina Pós-Importação Obrigatória (Controle de IDs)]]
5. [[#Regras de Negócio e Pontos Críticos de Falha]]

# Visão Geral da Ferramenta de Migração
A ferramenta de **Migração de Dados (Migrador Excel)** é um utilitário desenvolvido para auxiliar as revendas durante a fase de implantação do sistema (Go-Live). Seu propósito é extrair dados estáticos e históricos de sistemas legados de terceiros, organizá-los em planilhas padronizadas do Excel (`.xls` / `.xlsx`) e injetá-los diretamente no banco de dados Firebird do novo ERP. O pacote contém o aplicativo executável do importador e cinco planilhas modelos pré-formatadas: *Produtos, Clientes, Fornecedores, Contas a Pagar e Contas a Receber*.

> [!warning] Foco Exclusivo em Implantação
> Esta ferramenta destina-se **estritamente à carga inicial de dados** (antes do sistema entrar em operação na loja). A utilização deste importador em bases de dados em produção (com movimentação ativa de notas fiscais e caixa) pode causar quebras irreversíveis de integridade referencial. Não utilize o migrador para atualizar estoques ou cadastrar lotes de produtos mensalmente.

# Estrutura das Planilhas de Importação

### Planilha de Produtos (Campos Críticos)
A tabela de produtos é a entidade mais complexa e exige parametrização tributária exata. Ao alimentar o arquivo, atente-se às seguintes colunas:
*   **ID (Internal ID):** Número de identificação primária. Deve ser estritamente numérico inteiro (sem letras ou zeros à esquerda). 
*   **Código Fiscal:** Campo vital para a consistência fiscal (SPED/Sintegra). Se o cliente já operava com um código fiscal (código do item na SEFAZ), ele deve ser mantido idêntico nesta coluna para evitar divergências nas emissões futuras e autuações do fisco.
*   **Código de Barras:** Evite migrar "lixo eletrônico" (códigos gerados aleatoriamente pelo sistema antigo). Importe apenas códigos EAN (ex: iniciados em 789) ou GTINs reais.
*   **Atributos Fiscais:** As colunas de CST de ICMS, CSOSN e NCM são **obrigatórias**. O preenchimento em branco nestas colunas bloqueará a edição futura do produto no ERP. Em caso de desconhecimento, adote a flag de "Tributado" como *fallback* até a revisão do contador.
*   **Tipo de Produto:** Define a natureza de circulação do item (ex: `00` para Mercadoria para Revenda). Letras e numerações específicas devem seguir o dicionário de dados da contabilidade.

### Planilhas de Clientes e Fornecedores
O preenchimento destas planilhas engloba dados cadastrais convencionais (Razão Social, Nome Fantasia, CPF/CNPJ, Endereço e Contatos). 

### Planilhas Financeiras (Contas a Pagar / Receber)
Estas tabelas migram os saldos e títulos pendentes (ou baixados) do cliente.
*   **Status do Título:** A coluna de status aceita apenas dois parâmetros fixos: `AB` (Em Aberto) ou `BX` (Baixado/Pago).
*   **Vínculo com Pessoas (FK):** Para que o título seja atrelado ao sacado/cedente correto, a coluna de identificação do cliente/fornecedor aceita duas chaves de busca: o **ID Numérico** ou o **CPF/CNPJ**. 

> [!info] Fusão de Cadastros (Unificação de Entidades)
> O sistema UP adota o conceito de **Cadastro Único de Pessoas**, ou seja, não existem tabelas separadas para Clientes e Fornecedores; um mesmo ID atua nos dois papéis. Se o sistema legado do cliente possuía o "Cliente ID 1" e o "Fornecedor ID 1" (pessoas diferentes), ocorrerá um choque de chaves primárias.
> *   **Solução:** Faça o vínculo financeiro estritamente através do preenchimento da coluna de **CNPJ/CPF**.
> *   **Solução Alternativa (Incremento de IDs):** Na planilha de Fornecedores, some um valor alto aos IDs legados (ex: `ID original + 10.000`). O Fornecedor 1 passará a ser o `10001`. Utilize este novo ID na planilha de Contas a Pagar.

# Operação da Ferramenta Importadora
Com as planilhas validadas, a injeção dos dados deve seguir um fluxo sequencial:

1.  Abra o aplicativo Migrador de Dados.
2.  Preencha a **Porta** (padrão [[Banco de Dados / Firebird]]: `3050`) e o caminho físico local ou IP do arquivo de banco de dados (`.fdb`).
3.  Clique em **Conectar**. O sistema listará os CNPJs (Empresas) atrelados àquela base. Selecione a empresa desejada.
4.  Selecione o arquivo Excel correspondente.
5.  Defina o comportamento do motor em caso de colisão de dados (se encontrar um código já existente):
    *   *Substituir cadastro.*
    *   *Atualizar apenas o saldo de estoque.*
    *   *Ignorar o registro duplicado.*
6.  Defina a estratégia do Gerador de IDs (Manter o ID da planilha ou forçar o banco a Auto-Incrementar).
7.  Clique em **Importar**.

> [!warning] Ordem de Execução das Planilhas (Dependência Relacional)
> O banco de dados rejeitará a importação financeira se as pessoas não existirem. Você deve obrigatoriamente processar as planilhas na seguinte ordem:
> 1º - **Clientes** e **Fornecedores**
> 2º - **Produtos**
> 3º - **Contas a Receber** e **Contas a Pagar**

# Rotina Pós-Importação Obrigatória (Controle de IDs)
Ao injetar dados "por fora" da aplicação (via migrador), o controle nativo de auto-incremento (Generators/Sequences) do Firebird perde a referência de qual foi o último ID numérico utilizado nas tabelas. 

Se o integrador parar no ID `1500` e o operador tentar cadastrar um novo cliente no ERP manualmente, o sistema tentará usar o ID `1` (ou o último ID salvo no cache da aplicação), gerando o erro de violação de chave primária (*Primary Key Violation*).

1. Abra o ERP normalmente (após a carga de dados).
2. Acesse o menu **Ferramentas do Sistema > Controle de IDs**.
3. A tela exibirá os geradores de todas as tabelas (Clientes, Produtos, etc.).
4. Clique em **Atualizar IDs**. O sistema fará um `MAX(ID)` em cada tabela e sincronizará o motor do banco de dados, garantindo que o próximo cadastro inicie do número correto.

# Regras de Negócio e Pontos Críticos de Falha

> [!danger] Colisão de Código Fiscal em Substituições Futuras
> Se a revenda importar produtos e o campo "Código Fiscal" for preenchido com dados divergentes da base estadual da SEFAZ, o XML das notas de saída reportará números diferentes (Ex: Vende-se a Coca-Cola como código interno 20, mas o fisco a reconhecia como código 10 no software anterior). Isso quebra o inventário do SPED Fiscal e gera multas para o lojista. A integridade do código fiscal legado é intransigível durante a migração.
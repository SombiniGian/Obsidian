---
id: CASO-005
link: https://www.youtube.com/watch?v=jSPyG3JarvA
setor: Suporte, Implantação, Faturamento
modulo: Frente de Caixa / PDV
tags:
  - nfce
  - parâmetros
  - regras-fiscais
  - seguranca-pdv
  - formas-de-pagamento
data_criacao: 2026-06-24
---

# Documentação Técnica: Parametrização de Vendas e Diretrizes para Emissão de NFC-e

Esta documentação provê os requisitos lógicos, configurações estruturais de tela, regras de validação fiscal e controle de permissões de alçada para preparar o ERP para a emissão de Nota Fiscal de Consumidor Eletrônica ([[NFC-e]]).

---

## Sumário
1. [[#1. Configuração da Natureza de Operação Padrão]]
2. [[#2. Sincronização de Formas de Pagamento (Tipos de Documento)]]
3. [[#3. Mapeamento de Clientes e Fluxo de Venda Balcão]]
4. [[#4. Matriz de Configurações da Tela de Vendas (Engrenagem)]]
5. [[#5. Arquitetura de Segurança e Senhas de Liberação]]
6. [[#6. Estados de Item e Operações de Venda na Prática]]

---

## 1. Configuração da Natureza de Operação Padrão

A emissão de NFC-e requer que as movimentações de saída do PDV estejam vinculadas a uma natureza de operação devidamente parametrizada para evitar rejeições na SEFAZ.

* **Acesso:** **Cadastros > Natureza de Operação**.
* **Preço Referencial:** Deve ser definido para utilizar o **Preço de Venda** como o valor oficial de saída na nota.
* **Código Fiscal de Operação (CFOP):** O padrão interno inicial do sistema para vendas estaduais é o CFOP **5405** ou **5102**, dependendo do regime tributário do produto.
* **Modelo do Documento:** Configuração mandatória para o **Modelo 65** (específico para NFC-e).
* **Parâmetros de Nota:**
  * **Série:** Definição da série de emissão do terminal (ex: Série `1`).
  * **Finalidade:** Fixada como **1 - Normal**.
  * **Presença do Comprador:** Configurada obrigatoriamente como **1 - Operação Presencial** na maior parte das operações de varejo.

---

## 2. Sincronização de Formas de Pagamento (Tipos de Documento)

As formas de pagamento disponíveis na tela de fechamento do PDV dependem do vínculo estabelecido no cadastro financeiro do sistema.

* **Acesso:** **Financeiro > Tipos de Documentos**.
* **Flag de Ativação:** Para que um meio de pagamento fique disponível na listagem de fechamento do PDV (tecla **F9**), a propriedade **Utilizar no PDV/NFC-e** deve estar marcada. Se desmarcada (como exemplificado no caso do *Crédito*), o meio de pagamento é suprimido da tela, impedindo o operador de selecioná-lo.
* **Código de Integração SEFAZ:** Cada documento precisa estar mapeado com o código correspondente da tabela oficial da SEFAZ (ex: Dinheiro = `01`, Cartão de Crédito = `03`, etc.).

---

## 3. Mapeamento de Clientes e Fluxo de Venda Balcão

Para agilizar o atendimento no varejo, o sistema gerencia as vendas sem identificação nominal através de um cadastro genérico pré-existente.

* **Cliente Consumidor Padrão:** O sistema vem de fábrica com o registro **Consumidor Final** ativo.
* **Vínculo Automatizado:** Na aba de parametrização da tela balcão, este cliente é definido como o destino de todas as vendas nas quais o operador não informe um CPF ou CNPJ específico, centralizando os cupons de forma anônima.

---

## 4. Matriz de Configurações da Tela de Vendas (Engrenagem)

Ao acessar o menu de configurações interno da tela de vendas (ícone da engrenagem), o analista de suporte define as diretrizes operacionais do caixa:

### Comportamento Visual e de Layout
* **Tipo de Tela:** Define a usabilidade do módulo. O tipo **Pedido** formata a tela para rotinas de atacado/distribuição. O tipo **Balcão** ativa a interface otimizada para o varejo acelerado (PDV).
* **Exibição de Cabeçalho:** Habilita ou desabilita a barra de informações superiores na venda. Desativar o cabeçalho economiza espaço vertical no grid de itens.
* **Impressão Automática:** Define se o espelho gerencial do pedido deve ser visualizado na tela antes do envio ou se a impressão deve ser disparada direto para a porta térmica após gravar.

### Regras de Restrição Comercial
* **Bloqueio de Estoque:** Impede a conclusão da venda caso o produto atinja saldo menor ou igual a zero em estoque.
* **Modo de Envio Direto:** Permite que ao finalizar o pagamento, o sistema envie o XML da NFC-e em segundo plano sem abrir caixas de diálogo adicionais.
* **Obrigatoriedade de Cadastro:** Opção de travar a venda exigindo que o operador informe obrigatoriamente o código do **Vendedor** e do **Cliente** antes de lançar o primeiro produto.

---

## 5. Arquitetura de Segurança e Senhas de Liberação

Para mitigar fraudes e erros operacionais no PDV, certas operações críticas exigem a digitação de credenciais de gerência de forma síncrona.

* **Gatilhos de Segurança (Flags de Bloqueio):** Na tela de configurações, é possível marcar a obrigatoriedade de senha para as seguintes ações do operador:
  * Cancelamento de venda em andamento.
  * Exclusão de itens já inseridos no grid.
  * Concessão de Descontos acima do permitido.
  * Alteração manual do Preço Unitário do produto.
* **Módulo de Liberação:** O gerenciamento dessas chaves ocorre em **Cadastros > Senhas de Liberação**. O sistema possui o usuário master `UP` com a senha padrão `123` para fins de implantação técnica.

> [!warning] Alteração Obrigatória de Senha Padrão
> A senha padrão do suporte (`123`) deve ser alterada ou vinculada ao perfil do gerente real do estabelecimento logo após o treinamento. Mantê-la ativa expõe o sistema à quebra de integridade de preços por parte dos operadores de caixa.

---

## 6. Estados de Item e Operações de Venda na Prática

Durante o ciclo de digitação da venda no modo PDV, o grid exibe indicadores visuais de acordo com as ações do operador:
[ Inserção de Produto no Grid ] 
| +---> Valor Padrão (Sem alterações) -> Status Normal
| +---> Operador pressiona ALT (Alterar Preço) -> Pede Senha Gerencial -> Preço Alterado -> Status: Alterado pelo Usuário

Alteração Espontânea de Preço (Tecla ALT) 
1. Caso a flag **Pedir senha para alterar o valor unitário** esteja ativa, se o operador tentar modificar o preço do item digitando a tecla de atalho **ALT**, o ERP trava o foco da tela e exibe o prompt de segurança. 
2. Após a digitação correta da senha do gerente, o campo de preço é liberado. 
3. Ao confirmar a modificação, o sistema altera o status da linha do item no banco de dados, sinalizando graficamente no grid que aquele registro sofreu uma mutação de preço de tabela por interferência humana, registrando o evento para auditoria posterior. 

Finalização de Venda (Tecla F9) Ao teclar **F9**, o caixa avança para a tela de liquidação. O sistema monta a matriz de pagamentos baseada estritamente nos Tipos de Documento autorizados. Caso ocorra alguma falha na assinatura digital ou o certificado configurado na retaguarda apresente inconsistências (ex: cadeia de certificação corrompida), o ERP aborta a gravação da NFC-e e exibe o log de erro retornado pela API de mensageria para a devida correção técnica.
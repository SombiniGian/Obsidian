---
id: CASO-001
link: https://www.youtube.com/watch?v=IqIAS29hptE
setor: Financeiro
modulo: Conciliação de Cartão de Crédito
tags: [financeiro, conciliação, cartao-de-credito, bordero, automacao]
data_criacao: 2026-07-18
---

## Sumário
- [[#Visão Geral e Objetivo]]
- [[#Pré-requisitos e Configuração de Layouts]]
- [[#Regras de Negócio e Sistema de Vinculação]]
- [[#Fluxo de Execução (Passo a Passo)]]
- [[#Resolução de Conflitos e Tratamento de Erros]]

## Visão Geral e Objetivo

A rotina de importação de planilhas de administradoras de cartão de crédito (como Cielo, Rede, etc.) tem como objetivo automatizar a baixa de recebimentos no módulo financeiro. 

Anteriormente, o usuário precisava acessar o `[[Borderô de Compensação]]` e selecionar manualmente os títulos em aberto para alterar taxas e realizar a baixa, o que gerava um alto custo operacional. Com a nova funcionalidade, o sistema lê o extrato fornecido pela adquirente, localiza os registros correspondentes em `[[Contas a Receber]]` e efetua a baixa em lote, atualizando as taxas originais e movimentando a conta bancária automaticamente.

> [!info] Informação
> Como não existe um padrão de mercado para os extratos (cada administradora utiliza nomenclaturas, estruturas e posições de colunas diferentes), a ferramenta foi desenhada de forma flexível. Ela depende de um mapeamento prévio ("de-para") das colunas da planilha em relação às propriedades internas do sistema.

## Pré-requisitos e Configuração de Layouts

Para que a importação funcione corretamente, é obrigatório mapear a estrutura do arquivo gerado pela adquirente.

**Caminho da Interface:** **Cadastro** > **Outros Financeiros** > **Administradoras de Cartão de Crédito**

Selecione a administradora desejada e acesse a aba **Configuração de Arquivo**. As seguintes parametrizações devem ser realizadas de acordo com o extrato visualizado:

1. **Localização de Dados Estruturais:**
   - **Índice Planilha:** Define qual aba do arquivo de planilha contém os dados reais (ex: `1`).
   - **Linha com os Títulos:** Indica em qual linha da planilha o cabeçalho das colunas está posicionado (ex: na Rede pode ser a linha `2`, na Cielo a linha `5`).

2. **Mapeamento de Colunas (De-Para):**
   É necessário informar exatamente o título da coluna presente no arquivo da administradora para os seguintes dados vitais:
   - `Status` (situação da transação na adquirente).
   - `NSU` (Número Sequencial Único) ou `Código de Autorização`.
   - `Valor Total` (Bruto), `Valor Líquido` e `Valor da Taxa`.
   - `Parcela` (número da parcela atual).
   - `Data da Venda` e `Data do Pagamento`.
   - `Bandeira` (Visa, Master, etc).
   - `Estabelecimento` (Código que identifica a empresa perante a operadora).

3. **Status a Baixar:**
   Define quais literais na coluna de *Status* representam títulos que de fato devem ser liquidados pelo sistema. Isso evita a baixa de transações que constem no arquivo como "Agendadas" ou "Canceladas". Múltiplos valores devem ser separados por ponto e vírgula (`;`). Exemplo: `PAGA;PAGO;BAIXADO`.

4. **Multi-empresa (Mapeamento de Estabelecimentos):**
   Caso o mesmo extrato contenha movimentações de mais de uma empresa (matriz e filiais), o sistema precisa saber como rotear as baixas. Configure a grade de vinculação informando o código do estabelecimento gerado na planilha e associando-o à respectiva Empresa no banco de dados.

Exemplo conceitual do mapeamento gerado no banco de dados após a configuração:

```json
{
  "layout_administradora": "Cielo",
  "configuracoes": {
    "indice_planilha": 1,
    "linha_titulos": 5,
    "status_baixar": ["ENVIADA PARA O BANCO", "PAGO"],
    "colunas_mapeadas": {
      "status": "Status",
      "nsu": "NSU",
      "valor_total": "Valor Bruto",
      "estabelecimento": "Resumo de Vendas"
    }
  }
}



## Regras de Negócio e Sistema de Vinculação

Ao carregar o arquivo, o sistema utiliza uma heurística de busca para vincular a linha processada da planilha com o título pendente no `[[Contas a Receber]]`.

* **Prioridade 1 (Busca Exata):** O sistema tenta validar o código da coluna mapeada como **NSU** (ou Autorização) contra a chave registrada no título a receber.
* **Prioridade 2 (Busca Aproximada):** Caso não encontre o NSU (comum em clientes que utilizam POS manual e não digitam o código na venda), o sistema tenta triangular os dados através de: `Valor da Venda` + `Data de Emissão` + `Número da Parcela`.
* **Prevenção de Falso Positivo:** Se a busca aproximada retornar **mais de um recebimento** válido com os mesmos parâmetros, o vínculo automático é abortado e a linha exige intervenção manual para garantir a lisura da baixa.

> [!tip] Dica de Operação
> O uso de um sistema `[[TEF]]` integrado garante a gravação exata do NSU na venda, resultando em 100% de precisão na conciliação. Para clientes com POS ("maquininha"), recomenda-se habilitar o parâmetro do PDV que abre a tela obrigando o caixa a digitar o NSU ou Número de Autorização impresso no comprovante físico.

## Fluxo de Execução (Passo a Passo)

1. Acesse o módulo financeiro e abra a tela de `[[Borderô de Compensação de Cartão de Crédito]]`.
2. Clique no botão **Incluir** para iniciar um novo lote de baixa.
3. Preencha a **Conta Bancária** destino (onde o montante líquido cairá).
4. Clique no botão **Importar**.
5. Na janela de importação, selecione primeiro a **Administradora de Cartão** pertinente. Esta etapa engatilha a leitura do layout previamente configurado.
6. Clique para abrir e selecionar o arquivo de planilha (fornecido pela administradora).
7. O sistema exibirá uma interface de grade com o processamento da conciliação.
8. Após tratar registros não vinculados (ver seção abaixo), clique em **Confirmar**.
9. Retornando ao borderô principal, confira os totais e clique em **Finalizar**. Neste momento, a transação financeira é efetivada (baixa no Contas a Receber, recálculo de taxas e débito/crédito em Conta Bancária).

## Resolução de Conflitos e Tratamento de Erros

A grade de importação utiliza formatação de cores baseada em status operacionais para orientar a revisão do usuário antes da efetivação:

* 🟢 **Fundo Verde:** Título foi processado e o sistema encontrou o recebimento associado de forma perfeita.
* 🔴 **Fundo Vermelho:** O recebimento não foi localizado no sistema, exigindo intervenção:
* Clique no ícone de **Lupa** no registro correspondente.
* O sistema abrirá uma listagem de títulos a receber já pré-filtrada com a `Data de Emissão` da planilha.
* Identifique manualmente o registro, selecione-o e confirme. A linha deixará de ficar vermelha.


* 🔵 **Fundo Azul:** O título referente àquele NSU já consta como baixado (impendido assim a duplicação do crédito).
* **Status "Outro Estabelecimento":** Registros na planilha que pertencem a uma filial diferente da atual são ignorados nesta importação.

> [!warning] Atenção a Divergências de Valor
> Se o operador vincular um título através da "Lupa" e o sistema detectar que o valor lançado internamente diverge do valor informado na planilha, uma sinalização específica ocorrerá. Se o usuário tentar **Confirmar** a importação neste cenário, o sistema lançará um alerta restritivo: *"Deseja continuar? Você selecionou um recebimento cujo valor não bate"*.

> [!warning] Atenção a Múltiplos Estabelecimentos
> Extratos que englobam matriz e filial requerem que o processo seja executado em duas etapas. Os títulos da Empresa B não serão processados estando o usuário logado na Empresa A. O operador deverá finalizar o lote atual, alterar a empresa de acesso no software, e realizar um novo `[[Borderô de Compensação]]` carregando o mesmo arquivo.

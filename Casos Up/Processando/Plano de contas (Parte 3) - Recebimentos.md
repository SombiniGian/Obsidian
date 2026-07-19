---
id:
  - CASO-205
link: https://www.youtube.com/watch?v=rRxe8S_zPmg
setor:
  - Suporte
  - Financeiro
modulo:
  - Financeiro / Contas a Receber
tags:
  - plano-de-contas
  - baixas
  - juros
  - multas
  - conciliacao-financeira
  - dre
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Baixa de Títulos]]
2. [[#Origem dos Vínculos Contábeis de Mora]]
3. [[#Fluxo de Lançamento: Baixa de Título com Juros e Multa]]
4. [[#Impacto Prático no Saldo por Plano de Contas]]
5. [[#Reflexo e Consolidação no DRE]]
6. [[#Regras de Validação e Pontos Críticos]]

# Visão Geral da Baixa de Títulos
Esta documentação descreve o comportamento automatizado do sistema no momento em que é realizado o **Recebimento/Baixa de Títulos** no módulo de contas a receber. O foco principal é detalhar a engenharia de lançamentos contábeis gerenciais quando o valor pago pelo cliente difere do valor nominal do documento devido à incidência de acréscimos por atraso (**Juros e Multas de Mora**). O sistema realiza a conciliação automática das contas patrimoniais (Ativos) e das contas de resultado (Receitas de Mora).

# Origem dos Vínculos Contábeis de Mora
Para que o sistema consiga direcionar os valores de acréscimo sem gerar inconsistências de conciliação, as contas de receita de mora devem estar previamente mapeadas nas configurações gerais da retaguarda.

*   **Parâmetro de Configuração:** No painel de configuração do [[Plano de Contas]], existem campos específicos denominados **Mora / Juros Receber** e **Multas Receber**.
*   **Contrapartida de Saída (Contas a Pagar):** O sistema possui uma simetria exata para o módulo de contas a pagar, mapeada no campo **Mora / Juros Pagos**, que gerará uma despesa financeira quando a empresa pagar títulos com atraso aos fornecedores.

# Fluxo de Lançamento: Baixa de Título com Juros e Multa
Quando o operador realiza a baixa de um título em atraso recebendo um montante maior que o valor original do direito, o sistema processa três lançamentos gerenciais em segundo plano para manter as partidas dobradas íntegras.

### Cenário Técnico Exemplificado:
*   **Valor Nominal/Original do Documento:** R$ 10,00 (Registrado como Direito no Ativo).
*   **Acréscimo de Juros e Multa por Atraso:** R$ 19,00.
*   **Valor Total Recebido (Dinheiro):** R$ 29,00.

```json
{
  "movimentacao_baixa_com_mora": {
    "titulo_id": 4058,
    "valor_nominal": 10.00,
    "valor_acrescimo": 19.00,
    "valor_total_pago": 29.00,
    "lancamentos": [
      {
        "tipo": "DEBITO",
        "conta_plano": "Ativo / Disponibilidades / Caixa Geral",
        "valor": 29.00,
        "motivo": "Entrada total do recurso financeiro no Caixa"
      },
      {
        "tipo": "CREDITO",
        "conta_plano": "Ativo / Direitos / Contas a Receber",
        "valor": 29.00,
        "motivo": "Crédito totalizado para zerar a ficha financeira da baixa"
      },
      {
        "tipo": "DEBITO",
        "conta_plano": "Ativo / Direitos / Contas a Receber",
        "valor": 19.00,
        "motivo": "Ajuste de débito para neutralizar o crédito excedente do valor nominal"
      },
      {
        "tipo": "CREDITO",
        "conta_plano": "Receitas / Receitas Financeiras / Juros e Multas Recebidos",
        "valor": 19.00,
        "motivo": "Reconhecimento do ganho financeiro por atraso"
      }
    ]
  }
}
Impacto Prático no Saldo por Plano de Contas

A mecânica de débito e crédito descrita no fluxo acima garante que a conta patrimonial de **Contas a Receber** seja baixada exatamente em seu valor de direito original (**R$ 10,00**), mesmo que a movimentação inicial de crédito tenha sido processada pelo valor total do pagamento (**R$ 29,00**).

Ao consultar a tela **Financeiro > Saldo por Plano de Contas**:

1. A conta **Ativo / Disponibilidades / Caixa Geral** apresentará um incremento real de **R$ 29,00**.
    
2. A conta **Ativo / Direitos / Contas a Receber** sofrerá uma redução líquida de apenas **R$ 10,00** (Crédito de R$ 29,00 neutralizado pelo Débito de ajuste de R$ 19,00).
    
3. A conta **Receitas / Receitas Financeiras / Juros e Multas Recebidos** computará o saldo credor de **R$ 19,00**.
    

# Reflexo e Consolidação no DRE

As baixas de títulos com juros sensibilizam diretamente o [[DRE]] da empresa no período selecionado. O valor nominal do título recebido (R$ 10,00) não altera o DRE do mês corrente se a venda original ocorreu em períodos anteriores (regime de competência da receita de venda). No entanto, o valor de **R$ 19,00** referente aos juros é considerado uma receita financeira gerada no ato da liquidação.

- No encerramento do período do DRE, o grupo de **Receitas Financeiras** apresentará o valor acumulado de juros recebidos.
    
- Esse ganho se somará às receitas operacionais de vendas, expandindo o **Resultado Líquido (Lucro)** demonstrado no relatório final de fechamento.
    

# Regras de Validação e Pontos Críticos

> [!warning] Inconsistência de Saldo por Omissão de Parâmetro Se o campo **Mora / Juros Receber** estiver em branco nas tabelas de configuração do sistema, o motor de regras não conseguirá processar o débito de ajuste (R$ 19,00) e o crédito na conta de resultado. Como consequência, a conta de **Contas a Receber** acumulará um crédito indevido de R$ 29,00 para um título que valia R$ 10,00, gerando um saldo negativo artificial de R$ 19,00 nos direitos da empresa e omitindo o ganho financeiro do DRE.

> [!tip] Auditoria de Baixas por Cliente Para certificar-se de que os juros cobrados de um determinado cliente foram alocados corretamente, utilize a tela **Extrato de Plano de Contas**, filtrando especificamente pela conta analítica de `Juros e Multas Recebidos` dentro do período da operação. O sistema gerará a listagem cronológica individualizando os documentos associados aos acréscimos.
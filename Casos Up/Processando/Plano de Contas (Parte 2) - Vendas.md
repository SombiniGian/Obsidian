---
id: [CASO-006]
link: https://www.youtube.com/watch?v=4qNoG5NfTWM
setor: [Suporte, Desenvolvimento, Financeiro]
modulo: [Vendas / Plano de Contas]
tags: [plano-de-contas, faturamento-de-vendas, custo-medio-ponderado, cmv, baixa-de-estoque]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Integração de Vendas]]
2. [[#Hierarquia de Busca das Contas Contábeis]]
3. [[#Fluxo de Lançamento: Venda Mista (À Vista e A Prazo)]]
4. [[#Controle de Estoque e Cálculo do CMV]]
5. [[#Validação de Saldos Gerenciais]]
6. [[#Pontos Críticos e Arquitetura de Software]]

# Visão Geral da Integração de Vendas
Esta documentação detalha o comportamento do sistema UP Sistemas no faturamento de uma venda e o impacto automatizado no [[Plano de Contas]]. Ao concluir uma venda, o sistema realiza múltiplos lançamentos simultâneos: o registro do direito/disponibilidade financeira (Caixa ou Contas a Receber), o registro da receita gerada (Vendas) e a baixa patrimonial da mercadoria com o respectivo reconhecimento do Custo de Mercadoria Vendida (CMV).

# Hierarquia de Busca das Contas Contábeis
Para determinar quais contas analíticas receberão os créditos de receita, o sistema utiliza uma ordem de prioridade estrita na leitura dos parâmetros:

1.  **Espécie de Moeda / Tipo de Documento:** O sistema verifica se a forma de pagamento utilizada (ex: Dinheiro) possui uma conta específica vinculada em seu cadastro (ex: `Vendas no Dinheiro`).
2.  **Cadastro do Cliente:** Caso não encontre na espécie, para vendas a prazo, busca a conta padrão de recebíveis mapeada na aba financeira da pessoa.
3.  **Natureza de Operação:** Se nenhum dos parâmetros anteriores contiver um plano de contas específico, o motor de regras adota a conta padrão de receita configurada na Natureza de Operação da venda.

# Fluxo de Lançamento: Venda Mista (À Vista e A Prazo)
Ao processar uma venda contendo uma parcela à vista (em dinheiro) e uma parcela a prazo, o sistema desmembra os lançamentos gerenciais em tempo real. 

### Cenário Técnico Exemplificado:
*   **Valor Total da Venda:** R$ 50,00
*   **Forma de Pagamento 01:** R$ 20,00 à vista (Dinheiro)
*   **Forma de Pagamento 02:** R$ 30,00 a prazo

```json
{
  "movimentacao_faturamento_venda_mista": {
    "venda_id": 102,
    "valor_total": 50.00,
    "lancamentos_financeiros": [
      {
        "tipo": "DEBITO",
        "conta_plano": "Ativo / Disponibilidades / Caixa Geral",
        "valor": 20.00,
        "motivo": "Entrada de recurso físico no caixa selecionado"
      },
      {
        "tipo": "CREDITO",
        "conta_plano": "Receitas / Vendas / Vendas no Dinheiro",
        "valor": 20.00,
        "motivo": "Reconhecimento de receita à vista"
      },
      {
        "tipo": "DEBITO",
        "conta_plano": "Ativo / Direitos / Contas a Receber",
        "valor": 30.00,
        "motivo": "Geração de título a prazo para o cliente"
      },
      {
        "tipo": "CREDITO",
        "conta_plano": "Receitas / Vendas / Vendas a Prazo",
        "valor": 30.00,
        "motivo": "Reconhecimento de receita a prazo"
      }
    ]
  }
}

# Controle de Estoque e Cálculo do CMV

Paralelamente aos lançamentos de receita e caixa, o sistema executa a baixa patrimonial dos itens vendidos para refletir o custo real da operação (CMV):

- **Débito:** `Resultado / Custos / Custo de Mercadoria Vendida (CMV)`
    
- **Crédito:** `Ativo / Estoque de Mercadoria`
    

> [!info] Mecânica de Valoração (Custo Médio Ponderado) O valor financeiro retirado do estoque e alocado no CMV não corresponde ao preço de venda do produto, mas sim ao seu **Custo Médio Ponderado (CMP)** calculado no momento da última [[Entrada de Estoque]]. No exemplo executado, a saída física dos itens totalizou um custo de **R$ 5,73**, reduzindo o ativo circulante e sensibilizando a margem líquida no [[DRE]].

# Validação de Saldos Gerenciais

Para auditar a consistência da operação no painel gerencial:

1. Acesse o menu **Financeiro > Saldo por Plano de Contas**.
    
2. Desmarque a opção **Mostrar Zerado**.
    
3. Verifique o impacto consolidado das contas:
    
    - **Estoque de Mercadoria:** Reduzido no valor de custo dos produtos (ex: `-R$ 5,73`).
        
    - **Caixa Geral:** Incrementado no valor à vista recebido (ex: `+R$ 20,00`).
        
    - **Contas a Receber:** Incrementado no valor do direito a prazo gerado (ex: `+R$ 30,00`).
        
    - **Custo de Mercadoria Vendida:** Demonstrando o consumo patrimonial (ex: `R$ 5,73`).
        
    - **Receitas com Vendas:** Exibindo os créditos correspondentes nas ramificações de dinheiro e prazo (ex: `R$ 20,00` e `R$ 30,00`).
        

# Pontos Críticos e Arquitetura de Software

> [!warning] Validação Prévia do Caixa Operacional Antes de iniciar as vendas no **PDV**, é mandatório assegurar que a conta corrente ou caixa físico selecionado pelo operador possua a sua respectiva conta de destino parametrizada no [[Plano de Contas]]. A ausência dessa amarração resultará no travamento do faturamento ou na geração de movimentações de receita sem a contrapartida de débito no ativo.

> [!danger] Gargalo de Performance: Gatilho do Custo Médio O cálculo do Custo Médio Ponderado é processado nativamente via **Stored Procedure** no banco de dados. Em cenários de faturamento em lote ou clientes com alto volume de itens por venda, invocar a procedure em tempo real a cada item baixado gera lentidão na aplicação.
> 
> - **Estratégia de Correção de Engenharia:** A arquitetura do sistema deve migrar para um modelo assíncrono ou persistido. O custo médio deve ser calculado e gravado diretamente na tabela de cadastro do produto imediatamente no encerramento da **Entrada de Nota**. No ato da venda, o sistema apenas lê o valor estático pré-gravado, eliminando o processamento em tempo real no PDV.
>
>
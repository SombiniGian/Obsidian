# Tabela TB_CONTA

**Módulo:** Financeiro
Cadastro de contas de caixa e contas bancárias, com regras operacionais do caixa (fechamento cego, obrigatoriedade de abertura, validação de sangria/suprimento, limites e conferência).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CNT_ID` | INTEGER | Não | Identificador único da conta. |
| `CNT_EMPRESA` | INTEGER | Sim | Identificador da empresa à qual a conta pertence. |
| `CNT_DESCRICAO` | VARCHAR(100) | Sim | Descrição/nome da conta (ex.: Caixa Loja 1, Banco do Brasil CC 1234). |
| `CNT_TIPO` | VARCHAR(1) | Sim | Tipo da conta: C = Caixa; B = Bancária. |
| `CNT_OBSERVACAO` | VARCHAR(3000) | Sim | Observações gerais da conta. |
| `CNT_STATUS` | VARCHAR(1) | Sim | Status da conta (A = Ativo, I = Inativo). |
| `CNT_PLANO_CONTAS` | INTEGER | Sim | Identificador do plano de contas contábil associado. |
| `CNT_PADRAO` | VARCHAR(1) | Sim | Indica se é a conta padrão do sistema (S/N). |
| `CNT_OBRIGAR_ABRIR_CAIXA` | VARCHAR(1) | Sim | Obriga abertura de caixa antes de movimentar (S/N). |
| `CNT_FECHAMENTO_CEGAS` | VARCHAR(1) | Sim | Indica se o caixa trabalha com fechamento cego (S/N). |
| `CNT_CAIXA_DESTINO` | INTEGER | Sim | Conta de caixa de destino padrão para suprimentos/transferências. |
| `CNT_VALOR_MAX` | NUMERIC(15,2) | Sim | Valor máximo permitido em caixa. |
| `CNT_VALIDAR_SANGRIA` | VARCHAR(1) | Sim | Valida sangria no fechamento (S/N). |
| `CNT_SUP_SAN_CONTRAPARTIDA` | VARCHAR(1) | Sim | Suprimento/sangria exigem contrapartida (S/N). |
| `CNT_EXPORTAR` | VARCHAR(1) | Sim | Indica se a conta é exportada para integrações (S/N). |
| `CNT_NAO_FECHAR_PEDIDO_ABERTO` | VARCHAR(1) | Sim | Não permite fechar o caixa com pedidos em aberto (S/N). |
| `CNT_SEMPRE_CONFERIR` | VARCHAR(1) | Sim | Sempre exigir conferência do caixa no fechamento (S/N). |
| `CNT_PEDIR_SENHA_SANGRIA` | VARCHAR(1) | Sim | Exige senha de liberação para realizar sangria (S/N). |
| `CNT_PEDIR_SENHA_SUPRIMENTO` | VARCHAR(1) | Sim | Exige senha de liberação para realizar suprimento (S/N). |
| `CNT_OBRIGAR_HISTORICO_SANGRIA` | VARCHAR(1) | Sim | Obriga informar histórico na sangria (S/N). |
| `CNT_LOGOFF_FECHAR` | VARCHAR(1) | Sim | Fecha o caixa automaticamente no logoff (S/N). |

COMMENT ON COLUMN TB_CONTA.CNT_TIPO IS 'C - CAIXA
B - BANCARIA';
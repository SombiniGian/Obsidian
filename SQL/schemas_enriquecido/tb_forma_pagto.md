# Tabela TB_FORMA_PAGTO

**Módulo:** Financeiro / Vendas
Formas de pagamento utilizadas em pedidos, vendas e contas a receber/pagar. Define parcelamento, acréscimo/desconto, taxa de cartão, conta de destino, ajustes, despesas e se gera boleto automático.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `FPG_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `FPG_ID` | INTEGER | Não | Identificador único da forma de pagamento. |
| `FPG_DESCRICAO` | VARCHAR(100) | Sim | Descrição da forma de pagamento (ex.: À Vista, Cartão Crédito 3x, Boleto 30 dias). |
| `FPG_DESCRICAO_RESUMIDA` | VARCHAR(100) | Sim | Descrição curta para impressão em NFC-e/DANFE. |
| `FPG_NR_PARCELAS` | INTEGER | Sim | Número padrão de parcelas. |
| `FPG_ACRES_DESC` | VARCHAR(1) | Sim | Tipo de acréscimo/desconto aplicado (A = Acréscimo, D = Desconto). |
| `FPG_VALOR_ACRES_DESC` | NUMERIC(15,2) | Sim | Percentual/valor do acréscimo ou desconto. |
| `FPG_STATUS` | VARCHAR(1) | Sim | Status da forma de pagamento (A = Ativo, I = Inativo). |
| `FPG_ENTRADA` | VARCHAR(1) | Sim | Indica se exige valor de entrada (S/N). |
| `FPG_ESPECIE_MOEDA` | INTEGER | Sim | FK para TB_ESPECIE_MOEDA.ESP_ID — espécie de moeda padrão. |
| `FPG_TAXA_CARTAO` | NUMERIC(15,2) | Sim | Taxa (%) paga à operadora do cartão. |
| `FPG_AJUSTAR` | VARCHAR(1) | Sim | Permite ajustar valor da venda no faturamento (S/N). |
| `FPG_APLICAR_ACRES_DESC` | VARCHAR(1) | Sim | Aplica acréscimo/desconto automaticamente (S/N). |
| `FPG_EXPORTAR` | VARCHAR(1) | Sim | Indica se a forma de pagamento é exportada para o tablet (S/N). |
| `FPG_VALOR_MINIMO` | NUMERIC(15,2) | Sim | Valor mínimo para uso desta forma de pagamento. |
| `FPG_NOTA_FISCAL` | VARCHAR(1) | Sim | Indica se a venda à vista/a prazo para a NF-e (V = À Vista, P = A Prazo, O = Outros). |
| `FPG_AJUSTE` | NUMERIC(15,2) | Sim | Valor de ajuste fixo configurado. |
| `FPG_APLICAR_DESPESA` | VARCHAR(1) | Sim | Aplica despesa adicional (S/N). |
| `FPG_VALOR_DESPESA` | NUMERIC(15,2) | Sim | Valor/percentual da despesa adicional. |
| `FPG_VALOR_PEDIDO_DESPESA` | NUMERIC(15,2) | Sim | Valor de pedido mínimo para aplicação da despesa. |
| `FPG_CONTA` | INTEGER | Sim | FK para TB_CONTA.CNT_ID — conta destino padrão. |
| `FPG_AGRUPAR_RECEBIMENTOS` | VARCHAR(1) | Sim | Indica se os recebimentos desta forma devem ser agrupados em um único título (S/N). |
| `FPG_NAO_GERAR_FINAL_SEMANA` | VARCHAR(1) | Sim | Não gera título com vencimento em final de semana (S/N). |
| `FPG_EMITIR_BOLETO_AUTOMATICO` | VARCHAR(1) | Sim | Indica se emite boleto automaticamente ao gerar o recebimento (S/N). |

COMMENT ON COLUMN TB_FORMA_PAGTO.FPG_ACRES_DESC IS 'A = Acréscimo
D = Desconto';
COMMENT ON COLUMN TB_FORMA_PAGTO.FPG_NOTA_FISCAL IS 'V - A VISTA
P - A PRAZO
O - OUTROS';

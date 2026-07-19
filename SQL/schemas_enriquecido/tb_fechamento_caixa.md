# Tabela TB_FECHAMENTO_CAIXA

**Módulo:** Financeiro
Registro de abertura e fechamento do caixa (PDV). Consolida totais de venda, desconto, brinde, cancelamento, sangria, suprimento, débitos, créditos e troco pardoado; também guarda dados de turno, conferência e vínculo com borderô.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `FCX_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `FCX_ID` | INTEGER | Não | Identificador único do fechamento. Parte da chave primária composta. |
| `FCX_CAIXA` | INTEGER | Sim | FK para TB_CONTA.CNT_ID — caixa que foi aberto/fechado. |
| `FCX_USU_ABERTURA` | INTEGER | Sim | FK para TB_USUARIO.USU_ID — usuário que abriu o caixa. |
| `FCX_USU_FECHAMENTO` | INTEGER | Sim | FK para TB_USUARIO.USU_ID — usuário que fechou o caixa. |
| `FCX_DT_ABERTURA` | TIMESTAMP | Sim | Data e hora de abertura do caixa. |
| `FCX_DT_FECHAMENTO` | TIMESTAMP | Sim | Data e hora de fechamento do caixa. |
| `FCX_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro. |
| `FCX_STATUS` | VARCHAR(1) | Sim | Status do fechamento (A=Aberto, F=Fechado, C=Cancelado). |
| `FCX_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total apurado no caixa. |
| `FCX_VALOR_CAIXA` | NUMERIC(15,2) | Sim | Valor em caixa (soma de movimentações). |
| `FCX_VALOR_DIFERENCA` | NUMERIC(15,2) | Sim | Diferença entre valor apurado e valor esperado (quebra de caixa). |
| `FCX_CAIXA_DESTINO` | INTEGER | Sim | Caixa de destino das transferências (suprimento/sangria). |
| `FCX_VALOR_VENDA` | NUMERIC(15,2) | Sim | Soma do valor das vendas do caixa. |
| `FCX_QTDE_VENDA` | INTEGER | Sim | Quantidade de vendas realizadas. |
| `FCX_VALOR_DESCONTO` | NUMERIC(15,2) | Sim | Soma dos descontos concedidos. |
| `FCX_QTDE_DESCONTO` | INTEGER | Sim | Quantidade de descontos. |
| `FCX_VALOR_BRINDE` | NUMERIC(15,2) | Sim | Soma dos valores de brindes. |
| `FCX_QTDE_BRINDE` | INTEGER | Sim | Quantidade de brindes. |
| `FCX_VALOR_CANCELADOS` | NUMERIC(15,2) | Sim | Soma do valor de pedidos cancelados. |
| `FCX_QTDE_CANCELADOS` | INTEGER | Sim | Quantidade de pedidos cancelados. |
| `FCX_VALOR_SANGRIA` | NUMERIC(15,2) | Sim | Soma das saídas por sangria. |
| `FCX_QTDE_SANGRIA` | INTEGER | Sim | Quantidade de sangrias. |
| `FCX_VALOR_SUPRIMENTO` | NUMERIC(15,2) | Sim | Soma das entradas por suprimento. |
| `FCX_QTDE_SUPRIMENTO` | INTEGER | Sim | Quantidade de suprimentos. |
| `FCX_VALOR_DEBITO` | NUMERIC(15,2) | Sim | Soma dos débitos do caixa. |
| `FCX_VALOR_CREDITO` | NUMERIC(15,2) | Sim | Soma dos créditos do caixa. |
| `FCX_USU_CONFERENCIA` | INTEGER | Sim | Usuário que realizou a conferência cega. |
| `FCX_DT_CONFERENCIA` | TIMESTAMP | Sim | Data e hora da conferência. |
| `FCX_RECEBIMENTO` | INTEGER | Sim | Identificador do borderô de recebimento relacionado. |
| `FCX_PAGAMENTO` | INTEGER | Sim | Identificador do borderô de pagamento relacionado. |
| `FCX_VALOR_TROCO` | NUMERIC(15,2) | Sim | Soma dos trocos pagos no caixa. |
| `FCX_TURNO` | INTEGER | Sim | Identificador do turno. |
| `FCX_TROCO_PERDOADO` | NUMERIC(15,2) | Sim | Valor de troco perdoado/descartado pelo operador. |
| `FCX_VALOR_PRAZO` | NUMERIC(15,2) | Sim | Total de vendas a prazo. |
| `FCX_VALOR_BANC` | NUMERIC(15,2) | Sim | Total recebido em cartão/banco. |
| `FCX_GUID` | VARCHAR(50) | Sim | GUID para integração. |
| `FCX_ID_LOCAL` | INTEGER | Sim | FK para TB_LOCAL. |
| `FCX_ID_SERVIDOR` | INTEGER | Sim | FK para TB_SERVIDOR. |
| `FCX_ORIGEM` | VARCHAR(10) | Sim | Origem do fechamento (sigla da rotina). |
| `FCX_VENDEDOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (vendedor). |
| `FCX_OBSERVACAO` | VARCHAR(1000) | Sim | Observações do fechamento. |

COMMENT ON COLUMN TB_FECHAMENTO_CAIXA.FCX_CAIXA IS 'FK para TB_CONTA.CNT_ID';
COMMENT ON COLUMN TB_FECHAMENTO_CAIXA.FCX_USU_ABERTURA IS 'FK para TB_USUARIO.USU_ID';
COMMENT ON COLUMN TB_FECHAMENTO_CAIXA.FCX_USU_FECHAMENTO IS 'FK para TB_USUARIO.USU_ID';
COMMENT ON COLUMN TB_FECHAMENTO_CAIXA.FCX_VALOR_DIFERENCA IS 'Quando positivo, sobra de caixa; quando negativo, falta (quebra de caixa). Compare com FCX_VALOR_CAIXA para auditoria.';

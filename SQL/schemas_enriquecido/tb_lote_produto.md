# Tabela TB_LOTE_PRODUTO

**Módulo:** Estoque / Rastreabilidade
Tabela de lotes de produtos para controle de rastreabilidade, validade e quarentena. Cada lote pertence a um produto, empresa e fornecedor, com origem (compra, produção, ajuste) e quantidade em estoque. Suporta controle de quarentena (período em que o lote fica bloqueado antes de liberação). As movimentações por lote ficam em TB_LOTE_PROD_MOV.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `LOT_ID` | INTEGER | Não | Identificador único do lote. |
| `LOT_EMPRESA` | INTEGER | Não | Identificador da empresa. |
| `LOT_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO. Use JOIN por PROD_ID. |
| `LOT_FORNECEDOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID do fornecedor (use WHERE PES_FORNECEDOR = 'S'). |
| `LOT_ORIGEM` | VARCHAR(10) | Sim | Sigla do módulo/rotina de origem do lote (ex.: COMPRA, PRODUCAO, AJUSTE). |
| `LOT_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem. |
| `LOT_USUARIO` | INTEGER | Sim | Identificador do usuário que lançou o lote. |
| `LOT_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do lote no sistema. |
| `LOT_STATUS` | VARCHAR(1) | Sim | Status do lote (A=Ativo, Q=Quarentena, B=Bloqueado, C=Cancelado). |
| `LOT_QTDE_ESTOQUE` | NUMERIC(15,2) | Sim | Quantidade atual em estoque deste lote. |
| `LOT_LOTE` | VARCHAR(50) | Não | Código/descrição do lote. |
| `LOT_VALIDADE` | DATE | Sim | Data de validade do lote. |
| `LOT_QUARENTENA_ATE` | DATE | Sim | Data até a qual o lote permanece em quarentena. |
| `LOT_QUARENTENA_LIBERADA` | TIMESTAMP | Sim | Data e hora em que a quarentena foi liberada. |
| `LOT_QUARENTENA_LIBERADA_USU` | INTEGER | Sim | FK para TB_USUARIO que liberou a quarentena. |
| `LOT_SERIE_CANO` | VARCHAR(15) | Sim | Série/cano (usado em controle de armas/munições). |
| `LOT_ID_CHASSI` | INTEGER | Sim | Identificador de chassi (veículos) vinculado ao lote. |

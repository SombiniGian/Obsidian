# Tabela TB_ALMOXARIFADO

**Módulo:** Estoque / Movimentações
Tabela de movimentações internas de estoque entre locais (transferências, consumo interno, requisições de almoxarifado). Permite enviar produtos de um local de estoque de origem para outro destino, com tabela de preço aplicada, situação e integração com nota fiscal.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `ALM_ID` | INTEGER | Não | Identificador único do movimento de almoxarifado. |
| `ALM_STATUS` | VARCHAR(1) | Sim | Status do movimento (A=Ativo, C=Cancelado). |
| `ALM_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento do registro no sistema. |
| `ALM_DT_EMISSAO` | DATE | Sim | Data de emissão do movimento. |
| `ALM_USUARIO` | INTEGER | Sim | Identificador do usuário que lançou o movimento. |
| `ALM_EMP_ORIGEM` | INTEGER | Sim | Identificador da empresa de origem do movimento. |
| `ALM_TIPO_PRECO` | VARCHAR(1) | Sim | Tipo de preço aplicado (C=Compra, V=Venda). |
| `ALM_VALOR_TOTAL` | NUMERIC(15,2) | Sim | Valor total do movimento de almoxarifado. |
| `ALM_OBSERVACAO` | VARCHAR(1000) | Sim | Observações gerais do movimento. |
| `ALM_TABELA_PRECO` | INTEGER | Sim | FK para TB_TABELA_PRECO aplicada ao movimento. |
| `ALM_TIPO_TABELA_PRECO` | VARCHAR(1) | Sim | Tipo da tabela de preço (A=Acrescimo, D=Desconto). |
| `ALM_TABELA_DESC_ACRES` | NUMERIC(15,2) | Sim | Percentual/valor de desconto ou acréscimo aplicado. |
| `ALM_LOCAL_ORIGEM` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE.LOC_ID de origem. |
| `ALM_SITUACAO` | INTEGER | Sim | FK para TB_ALMOXARIFADO_SIT. Situação do movimento. |
| `ALM_NOTA_FISCAL` | INTEGER | Sim | FK para TB_NOTA_FISCAL vinculada ao movimento. |
| `ALM_GEROU_ESTOQUE` | VARCHAR(1) | Sim | Indica se o movimento gerou movimento de estoque (S/N). |

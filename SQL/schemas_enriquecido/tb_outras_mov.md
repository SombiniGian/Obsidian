# Tabela TB_OUTRAS_MOV

**Módulo:** Estoque / Movimentações
Tabela de cabeçalho de "outras movimentações" de estoque (entradas/saídas avulsas, ajustes, transferências manuais). Controla tipo, valores de entrada/saída, pessoa vinculada, local de estoque e parâmetros de comportamento (movimenta estoque/NF, percentual do estoque atual).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `OMP_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `OMP_ID` | INTEGER | Não | Identificador único da movimentação. Parte da chave primária composta. |
| `OMP_USUARIO` | INTEGER | Sim | FK para TB_USUARIO que lançou a movimentação. |
| `OMP_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de gravação do registro. |
| `OMP_DT_EMISSAO` | DATE | Sim | Data de emissão da movimentação. |
| `OMP_TIPO_OUT` | INTEGER | Sim | FK para TB_TIPO_OUTRAS_MOV. Tipo da movimentação. |
| `OMP_VALOR_ENTRADA` | NUMERIC(15,2) | Sim | Valor total de entrada. |
| `OMP_VALOR_SAIDA` | NUMERIC(15,2) | Sim | Valor total de saída. |
| `OMP_VALOR_DIFERENCA` | NUMERIC(15,2) | Sim | Diferença (entrada - saída). |
| `OMP_STATUS` | VARCHAR(1) | Sim | Status da movimentação (A=Aberta, F=Fechada, C=Cancelada). |
| `OMP_PESSOA` | INTEGER | Sim | FK para TB_PESSOA vinculada à movimentação. |
| `OMP_OBSERVACAO` | VARCHAR(1000) | Sim | Observações da movimentação. |
| `OMP_MOV_PADRAO` | VARCHAR(1) | Sim | Indica se é o tipo padrão (S/N). |
| `OMP_MOV_ESTOQUE_NF` | VARCHAR(1) | Sim | Indica se movimenta estoque com nota fiscal (S/N). |
| `OMP_MOV_ESTOQUE` | VARCHAR(1) | Sim | Indica se movimenta estoque (S/N). |
| `OMP_VINCULAR_PESSOA` | VARCHAR(1) | Sim | Indica se exige vinculação de pessoa (S/N). |
| `OMP_PERCENTUAL_EST_ATUAL` | NUMERIC(15,2) | Sim | Percentual aplicado sobre o estoque atual. |
| `OMP_LOCAL_ESTOQUE` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE.LOC_ID. Local de estoque da movimentação. |
| `OMP_NOTA_FISCAL` | INTEGER | Sim | FK para TB_NOTA_FISCAL vinculada, quando aplicável. |
# Tabela TB_TIPO_OUTRAS_MOV

**Módulo:** Estoque / Movimentações
Cadastro de tipos para "outras movimentações" de estoque. Define se o tipo movimenta estoque, se exige NF, se exige vinculação de pessoa, percentual sobre estoque atual, status e flags de tipo principal/preço.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TPM_ID` | INTEGER | Não | Identificador único do tipo de outras movimentações. |
| `TPM_EMPRESA` | INTEGER | Sim | Identificador da empresa à qual o tipo pertence. |
| `TPM_DESCRICAO` | VARCHAR(100) | Sim | Descrição do tipo de movimentação. |
| `TBM_MOV_PADRAO` | VARCHAR(1) | Sim | Indica se é o tipo padrão (S/N). |
| `TBM_MOV_ESTOQUE` | VARCHAR(1) | Sim | Indica se movimenta estoque (S/N). |
| `TBM_MOV_ESTOQUE_NF` | VARCHAR(1) | Sim | Indica se movimenta estoque com nota fiscal (S/N). |
| `TBM_VINCULAR_PESSOA` | VARCHAR(1) | Sim | Indica se exige vinculação de pessoa (S/N). |
| `TBM_PERCENTUAL_EST_ATUAL` | NUMERIC(15,2) | Sim | Percentual aplicado sobre o estoque atual. |
| `TBM_STATUS` | VARCHAR(1) | Sim | Status do tipo (A=Ativo, I=Inativo). |
| `TBM_PRINCIPAL` | VARCHAR(1) | Sim | Indica se é o tipo principal (S/N). |
| `TBM_TIPO_PRECO` | VARCHAR(1) | Sim | Tipo de preço aplicado (C=Compra, V=Venda, A=Custo Médio). |
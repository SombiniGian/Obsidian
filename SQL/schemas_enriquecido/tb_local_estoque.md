# Tabela TB_LOCAL_ESTOQUE

**Módulo:** Estoque / Cadastros
Cadastro de locais de estoque (lojas, depósitos, filiais). Permite indicar o local principal, status, e o proprietário do estoque (empresa dona ou terceiros), sendo referenciado por tabelas de movimento de produto, notas fiscais, pedidos e devoluções.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `LOC_ID` | INTEGER | Não | Identificador único do local de estoque. |
| `LOC_EMPRESA` | INTEGER | Sim | Identificador da empresa à qual o local pertence. |
| `LOC_DESCRICAO` | VARCHAR(100) | Sim | Descrição do local de estoque (ex.: Loja 01, Depósito Central, Filial SP). |
| `LOC_STATUS` | VARCHAR(1) | Sim | Status do local (A=Ativo, I=Inativo). |
| `LOC_PRINCIPAL` | VARCHAR(1) | Sim | Indica se é o local principal de estoque (S/N). Apenas um local por empresa deve estar marcado. |
| `LOC_INDICACAO_PROPRIETARIO` | VARCHAR(3) | Sim | Indicação do proprietário do estoque (PRO=Próprio, TER=Terceiro). |
| `LOC_PESSOA_PROPRIETARIO` | INTEGER | Sim | FK para TB_PESSOA.PES_ID — pessoa proprietária do estoque (em caso de terceiros). |

COMMENT ON COLUMN TB_LOCAL_ESTOQUE.LOC_ID IS 'Chave primária. É referenciada por TB_PRODUTO_MOVIMENTO.PRDM_LOCAL, TB_NOTA_FISCAL_ITEM, TB_DEVOLUCAO.DEV_LOCAL_ESTOQUE, TB_NATUREZA_OPERACAO.NOP_LOCAL_ESTOQUE, TB_VENDEDOR.VDR_LOCAL_ESTOQUE etc.';
COMMENT ON COLUMN TB_LOCAL_ESTOQUE.LOC_STATUS IS 'A - ATIVO
I - INATIVO';
COMMENT ON COLUMN TB_LOCAL_ESTOQUE.LOC_PRINCIPAL IS 'S - SIM (local padrão para movimentos sem local explícito)
N - NAO';
COMMENT ON COLUMN TB_LOCAL_ESTOQUE.LOC_INDICACAO_PROPRIETARIO IS 'PRO - PROPRIO
TER - TERCEIRO';

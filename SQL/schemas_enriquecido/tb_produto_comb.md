# Tabela TB_PRODUTO_COMB

**Módulo:** Fiscal / Combustíveis
Dados fiscais específicos de produtos do tipo combustível (vinculados a TB_PRODUTO). Armazena código ANP, percentuais de composição (GLP, gasolina, biodiesel), CFOPs de venda/interestadual/entrada e quantidade tributável para emissão de NF-e de combustíveis.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRDC_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID — produto combustível. Parte da chave primária. |
| `PRDC_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `PRDC_ANP` | INTEGER | Sim | Código ANP (Agência Nacional do Petróleo) do combustível. |
| `PRDC_DESC_ANP` | VARCHAR(100) | Sim | Descrição do combustível conforme tabela ANP. |
| `PRDC_PGLP` | NUMERIC(15,4) | Sim | Percentual de GLP na composição do combustível. |
| `PRDC_PGNN` | NUMERIC(15,4) | Sim | Percentual de gasolina na composição do combustível. |
| `PRDC_PGNI` | NUMERIC(15,4) | Sim | Percentual de gasolina importada na composição do combustível. |
| `PRDC_CFOP` | VARCHAR(4) | Sim | CFOP de venda do combustível (operação estadual). |
| `PRDC_PESO_LIQ` | NUMERIC(15,4) | Sim | Peso líquido do combustível. |
| `PRDC_CFOP_INTER` | VARCHAR(4) | Sim | CFOP de venda para operação interestadual. |
| `PRDC_QTDE_TRIB` | NUMERIC(15,6) | Sim | Quantidade tributável do combustível. |
| `PRDC_UN_TRIB` | VARCHAR(6) | Sim | Unidade de medida tributável (ex.: L, KG, M3). |
| `PRDC_CFOP_ENT` | VARCHAR(4) | Sim | CFOP de entrada do combustível (operação estadual). |
| `PRDC_CFOP_INTER_ENT` | VARCHAR(4) | Sim | CFOP de entrada do combustível para operação interestadual. |
| `PRDC_PERC_BIODISEL` | NUMERIC(15,4) | Sim | Percentual de biodiesel presente no combustível. |

COMMENT ON COLUMN TB_PRODUTO_COMB.PRDC_PRODUTO IS 'FK para TB_PRODUTO.PRD_ID — use JOIN com TB_PRODUTO para obter descrição e dados básicos do combustível.';

# Tabela TB_FORNECEDOR

**Módulo:** Cadastros / Compras
Dados complementares do fornecedor vinculados a TB_PESSOA.PES_ID. Contém regime tributário, mensagens de alerta, observação e alíquota de FUNRURAL.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `FOR_PESSOA` | INTEGER | Não | FK para TB_PESSOA.PES_ID. Parte da chave primária composta. Use SEMPRE por PES_ID. |
| `FOR_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `FOR_EMAIL_COMPRA` | VARCHAR(50) | Sim | E-mail do setor de compras do fornecedor. |
| `FOR_OBSERVACAO` | VARCHAR(2000) | Sim | Observações gerais do fornecedor. |
| `FOR_DT_CADASTRO` | DATE | Sim | Data de cadastro do fornecedor. |
| `FOR_MSG_ALERTA` | VARCHAR(2000) | Sim | Mensagem de alerta exibida ao lançar pedido/compra com este fornecedor. |
| `FOR_REGIME` | VARCHAR(1) | Sim | Regime tributário do fornecedor (1=Real, 2=Presumido, 3=Simples Nacional). |
| `FOR_EXPORTADOR` | VARCHAR(60) | Sim | Nome/razão social do exportador (importação). |
| `FOR_COD_FABRICANTE` | VARCHAR(60) | Sim | Código do fabricante (integração). |
| `FOR_ALIQUOTA_FUNRURAL` | NUMERIC(15,6) | Sim | Alíquota de retenção do FUNRURAL aplicada nas compras. |

COMMENT ON COLUMN TB_FORNECEDOR.FOR_PESSOA IS 'FK para TB_PESSOA.PES_ID — SEMPRE faça JOIN com TB_PESSOA por PES_ID. Para filtrar fornecedores utilize WHERE PES_FORNECEDOR = ''S'' em TB_PESSOA.';
COMMENT ON COLUMN TB_FORNECEDOR.FOR_REGIME IS '1 - REAL
2 - PRESUMIDO
3 - SIMPLES NACIONAL';
COMMENT ON COLUMN TB_FORNECEDOR.FOR_ALIQUOTA_FUNRURAL IS 'Alíquota de retenção de FUNRURAL aplicada nas compras deste fornecedor.';

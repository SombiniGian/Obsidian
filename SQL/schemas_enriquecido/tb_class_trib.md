# Tabela TB_CLASS_TRIB

**Módulo:** Fiscal / Reforma Tributária
Cadastro da Classificação Tributária (cClassTrib) utilizada na NF-e/NFC-e/CT-e/NFS-e para indicar o regime de tributação do IBS/CBS, com percentuais de redução, CST e indicadores para cada tipo de documento.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CTRB_CODIGO` | VARCHAR(20) | Não | Código da classificação tributária. |
| `CTRB_DESCRICAO` | VARCHAR(1000) | Sim | Descrição da classificação. |
| `CTRB_PERC_REDUCAO_IBS` | NUMERIC(15,2) | Sim | Percentual de redução de IBS. |
| `CTRB_PERC_REDUCAO_CBS` | NUMERIC(15,2) | Sim | Percentual de redução de CBS. |
| `CTRB_REDUCAO_BC` | VARCHAR(1) | Sim | Indica se há redução de base de cálculo (S/N). |
| `CTRB_TRIBUTACAO_REGULAR` | VARCHAR(1) | Sim | Indica se é tributação regular (S/N). |
| `CTRB_CREDITO_PRESUMIDO` | VARCHAR(1) | Sim | Indica se admite crédito presumido (S/N). |
| `CTRB_CST` | VARCHAR(10) | Não | Código CST vinculado à classificação. |
| `CTRB_STATUS` | VARCHAR(1) | Sim | Status da classificação (A=Ativo, I=Inativo). |
| `CTRB_ESTORNO_CREDITO` | VARCHAR(1) | Sim | Indica se há estorno de crédito (S/N). |
| `CTRB_NFE` | VARCHAR(1) | Sim | Disponível para NF-e (S/N). |
| `CTRB_NFCE` | VARCHAR(1) | Sim | Disponível para NFC-e (S/N). |
| `CTRB_CTE` | VARCHAR(1) | Sim | Disponível para CT-e (S/N). |
| `CTRB_CTE_OS` | VARCHAR(1) | Sim | Disponível para CT-e de OS (S/N). |
| `CTRB_NF3E` | VARCHAR(1) | Sim | Disponível para NF3e (S/N). |
| `CTRB_BPE` | VARCHAR(1) | Sim | Disponível para BP-e (S/N). |
| `CTRB_NFCOM` | VARCHAR(1) | Sim | Disponível para NFCom (S/N). |
| `CTRB_NFSE` | VARCHAR(1) | Sim | Disponível para NFS-e (S/N). |
| `CTRB_BPE_TM` | VARCHAR(1) | Sim | Disponível para BP-e TM (S/N). |
| `CTRB_BPE_TA` | VARCHAR(1) | Sim | Disponível para BP-e TA (S/N). |
| `CTRB_NFAG` | VARCHAR(1) | Sim | Disponível para NFAg (S/N). |
| `CTRB_NFSVIA` | VARCHAR(1) | Sim | Disponível para NFSvia (S/N). |
| `CTRB_NFABI` | VARCHAR(1) | Sim | Disponível para NFAbi (S/N). |
| `CTRB_NFGAS` | VARCHAR(1) | Sim | Disponível para NFGas (S/N). |
| `CTRB_DERE` | VARCHAR(1) | Sim | Disponível para DERE (S/N). |
| `CTRB_LEGISLACAO` | VARCHAR(200) | Sim | Legislação aplicável. |
| `CTRB_ANEXO` | VARCHAR(10) | Sim | Anexo/regime relacionado. |
| `CTRB_LISTA_NCM` | BLOB SUB_TYPE TEXT | Sim | Lista de NCMs vinculados à classificação. |

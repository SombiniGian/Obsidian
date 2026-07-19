# Tabela TB_PRODUTO_SERVICO

**Módulo:** Fiscal / NFS-e
Dados fiscais de serviços vinculados ao produto (TB_PRODUTO.PRD_ID). Define códigos da LC 116, código municipal, NBS, CNAE, alíquotas e indicadores de retenção (ISS, PIS, COFINS, CSLL, IR, INSS) utilizados na emissão de NFS-e.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRDS_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID. Parte da chave primária composta. |
| `PRDS_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PRDS_COD_NACIONAL` | VARCHAR(10) | Sim | Código nacional do serviço (LC 116). |
| `PRDS_COD_MUNICIPAL` | VARCHAR(10) | Sim | Código municipal do serviço. |
| `PRDS_NBS` | VARCHAR(10) | Sim | Código NBS (Nomenclatura Brasileira de Serviços). |
| `PRDS_CNAE` | VARCHAR(10) | Sim | Código CNAE da atividade. |
| `PRDS_RESP_RETENCAO` | INTEGER | Sim | Responsável pela retenção do ISS (1=Tomador, 2=Intermediário). |
| `PRDS_EXIGENCIA_ISS` | INTEGER | Sim | Exigibilidade do ISS (1=Exigível, 2=Não incidência, 3=Isenção, 4=Exportação, 5=Imunidade, 6/7=Exigibilidade suspensa). |
| `PRDS_NR_PROCESSO` | VARCHAR(30) | Sim | Número do processo judicial/administrativo. |
| `PRDS_ALIQ_ISS` | NUMERIC(18,4) | Sim | Alíquota do ISS. |
| `PRDS_ISS_RETIDO` | VARCHAR(1) | Sim | Indica se o ISS é retido (S/N). |
| `PRDS_ALIQ_PIS` | NUMERIC(15,2) | Sim | Alíquota do PIS. |
| `PRDS_PIS_RETIDO` | VARCHAR(1) | Sim | Indica se o PIS é retido (S/N). |
| `PRDS_ALIQ_COFINS` | NUMERIC(15,2) | Sim | Alíquota do COFINS. |
| `PRDS_COFINS_RETIDO` | VARCHAR(1) | Sim | Indica se o COFINS é retido (S/N). |
| `PRDS_ALIQ_CSLL` | NUMERIC(15,2) | Sim | Alíquota da CSLL. |
| `PRDS_CSLL_RETIDO` | VARCHAR(1) | Sim | Indica se a CSLL é retida (S/N). |
| `PRDS_ALIQ_IR` | NUMERIC(15,2) | Sim | Alíquota do IR. |
| `PRDS_IR_RETIDO` | VARCHAR(1) | Sim | Indica se o IR é retido (S/N). |
| `PRDS_ALIQ_INSS` | NUMERIC(15,2) | Sim | Alíquota do INSS. |
| `PRDS_INSS_RETIDO` | VARCHAR(1) | Sim | Indica se o INSS é retido (S/N). |
| `PRDS_INCENTIVADOR_CULTURAL` | VARCHAR(1) | Sim | Indica se é incentivador cultural (S/N). |
| `PRDS_CST_PIS_COFINS` | VARCHAR(2) | Sim | CST de PIS/COFINS. |
| `PRDS_COD_SIT_TRIB` | VARCHAR(1) | Sim | Código da situação tributária do ISS. |
| `PRDS_ALIQ_DEDUCAO` | NUMERIC(15,4) | Sim | Percentual de dedução aplicado sobre a base do ISS. |
| `PRDS_TIPO_MARCADOR` | VARCHAR(1) | Sim | Tipo do marcador (ex.: M = Marca, T = Tag). |
| `PRDS_CALCULA_AUT_MARCADOR` | VARCHAR(1) | Sim | Calcula automaticamente o total do marcador (S/N). |
| `PRDS_OBRIGA_CODIGO_MARCADOR` | VARCHAR(1) | Sim | Obriga informar o código do marcador (S/N). |

# Tabela TB_CONHEC_TRANSP_NUMERO

**Módulo:** Fiscal / Conhecimento de Transporte
Tabela de controle de numeração dos conhecimentos de transporte (CT-e). Armazena a sequência numérica por modelo, série e ambiente (Produção/Homologação) por empresa.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CTN_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `CTN_CONHEC_TRANSP` | INTEGER | Sim | FK para TB_CONHECIMENTO_TRANSP. Conhecimento relacionado. |
| `CTN_MODELO` | VARCHAR(2) | Não | Modelo do documento fiscal (ex.: 57=CT-e). Parte da chave primária composta. |
| `CTN_SERIE` | INTEGER | Não | Série do conhecimento. Parte da chave primária composta. |
| `CTN_NUMERO` | INTEGER | Não | Número sequencial do conhecimento. Parte da chave primária composta. |
| `CTN_AMBIENTE` | INTEGER | Sim | Ambiente de emissão (1=Produção, 2=Homologação). |
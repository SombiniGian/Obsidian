# Tabela TB_MANIFESTO_TRANSPORTADOR

**Módulo:** Fiscal / Manifesto Eletrônico
Tabela de transportadores vinculados a um manifesto eletrônico (MDF-e). Permite informar mais de um transportador por manifesto com nome e CPF.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `MET_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `MET_MANIFESTO` | INTEGER | Não | FK para TB_MANIFESTO_ELETRONICO. Identificador do manifesto. Parte da chave primária composta. |
| `MET_SEQUENCIA` | INTEGER | Não | Sequencial do transportador dentro do manifesto. Parte da chave primária composta. |
| `MET_TRANSPORTADOR` | INTEGER | Sim | FK para TB_PESSOA (PES_TRANSPORTADOR=S). Transportador vinculado. |
| `MET_NOME_TRANSP` | VARCHAR(60) | Sim | Nome do transportador (para transportador avulso, sem cadastro). |
| `MET_CPF` | VARCHAR(11) | Sim | CPF do transportador (somente números). |
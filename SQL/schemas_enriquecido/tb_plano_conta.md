# Tabela TB_PLANO_CONTA

**Módulo:** Contábil / Financeiro
Plano de contas contábil da empresa (estrutura hierárquica de até 3 níveis). É referenciado por praticamente todas as tabelas financeiras, fiscais e de estoque, indicando a classificação da conta de débito/crédito.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PLC_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `PLC_ID` | INTEGER | Não | Identificador único da conta. Parte da chave primária composta. |
| `PLC_CODIGO` | VARCHAR(30) | Sim | Código da conta (ex.: 1.01.001). |
| `PLC_PAI` | VARCHAR(30) | Sim | Código da conta pai (nível superior) no plano de contas. |
| `PLC_NIVEL_1` | INTEGER | Sim | Código do nível 1 (grupo). |
| `PLC_NIVEL_2` | INTEGER | Sim | Código do nível 2 (subgrupo). |
| `PLC_NIVEL_3` | INTEGER | Sim | Código do nível 3 (conta analítica). |
| `PLC_DESCRICAO` | VARCHAR(80) | Sim | Descrição da conta. |
| `PLC_TIPO_CONTA` | VARCHAR(1) | Sim | Tipo da conta (C = Crédito, D = Débito, A = Ativo/Passivo). |
| `PLC_USUARIO` | INTEGER | Sim | FK para TB_USUARIO — usuário que cadastrou. |
| `PLC_DT_CADASTRO` | TIMESTAMP | Sim | Data de cadastro da conta. |
| `PLC_STATUS` | VARCHAR(1) | Sim | Status da conta (A = Ativo, I = Inativo). |

# Tabela TB_CHEQUE_EMITENTE

**Módulo:** Financeiro / Cheques
Cadastro de emitentes de cheques próprios (contas da própria empresa) utilizados na emissão de cheques.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `EMT_CNPJ_CPF` | VARCHAR(14) | Sim | CNPJ/CPF do emitente (titular da conta). |
| `EMT_RSOCIAL_NOME` | VARCHAR(100) | Sim | Razão social ou nome do emitente. |
| `EMT_BANCO_CODIGO` | VARCHAR(10) | Não | Código do banco. |
| `EMT_AGENCIA` | VARCHAR(10) | Não | Número da agência. |
| `EMT_CONTA` | VARCHAR(14) | Não | Número da conta. |

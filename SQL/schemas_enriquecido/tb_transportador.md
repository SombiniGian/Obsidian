# Tabela TB_TRANSPORTADOR

**Módulo:** Cadastros / Frotas
Dados do transportador vinculados a TB_PESSOA.PES_ID. Permite armazenar observações e mensagens de alerta exibidas no momento do faturamento de pedidos com frete por este transportador.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TRP_PESSOA` | INTEGER | Não | FK para TB_PESSOA.PES_ID. Parte da chave primária composta. Use SEMPRE por PES_ID. |
| `TRP_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `TRP_OBSERVACAO` | VARCHAR(200) | Sim | Observações gerais do transportador. |
| `TRP_MENSAGEM_ALERTA` | INTEGER | Sim | Identificador da mensagem de alerta exibida ao usar este transportador. |

COMMENT ON COLUMN TB_TRANSPORTADOR.TRP_PESSOA IS 'FK para TB_PESSOA.PES_ID — SEMPRE faça JOIN com TB_PESSOA por PES_ID. Para filtrar transportadores utilize WHERE PES_TRANSPORTADOR = ''S'' em TB_PESSOA.';

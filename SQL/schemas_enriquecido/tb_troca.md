# Tabela TB_TROCA

**Módulo:** Vendas / Pós-venda
Tabela de trocas de produtos realizadas no pós-venda. Armazena dados do produto devolvido e do produto entregue na troca, valores (devolvido, troca, débito/crédito), quantidades, unidades, vínculo com o cliente e com o documento de origem (pedido de venda, NFC-e). Indica situação do produto (normal/defeito) e status da troca (ativo/cancelado).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `TRC_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `TRC_ID` | INTEGER | Não | Identificador único da troca. Parte da chave primária composta. |
| `TRC_STATUS` | VARCHAR(1) | Sim | Status da troca (A=Ativo, C=Cancelado). |
| `TRC_DT_LANCAMENTO` | TIMESTAMP | Sim | Data e hora de lançamento da troca no sistema. |
| `TRC_DT_TROCA` | DATE | Sim | Data em que a troca foi realizada. |
| `TRC_PROD_DEVOLVIDO` | INTEGER | Sim | FK para TB_PRODUTO do produto devolvido. Use JOIN por PROD_ID. |
| `TRC_PROD_TROCA` | INTEGER | Sim | FK para TB_PRODUTO do produto entregue na troca. Use JOIN por PROD_ID. |
| `TRC_UNIDADE_DEV` | VARCHAR(3) | Sim | Unidade de medida do produto devolvido. |
| `TRC_UNIDADE_TROCA` | VARCHAR(3) | Sim | Unidade de medida do produto da troca. |
| `TRC_VALOR_UN_DEVOLVIDO` | NUMERIC(15,4) | Sim | Valor unitário pelo qual o produto foi vendido. |
| `TRC_VALOR_UN_TROCA` | NUMERIC(15,4) | Sim | Valor unitário do produto entregue na troca. |
| `TRC_VALOR_DEVOLVIDO` | NUMERIC(15,2) | Sim | Valor total devolvido (produto original). |
| `TRC_VALOR_TROCA` | NUMERIC(15,2) | Sim | Valor total do produto entregue na troca. |
| `TRC_VALOR_DEBITO` | NUMERIC(15,2) | Sim | Valor de débito para o cliente (quando troca tem valor maior). |
| `TRC_VALOR_CREDITO` | NUMERIC(15,2) | Sim | Valor de crédito para o cliente (quando troca tem valor menor). |
| `TRC_QTDE_DEVOLVIDA` | NUMERIC(15,4) | Sim | Quantidade devolvida do produto original. |
| `TRC_QTDE_TROCA` | NUMERIC(15,4) | Sim | Quantidade entregue na troca. |
| `TRC_USUARIO` | INTEGER | Sim | Identificador do usuário que registrou a troca. |
| `TRC_ORIGEM` | VARCHAR(30) | Sim | Sigla do módulo/rotina de origem (ex.: PEDIDOVENDA, NOTAFISCAL). |
| `TRC_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem. |
| `TRC_CLIENTE` | INTEGER | Sim | FK para TB_PESSOA.PES_ID do cliente. Use JOIN por PES_ID. |
| `TRC_OBSERVACAO` | BLOB SUB_TYPE BINARY | Sim | Observações da troca em formato binário. NUNCA selecione em queries SELECT. |
| `TRC_SITUACAO_PRODUTO` | VARCHAR(1) | Sim | Situação do produto (N=Normal, D=Defeito). |

COMMENT ON COLUMN TB_TROCA.TRC_STATUS IS '''A''-> ATIVO
''C'' -> CANCELADO';
COMMENT ON COLUMN TB_TROCA.TRC_VALOR_DEVOLVIDO IS 'VALOR QUE O PRODUTO FOI VENDIDO';
COMMENT ON COLUMN TB_TROCA.TRC_VALOR_TROCA IS 'VALOR DO PRODUTO ENTREGUE AO CLIENTE';
COMMENT ON COLUMN TB_TROCA.TRC_SITUACAO_PRODUTO IS 'N - NORMAL
D - DEFEITO';
COMMENT ON COLUMN TB_TROCA.TRC_OBSERVACAO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

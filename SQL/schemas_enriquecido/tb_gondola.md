# Tabela TB_GONDOLA

**Módulo:** Estoque / Etiquetas
Tabela de produtos em gôndola/prateleira para geração de etiquetas de preço. Permite armazenar a quantidade de etiquetas a serem impressas por produto (e variação), descrição, unidade, preço de venda e marcador de seleção para impressão.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `GDL_EMPRESA` | INTEGER | Não | Identificador da empresa. Parte da chave primária composta. |
| `GDL_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO. Parte da chave primária composta. Use JOIN por PROD_ID. |
| `GDL_ID` | INTEGER | Não | Identificador único do registro de gôndola. Parte da chave primária composta. |
| `GDL_QUANTIDADE` | INTEGER | Sim | Quantidade de etiquetas a serem impressas. |
| `GDL_SELECIONADO` | VARCHAR(1) | Sim | Marcador para auxiliar quais produtos devem ser impressos (S/N). |
| `GDL_USUARIO` | INTEGER | Sim | Identificador do usuário que gerou o registro. |
| `GDL_UN` | VARCHAR(6) | Sim | Unidade de medida do produto para etiqueta. |
| `GDL_DESCRICAO` | VARCHAR(100) | Sim | Descrição do produto exibida na etiqueta. |
| `GDL_VARIACAO` | INTEGER | Sim | FK para TB_PRODUTO_VARIACAO (variação do produto). |
| `GDL_PRECO_VENDA` | NUMERIC(15,6) | Sim | Preço de venda a ser impresso na etiqueta. |

COMMENT ON COLUMN TB_GONDOLA.GDL_SELECIONADO IS 'CAMPO PARA AUXILIAR NA QUAL PRODUTO SERÁ IMPRESSO NA GÔNDOLA
''S'' - SIM
''N'' - NÃO';

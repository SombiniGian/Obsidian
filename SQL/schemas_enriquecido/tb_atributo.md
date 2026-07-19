# Tabela TB_ATRIBUTO

**Módulo:** Cadastros / Produto
Cadastro de atributos (ex.: Cor, Tamanho, Voltagem) vinculados a um tipo de atributo e utilizados para compor variações de produtos.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `ATR_ID` | INTEGER | Não | Identificador único do atributo. |
| `ATR_TIPO_ATRIBUTO` | INTEGER | Sim | FK para TB_TIPO_ATRIBUTO. |
| `ATR_DESCRICAO` | VARCHAR(100) | Sim | Descrição do atributo (ex.: Azul, M, 110V). |
| `ATR_ID_MELI` | VARCHAR(50) | Sim | ID do atributo na integração com Mercado Livre. |
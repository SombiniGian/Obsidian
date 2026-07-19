# Tabela TB_PRODUTO_VARIACAO

**Módulo:** Estoque / Vendas
Variações de um mesmo produto (cor, tamanho, modelo etc.). Cada variação pode ter NCM, código de barras, descrição, preço e imagem próprios, além de poder ser configurada para exibir o código de barras na NF-e.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `PRV_PRODUTO` | INTEGER | Não | FK para TB_PRODUTO.PRD_ID. Parte da chave primária composta. |
| `PRV_ID` | INTEGER | Não | Identificador único da variação. Parte da chave primária composta. |
| `PRV_MONTAR_DESCRICAO` | VARCHAR(1) | Sim | Indica se a descrição da variação deve ser montada automaticamente (S/N). |
| `PRV_DESCRICAO` | VARCHAR(100) | Sim | Descrição da variação (ex.: P, M, G, Cor Azul). |
| `PRV_PRECO` | NUMERIC(15,6) | Sim | Preço específico da variação (quando diferente do produto). |
| `PRV_NCM` | VARCHAR(10) | Sim | NCM próprio da variação. |
| `PRV_COD_BARRAS` | VARCHAR(20) | Sim | Código de barras (EAN) próprio da variação. |
| `PRV_STATUS` | VARCHAR(1) | Sim | Status da variação (A = Ativo, I = Inativo). |
| `PRV_IMAGEM` | BLOB SUB_TYPE BINARY | Sim | Imagem ilustrativa da variação em formato binário. NUNCA selecione em queries SELECT. |
| `PRV_REFERENCIA` | VARCHAR(30) | Sim | Referência/SKU da variação. |
| `PRV_DESCRICAO_MELI` | VARCHAR(100) | Sim | Descrição da variação na integração com Mercado Livre. |
| `PRV_MOSTRAR_BARRAS_NFE` | VARCHAR(1) | Sim | Indica se deve mostrar o código de barras na NF-e (S/N). |

COMMENT ON COLUMN TB_PRODUTO_VARIACAO.PRV_IMAGEM IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';

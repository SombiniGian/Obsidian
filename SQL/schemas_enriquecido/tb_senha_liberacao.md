# Tabela TB_SENHA_LIBERACAO

**Módulo:** Segurança / Vendas
Cadastro de senhas de liberação utilizadas no PDV/Vendas para exigir autorização do responsável em operações sensíveis (cancelamento, desconto, alteração de preço, sangria etc.). Cada coluna booleana indica uma permissão/restrição específica.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `SEN_LIB_ID` | INTEGER | Não | Identificador único da senha de liberação. |
| `SEN_LIB_EMPRESA` | INTEGER | Não | Identificador da empresa. |
| `SEN_LIB_NOME_RESPONSAVEL` | VARCHAR(40) | Sim | Nome do responsável pela senha. |
| `SEN_LIB_SENHA` | VARCHAR(13) | Sim | Senha de liberação. |
| `SEN_LIB_CONFIRMACAO_SENHA` | VARCHAR(13) | Sim | Confirmação da senha (validação no cadastro). |
| `SEN_LIB_DATA_CADASTRO` | DATE | Sim | Data do cadastro da senha. |
| `SEN_LIB_STATUS` | CHAR(1) | Sim | Status da senha (A=Ativo, I=Inativo). |
| `SEN_LIB_USUARIO` | INTEGER | Sim | FK para TB_USUARIO (usuário vinculado à senha). |
| `SEN_CANCELAR_VENDA` | VARCHAR(1) | Sim | Permite cancelar venda (S/N). |
| `SEN_CANCELAR_VENDA_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para cancelar venda (S/N). |
| `SEN_EXCLUIR_ITEM` | VARCHAR(1) | Sim | Permite excluir item (S/N). |
| `SEN_EXCLUIR_ITEM_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para excluir item (S/N). |
| `SEN_ACRESCIMO` | VARCHAR(1) | Sim | Permite aplicar acréscimo (S/N). |
| `SEN_ACRESCIMO_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para acréscimo (S/N). |
| `SEN_ALTERAR_TABELA` | VARCHAR(1) | Sim | Permite alterar tabela de preço (S/N). |
| `SEN_ALTERAR_TABELA_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para alterar tabela (S/N). |
| `SEN_ALTERAR_UNITARIO` | VARCHAR(1) | Sim | Permite alterar valor unitário (S/N). |
| `SEN_ALTERAR_UNIT_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para alterar unitário (S/N). |
| `SEN_DESCONTO` | VARCHAR(1) | Sim | Permite aplicar desconto (S/N). |
| `SEN_DESCONTO_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para desconto (S/N). |
| `SEN_PENDENCIA_FINANCEIRA` | VARCHAR(1) | Sim | Permite venda com pendência financeira (S/N). |
| `SEN_PENDENCIA_FINANC_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para vender com pendência (S/N). |
| `SEN_DESC_MAX_USU` | VARCHAR(1) | Sim | Permite aplicar desconto máximo do usuário (S/N). |
| `SEN_DESC_MAX_USU_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para desconto máximo (S/N). |
| `SEN_FATOR_CONTRA_SENHA` | NUMERIC(18,2) | Sim | Fator para exigir contra-senha (ex.: percentual mínimo). |
| `SEN_PRECO_MINIMO` | VARCHAR(1) | Sim | Permite vender abaixo do preço mínimo (S/N). |
| `SEN_PRECO_MINIMO_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para vender abaixo do mínimo (S/N). |
| `SEN_ALTERAR_VENDEDOR` | VARCHAR(1) | Sim | Permite alterar vendedor (S/N). |
| `SEN_ALTERAR_VEND_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para alterar vendedor (S/N). |
| `SEN_LIBERAR_LIM_CRED_CLI` | VARCHAR(1) | Sim | Permite liberar limite de crédito do cliente (S/N). |
| `SEN_LIBERAR_LIM_CRED_CLI_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para liberar limite de crédito (S/N). |
| `SEN_CANCELAR_HOSPEDAGEM` | VARCHAR(1) | Sim | Permite cancelar hospedagem (S/N). |
| `SEN_CANCELAR_HOSPEDAGEM_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para cancelar hospedagem (S/N). |
| `SEN_PULAR_ATT_OFFLINE` | VARCHAR(1) | Sim | Permite pular atualização offline (S/N). |
| `SEN_PULAR_ATT_OFF_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para pular atualização offline (S/N). |
| `SEN_LIBERAR_GATILHO` | VARCHAR(1) | Sim | Permite liberar gatilho (S/N). |
| `SEN_LIBERAR_GATILHO_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para liberar gatilho (S/N). |
| `SEN_LIBERAR_SANGRIA` | VARCHAR(1) | Sim | Permite liberar sangria (S/N). |
| `SEN_LIBERAR_SANGRIA_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para liberar sangria (S/N). |
| `SEN_LIBERAR_SUPRIMENTO` | VARCHAR(1) | Sim | Permite liberar suprimento (S/N). |
| `SEN_LIBERAR_SUPRIMENTO_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para liberar suprimento (S/N). |
| `SEN_ALTERA_TRIBUTACAO` | VARCHAR(1) | Sim | Permite alterar tributação (S/N). |
| `SEN_ALTERA_TRIBUTACAO_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para alterar tributação (S/N). |
| `SEN_PESQUISAR_PRODUTO` | VARCHAR(1) | Sim | Permite pesquisar produto (S/N). |
| `SEN_PESQUISAR_PRODUTO_CONTRA` | VARCHAR(1) | Sim | Exige contra-senha para pesquisar produto (S/N). |

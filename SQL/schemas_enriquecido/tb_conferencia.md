# Tabela TB_CONFERENCIA

**Módulo:** Estoque / Recebimento
Tabela de cabeçalho de conferência de mercadorias (recebimento, inventário, separação). Armazena dados da conferência: tipo, status, emissão, quantidade total x conferida, vínculo com vendedor e documento de origem, além de flag de geração de novo pedido. Os itens conferidos ficam em TB_CONFERENCIA_ITEM.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `CON_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `CON_ID` | INTEGER | Não | Identificador único da conferência. |
| `CON_TIPO` | VARCHAR(1) | Sim | Tipo da conferência (R=Recebimento, I=Inventário, S=Separação). |
| `CON_STATUS` | VARCHAR(1) | Sim | Status da conferência (A=Andamento, F=Finalizada, C=Cancelada). |
| `CON_DT_EMISSAO` | DATE | Sim | Data de emissão da conferência. |
| `CON_TIPO_ID` | INTEGER | Sim | FK para o documento conforme o tipo (ex.: TB_PEDIDO_COMPRA para tipo R). |
| `CON_USUARIO` | INTEGER | Sim | Identificador do usuário que realizou a conferência. |
| `CON_QTDE_TOTAL` | NUMERIC(15,4) | Sim | Quantidade total esperada para conferência. |
| `CON_QTDE_CONFERIDO` | NUMERIC(15,4) | Sim | Quantidade já conferida. |
| `CON_VENDEDOR` | INTEGER | Sim | FK para TB_VENDEDOR responsável. |
| `CON_ORIGEM` | VARCHAR(20) | Sim | Sigla do módulo/rotina de origem. |
| `CON_ID_ORIGEM` | INTEGER | Sim | Identificador do documento de origem. |
| `CON_NOVO_PEDIDO` | INTEGER | Sim | Identificador do novo pedido gerado a partir da conferência. |
| `CON_GERAR_PEDIDO` | VARCHAR(1) | Sim | Indica se a conferência deve gerar pedido (S/N). |
| `CON_GUID` | VARCHAR(50) | Sim | GUID para integração. |

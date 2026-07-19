# Tabela TB_VENDEDOR

**Módulo:** Vendas / Cadastros
Dados do vendedor vinculados a TB_PESSOA.PES_ID. Contém comissão, objetivos de venda, prêmios, permissões do PDV/App e configurações de login no tablet/PDA.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `VDR_PESSOA` | INTEGER | Não | FK para TB_PESSOA.PES_ID. Parte da chave primária composta. Use SEMPRE por PES_ID. |
| `VDR_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `VDR_TIPO_PESSOA` | VARCHAR(1) | Sim | Tipo de pessoa (F=Física, J=Jurídica). |
| `VDR_OBSERVACAO` | VARCHAR(100) | Sim | Observações gerais do vendedor. |
| `VDR_DT_CADASTRO` | DATE | Sim | Data de cadastro do vendedor. |
| `VDR_STATUS` | VARCHAR(1) | Sim | Status do vendedor: A=Ativo, I=Inativo. |
| `VDR_COMISSAO` | NUMERIC(15,2) | Sim | Percentual de comissão padrão do vendedor. |
| `VDR_SUPERVISOR` | VARCHAR(1) | Sim | Indica se o vendedor é supervisor (S/N). |
| `VDR_SENHA` | VARCHAR(20) | Sim | Senha de acesso do vendedor no PDV. |
| `VDR_LOGIN` | VARCHAR(50) | Sim | Login do vendedor no tablet/PDA. |
| `VDR_OBJETIVO_VENDA` | NUMERIC(15,2) | Sim | Valor de objetivo de vendas no período. |
| `VDR_PREMIO_OBJ_VENDA` | NUMERIC(15,2) | Sim | Valor do prêmio ao atingir o objetivo de vendas. |
| `VDR_ADIMPLENCIA` | NUMERIC(15,2) | Sim | Percentual mínimo de adimplência exigido. |
| `VDR_PREMIO_ADIMPLENCIA` | NUMERIC(15,2) | Sim | Valor do prêmio por adimplência. |
| `VDR_CLIENTES_TABLET` | VARCHAR(1) | Sim | Clientes visíveis no tablet (T=Todos, P=Privados). |
| `VDR_SETOR` | INTEGER | Sim | FK para TB_SETOR — setor padrão do vendedor. |
| `VDR_IMPRESSORA_PREFERENCIAL` | INTEGER | Sim | Identificador da impressora preferencial. |
| `VDR_ALTERAR_PRECO` | VARCHAR(1) | Sim | Permite alterar preço no PDV (S/N). |
| `VDR_VISUALIZAR_CUSTO` | VARCHAR(1) | Sim | Permite visualizar custo do produto (S/N). |
| `VDR_BLOQUEAR_PRECO_MINIMO` | VARCHAR(1) | Sim | Bloqueia vendas abaixo do preço mínimo (S/N). |
| `VDR_TIPO_DESC_MAX` | VARCHAR(1) | Sim | Tipo do desconto máximo (V=Valor, P=Percentual). |
| `VDR_DESC_MAX` | NUMERIC(15,2) | Sim | Valor/percentual máximo de desconto permitido. |
| `VDR_ALTERAR_TABELA` | VARCHAR(1) | Sim | Permite alterar tabela de preço (S/N). |
| `VDR_CAIXA` | INTEGER | Sim | FK para TB_CONTA.CNT_ID — caixa padrão. |
| `VDR_REPORT_NFE` | VARCHAR(255) | Sim | Caminho do relatório de NF-e. |
| `VDR_IMPRESSAO_PEDIDO` | VARCHAR(20) | Sim | Configuração de impressão do pedido. |
| `VDR_FATURAR_PEDIDO` | VARCHAR(1) | Sim | Permite faturar pedido (S/N). |
| `VDR_EMITIR_NF` | VARCHAR(1) | Sim | Permite emitir NF (S/N). |
| `VDR_REPORT_BOLETO` | VARCHAR(255) | Sim | Caminho do relatório de boleto. |
| `VDR_IMPRIMIR_RECEPCAO` | VARCHAR(1) | Sim | Imprimir recepção (S/N). |
| `VDR_NUMERO_CONSIGNADOS` | INTEGER | Sim | Limite de itens consignados permitidos. |
| `VDR_EXCLUIR_ITEM_APP` | VARCHAR(1) | Sim | Permite excluir item no app (S/N). |
| `VDR_TIPO_APP` | VARCHAR(1) | Sim | Tipo de app utilizado. |
| `VDR_SQL_DESC_CONDICIONAL` | BLOB SUB_TYPE BINARY | Sim | SQL de desconto condicional em binário. NUNCA selecione em queries SELECT. |
| `VDR_DIAS_DESC_CONDICIONAL` | INTEGER | Sim | Dias para aplicação do desconto condicional. |
| `VDR_PERMITIR_BLOQUEAR_PEDIDO` | VARCHAR(1) | Sim | Permite bloquear pedido (S/N). |
| `VDR_OBRIGAR_ATUALIZAR` | VARCHAR(1) | Sim | Obriga atualização periódica no app (S/N). |
| `VDR_DIA_ATUALIZAR` | INTEGER | Sim | Dia do mês para atualização obrigatória. |
| `VDR_HR_ATUALIZAR` | TIME | Sim | Hora da atualização obrigatória. |
| `VDR_VISUALIZAR_MAPA_APP` | VARCHAR(1) | Sim | Permite visualizar mapa no app (S/N). |
| `VDR_PERMITIR_TRANSFERIR_APP` | VARCHAR(1) | Sim | Permite transferir pedido entre vendedores no app (S/N). |
| `VDR_IMPRESSAO_PIX_VENCTO_APP` | VARCHAR(20) | Sim | Configuração de impressão do PIX com vencimento no app. |
| `VDR_VISUALIZAR_RECEBER` | VARCHAR(1) | Sim | Permite visualizar contas a receber (S/N). |
| `VDR_BLOQUEAR_DESC_MAX` | VARCHAR(1) | Sim | Bloqueia aplicação de desconto acima do máximo (S/N). |
| `VDR_PDV_APP` | VARCHAR(1) | Sim | Habilita PDV no app (S/N). |
| `VDR_MAQUINA_CARTAO` | INTEGER | Sim | FK para TB_MAQUINA_CARTAO — máquina padrão. |
| `VDR_DIAS_ATUALIZA_VENDAS` | INTEGER | Sim | Dias para atualização de vendas no app. |
| `VDR_LIMITE_APP` | VARCHAR(1) | Sim | Indica se o app tem limite (S/N). |
| `VDR_CHECKIN_APP` | VARCHAR(1) | Sim | Permite check-in no app (S/N). |
| `VDR_CHECKOUT_APP` | VARCHAR(1) | Sim | Permite check-out no app (S/N). |
| `VDR_VISUALIZAR_TOTAL_APP` | VARCHAR(1) | Sim | Permite visualizar total no app (S/N). |
| `VDR_CONTROLAR_CAIXA_APP` | VARCHAR(1) | Sim | Permite controlar caixa no app (S/N). |
| `VDR_APLICAR_DESC_APP` | VARCHAR(1) | Sim | Permite aplicar desconto no app (S/N). |
| `VDR_APLICAR_ACRESC_APP` | VARCHAR(1) | Sim | Permite aplicar acréscimo no app (S/N). |
| `VDR_ALTERAR_TX_SERV_APP` | VARCHAR(1) | Sim | Permite alterar taxa de serviço no app (S/N). |
| `VDR_ESTORNAR_PAGAMENTO_APP` | VARCHAR(1) | Sim | Permite estornar pagamento no app (S/N). |
| `VDR_ALTERACAO_PRECOS_APP` | VARCHAR(1) | Sim | Permite alterar preços no app (S/N). |
| `VDR_COMPRA_APP` | VARCHAR(1) | Sim | Habilita módulo de compra no app (S/N). |
| `VDR_CONFERENCIA_APP` | VARCHAR(1) | Sim | Habilita conferência no app (S/N). |
| `VDR_INFORMAR_MESA_COMANDA_APP` | VARCHAR(1) | Sim | Permite informar mesa/comanda no app (S/N). |
| `VDR_OS_APP` | VARCHAR(1) | Sim | Habilita ordem de serviço no app (S/N). |
| `VDR_IMP_FICHAS_APP` | VARCHAR(1) | Sim | Permite imprimir fichas no app (S/N). |
| `VDR_VALIDAR_SETORES` | VARCHAR(1) | Sim | Valida setores do vendedor (S/N). |
| `VDR_LOCAL_ESTOQUE` | INTEGER | Sim | FK para TB_LOCAL_ESTOQUE.LOC_ID — local de estoque padrão. |

COMMENT ON COLUMN TB_VENDEDOR.VDR_PESSOA IS 'FK para TB_PESSOA.PES_ID — SEMPRE faça JOIN com TB_PESSOA por PES_ID. Para filtrar vendedores utilize WHERE PES_VENDEDOR = ''S'' em TB_PESSOA.';
COMMENT ON COLUMN TB_VENDEDOR.VDR_STATUS IS 'A - ATIVO
I - INATIVO';
COMMENT ON COLUMN TB_VENDEDOR.VDR_CLIENTES_TABLET IS 'T - TODOS
P - PRIVADOS';
COMMENT ON COLUMN TB_VENDEDOR.VDR_SQL_DESC_CONDICIONAL IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_VENDEDOR.VDR_TIPO_DESC_MAX IS 'V - VALOR
P - PERCENTUAL';

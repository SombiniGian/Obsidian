# Tabela TB_USUARIO

**Módulo:** Usuários
Cadastro de usuários do sistema com permissões funcionais por tela/ação, configurações pessoais (e-mail, dashboard, restrições de desconto/alteração de itens) e dados para auditoria.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `USU_ID` | INTEGER | Não | Identificador único do usuário. |
| `USU_NOME` | VARCHAR(80) | Sim | Nome completo do usuário. |
| `USU_LOGIN` | VARCHAR(20) | Sim | Login de acesso ao sistema. |
| `USU_SENHA` | VARCHAR(20) | Sim | Senha de acesso (armazenada de forma protegida). |
| `USU_PERFIL` | INTEGER | Sim | FK para perfil de permissões. |
| `USU_ADMINISTRADOR` | VARCHAR(1) | Sim | Indica se o usuário é administrador (S/N). |
| `USU_PDV_SALVAR_VENDA` | VARCHAR(1) | Sim | Permite salvar venda no PDV sem finalizar (S/N). |
| `USU_PDV_FINALIZAR_VENDA` | VARCHAR(1) | Sim | Permite finalizar venda no PDV (S/N). |
| `USU_JUNTAR_PEDIDOS` | VARCHAR(1) | Sim | Permite juntar pedidos (S/N). |
| `USU_TIPO_DESC_MAX` | VARCHAR(1) | Sim | Tipo do desconto máximo permitido (V=Valor, P=Porcentagem). |
| `USU_DESC_MAX` | NUMERIC(15,2) | Sim | Valor/percentual máximo de desconto. |
| `USU_VENDEDOR` | INTEGER | Sim | FK para TB_PESSOA.PES_ID (vendedor vinculado). |
| `USU_SKIN` | VARCHAR(30) | Sim | Skin/tema da interface. |
| `USU_STYLE` | INTEGER | Sim | Estilo visual da interface. |
| `USU_APENAS_RIBBON` | VARCHAR(1) | Sim | Força uso de ribbon (S/N). |
| `USU_DESABILITAR_AERO` | VARCHAR(1) | Sim | Desabilita Aero do Windows (S/N). |
| `USU_MENU` | BLOB SUB_TYPE BINARY | Sim | Menu personalizado em binário. NUNCA selecione em queries SELECT. |
| `USU_CAIXA` | INTEGER | Sim | Caixa padrão do usuário. |
| `USU_IMPRESSORA` | INTEGER | Sim | Impressora padrão. |
| `USU_DASHBOARD` | VARCHAR(1) | Sim | Indica se usa dashboard (S/N). |
| `USU_EMAIL_HOST` | VARCHAR(100) | Sim | Host SMTP do e-mail. |
| `USU_EMAIL_PORTA` | VARCHAR(10) | Sim | Porta SMTP. |
| `USU_EMAIL_LOGIN` | VARCHAR(100) | Sim | Login SMTP. |
| `USU_EMAIL_NOME` | VARCHAR(100) | Sim | Nome exibido no envio de e-mail. |
| `USU_EMAIL_SENHA` | VARCHAR(40) | Sim | Senha SMTP. |
| `USU_EMAIL_ASSUNTO` | VARCHAR(200) | Sim | Assunto padrão do e-mail. |
| `USU_EMAIL_SSL` | VARCHAR(1) | Sim | Usa SSL no envio (S/N). |
| `USU_EMAIL_TSL` | VARCHAR(1) | Sim | Usa TLS no envio (S/N). |
| `USU_EMAIL_CONFIRMA` | VARCHAR(1) | Sim | Solicita confirmação de leitura (S/N). |
| `USU_EMAIL_THREAD` | VARCHAR(1) | Sim | Agrupa em thread (S/N). |
| `USU_EMAIL_REPLAY` | VARCHAR(100) | Sim | E-mail para reply. |
| `USU_EMAIL_REPLAY_NOME` | VARCHAR(100) | Sim | Nome para reply. |
| `USU_NAO_VISUALIZAR_CUSTO` | VARCHAR(1) | Sim | Não exibe custo de produtos (S/N). |
| `USU_FATURAR_OS` | VARCHAR(1) | Sim | Permite faturar ordem de serviço (S/N). |
| `USU_ALTERAR_SIT_OS` | VARCHAR(1) | Sim | Permite alterar situação da OS (S/N). |
| `USU_IDIOMA` | INTEGER | Sim | Idioma do usuário. |
| `USU_STATUS` | VARCHAR(1) | Sim | Status do usuário (A=Ativo, I=Inativo). |
| `USU_EXPORTAR` | VARCHAR(1) | Sim | Indica se o usuário é exportado para integrações (S/N). |
| `USU_PESSOA_APP` | INTEGER | Sim | FK para TB_PESSOA.PES_ID no app. |
| `USU_EMPRESA_APP` | INTEGER | Sim | FK para empresa do app. |
| `USU_OPCOES_PRODUTO` | VARCHAR(1) | Sim | Exibe opções de produto (S/N). Default 'S'. |
| `USU_PERMITE_ALTERAR_PRECO_OS` | VARCHAR(1) | Sim | Permite alterar preço na OS (S/N). |
| `USU_NAO_VISUALIZAR_INSUMOS` | VARCHAR(1) | Sim | Não visualiza insumos (S/N). |
| `USU_NAO_ALTERAR_ENTREGA` | VARCHAR(1) | Sim | Não altera dados de entrega (S/N). |
| `USU_BASE_DESC_MAX` | VARCHAR(1) | Sim | Define a base do desconto máximo. |
| `USU_NAO_ALTERA_INV_ATIVO` | VARCHAR(1) | Sim | Não altera inventário de ativo (S/N). |
| `USU_PERMITIR_ACESSOS_SIMULTANEO` | VARCHAR(1) | Sim | Permite mais de um acesso simultâneo (S/N). |
| `USU_ULTIMA_ALTERACAO` | TIMESTAMP | Sim | Timestamp da última alteração. Default: current_timestamp. |
| `USU_ALERTAR_COBRANCA_LICENCA` | VARCHAR(1) | Sim | Alerta cobrança de licença (S/N). |
| `USU_TIPO_ESTACAO` | VARCHAR(50) | Sim | Tipo da estação de trabalho. |
| `USU_HOTEL_ALTERAR_APARTAMENTO` | VARCHAR(1) | Sim | Módulo hotel: alterar apartamento (S/N). |
| `USU_HOTEL_ALTERAR_TIPO_HOSP` | VARCHAR(1) | Sim | Módulo hotel: alterar tipo de hospedagem (S/N). |
| `USU_HOTEL_ALTERAR_VALOR_HOSP` | VARCHAR(1) | Sim | Módulo hotel: alterar valor da hospedagem (S/N). |
| `USU_HOTEL_ALTERAR_ENT_SAI` | VARCHAR(1) | Sim | Módulo hotel: alterar entrada/saída (S/N). |
| `USU_HOTEL_ALTERAR_CHECKIO` | VARCHAR(1) | Sim | Módulo hotel: alterar check-in/check-out (S/N). |
| `USU_HOTEL_PERMITE_DESVINCULAR` | VARCHAR(1) | Sim | Módulo hotel: desvincular hospedagem (S/N). |
| `USU_HOTEL_SENHA_ALTERAR_TAXA` | VARCHAR(1) | Sim | Módulo hotel: senha para alterar taxa (S/N). |
| `USU_VISUALIZAR_DETALHES_VENDA` | VARCHAR(1) | Sim | Visualiza detalhes da venda (S/N). |
| `USU_NAO_CONCLUIR_SEM_FINANCEIRO` | VARCHAR(1) | Sim | Não conclui pedido sem financeiro (S/N). |
| `USU_VER_TODAS_TABELAS_PRECO` | VARCHAR(1) | Sim | Visualiza todas as tabelas de preço (S/N). |
| `USU_ENTREGA_ALT_VENDEDOR` | VARCHAR(1) | Sim | Permite alterar vendedor na entrega (S/N). |
| `USU_ENTREGA_ALT_COMPRADOR` | VARCHAR(1) | Sim | Permite alterar comprador na entrega (S/N). |
| `USU_CONSULTAR_ALTERADOS_IMENDES` | VARCHAR(1) | Sim | Consulta itens alterados IMENDES (S/N). |
| `USU_NAO_TRANSFERIR_ESTOQUE` | VARCHAR(1) | Sim | Não transfere estoque (S/N). |
| `USU_REABRE_HOSPEDAGEM` | VARCHAR(1) | Sim | Reabre hospedagem (S/N). |
| `USU_AGENDAMENTO_EMAIL` | VARCHAR(1) | Sim | Envia agendamento por e-mail (S/N). |
| `USU_NAO_CLICAR_VENDIDO` | VARCHAR(1) | Sim | Não permite clicar produto vendido (S/N). |
| `USU_NFE_RECEBIDA_DIGITANDO` | VARCHAR(1) | Sim | NF-e recebida digitando (S/N). |
| `USU_NFE_FINALIZAR_DIGITANDO` | VARCHAR(1) | Sim | Finaliza NF-e que está sendo digitada (S/N). |
| `USU_ALMOX_SOLICITACAO_USUARIO` | VARCHAR(1) | Sim | Vê somente suas solicitações no almoxarifado (S/N). |
| `USU_ALMOX_SOLICITACAO_TODOS` | VARCHAR(1) | Sim | Vê todas as solicitações no almoxarifado (S/N). |
| `USU_RECOLHER_CALENDARIO` | VARCHAR(1) | Sim | Recolhe calendário na interface (S/N). |
| `USU_AVISO_REMESSA` | VARCHAR(1) | Sim | Exibe aviso de remessa (S/N). |
| `USU_PRECO_EMPRESA` | VARCHAR(1) | Sim | Usa preço por empresa (S/N). |
| `USU_GEPLUG` | VARCHAR(1) | Sim | Indica uso do GEPlug (S/N). |
| `USU_NAO_FINALIZA_BALCAO` | VARCHAR(1) | Sim | Não finaliza venda balcão (S/N). |
| `USU_NAO_ALTERAR_ITENS` | VARCHAR(1) | Sim | Não permite alterar itens do pedido (S/N). |

COMMENT ON COLUMN TB_USUARIO.USU_VENDEDOR IS 'FK para TB_PESSOA.PES_ID — vendedor vinculado ao usuário';
COMMENT ON COLUMN TB_USUARIO.USU_STATUS IS 'A - Ativo
I - Inativo';
COMMENT ON COLUMN TB_USUARIO.USU_MENU IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT — elas quebram a serialização';

# Tabela TB_MAQUINA_CARTAO

**Módulo:** TEF / Cartão
Cadastro de máquinas de cartão (TEF) com configuração de integração (SiTef, Pinpad, etc.). Armazena dados de credenciamento, endpoint, token, timeouts e impressão de vias.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `MAQ_ID` | INTEGER | Não | Identificador único da máquina de cartão. |
| `MAQ_SERIAL` | VARCHAR(50) | Sim | Número de série da máquina. |
| `MAQ_DESCRICAO` | VARCHAR(100) | Sim | Descrição/identificação da máquina. |
| `MAQ_EMPRESA` | INTEGER | Sim | Identificador da empresa à qual a máquina pertence. |
| `MAQ_STATUS` | VARCHAR(1) | Sim | Status da máquina (A=Ativa, I=Inativa). |
| `MAQ_INTEGRACAO` | VARCHAR(20) | Sim | Tipo de integração (SiTef, PayGo, Stone, Cielo, etc.). |
| `MAQ_SITEF_EMPRESA` | VARCHAR(10) | Sim | Código de empresa SiTef. |
| `MAQ_SITEF_ENDERECO` | VARCHAR(100) | Sim | Endereço/IP do servidor SiTef. |
| `MAQ_SITEF_CNPJ` | VARCHAR(14) | Sim | CNPJ do estabelecimento no SiTef. |
| `MAQ_SITEF_COM_EXTERNA` | INTEGER | Sim | Indica se a comunicação com o SiTef é externa (0=Interna, 1=Externa). |
| `MAQ_SITEF_OPERADOR` | VARCHAR(20) | Sim | Operador SiTef. |
| `MAQ_SITEF_CNPJ_AUT` | VARCHAR(14) | Sim | CNPJ da autorizadora. |
| `MAQ_SITEF_END_SEM_TLS` | VARCHAR(100) | Sim | Endereço SiTef sem TLS (legado). |
| `MAQ_SITEF_TOKEN` | VARCHAR(100) | Sim | Token de autenticação SiTef. |
| `MAQ_SITEF_TIMEOUT` | INTEGER | Sim | Timeout (em segundos) da comunicação SiTef. |
| `MAQ_IMPRIMIR_VIA_EST` | VARCHAR(1) | Sim | Indica se imprime via do estabelecimento (S/N). |
| `MAQ_IMPRIMIR_VIA_CLIENTE` | VARCHAR(1) | Sim | Indica se imprime via do cliente (S/N). |
| `MAQ_SITEF_TIPO_END` | VARCHAR(10) | Sim | Tipo de endpoint SiTef (IP, DNS, etc.). |
| `MAQ_CODIGO_ATIVACAO` | VARCHAR(50) | Sim | Código de ativação/credenciamento da máquina. |
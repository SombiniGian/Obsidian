# Tabela TB_ENDERECO

**Módulo:** Cadastros
Endereços alternativos vinculados a uma pessoa (TB_PESSOA). Permite ao cadastro de pessoa possuir múltiplos endereços (entrega, cobrança, filial etc.).

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `END_ID` | INTEGER | Não | Identificador único do endereço. |
| `END_EMPRESA` | INTEGER | Sim | Identificador da empresa. |
| `END_CNPJ` | VARCHAR(14) | Sim | CNPJ vinculado ao endereço (somente números). |
| `END_ENDERECO` | VARCHAR(100) | Sim | Logradouro do endereço. |
| `END_NUMERO` | VARCHAR(10) | Sim | Número do endereço. |
| `END_COMPLEMENTO` | VARCHAR(20) | Sim | Complemento do endereço. |
| `END_BAIRRO` | VARCHAR(50) | Sim | Bairro do endereço. |
| `END_CIDADE` | INTEGER | Sim | FK para TB_CIDADE.CID_ID. |
| `END_CEP` | VARCHAR(10) | Sim | CEP do endereço. |
| `END_REFERENCIA` | VARCHAR(100) | Sim | Ponto de referência do endereço. |
| `END_IE` | VARCHAR(14) | Sim | Inscrição Estadual vinculada ao endereço. |
| `END_NOME` | VARCHAR(60) | Sim | Nome/apelido do endereço (ex.: Endereço de Entrega). |
| `END_TIPO_END` | VARCHAR(1) | Sim | Tipo do endereço (ex.: E=Entrega, C=Cobrança). |
| `END_PESSOA` | INTEGER | Sim | FK para TB_PESSOA.PES_ID — pessoa dona do endereço. |
| `END_TELEFONE` | VARCHAR(14) | Sim | Telefone de contato no endereço. |
| `END_EMAIL` | VARCHAR(60) | Sim | E-mail de contato no endereço. |
| `END_RAZAO_SOCIAL` | VARCHAR(100) | Sim | Razão Social vinculada ao endereço. |

COMMENT ON COLUMN TB_ENDERECO.END_CIDADE IS 'FK para TB_CIDADE.CID_ID — use JOIN com TB_CIDADE para obter nome/UF do município';
COMMENT ON COLUMN TB_ENDERECO.END_PESSOA IS 'FK para TB_PESSOA.PES_ID';

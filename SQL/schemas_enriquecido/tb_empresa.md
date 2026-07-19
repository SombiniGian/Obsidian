# Tabela TB_EMPRESA

**Módulo:** Cadastros
Cadastro das empresas (matriz e filiais) que utilizam o sistema. Reúne dados fiscais (CNPJ, IE, CRT), configurações (tipo, CNAE, conexões simultâneas, salário mínimo, RNTRC) e o logo em binário.

## Campos

| Coluna | Tipo | Nulo | Descrição |
|---|---|---|---|
| `EMP_ID` | INTEGER | Não | Identificador único da empresa. |
| `EMP_FANTASIA` | VARCHAR(80) | Sim | Nome fantasia. |
| `EMP_RAZAO_SOCIAL` | VARCHAR(80) | Sim | Razão Social. |
| `EMP_CNPJ` | VARCHAR(18) | Sim | CNPJ da empresa. |
| `EMP_IE` | VARCHAR(18) | Sim | Inscrição Estadual. |
| `EMP_ENDERECO` | VARCHAR(80) | Sim | Logradouro. |
| `EMP_COMPLEMENTO` | VARCHAR(20) | Sim | Complemento. |
| `EMP_NUMERO` | VARCHAR(10) | Sim | Número do endereço. |
| `EMP_BAIRRO` | VARCHAR(50) | Sim | Bairro. |
| `EMP_CIDADE` | INTEGER | Sim | FK para TB_CIDADE.CID_ID. |
| `EMP_CEP` | VARCHAR(10) | Sim | CEP. |
| `EMP_TELEFONE` | VARCHAR(20) | Sim | Telefone fixo. |
| `EMP_FAX` | VARCHAR(20) | Sim | Fax. |
| `EMP_CELULAR` | VARCHAR(20) | Sim | Celular. |
| `EMP_EMAIL` | VARCHAR(50) | Sim | E-mail. |
| `EMP_CONTATO` | VARCHAR(50) | Sim | Nome do contato principal. |
| `EMP_DT_INSTITUICAO` | DATE | Sim | Data de instituição da empresa. |
| `EMP_OBSERVACAO` | VARCHAR(100) | Sim | Observações. |
| `EMP_CRT` | INTEGER | Sim | Código de Regime Tributário: 1=Simples Nacional, 2=Simples Nacional Excesso de Sublimite, 3=Tributação Normal. |
| `EMP_TIPO` | VARCHAR(1) | Sim | Tipo da empresa: M=Matriz, F=Filial. |
| `EMP_EMPRESA_MATRIZ` | INTEGER | Sim | FK para TB_EMPRESA.EMP_ID da matriz (quando for filial). |
| `EMP_CAMINHO_DOC_FISCAIS` | VARCHAR(100) | Sim | Caminho de armazenamento dos documentos fiscais. |
| `EMP_EMITE_CUPOM_FISCAL` | VARCHAR(1) | Sim | Indica se emite cupom fiscal (S/N). |
| `EMP_VERSAO_IBPT` | VARCHAR(50) | Sim | Versão da tabela IBPT em uso. |
| `EMP_TIPO_EMPRESA` | VARCHAR(1) | Sim | Tipo da atividade: C=Comércio, I=Indústria. |
| `EMP_VALOR_SALARIO` | NUMERIC(15,2) | Sim | Valor do salário mínimo configurado. |
| `EMP_SERIAL` | VARCHAR(100) | Sim | Serial/licença de uso do sistema. |
| `EMP_STATUS` | VARCHAR(10) | Sim | Status da empresa. |
| `EMP_RNTRC` | VARCHAR(20) | Sim | RNTRC da transportadora. |
| `EMP_CIOT` | VARCHAR(20) | Sim | CIOT (Código de Identificação da Operação de Transporte). |
| `EMP_LOGO` | BLOB SUB_TYPE BINARY | Sim | Logotipo da empresa em formato binário. NUNCA selecione em queries SELECT. |
| `EMP_INSC_MUNICIPAL` | VARCHAR(20) | Sim | Inscrição Municipal. |
| `EMP_CONEXOES_SIMULTANEAS` | INTEGER | Sim | Quantidade de conexões simultâneas permitidas. Default 0. |
| `EMP_CNAE` | VARCHAR(10) | Sim | CNAE da empresa. |

COMMENT ON COLUMN TB_EMPRESA.EMP_CRT IS 'EMP_CRT
1 - SIMPLES NACIONAL
2 - SIMPLES NACIONAL - EXCESSO DE SUBLIMITE DA RECEITA BRUTA
3 - TRIBUTAÇÃO NORMAL';
COMMENT ON COLUMN TB_EMPRESA.EMP_TIPO IS 'M - MATRIZ
F - FILIAL';
COMMENT ON COLUMN TB_EMPRESA.EMP_TIPO_EMPRESA IS 'C - COMERCIO
I - INDUSTRIA';
COMMENT ON COLUMN TB_EMPRESA.EMP_LOGO IS 'NUNCA selecione colunas do tipo BLOB em queries SELECT';
COMMENT ON COLUMN TB_EMPRESA.EMP_EMPRESA_MATRIZ IS 'FK para TB_EMPRESA.EMP_ID da matriz — use JOIN para obter dados da matriz';

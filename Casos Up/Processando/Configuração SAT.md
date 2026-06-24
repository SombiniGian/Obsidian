---
id: CASO-002
link: https://www.youtube.com/watch?v=e7omZ0gkq5o
setor: Suporte, Implantação, Desenvolvimento
modulo: Documentos Fiscais
tags:
  - sat
  - cupom-fiscal
  - configuracao
  - integracao-fiscal
  - emulador
data_criacao: 2026-06-24
---

# Documentação Técnica: Parametrização e Configuração do Sistema SAT

Esta documentação provê as diretrizes técnicas necessárias para a instalação, parametrização e homologação do Sistema Autenticador e Transmissor de Cupons Fiscais Eletrônicos ([[SAT-CF-e]]) no ERP. O sistema suporta tanto a arquitetura de comunicação local direta quanto o modelo descentralizado via servidor de aplicação dedicado.

---

## Sumário
1. [[#1. Configuração do Emitente e Assinatura Digital]]
2. [[#2. Arquiteturas de Implantação (Local vs. Servidor)]]
3. [[#3. Parâmetros de Integração com o Hardware (DLL)]]
4. [[#4. Configurações de Rede e Comunicação SEFAZ]]
5. [[#5. Layout e Modelos de Impressão (Extrato SAT)]]
6. [[#6. Painel de Comandos e Diagnósticos Técnicos]]

---

## 1. Configuração do Emitente e Assinatura Digital

A validação jurídica dos cupons fiscais transmitidos pelo equipamento depende do correto vínculo entre a Software House desenvolvedora e o contribuinte (emitente).

### Parametrização no Cadastro da Empresa
1. Acesse o **Cadastro da Empresa** e navegue até a aba **SAT**.
2. Preencha rigorosamente os dados do emitente e as propriedades relativas à Software House (CNPJ do desenvolvedor).
3. **Assinatura Digital (Código de Vinculação):** O campo de assinatura armazena o hash de vinculação gerado a partir da combinação do CNPJ da Software House + CNPJ do Emitente.
   - O sistema possui o botão **Gerar Assinatura** para automatizar esse cálculo.

> [!warning] Validação de Ambiente de Produção
> Em ambiente de produção, a geração automática do hash exige obrigatoriamente que o Certificado Digital do emitente esteja devidamente instalado e válido no repositório do Windows, além de os CNPJs estarem previamente vinculados no portal da SEFAZ de São Paulo. Em ambientes de homologação utilizando o emulador, dados fictícios são aceitos sem a validação do certificado.

---

## 2. Arquiteturas de Implantação (Local vs. Servidor)

O sistema oferece flexibilidade na topologia de rede, permitindo otimizar custos com hardware de acordo com a quantidade de Pontos de Venda ([[PDV]]) instalados no cliente. A alternância de comportamento é controlada pela flag **Servidor SAT** na tela de configuração.

[Arquitetura Local Direct] 
+-----------------------------------+ 
| PDV |
| [ERP Client] -> [DLL] -> [SAT] |
+-----------------------------------+

[Arquitetura Servidor Concentrador]
+-----------------+ +-----------------+
| PDV 01 |         | PDV 02 | 
| [ERP Client] | | [ERP Client] | 
+--------+--------+ +--------+--------+ |
| +-----------+-------------+ |
(TCP/IP)
v 
+-------------------------------------------+
| Estação Servidora | | [Servidor SAT] -> [DLL] -> [Hardware SAT] |
+-------------------------------------------+

### Cenário A: Execução Local
* **Comportamento:** O ERP comunica-se diretamente com o hardware conectado à porta USB da própria estação de trabalho.
* **Campos Habilitados:** Caminhos locais de salvamento de arquivos XML, diretórios de logs locais e seleção direta da DLL do fabricante.

### Cenário B: Execução via Servidor Concentrador (Multi-PDV)
* **Comportamento:** Indicado para cenários onde múltiplas estações de venda (PDVs) compartilham um único equipamento SAT físico instalado em uma máquina central da rede.
* **Configuração no Client:** Ao marcar a opção **Servidor SAT**, o ERP oculta os campos de caminhos de arquivos e habilita os campos de **IP** e **Porta TCP** do servidor concentrador.
* **Mapeamento de Restrições:** No modo cliente-servidor, os comandos críticos de nível de hardware (como ativação e atualização de rede do aparelho) ficam ocultos na ponta, sendo centralizados exclusivamente na interface do executável do servidor.

> [!info] Inicialização do Serviço Concentrador
> O executável `Servidor SAT` deve ser configurado para iniciar junto com o sistema operacional na máquina que possui o hardware acoplado. Ele requer a indicação da **Porta de Escuta**, o **ID da Empresa** padrão (geralmente Empresa `1`) e a string de conexão com o banco de dados.

---

## 3. Parâmetros de Integração com o Hardware (DLL)

A camada de abstração com o hardware é realizada via chamadas de funções exportadas por bibliotecas dinâmicas (`.dll`).

* **Modelo do Equipamento:** Seleção do driver equivalente ao fabricante do hardware homologado (ex: Bematech, Gertec, Elgin, Kryptus, Dimep).
* **Código de Ativação:** Senha cadastrada pelo técnico/cliente no momento do primeiro recebimento e ativação do aparelho junto à SEFAZ. Este código é obrigatório para autenticar qualquer requisição enviada à DLL.
* **Caminho da DLL:** O campo **DLL de Comunicação** deve apontar explicitamente para o arquivo fornecido pelo fabricante (ex: `sat.dll`). 


> [!warning] Conflito de Nomenclatura de DLLs
> Grande parte dos fabricantes compila suas bibliotecas utilizando exatamente o mesmo nome padrão (`sat.dll`). Para evitar sobrescritas ou carregamento de versões incorretas na memória do Windows, isole a DLL de cada cliente/fabricante em pastas distintas ou dentro do diretório do emulador correspondente (`C:\EmuladorSAT\sat.dll`).

---

## 4. Configurações de Rede e Comunicação SEFAZ

O equipamento SAT necessita de conexão constante com a internet para descarregar os cupons emitidos e atualizar chaves de segurança na SEFAZ. A interface do ERP expõe a aba **Configuração de Rede** para instanciar essas propriedades dentro do hardware.

* **Tipos de Conexão:** Suporta atribuição via `DHCP`, `IP Fixo` ou conexão baseada em servidores de `Proxy`.
* **Fluxo de Aplicação:** Ao alterar os parâmetros nesta interface, o ERP encapsula os dados em um arquivo de comandos no formato XML e invoca a função da DLL para transferir e gravar as novas diretivas de rede na memória flash do aparelho.

---

## 5. Layout e Modelos de Impressão (Extrato SAT)

O sistema disponibiliza duas metodologias para a geração e impressão do Extrato do Cupom Fiscal Eletrônico:

1. **Impressão Direta (Esc/POS):** O sistema realiza a comunicação direta via comandos de impressora térmica não fiscal na porta mapeada (ex: `COM1`, `LPT1` ou compartilhamento de rede `\\localhost\Epson`). Dispensa a necessidade de drivers complexos e acelera a velocidade de impressão.
2. **Impressão via Gerador de Relatórios:** O fluxo consome as tags do XML retornado pelo SAT e popula um layout customizado desenvolvido na ferramenta interna de relatórios do ERP. Permite edições visuais sofisticadas e adição de logos personalizadas da empresa.

---

## 6. Painel de Comandos e Diagnósticos Técnicos

A aba de comandos serve como console de gerência técnica para testes de conectividade e validação do fluxo fiscal de ponta a ponta.

### Principais Ações do Console
* **Inicializar SAT:** Carrega a DLL na memória e valida o handshake inicial com a porta lógica do equipamento.
* **Consultar SAT:** Envia um sinal de *ping* ao aparelho para checar se ele responde aos comandos básicos e se o Código de Ativação fornecido confere.
* **Status Operacional:** Retorna um diagnóstico em tempo real exibindo o nível de armazenamento interno, quantidade de cupons pendentes de transmissão, estado da bateria interna e se o aparelho encontra-se bloqueado pelo fisco.
* **Enviar Teste de Emissão:** Gera um payload XML fictício baseado em dados de teste e força um ciclo completo de venda.

```sql
-- Exemplo conceitual para consulta de logs de transmissão interna
SELECT id_venda, chave_acesso_sat, status_retorno 
FROM log_transmissao_sat 
WHERE data_emissao = CURRENT_DATE;
````

> [!tip] Diagnóstico Rápido de Suporte Quando o cliente reportar erro de rejeição de cupons, utilize o botão **Status Operacional**. Se o retorno exibir os logs estruturados na caixa de texto do console com a tag `<status> Conectado / Ativo`, a falha está restrita a dados cadastrais do produto (ex: CFOP, NCM, Alíquota de ICMS incorreta) e não na comunicação física com o hardware.
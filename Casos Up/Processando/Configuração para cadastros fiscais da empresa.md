---
id: CASO-034
link: https://www.youtube.com/watch?v=Jb2_Tun9Zpw&t=13s
setor: Suporte, Implantação, Faturamento
modulo: Configurações Fiscais da Empresa
tags:
  - certificado-digital
  - nfce
  - nfe
  - sefaz
  - contingencia
data_criacao: 2026-06-24
---

# Documentação Técnica: Infraestrutura Fiscal, Certificado Digital e Parâmetros de Mensageria

Esta documentação provê os requisitos lógicos, parametrizações de diretórios, criptografia de dados e arquitetura de contingência para a validação fiscal das notas eletrônicas ([[NF-e]], [[NFC-e]], [[MDF-e]], [[CT-e]]) no núcleo de retaguarda do ERP.

---

## Sumário
1. [[#1. Configuração Cadastral Core e Dados do Contador]]
2. [[#2. Instanciação e Modos do Certificado Digital]]
3. [[#3. Arquitetura de Pastas e Mensageria Eletrônica (Webservices)]]
4. [[#4. Fluxo de Contingência e Emissão Offline da NFC-e]]
5. [[#5. Token CSC e Sequenciamento de Numeração Inicial]]
6. [[#6. SMTP de Notificação de XML e Validação Restrita de Estoque]]

---

## 1. Configuração Cadastral Core e Dados do Contador

As informações cadastrais primárias da empresa funcionam como chaves de validação primordiais nos nós dos arquivos XML gerados pelo sistema.

* **Acesso:** **Ficha Cadastral da Empresa**.
* **Campos Mandatórios:** CNPJ, Razão Social, Inscrição Estadual (IE), Inscrição Municipal (IM) e Endereço Logradouro completo.
* **Aba SPED/SINTEGRA:** Centraliza o registro cadastral dos dados do Contador (Nome, CPF, Registro CRC, Telefone e Endereço). Essas tags são injetadas de forma automática na exportação de arquivos fiscais mensais de escrituração do estabelecimento.

---

## 2. Instanciação e Modos do Certificado Digital

A assinatura dos documentos e o handshake com a SEFAZ exigem a parametrização do Certificado Digital. O sistema expõe duas metodologias para a leitura da chave criptográfica:

			[ Instanciação do Certificado ] 
						| 
		{ Escolha do Modelo de Armazenamento }
		/ 
									\
(Modelo A1 via Arquivo .PFX) 
								(Modelo A1/A3 via Windows) 
	/ 
 Aponta Caminho do Arquivo Físico ]										\
											[ Abre Repositorio Windows (Capicom) ]
			|												                                                  |								
[ Informa Senha de Criptografia ]                                       [ Captura Serial de Forma Automática ]
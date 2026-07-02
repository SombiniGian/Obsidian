---
id: CASO-004
link: https://www.youtube.com/watch?v=wxQE6ZDhXg8&t=2s
setor: Suporte, Implantação, Infraestrutura
modulo: Configurações de Sistema
tags:
  - arquivo-ini
  - banco-de-dados
  - pdv
  - firebird
  - suporte-tecnico
data_criacao: 2026-06-24
---

# Documentação Técnica: Arquivo de Inicialização (off.ini) e Modos de Operação

Esta documentação provê as diretrizes técnicas de infraestrutura e segurança sobre o arquivo de inicialização local do ERP (`off.ini`), descrevendo os fluxos de conexão ao banco de dados, os modos de comportamento das estações de trabalho e os protocolos de contingência do suporte técnico.

---

## Sumário
1. [[#1. Estrutura e Localização do Arquivo off.ini]]
2. [[#2. Fluxos de Instalação e Conexão Inicial]]
3. [[#3. Tipos de Estação (Modos de Operação)]]
4. [[#4. Protocolo de Segurança: Acesso de Suporte Técnico]]

---

## 1. Estrutura e Localização do Arquivo off.ini

O comportamento inicial do executável do ERP é governado por um arquivo de configuração estruturado em formato texto, localizado obrigatoriamente no diretório raiz de instalação do sistema.

* **Nome do Arquivo:** `off.ini`
* **Função Básica:** Armazenar os ponteiros físicos e lógicos que o executável necessita para instanciar a camada de persistência e definir o layout de tela inicial.

### Parâmetros Internos Fundamentais
* **Caminho do Banco de Dados:** String de conexão que define o servidor e o path absoluto do arquivo de banco de dados (ex: `192.168.1.100:C:\Automacao\Dados\SISTEMA.FDB`).
* **Caminho da DLL do Firebird:** Aponta explicitamente o driver cliente do banco de dados relacional (`fbclient.dll`) utilizado na comunicação.
* **Tipo da Estação:** Flag que instrui o executável sobre qual interface deve ser renderizada pós-autenticação.

---

## 2. Fluxos de Instalação e Conexão Inicial

O comportamento do sistema durante a sua primeira execução varia de acordo com o pacote de instalação selecionado no assistente (Wizard).

						[ Inicialização do ERP ]
								|
					{ Existe o arquivo off.ini? } 
						/				\ 
					(Sim) 
									(Não) 
	[ Carrega Dados do .INI ] 
			|					                   [ Abre Interface de Configuração ] 
												| 
			| 
	[ Exibe Tela de Login ] 
								[ Técnico Digita IP e Caminho FDB ] | [ Testa Conexão Bem-Sucedida ] | [ Grava off.ini Automaticamente ] | [ Direciona para Tela de Login ]
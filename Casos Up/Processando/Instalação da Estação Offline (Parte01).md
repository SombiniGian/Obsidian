---
id: [CASO-001]
link: https://www.youtube.com/watch?v=vKl4IehI_ww
setor: Implantação
modulo: PDV Offline
tags: [pdv-offline, instalacao, sincronizacao, servidor, erp]
data_criacao: 2026-07-18
---

# Instalação e Configuração da Estação PDV Offline

## Sumário
- [[#1. Visão Geral do Processo]]
- [[#2. Pré-requisitos]]
- [[#3. Configuração no Servidor Principal]]
- [[#4. Instalação e Vínculo no Terminal (PDV)]]
- [[#5. Regras de Negócio e Validações]]
- [[#6. Manutenção e Atualização de Dados]]

## 1. Visão Geral do Processo
Este documento descreve o fluxo inicial de configuração e instalação de um terminal de vendas no modo **PDV Offline**. O processo é dividido em duas etapas principais: a liberação e parametrização do perfil da estação diretamente no servidor, e a subsequente habilitação do terminal local para se comunicar, realizar a carga inicial da empresa e operar de forma autônoma, sincronizando-se periodicamente com a retaguarda.

> [!info] Informação: Sincronizador Central
> O aplicativo responsável pela sincronização de dados entre o Servidor Central e as estações PDV Offline é o mesmo motor já utilizado para o ecossistema de "Força de Vendas". Este serviço deve estar em execução ativa no servidor para garantir a comunicação de mão dupla (recebimento de parâmetros e recepção de pacotes de vendas).

## 2. Pré-requisitos
- Acesso administrativo ao módulo de retaguarda no Servidor Central.
- O serviço de sincronização ativado e operante na rede.
- Terminal local com os binários do software instalados, pronto para a primeira inicialização.
- Endereço IP (ou DNS) e Porta de comunicação do servidor na rede local ou externa.
- **CNPJ** exato da empresa cadastrada no servidor raiz.

## 3. Configuração no Servidor Principal
Antes de realizar a ativação do PDV na máquina do cliente, é imperativo alocar e registrar a estação no servidor. Esse procedimento provisiona um perfil seguro e dedicado para a comunicação.

### Fluxo de Cadastro
1. No sistema servidor, navegue até o menu **Outras configurações** > **Estação PDV**.
2. Clique em adicionar para mapear uma nova estação e preencha os parâmetros obrigatórios:
	- **Código:** Identificador alfanumérico da estação (ex: `004`).
	- **Status:** Defina o status operacional da estação (ex: `Disponível` ou `Ativo`).
	- **Descrição:** Nomenclatura humana para fácil identificação (ex: `Caixa Quatro`).
	- **Conta Caixa / Conta Financeira:** Selecione a conta financeira destino na retaguarda. Todos os lançamentos de vendas e o fechamento do caixa deste terminal serão injetados nesta conta, seguindo a mesma arquitetura de recebimentos do módulo de [[Pedido de Venda]].
	- **Obrigatório Atualizar:** Regra de sincronização forçada das tabelas base. Pode ser configurada como `Não`, `Ao abrir novo caixa` ou `Por dia`.
	- **Série da Nota Fiscal:** A série fiscal (ex: NFC-e ou CF-e) delegada exclusivamente a este terminal.
	- **Envio Automático:** Se ativado (`Sim`), a estação transmite vendas, cupons fiscais e relatórios financeiros sem intervenção do operador, utilizando rotinas em background (Workers).
	- **Segundos para Envio:** Define o *delay* de polling ou push da sincronização automática (ex: `60` segundos).
	- **Estação Configurada:** *Atenção: Deixe este campo em branco*. Ele será injetado automaticamente pela aplicação durante o handshake do terminal.

> [!warning] Atenção: Prevenção de Colisão Fiscal
> O backend possui uma trava de segurança estrita. Se o administrador tentar vincular uma **Série da Nota Fiscal** que já encontra-se atrelada a outra Estação PDV, a transação será abortada com o erro *Série em uso na estação X*. Isso impede rejeições do tipo *Duplicidade de Numeração* na SEFAZ, garantindo que dois caixas autônomos nunca incrementem a mesma série em paralelo.

## 4. Instalação e Vínculo no Terminal (PDV)
Após o provisionamento do slot no servidor, proceda com a autenticação física da máquina cliente.

1. Execute o sistema no terminal local. Tratando-se da primeira execução (`first_run`), a interface padrão de licenciamento exigirá a configuração da base com o alerta: *"É necessário atualizar os dados da empresa para utilizar o sistema"*.
2. Ignore o formulário de cadastro manual e localize a opção **PDV offline** na interface.
3. Insira as credenciais de roteamento para a API do servidor:
	- **Caminho do Servidor:** IP ou host da máquina (ex: `192.168.0.100` ou `localhost` para laboratório).
	- **Porta:** A porta TCP/IP em que o listener do Força de Vendas está escutando.
	- **CNPJ da Empresa:** O documento fiscal primário da empresa configurada.
4. Clique no botão **Habilitar PDV offline**.
5. O terminal iniciará uma requisição HTTP/Socket para o servidor e fará a validação do CNPJ. Havendo sucesso, abrirá uma modal exibindo o array de estações previamente provisionadas no Passo 3.
6. Selecione a estação correspondente a esta máquina (ex: `Estação 4`) e clique em **Confirmar**.
7. Será exibida a interface de **Atualização de Dados**. Aqui o sistema permite orquestrar as cargas parciais de domínio (produtos, clientes, tabelas de preços, vendedores). Esta janela pode ser fechada caso a estratégia seja forçar o sync completo em outro momento.
8. Ao retornar para o painel principal da empresa, o payload inicial com razão social e diretrizes fiscais já estará populado em memória. Clique em **Salvar**.
9. O layout do PDV será montado. O terminal iniciará "limpo" (base local vazia), aguardando ou executando a sincronização assíncrona inicial de catálogos.

## 5. Regras de Negócio e Validações

### Hash de Hardware e Anti-Clonagem
No momento em que o Passo 6 (seleção da estação) é finalizado, o PDV local captura variáveis do ambiente físico do cliente (como o **Nome da Máquina** no S.O. e o **Número de Série do HD/SSD**) e faz o post desses dados de volta ao servidor, preenchendo o campo `Estação Configurada`.

> [!warning] Atenção: Integridade do PDV
> Essa chave de hardware é imutável via interface para o usuário final. Isso impede que cópias não autorizadas da pasta do sistema ou clonagens de disco permitam que dois computadores distintos iniciem sessões simultâneas operando sob a mesma `Estação`, o que geraria corrupção de sequenciamento fiscal e transações orfãs.

### Modo de Envio (Síncrono vs Assíncrono)
Se a propriedade de configuração de **Envio Automático** estiver setada como `Não`, a arquitetura do PDV desabilita os cron jobs em segundo plano. O operador de caixa deverá assumir a responsabilidade arquitetural de, ao final do expediente ou turno, acessar o módulo de gestão e clicar manualmente no botão **Enviar** para realizar o *flush* dos dados gerados para o banco mestre.

## 6. Manutenção e Atualização de Dados
Para diagnosticar a comunicação, disparar cargas manuais ou reconfigurar apontamentos no terminal offline:

1. Na interface do PDV, navegue para o menu superior **Empresa** > **Configurações do sistema**.
2. Localize e clique no botão **Configuração Offline**.
3. O painel abrirá as opções de [[Gestão de Sincronização]], permitindo visualizar as URLs do endpoint central, o timer corrente para o próximo ciclo (se automático), além de habilitar os botões de ação para puxar dicionários e enviar blocos transacionais não confirmados.

> [!tip] Dica de Suporte Técnico
> Instrua o cliente final a sempre checar o painel de **Configuração Offline** caso haja lentidão no aparecimento das vendas no ERP central. Verifique o status da porta TCP local e assegure que regras de Firewall de borda ou do Windows não estão interceptando o tráfego do sincronizador entre as máquinas.
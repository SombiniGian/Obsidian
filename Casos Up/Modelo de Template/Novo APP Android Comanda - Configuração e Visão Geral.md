---
id: CASO-001
link: https://www.youtube.com/watch?v=YyK-xFjGmlw
setor: Suporte
modulo: Aplicativo Android Comanda
tags: [comanda, app, restaurante, configuracao, regras_de_negocio, impressao]
data_criacao: 2026-07-18
---

# App Android Comanda: Configuração e Visão Geral

## Sumário
- [1. Visão Geral e Arquitetura](#1-visão-geral-e-arquitetura)
- [2. Configurações de Usuários (Vendedores)](#2-configurações-de-usuários-vendedores)
- [3. Roteamento e Hierarquia de Impressão](#3-roteamento-e-hierarquia-de-impressão)
- [4. Parâmetros Globais do Servidor](#4-parâmetros-globais-do-servidor)
- [5. Regras de Negócio e Retaguarda](#5-regras-de-negócio-e-retaguarda)
- [6. Configuração e Fluxo no Aplicativo (Frontend)](#6-configuração-e-fluxo-no-aplicativo-frontend)

---

## 1. Visão Geral e Arquitetura

O novo **Aplicativo Android Comanda** compartilha a mesma base de código do aplicativo de [[Força de Vendas]]. A interface e as funcionalidades (Varejo vs. Restaurante) são ativadas dinamicamente com base no **tipo de usuário** autenticado. 

O foco deste aplicativo é refletir fielmente as regras de negócio já estabelecidas no sistema de [[Retaguarda]], eliminando inconsistências entre o ERP e a operação móvel.

---

## 2. Configurações de Usuários (Vendedores)

A criação do perfil do funcionário determina seu nível de acesso e comportamento dentro do app.

- **Tipos de Usuário Suportados:** Garçom, Vendedor, Administrador, Transportador (para controle de entregas).
- **Restrição de Exclusão:** Existe a flag `Não excluir item` no cadastro do vendedor.
  
> [!warning] Atenção: Permissão de Exclusão
> Se a opção **Não excluir item** estiver marcada, o garçom conseguirá lançar os produtos, mas será bloqueado caso tente cancelar ou remover um item da comanda após o envio. Para liberar exclusões diretamente pelo app, esta flag deve permanecer desmarcada.

---

## 3. Roteamento e Hierarquia de Impressão

O sistema de impressão para o fluxo de restaurante opera em uma arquitetura de fallback em duas camadas, permitindo adaptações para estabelecimentos complexos (ex: múltiplos andares).

### Configuração por Setor (Padrão)
Cada produto é vinculado a um **Setor** (ex: Cozinha, Bar). No cadastro do setor, define-se uma impressora. Qualquer pedido deste produto será encaminhado automaticamente para a impressora do setor correspondente.

### Configuração por Vendedor (Exceção/Preferencial)
É possível atrelar uma **Impressora Preferencial** diretamente ao cadastro do Vendedor/Garçom.

> [!info] Fluxo de Decisão do Sistema (Roteamento de Impressão)
> 1. O sistema verifica se o **Vendedor** possui uma impressora preferencial configurada.
> 2. **Se sim:** O pedido é impresso na impressora do Vendedor, ignorando a impressora do setor.
> 3. **Se não:** O pedido é impresso na impressora definida no **Setor** do produto.
> 
> *Caso de uso:* Um restaurante com dois andares. O garçom do 2º andar tira uma cerveja de um freezer local, enquanto o garçom do 1º andar pede da copa. A impressora do vendedor garante que a ficha saia na praça correta para o mesmo produto.

---

## 4. Parâmetros Globais do Servidor

As configurações do servidor de terminais ditam o comportamento geral de auditoria e segurança de interface:

- **Impressora Padrão para Conferência:** Utilizada quando o operador clica no botão **Encerrar** no app, gerando o extrato (PDF/Cupom) para entrega na mesa.
- **Ficha de Alteração e Cancelamento:** Permite configurar a impressão de alertas automáticos nos setores produtivos caso o garçom altere uma observação de um pedido já enviado ou faça a exclusão de um item.
- **Sempre Usar Câmera:**
  - Se ativada: Desabilita o teclado para digitação do número da mesa/comanda no app.
  - O garçom é obrigado a utilizar o leitor de código de barras pela câmera.
  - *Objetivo:* Evitar falhas operacionais e lançamentos em comandas de clientes incorretos.

---

## 5. Regras de Negócio e Retaguarda

Diferente da versão anterior, o novo app é 100% acoplado às travas de segurança configuradas na [[Retaguarda]]. Se uma ação não é permitida no caixa desktop, não será no app.

### Controle de Estruturas
No sistema, o administrador deve definir os modelos operacionais:
1. Usar apenas **Mesas**.
2. Usar apenas **Comandas**.
3. Usar **Mesas e Comandas** simultaneamente.
4. Aceitar várias comandas na mesma mesa.

### Bloqueio de Ingressos
> [!warning] Ponto de Falha Crítico: "Obrigar Ingresso"
> Se a flag **Obrigar Ingresso** estiver ativada na retaguarda (comum em boates e casas de show), o aplicativo **bloqueará a abertura de novas comandas**. 
> O pedido só poderá ser lançado no app após a comanda ser iniciada fisicamente através do módulo de [[Controle de Portaria / Entrada]].

---

## 6. Configuração e Fluxo no Aplicativo (Frontend)

### Conexão e Sincronização
Para conectar o app ao servidor:
1. Acesse **Configurações** na tela inicial do app.
2. Insira o **IP do Servidor** local e a **Porta** (ex: `8080`).
3. Clique em **Salvar** para resgatar as configurações do servidor.

```json
// Exemplo conceitual de payload de conexão
{
  "ip_local_servidor": "192.168.0.10",
  "porta_comunicacao": 8080,
  "usuario_id": "GARCOM_01"
}
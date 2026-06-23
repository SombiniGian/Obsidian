---
id: CASO-001
link: https://www.youtube.com/watch?v=d-bBrW8SH9o
setor: Suporte, Desenvolvimento, Implantação
modulo: Ordem de Serviço (OS)
tags: [configuracao_os, fluxo_de_trabalho, manutencao, faturamento]
data_criacao: 2026-06-23
---

# Documentação Técnica: Módulo de Ordem de Serviço (OS)

## Sumário
- [[#1. Estrutura e Cadastros Base]]
- [[#2. Configurações e Parametrizações Globais]]
- [[#3. Fluxo de Execução da Ordem de Serviço]]
- [[#4. Histórico, Comissões e Auditoria]]
- [[#5. Comportamentos Esperados e Pontos de Falha]]

---

## 1. Estrutura e Cadastros Base

O funcionamento do módulo de **Ordem de Serviço (OS)** é sustentado por três cadastros primários obrigatórios, os quais definem o comportamento das variáveis no momento da abertura do atendimento.

### 1.1 Tipos de Equipamentos
Define o nicho de atuação e as propriedades dinâmicas que o sistema exigirá. É nesta seção que são parametrizados os campos específicos (metadados) para cada modalidade de serviço.
- **Exemplos de aplicação:** - Oficina Mecânica: Configuração de campos como **Placa**, **Modelo**, **Chassi**.
  - Assistência de Celulares: Configuração de campos como **Modelo**, **IMEI**, **Operadora**.
- **Regra de Vínculo:** É possível parametrizar se o equipamento deve se associar obrigatoriamente a um cliente específico (ex: um veículo que sempre pertence ao mesmo proprietário) ou se operará de forma independente.

### 1.2 Equipamentos
Consiste no registro físico do item que receberá a manutenção. 
- O sistema permite vincular dados proprietários fixos como **Marca** e **Cliente**.
- > [!info] Flexibilidade de Registro
  > O cadastro prévio do equipamento no banco de dados não é mandatório por padrão, dependendo estritamente das diretrizes de governança configuradas na OS (ver seção de parametrização).

### 1.3 Situações (Status)
As situações determinam os estágios do fluxo de trabalho (*workflow*) pelos quais a OS tramitará dentro da empresa (ex: `Aguardando`, `Em Trabalho`, `Manutenção`, `Cancelada`, `Faturada`).
- **Customização Gráfica:** Permite definir cores específicas para cada status para facilitar a identificação visual na grade de registros.
- **Automação de Impressão:** Cada situação pode ser vinculada a um layout específico do gerador de relatórios. O sistema permite disparar a impressão de relatórios de forma automatizada sempre que a OS atingir determinado status.

---

## 2. Configurações e Parametrizações Globais

O comportamento operacional do módulo é gerenciado através do painel de parametrização do sistema (acessível por usuários com perfil de **Administrador**). Estas configurações determinam o nível de rigidez do processo operacional.

| Parâmetro / Campo | Descrição Funcional |
| :--- | :--- |
| **Natureza da Operação** | Define o padrão fiscal/operacional que será associado automaticamente à OS. |
| **Classificação** | Permite categorizar as OSs para priorização (ex: `Urgente`, `Prazo Maior`, etc.). |
| **Impressão Padrão** | Relatório base utilizado para saídas físicas quando não houver automação por status. |
| **Situações Padrão** | Define os status automáticos para as ações de: **Incluir**, **Faturar**, **Entregar** e **Cancelar**. |
| **Obrigar Cadastrar Equipamento** | Se ativado (`True`), bloqueia a digitação livre do item na OS, exigindo que ele exista no cadastro de Equipamentos. |
| **Obrigar Cadastrar Defeito** | Se ativado (`True`), força a seleção de um defeito pré-cadastrado no banco de dados. |
| **Imprimir Automaticamente** | Habilita o disparo do popup/impressão assim que ocorre a transição de status. |
| **Abrir Situação ao Incluir OS** | Força a exibição de uma tela de triagem inicial ao criar o documento. |

> [!warning] Impacto de Dados: Digitação Livre vs. Cadastro Estrito
> Permitir a digitação livre do equipamento ou defeito reduz o tempo de abertura da OS, porém gera inconsistências no banco de dados devido a erros de digitação (espaços extras, grafias incorretas). Ativar a obrigatoriedade dos cadastros garante a integridade referencial e precisão em relatórios analíticos futuros.

---

## 3. Fluxo de Execução da Ordem de Serviço

O ciclo de vida padrão de uma Ordem de Serviço compreende as etapas de abertura, execução técnica e encerramento financeiro.

### Passo 1: Abertura e Triagem Inicial
Ao clicar em **Incluir**, se o parâmetro "Abrir Situação ao Incluir OS
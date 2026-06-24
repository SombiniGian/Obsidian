---
id: CASO-UP-CONFIG-002
link: https://www.youtube.com/watch?v=2Qvk8hKJW20
setor: Suporte, Desenvolvimento, Implantação
modulo: Configurações Básicas, Cadastros Gerais
tags:
  - up-system
  - grid-personalizacao
  - auditoria-logs
  - relatorios-dinamicos
  - cadastro-unificado
data_criacao: 2026-06-24
---

# Personalização Avançada de Grids, Leiautes e Trilha de Auditoria

Este documento técnico detalha as diretrizes de funcionamento, customização de interface visual e mecanismos de segurança por auditoria do ERP da Código UP Sistemas. O sistema possui arquitetura flexível que permite a manipulação dinâmica de grades de dados (*grids*) e centralização cadastral para otimização de processos de negócio.

---

## Sumário
1. [[#1. Cadastro Unificado de Pessoas]]
2. [[#2. Mecanismo de Auditoria e Logs de Registros]]
3. [[#3. Customização e Engenharia de Grids]]
4. [[#4. Geração de Relatórios e Exportação Dinâmica]]
5. [[#5. Matriz de Permissões de Leiautes]]

---

## 1. Cadastro Unificado de Pessoas

O sistema utiliza o conceito de entidade unificada para o registro de indivíduos e organizações, mitigando a redundância de dados estruturais no banco de dados.

### 1.1 Fluxo de Funcionamento e Regras de Negócio
* **Entidade Única:** Uma mesma pessoa física ou jurídica pode desempenhar múltiplos papéis operacionais simultaneamente (ex: ser cliente, fornecedor e vendedor).
* **Alternância Interativa de Abas:** A ativação de marcadores específicos na interface expõe dinamicamente abas com campos parametrizados para cada perfil.

> [!info] Vantagem Arquitetural
> Evita-se a duplicidade de chaves primárias e registros financeiros dispersos. Se um **Vendedor** realiza uma compra na empresa, basta ativar a flag **Cliente** em seu cadastro existente. Isso unifica seu histórico de Contas a Receber e faturamento sob o mesmo ID relacional.

---

## 2. Mecanismo de Auditoria e Logs de Registros

A camada de persistência de dados do sistema conta com uma esteira de auditoria imutável integrada por padrão a todas as tabelas e telas do ecossistema (Pessoas, Produtos, Pedidos, Financeiro).

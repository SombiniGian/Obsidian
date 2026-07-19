---
id: [CASO-164]
link: https://www.youtube.com/watch?v=o7_GxaBdExA
setor: [Suporte, Implementação, Operacional]
modulo: [Configurações Globais / Interface Geral]
tags: [personalizacao-grade, campos-extras, salvar-filtros, gerador-de-relatorios, auditoria]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral dos Componentes Globais]]
2. [[#Mecanismo de Auditoria e Controle de Alterações]]
3. [[#Controle de Impressões e Disparos Multicanal (E-mail e WhatsApp)]]
4. [[#Injeção Dinâmica de Campos Extras (Campos Personalizados)]]
5. [[#Otimização de Performance e Governança (Salvar Filtros)]]
6. [[#Customização Avançada de Layouts de Grades (Grids)]]
7. [[#Pontos Críticos e Regras de Negócio]]

# Visão Geral dos Componentes Globais
O sistema é estruturado sob um modelo de arquitetura padronizada de componentes visuais e operacionais. Isso significa que as ferramentas de manipulação de dados, auditoria, exportação e filtragem estão presentes de maneira idêntica em todas as janelas de listagem do software (ex: cadastro de clientes, produtos, notas fiscais, pedidos de venda ou ordens de serviço). Esse paralelismo acelera a curva de aprendizado da revenda e confere ao sistema alto poder de customização em tempo de execução.

# Mecanismo de Auditoria e Controle de Alterações
O botão **Auditoria** realiza o rastreamento cronológico detalhado de todas as operações de mutação de dados efetuadas sobre um registro específico (Quem criou, quem alterou, qual campo foi modificado, o valor anterior e o novo valor).

> [!tip] Auditoria Comparativa Simultânea
> Embora o cadastro interno de cada entidade possua uma aba de auditoria, o acionamento do botão **Auditoria** localizado no menu externo de opções permite abrir múltiplas janelas de logs simultâneas na tela. O analista ou gestor pode, por exemplo, abrir e arrastar lado a lado o histórico de alterações de dois produtos distintos ou de duas notas fiscais para fins de conciliação e perícia de dados.

# Controle de Impressões e Disparos Multicanal (E-mail e WhatsApp)
A emissão de relatórios e faturamentos é gerida de forma unificada através do **Controle de Impressões**, que interage diretamente com o gerador de relatórios do ERP (desenvolvido em FastReport).

---
id: [CASO-059]
link: https://www.youtube.com/watch?v=p5XTDAnIiro
setor: [Suporte, Desenvolvimento, Implantação]
modulo: [Impressões]
tags:
  - controle-impressoes
  - gerador-relatorios
  - customizacao-layouts
  - passagem-parametros
data_criacao: 2026-06-24
---

# Controle e Centralização de Impressões por Tela do Sistema

Este documento técnico descreve as regras de negócio, a arquitetura de dados e o fluxo de parametrização da ferramenta global de **Controle de Impressões**. O recurso permite vincular layouts customizados do gerador de relatórios a qualquer interface de cadastro ou movimentação do ERP (Clientes, Ordens de Serviço, Pedidos, Notas Fiscais, etc.), mapeando filtros por chaves primárias e permissões por operador.

---

## Sumário
1. [[#Conceito e Lógica de Funcionamento]]
2. [[#Vinculação de Relatórios às Interfaces]]
3. [[#Passagem Genérica de Parâmetros (ID)]]
4. [[#Controle de Acesso por Operador]]
5. [[#Pontos Críticos e Validações]]

---

## Conceito e Lógica de Funcionamento

O módulo de Controle de Impressões foi concebido para conceder autonomia total às revendas e administradores de TI na criação e entrega de relatórios e fichas customizadas. 

Anteriormente restrito a layouts engessados por tela, o ecossistema agora intercepta o gatilho do botão **Imprimir** de qualquer formulário e renderiza uma lista flutuante contendo os templates previamente assinados e compatíveis com aquele contexto específico.

### Casos de Uso Comuns:
* **Cadastro de Clientes:** Emissão de uma ficha cadastral formatada para assinatura ou colheita de dados com foto.
* **Ordem de Serviço (OS):** Emissão de uma via simplificada de "Entrada de OS" (sem exibição de valores fiscais ou de peças) e outra via detalhada de "Saída de OS" (com precificação final e termos de garantia).
* **Movimentações Comerciais:** Customização de espelhos de pedidos de venda ou faturamento de notas de acordo com as exigências visuais de cada segmento de cliente.

---

## Vinculação de Relatórios às Interfaces

Para disponibilizar um layout de impressão em uma tela de movimento ou cadastro, deve-se realizar a associação direta no painel gerencial.

* **Caminho de Acesso:** Botão/Menu **Controle Impressões** contido na barra de ferramentas da tela que receberá os relatórios.

### Fluxo de Associação:
1. Acesse o formulário desejado (ex: tela de **Ordem de Serviço**) e clique em **Controle Impressões**.
2. Clique no comando **Incluir**.
3. O sistema abrirá uma listagem exibindo todos os relatórios desenvolvidos e compilados na central do **Gerador de Relatórios**.
4. Selecione o template desejado (ex: `OS - Entrada Simples`) e confirme.
5. Repita o processo caso pretenda assinar múltiplos layouts para a mesma tela (ex: adicionar também o layout `OS - Saída Completa`).

---

## Passagem Genérica de Parâmetros (ID)

Para garantir que o gerador renderize as informações exclusivas do registro selecionado em tela (e não a listagem total do banco de dados), a aplicação adota uma diretriz de passagem de chaves via parâmetro dinâmico.

> [!info] A Regra do Parâmetro ID
> Independentemente da tela onde o gatilho de impressão for acionado, o ERP injetará automaticamente o valor numérico da chave primária do registro ativo para dentro de uma variável global padrão denominada obrigatoriamente como `ID`.

┌────────────────────────┐ Injeção de Parâmetro
┌────────────────────────┐ 
│ Formulário do ERP │ ───────────────────────────────> │ Gerador de Relatórios │ 
│ (Ex: OS Selecionada) │ Variável Global: "ID" │ (Filtro: ID_OS = :ID) 
│ └────────────────────────┘ └────────────────────────┘

 Configuração no Gerador de Relatórios: * Ao estruturar a consulta SQL no dataset do relatório customizado, o desenvolvedor da revenda deve capturar e tratar este parâmetro nativo. * A cláusula de filtragem da query (`WHERE`) deve conter a sintaxe direcionada ao ID dinâmico. Por exemplo: ```sql SELECT * FROM ordens_servico WHERE id_os = :id

## Controle de Acesso por Operador

O Controle de Impressões atua também como uma camada de segurança e governança de dados da empresa, permitindo restringir quais colaboradores possuem privilégios para gerar determinados layouts.

> [!tip] Restrição por Perfil Durante o vínculo do relatório no painel de controle, utilize o campo **Usuário**. Se associado a um operador específico, o relatório em questão ficará visível e disponível para emissão estritamente sob as credenciais daquele usuário, ocultando-se dos demais colaboradores da empresa.

## Pontos Críticos e Validações

> [!warning] Validações Técnicas de Variáveis e Sintaxe SQL
> 
> 1. **Divergência na Nomenclatura do Parâmetro:** O gerador de relatórios é estritamente _case-sensitive_ e tipado em relação à variável nativa de controle. Se o desenvolvedor configurar a query utilizando termos alternativos (como `:id_os`, `:codigo` ou `:ID_OS`), o mecanismo de integração do ERP não reconhecerá a instrução e o relatório falhará no processamento ou trará uma listagem em branco por ausência de dados. Mantenha estritamente o termo `:id`.
>     
> 2. **Processamento em Lote:** Quando o usuário clica no comando geral de impressão e confirma múltiplos layouts simultaneamente na caixa de seleção, o sistema gera sessões de visualização/impressão apartadas e consecutivas em tela, demandando atenção do operador em relação ao consumo de hardware e impressoras de destino.
>

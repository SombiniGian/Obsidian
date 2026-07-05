## 📜 DIRETRIZES PARA AGENTES DE IA

Este repositório deve ser executado por agentes de IA seguindo estas diretrizes rígidas:

### ✅ O QUE FAZER (MANTIDO CONFORME DISCUSSÃO)

1. **Preservar intencionalmente a sintaxe Obsidian:**
   - Manter `![](images/...)` para imagens (não converter para HTML)
   - Manter links do tipo `[[c]](#cmnt3)` se forem intencionais do fluxo de trabalho da equipe
   - Manter links internos do tipo `[[Nome do Documento]]` que forem parte do sistema de navegação

2. **Preservar terminologia em português:**
   - Manter siglas como: NF-e, NFC-e, SAT, MFE, CST, CSOSN, CFOP, etc.
   - Manter termos técnicos em português quando forem padrão do domínio
   - Não traduzir termos que são comumente usados em inglês no contexto brasileiro de ERP/fiscal

3. **Manter foco em usabilidade para RAG:**
   - Criar documentos com tema único e bem definido
   - Evitar misturar conceitos não relacionados no mesmo documento
   - Usar headings claros e descritivos que facilitam o chunking

4. **Aplicar melhorias de formatação universalmente úteis:**
   - Padronizar hierarquia de markdown (`###`, `####`, `#####`)
   - Limpar URLs com parâmetros de rastreamento desnecessários
   - Padronizar estilo de listas (escolher `-` ou `*` e aplicar consistentemente)
   - Adicionar navegação e sumários onde melhoram a usabilidade

### ❌ O QUE NÃO FAZER (EVITAR ALUCINAÇÕES)

1. **Não inventar regras ou requisitos:**
   - Não impor padrões de formatação que não foram discutidos
   - Não mudar terminologia estabelecida pela equipe
   - Não remover sintaxe Obsidian intencional sob presumo de "melhoria"

2. **Não alterar conteúdo substancial:**
   - Não reescrever explicações técnicas
   - Não adicionar informações que não estavam no documento original
   - Não interpretar ou "corrigir" conteúdo técnico baseado em conhecimento externo

3. **Não mudar a estrutura sem validação:**
   - Não criar novas pastas ou arquivos além do plano aprovado
   - Não mover conteúdo entre categorias sem clara justificativa no documento original

4. **Não presumir conhecimento de domínio:**
   - Se houver dúvida sobre se um termo deve ser mantido em português ou traduzido, manter o original do documento
   - Se houver dúvida sobre se uma sintaxe é intencional, preservá-la e marcar para revisão humana

### 🔧 COMO TRABALHAR

1. **Trabalhar incrementalmente:** Concluir cada sprint antes de passar para a próxima
2. **Validar continuamente:** Após cada tarefa, verificar se o critério de aceitação foi atendido
3. **Documentar decisões:** Quando houver ambiguidade, registrar a decisão tomada para revisão
4. **Preservar o original:** Nunca modificar o documento original; trabalhar em cópias ou novos arquivos
5. **Focar na executabilidade:** Cada tarefa deve ser clara o suficiente para ser executada sem interpretação subjetiva

---

## 📌REGRAS

1. **Respeito ao trabalho humano:** Este plano foi criado com base explícita nas discussões anteriores sobre o que é intencional (sintaxe Obsidian, terminologia) versus o que pode ser melhorado (formatação, links do YouTube, estrutura).

2. **Abordagem conservadora:** Quando houver dúvida sobre se algo é intencional ou não, a presunção será a favor de preservar o estado atual - cabe à equipe humana revisar e decidir posteriormente.

3. **Compatibilidade total:** O documento original permanece intocável para referência histórica. Todo o trabalho é feito em novos arquivos ou cópias.

4. **Prontidão para RAG:** A estrutura resultante é otimizada para sistemas de Recuperação Augmentada por Geração (RAG) através de:
   - Chunks menores e mais focados
   - Menos ruído por documento
   - Melhor sinal-ruído para recuperação de informações específicas
   - Metadados implícitos na estrutura de pastas e nomes de arquivos

5. **Escalabilidade futura:** A estrutura permite fácil expansão com novos tópicos sem reorganização major.

---

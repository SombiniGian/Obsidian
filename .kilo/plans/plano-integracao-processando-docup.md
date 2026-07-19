# Prompt de implementação + plano de referência

> **Uso:** copiar a **Seção A** inteira e colar como `user_query` em uma nova sessão Grok no vault  
> `D:\Projetos\DocUpSystem\Obsidian`  
> **Seção B** é o plano de análise (referência detalhada). O agente de implementação deve seguir a Seção A e consultar a Seção B / paths do vault.

---

## Seção A — Prompt pronto para colar (implementação ponta a ponta)

```markdown
# Missão: Implementar integração Processando → Documentação Técnica Código Up

## Papel
Você é o orquestrador de implementação de documentação neste vault Obsidian (ERP UpSystem / Código Up).
Execute a integração **ponta a ponta** dos vídeos processados em staging na documentação **oficial e canônica**.

Você **DEVE** orquestrar **subagentes** (explore / general-purpose / plan conforme necessário) para paralelizar leitura, diffs, merges por cluster e verificação. Você (orquestrador) consolida, resolve conflitos de fronteira e faz a governança final de índices.

## Objetivo
Integrar o conhecimento de:

`D:\Projetos\DocUpSystem\Obsidian\Casos Up\Processando\` (~103 `.md`)

na documentação oficial:

`D:\Projetos\DocUpSystem\Obsidian\Documentação Técnica Código Up\`

sem inventar fatos do ERP, sem merge cego de truncados, sem sobrescrever trabalho oficial sem delta material.

## Plano de especificação (fonte da verdade das decisões)

1. **Primeiro passo obrigatório:** se ainda não existir, copiar/garantir o plano de análise em:
   `D:\Projetos\DocUpSystem\Obsidian\.kilo\plans\plano-integracao-processando-docup.md`
   - Se o arquivo não existir no vault, ele deve ser recuperado do plano da sessão de análise (ou reconstituído a partir da matriz/decisões abaixo + leitura do vault). Não improvise decisões que contradigam a matriz.

2. Ler e obedecer integralmente:
   - Esse plano (matriz 103 itens, NOVOs 047–058, HOLDs, merges por DOCUP, sprints)
   - `D:\Projetos\DocUpSystem\Obsidian\AGENTS.md`
   - `D:\Projetos\DocUpSystem\Obsidian\Modelo de Template\doc-tecnico.md`
   - `D:\Projetos\DocUpSystem\Obsidian\Documentação Técnica Código Up\00_SUMÁRIO_E_INDÍCES\00.3_MAPA_INTEGRACAO_CASOS_UP.md`
   - `D:\Projetos\DocUpSystem\Obsidian\Documentação Técnica Código Up\MAPA_SINONIMOS_TAGS.md`
   - `00.1_SUMÁRIO_GERAL.md` e `00.2_GLOSSÁRIO_DE_TERMOS.md`

## Restrições inegociáveis
1. **Zero invenção** de regras, menus, campos ou erros do ERP. Só o que estiver em Processando e/ou DOCUP oficial.
2. **Não modificar** arquivos em `Casos Up\Processando\` (staging permanece como histórico; não apagar).
3. **HOLD_REVISAO** da matriz: **não integrar** até reprocessamento humano — no máximo registrar no mapa 00.3 como pendente.
4. **MISMATCH nome×conteúdo:** integrar pelo **conteúdo real** (ex.: “Movimentação de Consignado” = NFS-e → DOCUP-052, **nunca** DOCUP-027).
5. **Delta material obrigatório** em MERGE: se o oficial já cobre, SKIP; não reformular por reformular.
6. Em conflito factual: **oficial prevalece**; se Processando contradiz sem resolução → não copiar o trecho; anotar no mapa.
7. Preservar sintaxe Obsidian `![](images/...)`, wikilinks `[[...]]`, termos fiscais PT (NF-e, NFC-e, SAT, CST, CSOSN, CFOP, SEFAZ, NFS-e…).
8. Tags só canônicas via `MAPA_SINONIMOS_TAGS.md` (estender o mapa se criar tags novas listadas no plano).
9. `fontes:` com `tipo: video`, `video_id`, `url`, `titulo` no YAML dos DOCUPs tocados.
10. Chave estável no mapa: **`filename` + `video_id`** (IDs `CASO-001` colidem — não confiar só no CASO).
11. Não engordar `02.3_VENDAS_PDV` (DOCUP-009) com restaurante full / hotelaria / portaria — usar NOVOs do plano.
12. Imagens: só copiar de `Processando\Imagens Documentação\` para `Documentação Técnica Código Up\images\` se forem essenciais ao passo; nomear sem sobrescrever (`image141+`); senão omitir.

## Orquestração obrigatória por subagentes

Trabalhe como **orquestrador**. Não faça tudo em série sozinho se puder paralelizar com segurança.

### Fase 0 — Bootstrap (orquestrador)
- Garantir plano em `.kilo/plans/plano-integracao-processando-docup.md`
- Inventariar Processando (103) e DOCUPs oficiais; confirmar próximo ID livre (deve ser **DOCUP-047** se 046 existe)
- Criar TODO de sprints 5B→5H (pular 5A HOLD, só registrar)

### Fase 1 — Subagentes de preparação (paralelo, read-only)
Spawn **explore** (ou general-purpose read-only) em paralelo:
- **A:** listar HOLD/SKIP/MISMATCH da matriz e validar com amostragem de arquivos
- **B:** ler DOCUPs alvos dos merges P0 (003,004,007,008,009,011,014,016,017,018,025,034,035,036,037,041,042,045,046…) e resumir seções onde o delta deve entrar
- **C:** validar template frontmatter + exemplos de `fontes` existentes

Consolide no orquestrador antes de escrever.

### Fase 2 — Implementação por sprints (write), com subagentes por cluster

Para **cada sprint**, spawn 1+ subagentes **general-purpose** (ou write-capable) com prompt fechado contendo:
- lista exata de `processando_file` → `docup_alvo` / decisão
- paths absolutos
- o que **não** copiar
- formato de seção de merge:

```markdown
## Origem: vídeo — {Título amigável}

> Fonte: [YouTube](url) · arquivo: `{filename}` · video_id: `{id}`

### {Subtema do delta}
...somente delta factual...
```

**Sprints (ordem):**

| Sprint | Foco | Paralelo seguro |
|--------|------|-----------------|
| **5B** | Merges P0 cadastros/financeiro/PDV base: 007,008,009(parcial),011,036,037,018,003,004,014 + fontes #004-006,#014-016,#019,#022,#026,#028,#036,#055,#059,#067,#079,#101 | Subagentes em **arquivos DOCUP distintos** em paralelo |
| **5C** | Transporte/SAT/contingência/carga: 041,004(SAT),042,025 + #020,#023,#037-dicas,#041,#042cte,#051,#052-mismatch-contig,#060,#068,#077,#008,#009-carga | Paralelo por DOCUP |
| **5D** | Offline/OS/estoque/conversão/migração/TEF: 017,016,035,020,024,019,046,009(TEF) | Paralelo por DOCUP |
| **5E** | **NOVOs** 052 NFS-e, 051 Plano Contas/DRE, 054 Ativação, 058 NFC-e Futuro RS | 1 subagente por NOVO (paralelo) |
| **5F** | **NOVOs** 047 Restaurante, 048 Apps Android | 2 subagentes paralelos |
| **5G** | **NOVOs** 049 Hotelaria, 050 Portaria, 053 iMendes/Scanntech, 056 Impressões, 057 Frete | Paralelo; Hotelaria: **não** resolver contradição consumo — omitir trecho conflituoso e anotar |
| **5H** | Governança: 00.1, 00.2 (só termos literais), 00.3 (histórico Sprint 5 + mapa filename→DOCUP), MAPA_SINONIMOS_TAGS, auditoria wikilinks/tags | Orquestrador + 1 subagente de verificação |

**NOVOs a criar (paths do plano):**
- DOCUP-047 `02_OPERACOES_DIARIAS\02.11_MODULO_RESTAURANTE.md`
- DOCUP-048 `03_MANUTENCAO_TECNICA\03.16_APPS_ANDROID_FORCA_VENDAS_PDV.md`
- DOCUP-049 `02_OPERACOES_DIARIAS\02.12_MODULO_HOTELARIA.md`
- DOCUP-050 `02_OPERACOES_DIARIAS\02.13_PORTARIA_INGRESSOS.md`
- DOCUP-051 `02_OPERACOES_DIARIAS\02.14_PLANO_DE_CONTAS_DRE.md`
- DOCUP-052 `01_CONFIGURACAO_INICIAL\01.7_NFSE_NOTA_SERVICO.md`
- DOCUP-053 `03_MANUTENCAO_TECNICA\03.17_INTEGRACOES_IMENDES_SCANNTECH.md`
- DOCUP-054 `01_CONFIGURACAO_INICIAL\01.8_ATIVACAO_LICENCIAMENTO.md`
- DOCUP-056 `03_MANUTENCAO_TECNICA\03.18_CONTROLE_IMPRESSOES.md`
- DOCUP-057 `04_TROUBLESHOOTING_E_DICAS\04.11_FRETE_POR_REGIAO.md`
- DOCUP-058 `04_TROUBLESHOOTING_E_DICAS\04.12_NFCE_RECEBIMENTO_FUTURO_RS.md`
- DOCUP-055: **não criar** nesta leva (self-checkout como seção em 009 se delta; totem HOLD)

Cada NOVO deve usar frontmatter do template (`doc-tecnico.md`): id, setor, modulo, categoria, tags, navegacao, relacionados, aliases, resumo, fontes, data_criacao.

### Fase 3 — Verificação (subagente check / explore)
Após as sprints de escrita, spawn verificação:
1. 100% dos Processando da matriz classificados no 00.3 (integrado / skip / hold)
2. Nenhum HOLD foi mergeado
3. Grep: mismatches clássicos não foram para o DOCUP errado
   - NFS-e do arquivo Consignado **não** está em 04.6_CONSIGNADOS
   - “Entrada NFE XML…” (conteúdo entrega futura) **não** foi re-mergeado em 03.3 se zero delta
4. Tags minúsculas/hífen; sem variantes não mapeadas
5. Wikilinks dos NOVOs resolvem
6. `fontes.tipo: video` nos DOCUPs tocados que receberam vídeo
7. Contagem de arquivos oficiais coerente (46 + NOVOs criados)

Se a skill `/check-work` ou `check-work` estiver disponível, use-a ao final.

### Fase 4 — Entrega ao usuário
Responder em **português (Brasil)** com:
- Quantos MERGE / NOVO / SKIP / HOLD processados
- Lista de paths criados e paths modificados
- HOLD ainda pendentes (com video_id para reprocessar)
- Riscos remanescentes
- Trecho atualizado do histórico no 00.3

## Regras de qualidade de merge
- Preferir subseção sob H2 existente a monólito novo quando for o mesmo tema
- Remover lixo de transcrição (`googleusercontent.com/youtube_content`, `{{date}}`, fences abertas, callouts colados sem sentido)
- Não copiar sumários-só-âncora do Processando
- MULTI_SOURCE: escolher canônico; do clone só delta único
- SPLIT: repartir por tema canônico sem duplicar parágrafos inteiros em dois DOCUPs sem necessidade
- DOCUP-009 já é grande: só deltas PDV/TEF/NFC-e/self-checkout; restaurante → 047

## Fora de escopo
- Reprocessar YouTube (só listar HOLD com link)
- Apagar ou reescrever Processando
- `Casos Up\Processando4\` se existir
- Alterar regras de negócio “de cabeça”
- Commit/PR a menos que o usuário peça explicitamente no chat

## Critério de aceite global
- [ ] Plano em `.kilo/plans/`
- [ ] Todos os itens não-HOLD da matriz tratados (merge, novo, skip registrado)
- [ ] NOVOs 047–054 e 056–058 criados com template
- [ ] Índices 00.1 / 00.2 (se termos) / 00.3 / MAPA_SINONIMOS atualizados
- [ ] Zero merge de truncados da lista HOLD
- [ ] Subagentes foram usados de forma evidenciada (clusters em paralelo)
- [ ] Documentação oficial consistente para RAG e Obsidian

Comece pela Fase 0 sem pedir confirmação para iniciar. Se um NOVO de alto impacto estiver ambíguo além do plano, registre a decisão no 00.3 e siga a fronteira do plano (não trave a sprint inteira).
```

---

## Seção B — Resumo do plano de análise (referência rápida)

### Premissa
Análise 2026-07-19 sobre **103** arquivos em `Casos Up\Processando\` → **46** DOCUPs oficiais (próximo ID **047**). Sprint anterior: 4 (Aulões → 034–046).

### Contagens de decisão (ordem de grandeza)
| Classe | Qtd |
|--------|-----|
| Alimentam **NOVO** (clusters) | ~38 arquivos → 11 DOCUPs (047–054, 056–058) |
| **MERGE / SPLIT** em DOCUP existente | ~40 |
| **SKIP** | ~5–9 |
| **HOLD** | ~12 |
| **MISMATCH** graves | 6 |

### Mismatches críticos (conteúdo real)
| Filename | Conteúdo real | Destino |
|----------|---------------|---------|
| Movimentação de Consignado.md | NFS-e | DOCUP-052 (não 027) |
| PDV Novo totalmente personalizável.md | Rejeição/cert/contingência NF-e | DOCUP-042 |
| Incluir Campos Extras….md | Contingência NF-e | DOCUP-042 |
| Entrada NFE XML Manifestação….md | Entrega futura (clone vídeo 025) | SKIP |
| Exemplo White Label.md | Epson margens | DOCUP-022 |
| Config Empresa (Parte 01).md | Ativação (= clone) | SKIP; canônico Ativação → 054 |

### HOLD (não integrar)
Firebird multi (trunc), Config INI, Config Básicas P2, Integrações Pagamentos, OS base trunc, Personalização Grids, Plano Contas P1, Senha Liberação Remota, Terminal Auto Pagamento, Variações grade, White Label Config (trunc), links YT inválidos/genéricos (Carga; NFC-e offline; Plano Contas overview).

### NOVOs
047 Restaurante · 048 Android · 049 Hotelaria · 050 Portaria · 051 Plano Contas/DRE · 052 NFS-e · 053 iMendes/Scanntech · 054 Ativação · 056 Impressões · 057 Frete · 058 NFC-e Receb. Futuro RS · (055 não criar)

### Top riscos
1. Inflar DOCUP-009  
2. NFS-e em Consignados  
3. Merge de truncados  
4. Duplicar entrega futura já em 025  
5. Contradição Hotelaria consumo  
6. Mapa por CASO-id colidido  

### Path canônico do plano detalhado no vault
`D:\Projetos\DocUpSystem\Obsidian\.kilo\plans\plano-integracao-processando-docup.md`

> **Nota:** a matriz completa de 103 linhas, outlines dos NOVOs, merges por DOCUP e sprints detalhadas foram produzidas na sessão de análise. Se o arquivo longo ainda estiver só no `plan.md` da sessão Grok, a **Fase 0** da implementação deve materializá-lo no path `.kilo/plans/` **antes** dos merges (conteúdo integral da análise anterior + esta Seção A).

### O que esta “revisão de plano” entrega
- **Produto principal para o usuário:** Seção A (prompt colável).  
- **Não implementa** merges nesta sessão de planejamento.  
- Sessão futura: colar Seção A e deixar o orquestrador + subagentes executarem.

---

*Fim — prompt de implementação + âncora do plano de integração Processando → DOCUP.*


--- 

## Matriz materializada (Sprint 5)

Ver arquivo canônico: `.kilo/plans/matriz-processando-103.md` (103/103 classificados e implementados em 2026-07-19).


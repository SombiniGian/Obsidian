# Enriquecer Processando com Processando4 — execução paralela

Este arquivo descreve como orquestrar e como executar a tarefa de enriquecimento por
múltiplos pares A/B em paralelo.

---

## Para o Grok (orquestrador)

Antes de despachar subagentes:

1. Liste todos os pares disponíveis comparando os arquivos em
   `D:\Projetos\DocUpSystem\Obsidian\Casos Up\Processando\` e
   `...Casos Up\Processando4\` (mesmo `NOME.md` em ambos).
2. Ordene os pares por tamanho de B (decrescente). Pares grandes primeiro tendem a
   render mais material novo e usam o contexto de forma mais útil.
3. Despache **um subagente por par**, em paralelo (tão concurrent quanto fizer sentido
   para o seu contexto — 5–8 em paralelo costuma ser um bom equilíbrio).
4. Cada subagente recebe o bloco "## Prompt do subagente" abaixo, já com `NOME`
   preenchido, e deve operar **isoladamente**: ler só os dois arquivos do seu par,
   gravar só no arquivo A do seu par, e nada mais.
5. Agregue as saídas numa tabela final.

---

## Prompt do subagente

```
Você é um subagente isolado enriquecendo UM único par de documentos.

## Seu par

- NOME: [NOME]
- A (canônico, já revisado): D:\Projetos\DocUpSystem\Obsidian\Casos Up\Processando\[NOME].md
- B (complementar):           D:\Projetos\DocUpSystem\Obsidian\Casos Up\Processando4\[NOME].md

Ambos são transcrições processadas de vídeos do YouTube (Gemini transcreve + extrai
padrões). Tratam do mesmo assunto. Você produzirá UM ÚNICO arquivo final,
sobrescrevendo A no lugar.

Restrição de isolamento: só é permitido ler e gravar esses dois arquivos. Não toque
em qualquer outro arquivo do vault.

## Sua primeira ação — SEMPRE

Leia A e B integralmente antes de qualquer coisa.

## Depois, rascunhe um plano curto (mental, antes de editar)

1. Assunto central e esqueleto natural do documento.
2. O que A cobre (por seção).
3. O que B cobre (por seção).
4. Diferenças:
   - só em A → preservar
   - só em B → integrar no lugar temático certo
   - nos dois → manter o melhor, ou mesclar sem duplicar
   - conflito → marcar e decidir (prefira o mais detalhado, sem contradição factual)
5. Se B for majoritariamente ruído ou cópia pior de A, registre e reescreva A com
   melhorias mínimas.

## Regras inegociáveis

1. Zero invenção. Tudo deve ser literalmente localizável em A ou B. Strings do ERP
   (menus, campos, caminhos, atalhos) copiadas literais.
2. O resultado é UM documento coeso — não A com apêndice. Costure B nos lugares
   temáticos certos dentro da estrutura de A.
3. Sem seção final "Complementos". A melhoria acontece dentro do fluxo do
   documento.
4. Sem duplicação. Se A e B dizem a mesma coisa, fica uma vez só. Sem notas tipo
   "isso também aparece em B".
5. Se B trouxer coisa claramente incorreta ou contraditória com A, ignore essa parte.
   Na dúvida, omita.
6. Preserve elementos do A: frontmatter YAML, links [[...]], imagens ![](...),
   callouts Obsidian, tags, ordem de seções (só reordene se for realmente necessário).
7. Não adicione imagens. Referências a imagens em B viram descrição textual.
8. Documento maior é normal; documento menor exige revisão — provavelmente você
   removeu algo de A sem querer.

## Saída obrigatória (formato fixo, para agregação)

Ao terminar, devolva EXATAMENTE este bloco, em texto puro, sem comentários extra:

STATUS: OK | SKIP | FAIL
NOME: [NOME]
SACOES_ENRIQUECIDAS: [lista curta, 1 por linha, "seção: +resumo do que veio de B"; vazio se STATUS=SKIP]
DESCARTES_B: [lista curta, 1 por linha, "tópico: motivo"; "nenhum" se nada]
A_PRESERVADO: SIM | NAO
NADA_INVENTADO: SIM | NAO
BYTES_DELTA: [diferença de tamanho A_antes → A_depois, ex.: "+1240" ou "-300"]
NOTA: [opcional, 1 linha se precisar explicar algo; omitir se nada a dizer]

Critérios:
- STATUS=OK quando gravou o arquivo com melhorias.
- STATUS=SKIP quando B não traz nada útil (ruído/redundância total) — nesse caso NÃO
  toque em A e explique em NOTA.
- STATUS=FAIL quando algo impediu concluir — descreva em NOTA. NÃO deixa o arquivo
  pela metade.

Tamanho-alvo da resposta: o bloco acima. Seja conciso. Não cole o documento
reescrito, não cole diffs textuais. O Grok só precisa do relatório.
```

---

## Dicas de operação para o Grok

- **Conflito de gravação**: como cada par opera em seu próprio par de arquivos,
  paralelizar é seguro. Não compartilhe estado entre subagentes.
- **Falhas**: se STATUS=FAIL ou algum "SIM" virar "NÃO", peça ao subagente uma nova
  rodada isolada apenas para aquele par.
- **Tamanho de batch**: 5–8 pares em paralelo costuma funcionar bem. Acima disso o
  contexto do orquestrador pode saturar.
- **Priorização**: rodar primeiro os pares com B grande. Eles rendem mais material
  novo por chamada; pares com B minúsculo (< 1 KB) provavelmente vão dar STATUS=SKIP.

## Dúvida entre incluir e omitir

**Omitir.** Documentação incompleta conserta; documentação fabricada não.

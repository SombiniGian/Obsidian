# Matriz 103 — Processando → DOCUP (Sprint 5)

> Gerada 2026-07-19 por leitura real de conteúdo + plano. Chave estável: `filename` + `video_id`.
> HOLD por truncamento ou link YT inválido/genérico: **não integrar**.
> MISMATCH: classificar pelo **conteúdo real**.

## Legenda

| Código | Significado |
|--------|-------------|
| NOVO | Alimenta DOCUP novo (047–054, 056–058) |
| MERGE | Delta material em DOCUP existente |
| SKIP | Clone / zero delta / já coberto |
| HOLD | Truncado ou link inválido — só registrar |

## Contagens planejadas

| Classe | Qtd |
|--------|-----|
| HOLD | 14 |
| SKIP | 5 |
| NOVO (arquivos-fonte) | ~38 |
| MERGE | ~46 |
| **Total** | **103** |

---

## HOLD (14) — não mergear

| # | filename | video_id | motivo |
|---|----------|----------|--------|
| 1 | Como colocar vários Firebirds rodando na mesma máquina.md | PP45iBGkDtI | Truncado mid-doc |
| 2 | Configuração INI.md | wxQE6ZDhXg8 | Truncado |
| 3 | Configurações Básicas (Parte 2) - Personalização dos Grids e Auditoria.md | 2Qvk8hKJW20 | Truncado |
| 4 | Integrações de Pagamentos.md | 5TH97Tf5-_s | Truncado |
| 5 | Ordem de Serviço.md | d-bBrW8SH9o | Truncado (seções 3–5 faltam) |
| 6 | Personalização de Grids e outras configurações.md | o7_GxaBdExA | Truncado (~30 linhas) |
| 7 | Plano de Contas (Parte 1) - Entrada Estoque.md | 6esDjdhiSWU | Truncado |
| 8 | Senha De Liberação Remota.md | k2uTk0p-1ig | Truncado |
| 9 | Terminal de Auto Pagamento.md | owotxmsJVW8 | Truncado (totem) |
| 10 | Variações (grade) - Configurações iniciais.md | 9Tj_beHAWs0 | Truncado |
| 11 | White Label - Configurações.md | 1GcQoYImK58 | Truncado |
| 12 | Carga - Montagem, faturamento e algumas configurações.md | NO_ID | Link YT genérico/inválido |
| 13 | NFC-e - Tipo de emissão OFFLINE.md | NO_ID | Link YT genérico/inválido |
| 14 | Plano de Contas.md | NO_ID | Link YT genérico/inválido |

---

## SKIP (5)

| filename | video_id | motivo |
|----------|----------|--------|
| Configuração do Cadastro da Empresa (Parte 01).md | ZswVaygjzq8 | Clone de Ativação → canônico DOCUP-054 |
| Entrada NFE XML Manifestação Destinatário.md | LdNEwnR4Emg | Clone entrega futura (mesmo vídeo Controle de entregas) → DOCUP-025 |
| Emissão boletos a partir do Faturamento de um Pedido.md | 2EDlh07da_g | Subset de Boletos Bancários (mesmo id + canônico mais completo) |
| Incluir Campos Extras - Ferramenta que permite adicionar mais informações no cadastro.md | 7YhAEYcWDVk | Conteúdo contingência; overlap com PDV Novo → delta único em 042 via canônico PDV Novo; este SKIP se zero delta residual após merge de eZLAMLHAm2k (tratar como MULTI_SOURCE: canônico PDV Novo; se houver passo único, MERGE 042) |
| (reserva) zero-delta pós-diff | — | Registrar no 00.3 se merge encontrar cobertura total |

**Decisão conservadora Incluir Campos Extras:** MERGE_ENRIQUECER DOCUP-042 se houver passo de contingência ausente no oficial e no merge do PDV Novo; senão SKIP. Default implementador: ler ambos e unir delta único em 042 sob um bloco.

---

## MISMATCH (6) — destino pelo conteúdo

| filename | video_id | Conteúdo real | Destino |
|----------|----------|---------------|---------|
| Movimentação de Consignado.md | g58YmDXDTT0 | NFS-e | **DOCUP-052** (nunca 027) |
| PDV Novo totalmente personalizável.md | eZLAMLHAm2k | Rejeição/cert/contingência NF-e | **DOCUP-042** |
| Incluir Campos Extras….md | 7YhAEYcWDVk | Contingência NF-e | **DOCUP-042** (MULTI_SOURCE) |
| Entrada NFE XML Manifestação….md | LdNEwnR4Emg | Entrega futura | **SKIP** |
| Exemplo White Label.md | RTu4TUVlax4 | Margens Epson TM-T20X | **DOCUP-022** |
| Configuração do Cadastro da Empresa (Parte 01).md | ZswVaygjzq8 | Ativação/licença | **SKIP** → 054 canônico |

---

## NOVO — clusters de fontes

### DOCUP-047 `02_OPERACOES_DIARIAS\02.11_MODULO_RESTAURANTE.md`
| filename | video_id |
|----------|----------|
| Restaurante (Parte 1) - Cadastro e configuração de mesas e comandas.md | maOauuYQAL8 |
| Restaurante (Parte 2) - Configuração do Grupos de Produto e Setor Impressão.md | 9ACMVSadk7M |
| Restaurante (Parte 3) - Vendas através das Mesas e Comandas.md | 1ePQG1Qz89w |
| Restaurante - Controle de Produção.md | GE2KXOK7k60 |
| Controle de Produtos - Pizza para Restaurante.md | CqmDR_S98Lc |
| Melhorias Aplicativo Android Restaurante (Garçom).md | -lnCOQZzxlY |

### DOCUP-048 `03_MANUTENCAO_TECNICA\03.16_APPS_ANDROID_FORCA_VENDAS_PDV.md`
| filename | video_id |
|----------|----------|
| Configuração do APP Android Força de Vendas Up.md | pQvqPpjv4sI |
| PDV ANDROID.md | jn6MB5IDtkg |
| PDV ANDROID - FICHAS.md | BJLC-Bh5dls |
| Abertura e Fechamento de Caixa App Android.md | e0cxJXNm-xI |
| Alteração de Preço pelo App Mobile.md | Js6IxkbboKw |
| Dashboard App.md | 0xjb81vmN0s |
| Ferramenta de Inventário Android.md | 2Dch3z1og-8 |
| Emissão Nota Fiscal pelo Força de Vendas.md | gJiw7KHctfc |
| Pagamento da Comanda Mesa ou recebimento do vendedor externo via APP Força de Vendas (PIX).md | zQ2AfOU1J54 |

### DOCUP-049 `02_OPERACOES_DIARIAS\02.12_MODULO_HOTELARIA.md`
| filename | video_id | Nota |
|----------|----------|------|
| Módulo Hotelaria - Controle de hospedagem e consumo.md | 7b7aCBHshUg | Omitir trecho consumo se conflitar com oficial |
| Módulo Hotelaria - Ferramenta e suas funções (Parte 01).md | au0WvoEDTB0 | |
| Módulo Hotelaria - Ferramenta e suas funções (Parte 02).md | MBfrSKjoiRA | |

### DOCUP-050 `02_OPERACOES_DIARIAS\02.13_PORTARIA_INGRESSOS.md`
| filename | video_id |
|----------|----------|
| Portaria e controle de ingressos (Parte 1).md | OBLF_swZOtM |
| Portaria e controle de ingressos (Parte 2).md | TxpXXFsQ770 |
| Controle de Portaria no Android - Entrada e Saída (Check in Check out).md | 8dxX8EAogKQ |

### DOCUP-051 `02_OPERACOES_DIARIAS\02.14_PLANO_DE_CONTAS_DRE.md`
| filename | video_id |
|----------|----------|
| Plano de Contas (Parte 2) - Vendas.md | 4qNoG5NfTWM |
| Plano de contas (Parte 3) - Recebimentos.md | rRxe8S_zPmg |
| Plano de Contas ao Vender - Exemplo 2.md | 1i5fiaKjcuk |
| Plano de Contas nas Entradas de mercadoria (Compras) - Exemplo 1.md | Uk0m0jf-Reg |
| DRE - Demonstrativo Resultado Exercício.md | LUyzuUOmV8c |

### DOCUP-052 `01_CONFIGURACAO_INICIAL\01.7_NFSE_NOTA_SERVICO.md`
| filename | video_id |
|----------|----------|
| Movimentação de Consignado.md | g58YmDXDTT0 |
| Cobrança Gerando Boletos e Nota Fiscal de Serviço Eletrônica (NFS-e).md | gWdr8g_slq4 |
| Cobrança Automatizada dos Clientes da Revenda.md | ScQyFTO2PDA |

### DOCUP-053 `03_MANUTENCAO_TECNICA\03.17_INTEGRACOES_IMENDES_SCANNTECH.md`
| filename | video_id |
|----------|----------|
| Integração iMendes.md | NBWsm9IshRU |
| Integração SCANNTECH.md | _K0AtMU6S3w |

### DOCUP-054 `01_CONFIGURACAO_INICIAL\01.8_ATIVACAO_LICENCIAMENTO.md`
| filename | video_id |
|----------|----------|
| Ativação de um novo cliente.md | ZswVaygjzq8 |

### DOCUP-056 `03_MANUTENCAO_TECNICA\03.18_CONTROLE_IMPRESSOES.md`
| filename | video_id |
|----------|----------|
| Controle de Impressões.md | p5XTDAnIiro |

### DOCUP-057 `04_TROUBLESHOOTING_E_DICAS\04.11_FRETE_POR_REGIAO.md`
| filename | video_id |
|----------|----------|
| Frete por Região - Configurando o calculo das taxas.md | g3zan5z8xZQ |

### DOCUP-058 `04_TROUBLESHOOTING_E_DICAS\04.12_NFCE_RECEBIMENTO_FUTURO_RS.md`
| filename | video_id |
|----------|----------|
| NFC-e de Recebimento Futuro.md | Igt7y_i3Ips |

**Não criar DOCUP-055** — Self-checkout: seção em DOCUP-009 se delta; totem HOLD.

---

## MERGE por DOCUP alvo

| DOCUP | Path | Fontes Processando (filename · video_id) |
|-------|------|------------------------------------------|
| 003 | 01.1_CADASTRO_EMPRESA | Config Empresa Parte 02 · ZvmiEbYt9kY; Config cadastros fiscais · Jb2_Tun9Zpw; Config Básicas P1 · Q0cCN1rgEOQ |
| 004 | 01.2_DOCUMENTOS_ELETRONICOS | Configuração SAT · e7omZ0gkq5o; Emissão CF-e SAT · elcnR9FsFyY; Venda PDV transmissão NFC-e · pTcujjfK-l0 |
| 006 | 01.4_CONFIGURACOES_SISTEMA | (delta residual Config Básicas se não for 003/015) |
| 007 | 02.1_CADASTRO_PRODUTOS | Cadastro de Produtos · 20SR89LnkR4; Precificação · J53MXVqSt9U; Compra e Venda Lote/Série · QbvBA4qiOMY |
| 008 | 02.2_CADASTRO_PESSOAS | Cadastro de Pessoas · uZ1yzSYDewU; Cadastros vários · WHJUlS48MaM |
| 009 | 02.3_VENDAS_PDV | Configuração de Venda · jSPyG3JarvA; Config Vendas Gerais · TQTc8uw_4TI; Config Básicas P3 Pedido · 8YTvz7S20Z8; Estação PDV · EsjGMFQM9yg; TEF POS Stone · tQ0DiLPTURc; TEF UP Stone · 3K7ZB_JITHo; Self-Checkout · T7sw506c4SE — **sem** restaurante/hotelaria/portaria |
| 011 | 02.5_NATUREZA_OPERACAO_CFOP | Natureza de Operação · hR6qMHhVtH4 |
| 014 | 03.3_ENTRADA_NFE_XML | Manifestação Destinatário · W6o5S9XL994 |
| 016 | 03.5_ORDEM_SERVICO | OS Garantia NFe · LtdMeLDREgc; OS Garantia NF-e · wy_xhhilA70 |
| 017 | 03.6_PDV_OFFLINE | Instalação Offline P01 · vKl4IehI_ww; P02 · _enM9gDSHDc; Tutorial PDV Offline · t25FevbSDCQ |
| 018 | 03.7_INTEGRACOES_PIX | Integração com PIX · VzSDwaiqJlQ; PIX Cobrança · JClmTdw6YM0 |
| 019 | 03.8_PRODUTO_DESMEMBRAVEL | Gerando Lote de Produção · yHdVRO36xko |
| 020 | 03.9_CONVERSAO_UNIDADE | Vender CAIXA preço UNITÁRIO · NMpL_RqdEHg |
| 021 | 03.10_RELATORIOS_MOBILE | Relatórios Online · Q8QsC_Y4Pp0 |
| 022 | 04.1_PROBLEMAS_COMUNS | Exemplo White Label (Epson) · RTu4TUVlax4 |
| 024 | 04.3_ESTOQUE_LOCAIS_ENDERECOS | Vários Locais de Estoque · SbN02Qu57Zc |
| 025 | 04.4_ENTREGA_FUTURA | Controle de entregas · LdNEwnR4Emg; Carga multi empresa · wYhb3-lqLKU |
| 030 | 04.9_DIVISAO_CONTA_COUVERT | Divisão de conta por itens comanda · cZLiAbEZSbM |
| 034 | 02.6_PEDIDO_COMPRA_COTACAO | Cotação de compra · dBfezWDDObQ |
| 035 | 03.11_MOVIMENTACOES_AUXILIARES_ESTOQUE | Outras Movimentações · lcF3vph1Mz4; Config Básicas P4 Inventário · PSFIRDwYxF4 |
| 036 | 02.7_CONTAS_A_RECEBER_COBRANCAS | Boletos Bancários · 2EDlh07da_g; Desconto Condicional boleto · gSAvVdiPdwY |
| 037 | 03.12_INTEGRACOES_FINANCEIRAS | Boleto Sicredi API · 2In73uzu2O8; Conciliação cartão · IqIAS29hptE |
| 041 | 01.6_TRANSPORTE_FISCAL_CTE_MDFE | Config CT-e · gEYSJ-6OIIY; Emissão CT-e XML · Xnfll-GhduI; MDF-e Config · J1ry6DycKDM; Dicas MDF-e · ZyRyXdCvpKs; GNRE · iD0cBcoU_c0 |
| 042 | 03.13_NFE_EMITIDAS_CONTINGENCIA | PDV Novo (mismatch) · eZLAMLHAm2k; Incluir Campos Extras (mismatch) · 7YhAEYcWDVk |
| 045 | 02.10_CONTAS_REGRAS_PAGAMENTO | (delta se Config Venda/Formas não couber em 009/037) |
| 046 | ANEXOS/ARQUITETURA_TECNOLOGICA | Migração Excel · n8W6kmwZ6f8; VPN APIs · OmAoied-4-8 |

---

## Sprints

| Sprint | Escopo |
|--------|--------|
| 5B | Merges 003,004,007,008,009,011,014,018,036,037 (+022 Epson,030,034 se delta) |
| 5C | 041,004-SAT residual,042,025 |
| 5D | 017,016,035,020,024,019,046,009-TEF residual |
| 5E | NOVOs 052,051,054,058 |
| 5F | NOVOs 047,048 |
| 5G | NOVOs 049,050,053,056,057 |
| 5H | 00.1,00.2,00.3,MAPA_SINONIMOS, auditoria |

## Formato merge no corpo

```markdown
## Origem: vídeo — {Título amigável}

> Fonte: [YouTube](url) · arquivo: `{filename}` · video_id: `{id}`

### {Subtema do delta}
...somente delta factual...
```

## Regras de qualidade
- Zero invenção; oficial prevalece em conflito
- Só delta material
- Tags canônicas (estender MAPA se necessário)
- `fontes.tipo: video` em todo DOCUP tocado
- Não modificar `Casos Up\Processando\`
- Não criar DOCUP-055

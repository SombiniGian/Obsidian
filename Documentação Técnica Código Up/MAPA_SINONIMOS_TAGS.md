# Mapa de Sinônimos de Tags

> Documento de referência para padronização de tags entre `Documentação Técnica Código Up\` e `Casos Up\Processando\`.
> Última atualização: 2026-07-19 (Sprint 6 RAG)

## Canônicas vs Variantes

| Canônica | Variantes unificadas |
|----------|----------------------|
| `nfe` | `nf-e`, `Nf-e`, `NFe` |
| `nfce` | `nfc-e`, `NFC-e` |
| `nfs-e` | `nfse`, `NFS-e` |
| `ct-e` | `cte`, `CT-e` |
| `ct-e-os` | `cte-os`, `CT-e OS` |
| `mdf-e` | `mdfe`, `MDF-e` |
| `gnre` | `GNRE` |
| `controle-estoque` | `controle-de-estoque`, `gerenciamento-de-estoque` |
| `ordem-servico` | `ordem-de-servico` |
| `ordem-producao` | `op` |
| `cfop` | `CFOP` |
| `cst` | `CST` |
| `csosn` | `CSOSN` |
| `natureza-operacao` | `natureza-de-operacao` |
| `pdv` | `PDV` |
| `pdv-offline` | `pdv-off` |
| `pdv-super` | `PDV Super`, `pdv-enxuto` |
| `grid-personalizacao` | `personalizacao-grid` |
| `customizacao-layouts` | `customizacao-layout`, `layout-customizado` |
| `campos-personalizados` | `campos-extras` |
| `formas-de-pagamento` | `forma-pagamento` |
| `tef` | `TEF` |
| `pos` | `POS` |
| `smart-pos` | `smartpos`, `tef-embarcado` |
| `certificado-digital` | `certificado-A1`, `e-CNPJ` |
| `autxml` | `aut-xml`, `autorizacao-download` |
| `contabilidade` | `contador`, `escrituracao` |
| `xml` | `XML` |
| `manifesto-destinatario` | `manifestacao-destinatario` |
| `sped` | `SPED` |
| `sintegra` | `SINTEGRA` |
| `bordero-recebimento` | `bordero-de-recebimento` |
| `bordero-negociacao` | `bordero-de-negociacao` |
| `bordero-cobranca` | `bordero-de-cobranca` |
| `trigger-engine` | `motor-gatilhos`, `triggers-engine` |
| `white-label` | `whitelabel`, `rebranding` |
| `innosetup` | `inno-setup`, `instalador-personalizado` |
| `flutter` | `Flutter` |
| `delphi` | `Delphi` |
| `firebird` | `Firebird` |
| `comissao` | `comissionamento` |
| `consignado` | `venda-consignada` |
| `entrega-futura` | `entrega-programada` |
| `controle-carga` | `romaneio`, `carga-distribuicao` |
| `frota` | `controle-frota` |
| `almoxarifado` | `consumo-interno` |
| `inventario` | `contagem-estoque` |
| `compras` | `pedido-compra` |
| `cotacao` | `cotacao-compra`, `bidding` |
| `recebimento` | `contas-receber` |
| `pagamento` | `contas-pagar` |
| `cheque` | `controle-cheques` |
| `caixa` | `controle-caixa`, `fechamento-caixa` |
| `boleto` | `boleto-bancario` |
| `cartao` | `cartao-credito`, `conciliacao-cartao` |
| `pix` | `PIX` |
| `restaurante` | `modulo-restaurante`, `food-service` |
| `mapa-mesas` | `mapa-de-mesas`, `mesas` |
| `comanda` | `comandas`, `comanda-individual` |
| `impressao-setor` | `setor-impressao`, `setor-de-impressao` |
| `kds` | `controle-producao-cozinha`, `kitchen-display` |
| `hotelaria` | `hotel`, `hospedagem` |
| `portaria` | `controle-portaria` |
| `ingressos` | `ingresso`, `controle-ingressos` |
| `plano-contas` | `plano-de-contas` |
| `dre` | `DRE`, `demonstrativo-resultado` |
| `android` | `app-android` |
| `forca-vendas` | `força-de-vendas`, `forca-de-vendas` |
| `imendes` | `i-mendes`, `iMendes` |
| `scanntech` | `scan-tech`, `Scanntech` |
| `frete` | `taxa-de-entrega`, `configuracao-frete` |
| `frete-regiao` | `frete-por-regiao` |
| `delivery` | `entrega-delivery` |
| `controle-impressoes` | `controle-de-impressoes` |
| `ativacao` | `ativação`, `ativacao-cliente` |
| `licenciamento` | `licenca`, `licença` |
| `demonstracao` | `demo`, `trial` |
| `self-checkout` | `self-chekout`, `autoatendimento` |
| `recebimento-futuro` | `nfce-recebimento-futuro` |
| `issqn` | `ISS`, `iss` |
| `integracao` | `integração`, `integracoes` |
| `mobile` | `app-mobile` |
| `inventario` | `contagem-estoque` |
| `reserva` | `reservas-hotel` |
| `checkout` | `check-out`, `check-in-out` |
| `navegacao` | `indice-navegacao` |
| `replicacao-dados` | `replicacao`, `sync-pdv` |
| `ncm` | `NCM` |
| `cnab` | `CNAB`, `remessa-retorno` |
| `sefaz` | `SEFAZ` |
| `danfe` | `DANFE`, `danfce` |
| `mfe` | `MFE`, `mfe-ce` |
| `sat` | `SAT`, `cf-e-sat`, `cfe-sat` |
| `cobranca` | `cobrança`, `cobrancas` |
| `devolucao` | `devolução`, `devolucoes` |
| `cashback` | `cash-back` |
| `desconto` | `descontos`, `desconto-maximo` |

## Convenção de tags

- **Apenas minúsculas** — sem acentos, sem espaços.
- **Hífens** como separador de palavras (ex: `controle-estoque`, não `controle_estoque` nem `ControleEstoque`).
- **Sem plural redundante** — preferir singular (`cliente` em vez de `clientes`).
- Tags devem ser **substantivos ou temas**, não verbos de ação.

## Aplicação

- Ao mesclar documentos novos vindos de `Casos Up\Processando\`, normalizar tags usando esta tabela antes de adicionar ao arquivo final.
- Tags canônicas são imutáveis: nunca criar uma variante nova se já existe canônica equivalente.
- Para propor uma nova tag canônica, criar issue/discussão antes de aplicar em massa.

## Histórico de Ampliações

- **Sprint 3 (2026-07-04):** Construção inicial da tabela com base em auditoria de 32 documentos.
- **Sprint 4 (2026-07-05):** Ampliação pós-merge dos Aulões (24 módulos). Adicionadas tags de: documentos eletrônicos de transporte (`ct-e`, `ct-e-os`, `mdf-e`, `gnre`), operação de PDV (`pdv-super`, `smart-pos`), automação (`trigger-engine`, `autxml`), manifests e obrigações acessórias (`manifesto-destinatario`, `sped`, `sintegra`), borderôs, infraestrutura (`flutter`, `delphi`, `firebird`, `innosetup`, `white-label`), supply chain (`compras`, `cotacao`, `controle-carga`), financeiro (`bordero-recebimento`, `bordero-negociacao`, `bordero-cobranca`, `caixa`, `cheque`, `boleto`, `cartao`, `pix`, `recebimento`, `pagamento`, `comissao`), operação (`consignado`, `entrega-futura`, `frota`, `almoxarifado`, `inventario`).
- **Sprint 5 (2026-07-19):** Integração `Casos Up\Processando\` (103 vídeos). Verticais: `restaurante`, `mapa-mesas`, `comanda`, `impressao-setor`, `kds`, `hotelaria`, `portaria`, `ingressos`, `plano-contas`, `dre`, `android`, `forca-vendas`, `imendes`, `scanntech`, `frete`, `frete-regiao`, `delivery`, `controle-impressoes`, `ativacao`, `licenciamento`, `demonstracao`, `self-checkout`, `recebimento-futuro`, `issqn`, `integracao`, `mobile`.
- **Sprint 6 (2026-07-19):** Enriquecimento RAG do corpus oficial. Tags de operação/suporte: `desconto`, `cashback`, `devolucao`, `cobranca`, `sat`, `mfe`, `danfe`, `sefaz`, `cnab`, `ncm`, `replicacao-dados`, `navegacao`.

## Auditoria

Esta tabela foi construída na Sprint 3 com base na auditoria de 32 documentos da `Documentação Técnica Código Up\`. Nenhuma substituição foi necessária dentro desse diretório (todas as tags já estavam canônicas). O mapa serve como contrato para o merge futuro com `Casos Up\`.
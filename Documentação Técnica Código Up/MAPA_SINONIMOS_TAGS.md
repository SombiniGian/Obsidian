# Mapa de Sinônimos de Tags

> Documento de referência para padronização de tags entre `Documentação Técnica Código Up\` e `Casos Up\Processando\`.
> Última atualização: 2026-07-04

## Canônicas vs Variantes

| Canônica | Variantes unificadas |
|----------|----------------------|
| `nfe` | `nf-e`, `Nf-e`, `NFe` |
| `nfce` | `nfc-e`, `NFC-e` |
| `nfs-e` | `nfse`, `NFS-e` |
| `controle-estoque` | `controle-de-estoque`, `gerenciamento-de-estoque` |
| `ordem-servico` | `ordem-de-servico` |
| `cfop` | `CFOP` |
| `natureza-operacao` | `natureza-de-operacao` |
| `pdv` | `PDV` |
| `pdv-offline` | `pdv-off` |
| `grid-personalizacao` | `personalizacao-grid` |
| `customizacao-layouts` | `customizacao-layout`, `layout-customizado` |
| `formas-de-pagamento` | `forma-pagamento` |
| `certificado-digital` | `certificado-A1`, `e-CNPJ` |
| `contabilidade` | `contador`, `escrituracao` |
| `xml` | `XML` |

## Convenção de tags

- **Apenas minúsculas** — sem acentos, sem espaços.
- **Hífens** como separador de palavras (ex: `controle-estoque`, não `controle_estoque` nem `ControleEstoque`).
- **Sem plural redundante** — preferir singular (`cliente` em vez de `clientes`).
- Tags devem ser **substantivos ou temas**, não verbos de ação.

## Aplicação

- Ao mesclar documentos novos vindos de `Casos Up\Processando\`, normalizar tags usando esta tabela antes de adicionar ao arquivo final.
- Tags canônicas são imutáveis: nunca criar uma variante nova se já existe canônica equivalente.
- Para propor uma nova tag canônica, criar issue/discussão antes de aplicar em massa.

## Auditoria

Esta tabela foi construída na Sprint 3 com base na auditoria de 32 documentos da `Documentação Técnica Código Up\`. Nenhuma substituição foi necessária dentro desse diretório (todas as tags já estavam canônicas). O mapa serve como contrato para o merge futuro com `Casos Up\`.
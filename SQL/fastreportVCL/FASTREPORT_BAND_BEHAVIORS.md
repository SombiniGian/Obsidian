# FastReport VCL Band Behaviors and Events - Knowledge Base

## BandBase Common Properties

Todos os tipos de band herdam de `BandBase` e compartilham propriedades comuns:

### Sizing Behavior
| Property       | XML Attribute | Values     | Description                      |
| -------------- | ------------- | ---------- | -------------------------------- |
| `CanGrow`      | CanGrow       | true/false | Band pode crescer verticalmente  |
| `CanShrink`    | CanShrink     | true/false | Band pode encolher verticalmente |
| `GrowToBottom` | GrowToBottom  | true/false | Cresce até o fundo da página     |

### Style Properties
| Property | XML Attribute | Description |
|----------|---------------|-------------|
| `Border` | Border.Lines, Border.Color | Configura bordas |
| `Fill` | Fill.Color, Fill.* | Configura preenchimento |
| `Style` | Style | Estilo pré-definido |
| `EvenStyle` | EvenStyle | Estilo para linhas pares |
| `HoverStyle` | HoverStyle | Estilo ao passar mouse |

### Events
| Property | XML Trigger | Description |
|----------|-------------|-------------|
| `BeforePrint` | BeforePrintEvent | Antes de imprimir band |
| `AfterPrint` | AfterPrintEvent | Depois de imprimir band |
| `AfterData` | AfterDataEvent | Depois de processar dados |
| `Click` | ClickEvent | Clique no band |

## Band Types Reference

### Band Hierarchy
```
Base
  -> ComponentBase
    -> ReportComponentBase
      -> BreakableComponent
        -> BandBase
          -> ChildBand
          -> ColumnFooterBand
          -> ColumnHeaderBand
          -> DataBand
          -> HeaderFooterBandBase
            -> PageFooterBand
            -> PageHeaderBand
            -> ReportSummaryBand
          -> OverlayBand
          -> ReportTitleBand
```

### Band Processing Order
1. **ReportTitleBand** - Uma vez no início
2. **PageHeaderBand** - Antes de cada página
3. **ColumnHeaderBand** - Antes de cada coluna
4. **DataBand** - Para cada linha de dados
5. **ColumnFooterBand** - Após cada coluna
6. **PageFooterBand** - Após cada página
7. **ReportSummaryBand** - Uma vez no final

## Band XML Attributes

### Posicionamento
| Attribute | Required | Description |
|-----------|----------|-------------|
| `Top` | **Sim** | Posição vertical (mm) |
| `Width` | **Sim** | Largura (mm) |
| `Height` | **Sim** | Altura (mm) |

### Band Específicas

#### DataBand
| Attribute | Required | Description |
|-----------|----------|-------------|
| `DataSource` | No | Nome da TableDataSource |
| `Filter` | No | Expressão de filtro |

#### HeaderFooterBandBase (PageHeader/Footer)
| Attribute | Description |
|-----------|-------------|
| `PrintOnFirstPage` | Imprimir na primeira página |
| `PrintOnLastPage` | Imprimir na última página |

#### ReportSummaryBand
- Aparece uma vez no final do relatório
- Usado para totais, sumários

## ChildBand

Band secundário associado a outro band:

```xml
<ReportTitleBand Name="ReportTitle1">
  <ChildBand Name="Child1" Top="325.74" Width="718.2" Height="18.9"/>
</ReportTitleBand>
```

| Attribute | Description |
|-----------|-------------|
| `Top` | Posição relativa ao band pai |
| `Width` | Largura (igual ao pai) |
| `Height` | Altura do child band |

## Print Control Properties

### Flags
| Property | Description |
|----------|-------------|
| `PrintOn` | Condições de impressão |
| `FlagPreviewVisible` | Visível na pré-visualização |
| `Exportable` | Incluído na exportação |

## Validation Rules for Bands

### Required Attributes
- `Name` - Identificador único
- `Width` > 0
- `Height` > 0

### Business Rules
- DataBand com DataSource deve existir em Dictionary
- Top deve ser >= 0
- CanGrow/CanShrink não aplicável a todos os bands
- ChildBand deve ter Top > pai.Height

### Layout Rules
- Bands dentro de ReportPage não podem ter objetos diretos (apenas em bands)
- Ordem de bands afeta processamento
- Width máximo: PaperWidth - LeftMargin - RightMargin
# FastReport VCL Page Layout - Knowledge Base

## ReportPage Properties

### Dimensões do Papel
Todas as dimensões são em **milímetros**.

| Property | Description | Default | A4 Example |
|----------|-------------|---------|------------|
| `PaperWidth` | Largura do papel | - | 210mm |
| `PaperHeight` | Altura do papel | - | 297mm |
| `Landscape` | Orientação paisagem | false | - |

### Margens
| Property | Description | Unit |
|----------|-------------|------|
| `TopMargin` | Margem superior | mm |
| `BottomMargin` | Margem inferior | mm |
| `LeftMargin` | Margem esquerda | mm |
| `RightMargin` | Margem direita | mm |

### Page Bands Collection
| Property | Band Type | Description |
|----------|-----------|-------------|
| `ReportTitle` | ReportTitleBand | Título do relatório |
| `ReportSummary` | ReportSummaryBand | Sumário do relatório |
| `PageHeader` | PageHeaderBand | Cabeçalho de página |
| `PageFooter` | PageFooterBand | Rodapé de página |
| `ColumnHeader` | ColumnHeaderBand | Cabeçalho de coluna |
| `ColumnFooter` | ColumnFooterBand | Rodapé de coluna |
| `Overlay` | OverlayBand | Camada sobre outros elementos |
| `Bands` | BandCollection | Lista de DataBand/GroupHeader |

## Units Conversion

FastReport usa pixels internamente, com conversão via `Units.Millimeters`:

```csharp
// 1mm = Units.Millimeters (constante de conversão)
text1.Left = Units.Millimeters * 10;  // 10mm
text1.Top = Units.Millimeters * 5;    // 5mm
```

## Tamanhos de Papel Comuns

| Size | Width (mm) | Height (mm) |
|------|------------|-------------|
| A4 | 210 | 297 |
| A3 | 297 | 420 |
| Letter | 216 | 279 |
| Legal | 216 | 356 |
| Executive | 191 | 254 |

## Validation Rules for Layout

### Tamanhos Mínimos
- `PaperWidth` e `PaperHeight` devem ser > 0
- `Width` e `Height` de bands devem ser > 0
- `Left`, `Top` não negativos (relativo à margem)

### Margens
- Margens devem ser >= 0
- Margens não podem exceder metade do tamanho do papel

### Band Positioning
- `Top` do primeiro band deve considerar a margem superior
- `Top` subsequente deve ser > `Top + Height` do band anterior
- `Width` do band deve ser <= `PaperWidth - LeftMargin - RightMargin`

## XML Page Layout Example

```xml
<ReportPage Name="Page1" 
            PaperWidth="210" 
            PaperHeight="297"
            Landscape="false"
            TopMargin="10" 
            BottomMargin="10"
            LeftMargin="10" 
            RightMargin="10">
  <ReportTitleBand Name="ReportTitle1" 
                   Top="0" 
                   Width="190" 
                   Height="20" 
                   CanGrow="true"/>
  <DataBand Name="Data1" 
            Top="30" 
            Width="190" 
            Height="15" 
            DataSource="DataSource1"/>
</ReportPage>
```
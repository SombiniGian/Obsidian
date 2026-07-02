# FastReport VCL XML Elements Checklist - Knowledge Base

## Complete XML Element Reference

Checklist de elementos e atributos para validação de templates FastReport.

## Root Element

```
<Report>
├── ScriptLanguage="CSharp|VB|PascalScript"  [No]
├── TextQuality="Regular|Wysiwyg"          [No]
├── ReportInfo.Name=""                     [No]
├── ReportInfo.Author=""                   [No]
├── ReportInfo.Description=""              [No]
├── ReportInfo.Created=""                 [No]
├── ReportInfo.Modified=""                [No]
├── ReportInfo.CreatorVersion=""          [No]
├── <Dictionary>                           [Recomendado]
└── <ReportPage>                          [Mínimo 1]
```

## Dictionary Elements

### TableDataSource
```
<TableDataSource>
├── Name=""                                [Sim]
├── ReferenceName=""                      [No]
├── DataType="System.*"                   [No]
├── Enabled="true|false"                  [No]
└── <Column>                              [0+]
    ├── Name=""                           [Sim]
    ├── DataType="System.*"              [No]
    ├── BindableControl="Text|Picture|CheckBox|RichText|Custom"
    ├── Calculated="true|false"          [No]
    └── Expression=""                     [Se Calculated=true]
```

### DataConnection (variantes)
```
<MsSqlDataConnection|FirebirdConnection|...>  [0+]
├── Name=""                                [Sim]
├── ConnectionString=""                    [Sim]
└── LoginPrompt="true|false"              [No]
```

### Parameter
```
<Parameter>
├── Name=""                                [Sim]
├── DataType="System.*"                   [No]
└── Value=""                              [No]
```

### Relation
```
<Relation>
├── Name=""                                [Sim]
├── MasterDataSource=""                  [Sim]
├── DetailDataSource=""                  [Sim]
├── MasterColumn=""                      [Sim]
└── DetailColumn=""                      [Sim]
```

### Total
```
<Total>
├── Name=""                                [Sim]
├── DataSource=""                         [Sim]
├── Column=""                             [Sim]
└── Function="Sum|Avg|Min|Max|Count"     [Sim]
```

## ReportPage Elements

```
<ReportPage>
├── Name=""                                [Sim]
├── PaperWidth="" (mm)                   [Mínimo 1]
├── PaperHeight="" (mm)                  [Mínimo 1]
├── Landscape="true|false"               [No]
├── TopMargin="" (mm)                    [No]
├── BottomMargin="" (mm)                  [No]
├── LeftMargin="" (mm)                  [No]
├── RightMargin="" (mm)                  [No]
├── <ReportTitleBand>                    [0-1]
├── <PageHeaderBand>                     [0-1]
├── <ColumnHeaderBand>                   [0-1]
├── <GroupHeaderBand>                    [0+]
├── <DataBand>                           [0+]
├── <GroupFooterBand>                    [0+]
├── <ColumnFooterBand>                   [0-1]
├── <PageFooterBand>                     [0-1]
├── <ReportSummaryBand>                  [0-1]
├── <ChildBand>                          [0+]
└── <OverlayBand>                        [0-1]
```

## Band Common Attributes

### Todos os Bands (herdam de BandBase)
```
* Name=""                                [Sim]
* Top="" (mm)                           [Sim]
* Width="" (mm)                         [Sim]
* Height="" (mm)                        [Sim]
* CanGrow="true|false"                  [No]
* CanShrink="true|false"                [No]
* Border.Lines="All|None|Left|..."      [No]
* Border.Color=""                       [No]
* Fill.Color=""                         [No]
```

### DataBand Específico
```
<DataBand>
├── DataSource=""                         [Se conectar dados]
├── Filter=""                             [No]
├── Sort=""                               [No]
└── <TextObject|PictureObject|...>      [Objects dentro]
```

### GroupHeaderBand Específico
```
<GroupHeaderBand>
├── DataSource=""                         [Sim]
├── GroupExpression=""                   [Sim]
├── BandSortPriority=""                  [No]
├── KeepTogether="true|false"            [No]
└── PrintOnEachPage="true|false"       [No]
```

## ReportObject Elements (dentro de bands)

### TextObject
```
<TextObject>
├── Name=""                               [Sim]
├── Left="" (mm)                        [No]
├── Top="" (mm)                         [No]
├── Width="" (mm)                       [Sim]
├── Height="" (mm)                      [Sim]
├── Text=""                               [No]
├── Font="Family, Sizept, style=..."    [No]
├── HorzAlign="Left|Center|Right"     [No]
├── VertAlign="Top|Center|Bottom"     [No]
├── Format="Date|Number|Currency|..." [No]
├── Format.Format=""                    [Se Format definido]
├── CanGrow="true|false"                [No]
├── CanShrink="true|false"              [No]
├── Border.Lines=""                     [No]
├── Border.Color=""                     [No]
├── Fill.Color=""                       [No]
└── TextFill.Color=""                   [No]
```

### PictureObject
```
<PictureObject>
├── Name=""                               [Sim]
├── DataColumn=""                       [No]
├── Image=""                              [No]
├── CanGrow="true|false"                [No]
├── CanShrink="true|false"              [No]
└── Border.Lines, Color, etc.         [Visual props]
```

### ShapeObject
```
<ShapeObject>
├── Name=""                               [Sim]
├── Shape="Rectangle|Ellipse|RoundedRectangle|Triangle|Diamond"
├── CornerRadius=""                     [Se Shape=RoundedRectangle]
└── [Visual properties comuns]
```

### LineObject
```
<LineObject>
├── Name=""                               [Sim]
├── Diagonal="true|false"               [No]
├── StartCap=""                          [No]
├── EndCap=""                            [No]
└── Border.* (para linha)              [Visual]
```

### BarcodeObject
```
<BarcodeObject>
├── Name=""                               [Sim]
├── Text=""                               [No]
├── Expression=""                         [No]
├── DataColumn=""                       [No]
├── Barcode.Type=""                     [No]
├── AutoSize="true|false"               [No]
└── Zoom=""                               [Se AutoSize=false]
```

### CheckBoxObject
```
<CheckBoxObject>
├── Name=""                               [Sim]
├── DataColumn=""                       [No]
├── Checked=""                            [No]
└── [Visual properties comuns]
```

## Validation Checklist Summary

### Estrutura
- [ ] `<Report>` é elemento raiz
- [ ] Pelo menos uma `<ReportPage>` existe
- [ ] `<Dictionary>` existe se houver DataSource

### Nomes Únicos
- [ ] TableDataSource.Name únicos
- [ ] ReportPage.Name únicos
- [ ] Band Name únicos dentro de página
- [ ] Object Name únicos dentro de band

### Referências
- [ ] DataBand.DataSource existe em Dictionary
- [ ] PictureObject.DataColumn tem DataSource válido
- [ ] GroupHeaderBand.DataSource existe

### Dimensões
- [ ] Width > 0
- [ ] Height > 0
- [ ] Left, Top >= 0
- [ ] PaperWidth, PaperHeight > 0

### Visual
- [ ] Border.Lines valor válido
- [ ] Font formato válido
- [ ] Alignment valores válidos
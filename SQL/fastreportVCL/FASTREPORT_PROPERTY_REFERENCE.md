# FastReport VCL Property Reference - Knowledge Base

## Core Property Types

### Unit Types
- **Length**: Width, Height, Left, Top, Border.Width (milímetros no XML)
- **Margin**: TopMargin, BottomMargin, LeftMargin, RightMargin (mm)
- **Padding**: "left,top,right,bottom" (pixels)

### Color Types
- Nomes: Maroon, WhiteSmoke, Black, Blue, Red, Green, Yellow
- Hex: "#FF0000" (dependendo da versão)
- RGB: Função Color.FromArgb(r,g,b) (não no XML)

### Enum Values Reference

#### BorderLines
```
None, Left, Right, Top, Bottom, TopBottom, LeftRight, All
```

#### LineStyle
```
Solid, Dash, Dot, DashDot, DashDotDot
```

#### HorzAlign / VertAlign
```
Left/Center/Right, Top/Center/Bottom
```

#### ScriptLanguage (Report attribute)
```
CSharp, VB, PascalScript
```

#### TextQuality
```
Regular, Wysiwyg
```

## Default Values

### ReportPage Defaults
| Property | Default |
|----------|---------|
| PaperWidth | 210 (A4) |
| PaperHeight | 297 (A4) |
| Landscape | false |
| Margins | 0 |

### Band Defaults
| Property | Default |
|----------|---------|
| CanGrow | false |
| CanShrink | false |
| Border.Lines | None |
| Visible | true |

### Object Defaults
| Property | Default |
|----------|---------|
| Width | 0 (inválido - deve ser > 0) |
| Height | 0 (inválido - deve ser > 0) |
| Text | "" |
| Font | (depende do sistema) |

## Property Composition Patterns

### Border Properties
```xml
Border.Lines="All"
Border.Color="Maroon"
Border.Style="Solid"
Border.Width="1"
Border.Shadow="false"
Border.ShadowColor="Black"
Border.ShadowWidth="0"
```

### Fill Properties
```xml
Fill="Solid"
Fill.Color="WhiteSmoke"
Fill.StartColor="White"
Fill.EndColor="Black"
Fill.Angle="0"
Fill.Focus="0"
Fill.Contrast="1"
```

### Font Properties
Formato: `"FontFamily, Sizept[, style=Style1, Style2...]"`
```xml
Font="Tahoma, 9pt"
Font="Arial, 12pt, style=Bold"
Font="Courier New, 10pt, style=Bold, Italic"
Font="Times New Roman, 8pt, style=Underline"
```

### Location/Size Properties
```xml
Left="10"    <!-- mm -->
Top="20"     <!-- mm -->
Width="190"  <!-- mm -->
Height="15"  <!-- mm -->
```

## Validation Property Ranges

### Numeric Ranges
| Property | Min | Max | Notes |
|----------|-----|-----|-------|
| PaperWidth | > 0 | | mm |
| PaperHeight | > 0 | | mm |
| Width | > 0 | | mm |
| Height | > 0 | | mm |
| Left | >= 0 | | mm |
| Top | >= 0 | | mm |
| Border.Width | >= 0 | | pixels |
| Font.Size | > 0 | | points |
| CornerRadius | >= 0 | | mm |

### String Formats
| Property | Pattern | Required |
|----------|---------|----------|
| Font | `"Family, Sizept[, style=...]"` | false |
| Padding | `"n,n,n,n"` (4 numbers) | false |
| Color | Named color ou hex | false |
| DataType | `"System.TypeName"` | false |
| Format.Format | String válido | Se Format definido |

## Error Recovery Patterns

### Missing Required Properties
- `Name` vazio → erro fatal
- `Width`/`Height` = 0 → warning
- `DataSource` inexistente → warning

### Invalid Property Values
- `Border.Lines="Invalid"` → ignorar ou error
- `Font` formato inválido → usar default
- `Left` negativo → corrigir para 0

### Duplicate Names
- Nomes duplicados → warning de ambiguidade

## XML Special Cases

### Expressions em strings
```xml
Text="[DataSource.Column]"           <!-- Binding -->
Text="[Report.ReportInfo.Name]"      <!-- Sistema -->
Text="[Date]"                        <!-- Função -->
```

### Escape Sequences
```xml
Text="Line1&#xD;&#xA;Line2"        <!-- \r\n -->
Text="Price: &amp;euro; 100"       <!-- & -->
```

### Newline em Text
- `\r\n` ou `&#xD;&#xA;` no XML
- `Padding` não afeta quebra de linha

## FastReport VCL Specific Notes

### vs FastReport .NET
- VCL usa PascalScript (não CSharp)
- Estrutura XML similar mas tipos podem diferir
- Units em milímetros tanto VCL quanto .NET
- Propriedades herdados são as mesmas

### FR3 vs FRX
- `.fr3` = formato XML antigo
- `.frx` = formato XML atual
- Estrutura praticamente idêntica
- Tags de propriedades compostas podem variar
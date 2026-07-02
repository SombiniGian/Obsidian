# FastReport VCL Visual Properties - Knowledge Base

## Common Visual Properties

Propriedades visuais compartilhadas entre objetos e bands via `ReportComponentBase`:

### Border Properties
```xml
Border.Lines="All"           <!-- All, Left, Right, Top, Bottom -->
Border.Color="Maroon"      <!-- System.Color name ou hex -->
Border.Style="Solid"       <!-- Solid, Dash, Dot, DashDot, DashDotDot -->
Border.Width="1"           <!-- Largura em pixels -->
```

#### BorderLine Structure
Cada linha tem:
- `Color` - Cor da linha
- `Style` - Estilo (Solid, Dash, Dot)
- `Width` - Largura em pixels

### Fill Properties
```xml
Fill.Color="WhiteSmoke"      <!-- Cor sólida -->
Fill="LinearGradient"        <!-- Solid, LinearGradient, Hatch, Glass, Texture -->
Fill.StartColor="IndianRed"  <!-- Para gradient -->
Fill.EndColor="Maroon"     <!-- Para gradient -->
Fill.Angle="90"            <!-- Ângulo em graus -->
Fill.Focus="0.52"          <!-- Foco do gradient -->
Fill.Contrast="1"          <!-- Contraste -->
```

Fill Types:
- `SolidFill` - Cor sólida
- `LinearGradientFill` - Gradiente linear
- `HatchFill` - Hatch pattern
- `GlassFill` - Efeito vidro
- `TextureFill` - Textura

### Font Properties
Formato XML: `"FontFamily, Sizept, style=Bold,Italic,Underline,Strikeout"`

Exemplos:
```xml
Font="Tahoma, 9pt, style=Bold"
Font="Arial, 12pt"
Font="Courier New, 10pt, style=Bold, Italic"
```

Font Properties individuais:
- `FontFamily` - Família da fonte
- `FontSize` - Tamanho em pontos
- `FontStyle` - Bold, Italic, Regular
- `FontWidthRatio` - Proporção de largura

### Text Alignment
```xml
HorzAlign="Center"    <!-- Left, Center, Right -->
VertAlign="Center"    <!-- Top, Center, Bottom -->
```

### Padding
Formato: `"left, top, right, bottom"` (em pixels ou mm)
```xml
Padding="4, 4, 4, 4"
Padding="10, 0, 2, 0"
```

## ShapeObject Specific

### Tipos de Shape
```xml
<ShapeObject Shape="Rectangle"/>
<ShapeObject Shape="Ellipse"/>
<ShapeObject Shape="RoundedRectangle"/>
<ShapeObject Shape="Triangle"/>
<ShapeObject Shape="Diamond"/>
```

### CornerRadius
Para `RoundedRectangle`:
```xml
CornerRadius="5"  <!-- Raio dos cantos arredondados -->
```

## LineObject Specific

### Diagonal
```xml
Diagonal="true"  <!-- Linha diagonal (não horizontal/vertical) -->
```

### Cap Settings
```xml
StartCap="Arrow"    <!-- Arrow, Circle, Diamond, Square, etc -->
EndCap="Arrow"
```

## Color Values

Cores suportadas pelo FastReport:
- Nomes de cores: `Maroon`, `WhiteSmoke`, `IndianRed`, `Blue`, `Red`, `Green`, etc.
- RGB: `Color.FromArgb(255, 0, 0)` - não no XML
- Hex: `#FF0000` - dependendo da versão

## Common Values Table

### BorderLines Enum
| Value | Visible Sides |
|-------|---------------|
| `None` | Nenhuma |
| `Left` | Apenas esquerda |
| `Right` | Apenas direita |
| `Top` | Apenas topo |
| `Bottom` | Apenas base |
| `TopBottom` | Topo e base |
| `LeftRight` | Esquerda e direita |
| `All` | Todas as bordas |

### LineStyle Enum
| Value | Pattern |
|-------|---------|
| `Solid` | Sólido |
| `Dash` | Tracejado |
| `Dot` | Pontilhado |
| `DashDot` | Tracejado-ponto |
| `DashDotDot` | Tracejado-ponto-ponto |

### HorzAlign/VertAlign
| Value | Description |
|-------|-------------|
| `Left` / `Top` | Alinha à esquerda/cima |
| `Center` | Centralizado |
| `Right` / `Bottom` | Alinha à direita/base |

## Validation Rules for Visual Properties

### Required Visual Checks
1. Border.Lines não vazio se Border.Color definido
2. Border.Style válido
3. Font.Size > 0 se Font definido
4. Fill propiedades condizentes (StartColor+EndColor para gradient)
5. Padding formato "n,n,n,n" válido

### Consistency Rules
- Width, Height > 0 para todos objetos
- Left, Top >= 0
- Diagonal=true exige mais pontos
- CornerRadius > 0 apenas para shapes arredondados
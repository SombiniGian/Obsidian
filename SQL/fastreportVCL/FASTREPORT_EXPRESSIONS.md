# FastReport VCL Expressions and Data Binding - Knowledge Base

## Expression Syntax

FastReport usa expressões entre colchetes `[]` para binding:

### Basic Binding
```
[DataSource.Column]
[Employees.FirstName]
[Orders.OrderDate]
```

### Calculated Columns
Colunas marcadas como `Calculated="true"` podem usar expressões:
```xml
<Column Name="Total" DataType="System.Decimal" Calculated="true">
  Expression="[Quantity] * [UnitPrice]"
</Column>
```

## Expression Context

### Variables de Sistema
- `[PageN]` - Número da página (string)
- `[PageNo]` - Número da página (integer)
- `[TotalPages]` - Total de páginas
- `[PageNofM]` - "Page X of Y"
- `[Date]` - Data atual
- `[Time]` - Hora atual

### Report Info Access
```
[Report.ReportInfo.Name]
[Report.ReportInfo.Author]
[Report.ReportInfo.Description]
```

### Parameter Access
```
[Report.Parameter.StartDate]
[Report.Parameter.EndDate]
```

## Format Properties in Expressions

### Date Format
```xml
<Column Name="OrderDate" DataType="System.DateTime" Format="Date"/>
```

XML attributes para formatação:
```xml
<TextObject Text="[Orders.OrderDate]" 
            Format="Date" 
            Format.Format="D"/>  <!-- Long Date -->
```

### Format Types
| Format | Format.Format Values |
|--------|---------------------|
| `Date` | D (Long), d (Short), T (Long Time), t (Short Time) |
| `Number` | Custom format string |
| `Currency` | Currency format |
| `Percent` | Percent format |

## DataColumn Binding Pattern

### Formato Válido
```
DataSourceName.ColumnName
```

### Exemplo
```xml
<PictureObject DataColumn="Employees.Photo"/>
<CheckBoxObject DataColumn="Orders.Shipped"/>
<TextObject Text="[Employees.BirthDate]" Format="Date" Format.Format="D"/>
```

## Calculated Columns

### Properties
| Property | Description |
|----------|-------------|
| `Calculated` | true/false |
| `Expression` | Expressão calculada |
| `Calculated` = true requer `Expression` |

### Expression Examples
```csharp
// Math
"[Quantity] * [UnitPrice]"
"[Price * 1.1]"

// String operations
"[FirstName] + ' ' + [LastName]"

// Conditional
"Iif([Total] > 1000, 'Grand', 'Normal')"
```

## Aggregate Functions

### Em TextObject ou Total
- `Sum(DataSource.Column)`
- `Avg(DataSource.Column)`
- `Min(DataSource.Column)`
- `Max(DataSource.Column)`
- `Count(DataSource.Column)`

## Validation Rules for Expressions

### Syntax Validation
1. Colchetes balanceados: `[ ]`
2. DataSource.Column válido
3. Referências circulares não permitidas

### DataType Compatibility
| DataType | Format | Can Bind To |
|----------|--------|-------------|
| System.DateTime | Date | TextObject com Format="Date" |
| System.Boolean | Boolean | CheckBoxObject |
| System.Byte[] | Binary | PictureObject |
| System.String | Text | TextObject |
| System.Int32, Decimal | Number/Currency | TextObject |

### Expression Validation
- Variáveis existentes devem existir
- Literais devem ser tipos válidos
- Operadores suportados: +, -, *, /, etc.

## Special Characters in Text

### Escape XML
- `&` -> `&amp;`
- `<` -> `&lt;`
- `>` -> `&gt;`

### Newlines
- `\r\n` no conteúdo do texto
- `Padding` em formato "left,top,right,bottom"

## Format Tags (TextObject)

Se `HasHtmlTags=true`:
- `<b>` `<i>` `<u>` `<strike>` `<sub>` `<sup>`
- `<font color="...">`

## Error Handling in Expressions

### Common Errors
1. DataSource não existe
2. Column não existe
3. Tipo incompatível
4. Sintaxe inválida
5. Referência circular
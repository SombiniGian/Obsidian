# FastReport VCL Data Formatting - Knowledge Base

## Format Types

FastReport suporta diversos tipos de formatação para colunas e objetos de texto:

### DateFormat
Formata valores de data/hora.

**XML Attributes:**
```xml
Format="Date"
Format.Format="D"  <!-- Long Date -->
Format.Format="d"  <!-- Short Date -->
Format.Format="T"  <!-- Long Time -->
Format.Format="t"  <!-- Short Time -->
```

### NumberFormat
Formata valores numéricos.

**Properties:**
- `DecimalDigits` - Número de casas decimais
- `DecimalSeparator` - Separador decimal (ex: ",")
- `GroupSeparator` - Separador de milhar (ex: ".")
- `NegativePattern` - Padrão para negativos (0-4)
- `UseLocale` - Usar configurações de locale

### CurrencyFormat
Formata valores monetários.

**Properties:**
- `CurrencySymbol` - Símbolo da moeda (ex: "$", "R$")
- `DecimalDigits` - Casas decimais
- `DecimalSeparator` - Separador decimal
- `GroupSeparator` - Separador de grupos
- `PositivePattern` - Padrão positivo (0-3)
- `NegativePattern` - Padrão negativo (0-15)

### PercentFormat
Formata valores percentuais.

### BooleanFormat
Formata valores booleanos.

### CustomFormat
Formatação customizada com string de formato.

## Format Application

### Em TextObject
```xml
<TextObject Name="Text4" Left="113.4" Top="66.15" Width="453.6" Height="18.9" 
           Text="[Employees.BirthDate]" 
           Format="Date" Format.Format="D" 
           VertAlign="Center" Font="Tahoma, 9pt"/>
```

### Em Column Definition
```xml
<Column Name="BirthDate" DataType="System.DateTime" />
```

## Data Binding Patterns

### Column Reference
- `[DataSource.ColumnName]` - Referência direta
- `[DataSource.ColumnName]` com `Format="Date"` - Formata data

### Expression Support
- Expressions matemáticas
- Funções embutidas (FormatDateTime, FormatCurrency, etc.)
- Referências a variáveis de sistema

## Tipos de Dados Suportados para Formatação

| DataType | Format Recomendado |
|----------|-------------------|
| System.DateTime | Date |
| System.Int32 | Number |
| System.Decimal | Currency ou Number |
| System.Double | Number |
| System.Boolean | Boolean |
| System.String | Custom ou nenhum |
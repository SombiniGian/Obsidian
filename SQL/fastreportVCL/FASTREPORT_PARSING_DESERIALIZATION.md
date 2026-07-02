# FastReport VCL XML Parsing and Deserialization - Knowledge Base

## Serialization Framework

FastReport usa um framework customizado de serialização baseado na interface `IFRSerializable`:

```csharp
public interface IFRSerializable
{
    void Deserialize(FRReader reader);
    void Serialize(FRWriter writer);
}
```

## FRReader Class

Classe responsável por desserializar objetos XML:

### Métodos Principais
| Method | Description |
|--------|-------------|
| `ReadProperties(object obj)` | Lê propriedades simples e compostas |
| `Read()` | Cria instância e chama Deserialize() |
| `NextItem()` | Move para próximo item XML |
| `HasProperty(string name)` | Verifica se propriedade existe |

### Tipos de Propriedade Suportados
- `ReadBool(string name)` - boolean
- `ReadInt(string name)` - integer
- `ReadFloat(string name)` - float
- `ReadDouble(string name)` - double
- `ReadStr(string name)` - string
- `ReadValue(string name, Type typ)` - enum

## XmlDocument Class

Wrapper para manipulação de XML:

```csharp
XmlDocument xmlDoc = new XmlDocument();
xmlDoc.Load("template.frx");
xmlDoc.Save("output.frx");
xmlDoc.ToString();  // XML como string
```

## XML Structure Parsing

### Notação de Propriedades
- Propriedade simples: `Property="value"`
- Propriedade composta: `Property.SubProperty="value"`

Exemplo:
```xml
<TextObject Text="[Employees.Name]" 
            Font="Tahoma, 10pt, style=Bold"
            Border.Lines="All"
            Border.Color="Black"/>
```

### Collections e Children
```xml
<DataBand Name="Data1">
  <TextObject Name="Text1"/>  <!-- Children -->
  <Column Name="Col1"/>       <!-- Children de Dictionary -->
</DataBand>
```

## Pattern for Deserialization

Todo objeto FastReport seguir um padrão:

```csharp
public void Deserialize(FRReader reader)
{
    // 1. Ler propriedades simples
    reader.ReadProperties(this);
    
    // 2. Ler children via NextItem loop
    while (reader.NextItem())
    {
        if (reader.ItemName == "TextObject")
        {
            TextObject obj = new TextObject();
            obj.Deserialize(reader);
            this.Objects.Add(obj);
        }
    }
}
```

## XML Property Format Reference

### Propriedades Numéricas
- `Top`, `Left`, `Width`, `Height` - valores em mm (milímetros)
- `Border.Width` - pixels
- `Padding` - "left,top,right,bottom"

### Propriedades Enum
- `Border.Lines` - "All", "Left", "Right", "Top", "Bottom", etc.
- `Border.Style` - "Solid", "Dash", "Dot", "DashDot", "DashDotDot"
- `HorzAlign` - "Left", "Center", "Right"
- `VertAlign` - "Top", "Center", "Bottom"

### Propriedades Boolean
- `CanGrow="true"`
- `CanShrink="true"`
- `Enabled="true"`

### Propriedades String
- `Font="Tahoma, 9pt, style=Bold"`
- `Color="Maroon"` ou `Fill.Color="WhiteSmoke"`

## Validation for Parsing

### Before Parsing
1. Verificar `<?xml version="1.0"?>` header
2. Encoding deve ser UTF-8
3. Root element é `<Report>`

### During Parse
1. Propriedades obrigatórias presentes
2. Propriedades compostas têm padrão válido
3. Children referenciam objetos válidos
4. Nomes únicos no escopo

### Error Recovery
- Propriedade faltando: usar valor default
- Child inválido: pular ou erro fatal
- Formato inválido: tentar converter ou erro

## Element Name Matching

O FRReader usa `String.Compare(reader.ItemName, "TargetName", true)`:

- Case-insensitive matching
- Children são processados via `NextItem()` loop
- Property names seguem padrão `Property.SubProperty.SubSubProperty`

## XmlItem Structure

```csharp
class XmlItem
{
    string Name;           // Nome do elemento
    XmlItem Parent;        // Elemento pai
    List<XmlItem> Items;   // Filhos
    XmlProperty[] Properties; // Atributos
    string Value;          // Valor de texto
}
```

## Recommended Parsing Approach for Lint Tool

1. Carregar XML com XmlDocument
2. Parsear root `<Report>`
3. Extrair `<Dictionary>` primeiro
4. Validar todas as referências DataSource
5. Parsear cada `<ReportPage>`
6. Validar hierarquia e posicionamento de bands
7. Validar objetos dentro de bands
8. Relatar inconsistências
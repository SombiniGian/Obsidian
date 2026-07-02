# FastReport VCL Validation Rules - Knowledge Base

## Serialization Framework

FastReport usa o padrão `IFRSerializable` para serialização/desserialização de objetos:

```csharp
public interface IFRSerializable
{
    void Deserialize(FRReader reader);
    void Serialize(FRWriter writer);
}
```

## XML Serialization Structure

### Propriedades Simples
Formato: `PropertyName="value"`

### Propriedades Compostas
Formato: `Property.SubProperty="value"`

Exemplo:
```xml
Border.Lines="All"
Border.Color="Maroon"
Format.Format="D"
```

### Children
Elementos filhos são serializados como elementos XML aninhados:
```xml
<DataBand Name="Data1">
  <TextObject Name="Text1" ... />
</DataBand>
```

## Regras de Validação Estrutural

### 1. Validação de Estrutura XML Base
- **Obrigatório**: Elemento raiz `<Report>`
- **Recomendado**: `<Dictionary>` antes de `<ReportPage>`
- **Obrigatório**: Pelo menos uma `<ReportPage>`

### 2. Validação de Nomes Únicos
Dentro de um escopo, nomes devem ser únicos:
- `Name` em `<TableDataSource>`
- `Name` em `<ReportPage>`
- `Name` em bands (`<DataBand>`, `<ReportTitleBand>`, etc.)
- `Name` em objetos (`<TextObject>`, `<PictureObject>`, etc.)

### 3. Validação de Referências Cruzadas
- `DataSource` em `<DataBand>` deve existir em `<Dictionary>`
- `DataColumn` deve seguir padrão `DataSource.ColumnName`
- `Column.Name` deve ser único dentro de cada `TableDataSource`

### 4. Validação de DataType vs BindableControl
| DataType | BindableControl Recomendado |
|----------|----------------------------|
| System.String | Text |
| System.Int32 | Text |
| System.Decimal, System.Double | Text |
| System.DateTime | Text |
| System.Boolean | CheckBox |
| System.Byte[] | Picture |

## Regras de Validação de Objetos

### TextObject
| Campo | Validação |
|-------|-----------|
| `Name` | Obrigatório, único |
| `Text` | Pode conter expressões `[DataSource.Column]` |
| `Width`, `Height` | Deve ser > 0 |
| `Left`, `Top` | >= 0 (relativo à margem) |
| `Font` | Formato: "FontFamily, Sizept, style=Bold,Italic" |

### PictureObject
| Campo | Validação |
|-------|-----------|
| `Name` | Obrigatório, único |
| `DataColumn` | Formato "DataSource.Column" ou vazio |
| `Width`, `Height` | Deve ser > 0 |

### ShapeObject
- Suporta formas geométricas básicas

### BarcodeObject
| Campo | Validação |
|-------|-----------|
| `Text` ou `Expression` ou `DataColumn` | Pelo menos um deve existir |
| `AutoSize` | Se false, Width/Height obrigatório |

## Regras de Validação de Bands

### Posição e Tamanho
- `Top` deve ser >= 0
- `Width`, `Height` > 0
- Bands não podem se sobrepor (validação de layout)

### DataBand Específico
- `DataSource` deve referenciar TableDataSource existente
- Se `DataSource` existe, ao menos uma coluna deve existir

## Regras de Validação de DataSources

### TableDataSource
| Campo | Validação |
|-------|-----------|
| `Name` | Obrigatório, único |
| `Enabled` | true/false |
| `Column.Name` | Único dentro da TableDataSource |

### Column
| Campo | Validação |
|-------|-----------|
| `Name` | Obrigatório, único |
| `DataType` | Deve ser tipo .NET válido |
| `Calculated=true` | Requer `Expression` |

## Schema XML Implícito

FastReport não usa XSD formal. A estrutura é implícita no código. Para linting:

### Elementos Raiz Obrigatórios
```xml
<Report [attributes]>
  <Dictionary>
    <TableDataSource Name="...">
      <Column Name="..." [DataType="..."]/>
    </TableDataSource>
  </Dictionary>
  <ReportPage Name="...">
    <ReportTitleBand .../>
    <DataBand DataSource="..."/>
  </ReportPage>
</Report>
```

### Ordem Recomendada
1. `<Dictionary>` (conexões e datasources)
2. `<ReportPage>` (páginas do relatório)
3. Bands em ordem de processamento (Title -> Header -> Data -> Footer -> Summary)

## Warnings Comuns

| Warning | Descrição |
|---------|-----------|
| DataSource não usado | TableDataSource sem colunas vinculadas |
| Column não usada | Coluna sem objeto vinculado |
| Text vazio | TextObject sem conteúdo |
| Format incompatível | DataType não corresponde ao Format |
| Overlap bands | Bands sobrepostos no layout |
| Name duplicado | Nome não único no escopo |
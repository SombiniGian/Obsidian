# FastReport VCL Data Sources and Connections - Knowledge Base

## Dictionary Structure

O elemento `<Dictionary>` contém todos os recursos de dados do relatório:

- `TableDataSource` - Fontes de dados baseadas em tabelas
- `DataConnection` - Conexões com bancos (MsSql, Firebird, etc)
- `Parameter` - Parâmetros do relatório
- `Relation` - Relacionamentos entre tabelas
- `Total` - Totais/agregações

## TableDataSource

### Estrutura XML
```xml
<TableDataSource Name="Employees" 
                ReferenceName="NorthWind.Employees" 
                DataType="System.Int32" 
                Enabled="true">
  <Column Name="EmployeeID" DataType="System.Int32"/>
  <Column Name="LastName" DataType="System.String"/>
  <Column Name="BirthDate" DataType="System.DateTime"/>
  <Column Name="Photo" DataType="System.Byte[]" BindableControl="Picture"/>
</TableDataSource>
```

### Atributos
| Attribute       | Description             | Required           |
| --------------- | ----------------------- | ------------------ |
| `Name`          | Identificador único     | **Sim**            |
| `ReferenceName` | Nome da tabela/consulta | No                 |
| `DataType`      | Tipo de dado principal  | No                 |
| `Enabled`       | Fonte ativa             | No (default: true) |

## Column Properties

### Atributos XML
| Attribute | Description | Required |
|-----------|-------------|----------|
| `Name` | Nome da coluna | **Sim** |
| `DataType` | Tipo .NET | No (default: System.String) |
| `BindableControl` | Controle criado ao arrastar | No |

### BindableControl Values
| Value | Object Criado |
|-------|---------------|
| `Text` | TextObject |
| `Picture` | PictureObject |
| `CheckBox` | CheckBoxObject |
| `RichText` | RichTextObject |
| `Custom` | Usa `CustomBindableControl` |

## Data Connections

### Tipos Comuns
- `MsSqlDataConnection` - SQL Server
- `FirebirdConnection` - Firebird/InterBase
- `MySqlDataConnection` - MySQL
- `PostgresDataConnection` - PostgreSQL
- `XmlDataConnection` - Arquivos XML

### XmlDataConnection
```csharp
XmlDataConnection conn = new XmlDataConnection();
conn.XmlFile = "c:\\data\\source.xml";
conn.XsdFile = "c:\\data\\schema.xsd";
```

### ConnectionString em XML
```xml
<MsSqlDataConnection Name="db1" ConnectionString="Server=...;Database=...;"/>
```

## Parameters

### Estrutura
```xml
<Parameter Name="ReportDate" DataType="System.DateTime" Value="[Date]"/>
```

| Attribute | Description |
|-----------|-------------|
| `Name` | Identificador |
| `DataType` | Tipo de dado |
| `Value` | Valor ou expressão |

## Relation (Master-Detail)

### Estrutura
```xml
<Relation Name="EmployeeOrders" 
          MasterDataSource="Employees" 
          DetailDataSource="Orders"
          MasterColumn="EmployeeID" 
          DetailColumn="EmployeeID"/>
```

## Total (Aggregações)

### Tipos
- `Sum` - Soma
- `Avg` - Média
- `Min` - Mínimo
- `Max` - Máximo
- `Count` - Contagem

## Validation: DataSource References

### Regra de Integridade
Todo `DataSource` referenciado em `<DataBand>` deve existir:

```xml
<!-- Valid -->
<DataBand DataSource="Employees"/>
<TableDataSource Name="Employees"/>

<!-- Invalid - DataSource not found -->
<DataBand DataSource="NonExistent"/>
```

### Regra de DataColumn
`DataColumn` deve referenciar coluna existente:

```xml
<!-- Valid -->
<Column Name="Photo" DataType="System.Byte[]"/>
<PictureObject DataColumn="Employees.Photo"/>

<!-- Invalid - column doesn't exist -->
<Column Name="Name" DataType="System.String"/>
<TextObject DataColumn="Employees.NonExistent"/>
```

## Binding Expressions

### Sintaxe
- `[DataSource.Column]` - Valor direto
- `[DataSource.Column.Format]` - Formato aplicado
- `[Report.Parameter.ParamName]` - Valor de parâmetro

### Expressões Complexas
- Usar em `Expression` property
- Exemplo: `[Employees.Salary * 1.1]`
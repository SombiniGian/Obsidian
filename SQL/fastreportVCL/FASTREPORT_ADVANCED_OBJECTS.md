# FastReport VCL Advanced Objects - Knowledge Base

## Complex Report Objects

Objetos avançados suportados pelo FastReport VCL/XML:

| Object            | Descrição                   | Namespace         |
| ----------------- | --------------------------- | ----------------- |
| `TableObject`     | Tabela com linhas/colunas   | FastReport.Table  |
| `MatrixObject`    | Cross-tab / Matriz de dados | FastReport.Matrix |
| `GroupHeaderBand` | Cabeçalho de grupo          | -                 |
| `GroupFooterBand` | Rodapé de grupo             | -                 |
| `SubreportObject` | Relatório aninhado          | -                 |
| `ChartObject`     | Gráficos                    | FastReport.Chart  |

## Group Bands

### GroupHeaderBand
```xml
<GroupHeaderBand Name="Group1" 
                DataSource="Employees" 
                GroupExpression="[Employees.City]"
                Width="718.2" 
                Height="28.35"
                CanGrow="true"
                BandSortPriority="0">
  <TextObject Name="CityHeader" Text="[Employees.City]" Font="Tahoma, 10pt, style=Bold"/>
</GroupHeaderBand>
```

### GroupFooterBand
```xml
<GroupFooterBand Name="GroupFooter1" 
                Width="718.2" 
                Height="18.9"/>
```

### Group Properties
| Attribute | Description |
|-----------|-------------|
| `GroupExpression` | Expressão de agrupamento |
| `BandSortPriority` | Prioridade do grupo (0, 1, 2...) |
| `KeepTogether` | Manter grupo em uma página |
| `ResetPageNumber` | Resetar numeração de página |
| `PrintOnEachPage` | Imprimir cabeçalho em cada página |

## TableObject Structure

```xml
<TableObject Name="Table1" 
             Top="10" 
             Left="10" 
             Width="500" 
             Height="200"
             ColumnCount="3"
             RowCount="5">
  <TableCell Name="Cell1" Text="[Employees.Name]"/>
  <TableCell Name="Cell2" Text="[Employees.Age]"/>
</TableObject>
```

## MatrixObject (Cross-tab)

```xml
<MatrixObject Name="Matrix1" 
              Top="100" 
              Left="10" 
              Width="400" 
              Height="300">
  <MatrixCells>
    <MatrixCell Text="[Employees.Salary]" Format="Currency"/>
  </MatrixCells>
  <MatrixRows>
    <MatrixRow Value="[Employees.City]"/>
  </MatrixRows>
  <MatrixColumns>
    <MatrixColumn Value="[Employees.Year]"/>
  </MatrixColumns>
</MatrixObject>
```

## SubreportObject

```xml
<SubreportObject Name="Subreport1" 
                 Top="500" 
                 Left="10" 
                 Width="500" 
                 Height="200"
                 ReportName="DetailReport"/>
```

| Attribute    | Description             |
| ------------ | ----------------------- |
| `ReportName` | Nome do relatório filho |

## ChartObject

```xml
<ChartObject Name="Chart1" 
             Top="100" 
             Left="10" 
             Width="400" 
             Height="300">
  <ChartDataSet Name="DataSet1" 
                DataSource="Sales" 
                XAxis="[Sales.Month]" 
                YAxis="[Sales.Amount]"/>
</ChartObject>
```

## Gauges e Objetos Gráficos

### LinearGauge
```xml
<LinearGauge Name="Gauge1" 
             Top="100" 
             Left="10" 
             Width="200" 
             Height="50"
             Value="[Orders.Progress]"/>
```

### RadialGauge
Similar ao LinearGauge, mas circular.

### SimpleProgressGauge
```xml
<SimpleProgressGauge Name="Progress1" 
                      Top="100" 
                      Left="10" 
                      Width="200" 
                      Height="30"
                      Value="[Tasks.PercentComplete]"/>
```

## PolyLineObject e PolygonObject

```xml
<PolyLineObject Name="Line1" 
                Top="100" 
                Left="10" 
                Points="10,0;20,20;0,30"/>

<PolygonObject Name="Shape1" 
               Top="100" 
               Left="10" 
               Points="0,0;50,0;50,50;0,50"/>
```

## ZipCodeObject

```xml
<ZipCodeObject Name="Zip1" 
               Top="100" 
               Left="10" 
               Width="100" 
               Height="30"
               Text="[Orders.ZipCode]"/>
```

## CellularTextObject

```xml
<CellularTextObject Name="Cellular1" 
                    Top="100" 
                    Left="10" 
                    Width="100" 
                    Height="30"
                    Text="[Order.Code]"/>
```

## Validation Rules for Advanced Objects

### Group Bands
- `GroupExpression` obrigatório
- `DataSource` deve existir em Dictionary
- `KeepTogether=true` pode causar overflow

### MatrixObject
- `MatrixRows` e `MatrixColumns` necessários
- Valores devem existir no DataSource
- `MatrixCells` contém expressão de valor

### SubreportObject
- `ReportName` deve referenciar relatório válido
- Pode criar dependência circular

### TableObject
- `ColumnCount` e `RowCount` devem ser > 0
- Células dentro da tabela

### ChartObject
- DataSource obrigatório
- `XAxis` e `YAxis` necessários
- Formatos compatíveis com gráficos
# FastReport VCL Knowledge Repository - Index

Repositório de conhecimento para desenvolvimento de validador/lint de arquivos XML FastReport (`.frx`, `.fr3`).

## Arquivos do Repositório

| Arquivo | Descrição |
|---------|-----------|
| `FASTREPORT_XML_STRUCTURE.md` | Estrutura XML principal, elementos raiz, Dictionary, ReportPage |
| `FASTREPORT_FORMAT_RULES.md` | Formatação de dados (DateFormat, NumberFormat, CurrencyFormat) |
| `FASTREPORT_PAGE_LAYOUT.md` | Layout de páginas, margens, orientação, units |
| `FASTREPORT_DATA_SOURCES.md` | DataSources, Columns, Connections, Parameters, Relations |
| `FASTREPORT_BAND_BEHAVIORS.md` | Comportamentos de bands, eventos, ChildBand |
| `FASTREPORT_EXPRESSIONS.md` | Expressões de binding, cálculos, agregações |
| `FASTREPORT_VALIDATION_RULES.md` | Regras de validação estrutural para linting |

## Schema XML Resumido

```xml
<?xml version="1.0" encoding="utf-8"?>
<Report>
  <Dictionary>
    <TableDataSource Name="DataSource1">
      <Column Name="Col1" DataType="System.Int32"/>
      <Column Name="Col2" DataType="System.String"/>
    </TableDataSource>
  </Dictionary>
  <ReportPage Name="Page1" PaperWidth="210" PaperHeight="297">
    <ReportTitleBand Name="Title" Width="..." Height="..."/>
    <DataBand Name="Data" DataSource="DataSource1" Width="..." Height="...">
      <TextObject Name="Field1" Text="[DataSource1.Col1]"/>
    </DataBand>
  </ReportPage>
</Report>
```

## Tipos de Arquivo FastReport

| Extensão | Descrição |
|----------|-----------|
| `.frx` | Template XML (mais comum) |
| `.fr3` | Template XML (versão antiga) |
| `.fpx` | Preview prepared |

## Unidades de Medida

- **Milímetros** são usados no XML
- Conversão interna via `Units.Millimeters`
- 1mm = aproximadamente 3.78 pixels (dependendo DPI)
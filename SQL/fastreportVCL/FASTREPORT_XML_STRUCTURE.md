# FastReport VCL XML Structure - Knowledge Base

## Overview
FastReport salva templates de relatórios em formato XML com extensões `.frx` ou `.fr3`. Este documento descreve a estrutura XML para validação e linting.

## Root Element: `<Report>`

### Attributes Principais
| Attribute | Description | Required |
|-----------|-------------|----------|
| `ScriptLanguage` | Linguagem do script (CSharp, VB, PascalScript) | No |
| `TextQuality` | Qualidade do texto (Regular, Wysiwyg) | No |
| `ReportInfo.Name` | Nome do relatório | No |
| `ReportInfo.Author` | Autor do relatório | No |
| `ReportInfo.Description` | Descrição do relatório | No |
| `ReportInfo.Created` | Data/hora criação (MM/dd/yyyy HH:mm:ss) | No |
| `ReportInfo.Modified` | Data/hora modificação (MM/dd/yyyy HH:mm:ss) | No |
| `ReportInfo.CreatorVersion` | Versão do FastReport criador | No |

### Exemplo
```xml
<?xml version="1.0" encoding="utf-8"?>
<Report ScriptLanguage="CSharp" TextQuality="Regular" 
       ReportInfo.Name="Simple List" 
       ReportInfo.Author="Fast Reports Inc" 
       ReportInfo.Created="01/17/2008 03:05:57" 
       ReportInfo.Modified="07/26/2018 12:14:37" 
       ReportInfo.CreatorVersion="1.0.0.0">
```

## Element: `<Dictionary>`

Contém definições de fontes de dados, conexões e parâmetros.

### `<TableDataSource>`
Fonte de dados baseada em tabela para conexão com banco de dados.

| Attribute       | Description                                      | Required |
| --------------- | ------------------------------------------------ | -------- |
| `Name`          | Nome único da fonte de dados                     | **Sim**  |
| `ReferenceName` | Nome da tabela referenciada                      | No       |
| `DataType`      | Tipo de dado (System.Int32, System.String, etc.) | No       |
| `Enabled`       | Se a fonte está habilitada                       | No       |

#### `<Column>` - Filhos de TableDataSource
| Attribute | Description | Required |
|-----------|-------------|----------|
| `Name` | Nome da coluna | **Sim** |
| `DataType` | Tipo do dado (System.Int32, System.String, System.DateTime, System.Byte[]) | No |
| `BindableControl` | Tipo de controle criado ao arrastar (Text, Picture, CheckBox, RichText, Custom) | No |

##### DataType Suportados
- `System.Int32` - Inteiro
- `System.String` - Texto
- `System.DateTime` - Data/hora
- `System.Byte[]` - Array de bytes (imagens binárias)
- `System.Decimal` - Decimal
- `System.Boolean` - Booleano

## Report Pages

### `<ReportPage>`
Representa uma página no relatório.

| Attribute | Description | Required |
|-----------|-------------|----------|
| `Name` | Nome único da página | **Sim** |

## Band Types (Ordem de Processamento)

### `<ReportTitleBand>`
Band executado uma única vez no início do relatório.

| Attribute | Description | Required |
|-----------|-------------|----------|
| `Name` | Nome único | **Sim** |
| `Width` | Largura (em unidades configuradas) | **Sim** |
| `Height` | Altura | **Sim** |
| `CanGrow` | Se pode crescer verticalmente | No |
| `CanShrink` | Se pode encolher verticalmente | No |

### `<PageHeaderBand>`
Band executado no início de cada página.

### `<ColumnHeaderBand>`
Band executado no início de cada coluna.

### `<DataBand>`
Band principal para exibição de dados - pode ter DataSource.

| Attribute | Description | Required |
|-----------|-------------|----------|
| `Name` | Nome único | **Sim** |
| `DataSource` | Nome do TableDataSource associado | No |
| `Top` | Posição vertical | **Sim** |
| `Width` | Largura | **Sim** |
| `Height` | Altura | **Sim** |
| `CanGrow` | Se pode crescer | No |
| `Border.Lines` | Linhas visíveis (All, Left, Right, Top, Bottom) | No |
| `Border.Color` | Cor da borda | No |

### `<PageFooterBand>`
Band executado no final de cada página.

### `<ReportSummaryBand>`
Band executado no final do relatório.

### `<ChildBand>`
Sub-band associado a outro band.

## Report Objects

### `<TextObject>`
Exibe um ou mais linhas de texto.

| Attribute | Description | Required |
|-----------|-------------|----------|
| `Name` | Nome único | **Sim** |
| `Left` | Posição horizontal | No |
| `Top` | Posição vertical | No |
| `Width` | Largura | **Sim** |
| `Height` | Altura | **Sim** |
| `Text` | Conteúdo do texto | No |
| `Font` | Fonte (ex: "Tahoma, 9pt") | No |
| `HorzAlign` | Alinhamento horizontal (Left, Center, Right) | No |
| `VertAlign` | Alinhamento vertical (Top, Center, Bottom) | No |

#### TextObject Data Binding
- `[DataSource.ColumnName]` - Bind direto
- `Format="Date"` + `Format.Format="D"` - Formatação de data

### `<PictureObject>`
Exibe imagens.

| Attribute | Description | Required |
|-----------|-------------|----------|
| `Name` | Nome único | **Sim** |
| `DataColumn` | Coluna de dados (formato "DataSource.Column") | No |
| `CanGrow` | Se pode crescer | No |
| `CanShrink` | Se pode encolher | No |

### `<ShapeObject>`
Formas geométricas (retângulo, elipse, triângulo).

### `<LineObject>`
Linhas (vertical, horizontal ou diagonal).

### `<BarcodeObject>`
Representa códigos de barras.

| Attribute | Description | Required |
|-----------|-------------|----------|
| `Name` | Nome único | **Sim** |
| `Text` | Dados do código de barras | No |
| `DataColumn` | Coluna vinculada | No |
| `Expression` | Expressão para dados | No |

### `<CheckBoxObject>`
Checkbox com estados "Enabled" ou "Disabled".

## Border Properties
```xml
Border.Lines="All"           <!-- All, Left, Right, Top, Bottom -->
Border.Color="Maroon"      <!-- Cor da borda -->
Border.Style="Solid"       <!-- Estilo da linha -->
Border.Width="1"           <!-- Largura em pixels -->
```

## Fill Properties
```xml
Fill.Color="WhiteSmoke"      <!-- Cor solid fill -->
Fill="LinearGradient"        <!-- Tipo de fill -->
Fill.StartColor="IndianRed"
Fill.EndColor="Maroon"
Fill.Angle="90"
```

## Validação de Estrutura

### Regras Obrigatórias
1. Elemento raiz `<Report>` deve existir
2. `<Dictionary>` é obrigatório se houver DataSource
3. Cada `TableDataSource` deve ter `<Column>` definidos
4. `<DataBand>` com `DataSource` deve referenciar uma fonte existente
5. Atributos `Name` devem ser únicos dentro do escopo

### Validação de References
- `DataSource` em DataBand deve existir em Dictionary
- `DataColumn` deve seguir padrão "DataSource.ColumnName"
- Format data deve ser compatível com DataType

### Schema XML
FastReport usa serialização personalizada via FRReader/FRWriter. A estrutura segue padrão:
- Elementos com propriedades são atributos no formato `PropertyName.Value`
- Hijos são elementos aninhados
- Propriedades compostas usam notação `Property.SubProperty`
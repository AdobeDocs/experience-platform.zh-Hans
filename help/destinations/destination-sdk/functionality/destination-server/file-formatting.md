---
description: 了解如何通过“/destination-servers”端点为使用Adobe Experience Platform Destination SDK构建的基于文件的目标配置文件格式选项。
title: 文件格式配置
source-git-commit: 5a6359e5731b36763e86eba8c79e60d74fb3b4c8
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 4%

---


# 文件格式配置

Destination SDK支持一组灵活的功能，您可以根据集成需求配置这些功能。 这些功能包括支持 [!DNL CSV] 文件格式化。

当您通过Destination SDK创建基于文件的目标时，可以定义导出的CSV文件的格式设置。 您可以自定义许多格式选项，例如但不限于：

* CSV文件是否应包含标头；
* 用于引用值的字符；
* 空值应当是什么样的。

根据您的目标配置，当连接到基于文件的目标时，用户将在UI中看到某些选项。 您可以在 [基于文件的目标的文件格式选项](../../../ui/batch-destinations-file-formatting-options.md) 文档。


文件格式设置是基于文件的目标的目标服务器配置的一部分。

要了解此组件在何处适合使用Destination SDK创建的集成，请参阅 [配置选项](../configuration-options.md) 文档或参阅指南，了解如何 [使用Destination SDK配置基于文件的目标](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

您可以通过以下方式配置文件格式选项 `/authoring/destination-servers` 端点。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标服务器配置](../../authoring-api/destination-server/create-destination-server.md)
* [更新目标服务器配置](../../authoring-api/destination-server/update-destination-server.md)

本页介绍了所有支持的导出文件格式设置 `CSV` 文件。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免区分大小写错误，请完全按照文档中所示使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 否 |
| 基于文件（批处理）的集成 | 是 |

## 支持的参数 {#supported-parameters}

您可以修改导出文件的多个属性，以符合目标文件接收系统的要求，从而以最佳方式读取和解释从Experience Platform接收的文件。

>[!NOTE]
>
>只有在导出CSV文件时才支持CSV选项。 此 `fileConfigurations` 设置新目标服务器时，部分不是必需的。 如果您没有在API调用中为CSV选项传递任何值，则默认值来自 [参考表格见下文](#file-formatting-reference-and-example) 将被使用。


## 用户无法选择配置选项的CSV选项 {#file-configuration-templating-none}

在下面的配置示例中，所有CSV选项都是预定义的。 中定义的导出设置 `csvOptions` 参数为最终参数，用户无法对其进行修改。

```json
"fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        },
        "maxFileRowCount":5000000
    }
```

## 用户可选择配置选项的CSV选项 {#file-configuration-templating-pebble}

在以下配置示例中，未预定义任何CSV选项。 此 `value` 在每个 `csvOptions` 参数是通过 `/destinations` 端点(例如 [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) 对于 `quote` 文件格式选项)，用户可以使用Experience PlatformUI在您在对应的客户数据字段中配置的各种选项之间进行选择。 您可以在 [基于文件的目标的文件格式选项](../../../ui/batch-destinations-file-formatting-options.md) 文档。

```json
{
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
         }
      },
      "maxFileRowCount":5000000
   }
}
```

## 支持的文件格式选项的完整参考和示例 {#file-formatting-reference-and-example}

>[!TIP]
>
>以下描述的CSV文件格式选项也记录在中 [适用于CSV文件的Apache Spark指南](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). 以下使用的描述摘自Apache Spark指南。

以下是Destination SDK中所有可用文件格式选项的完整参考，以及每个选项的输出示例。

| 字段 | 必填/可选 | 描述 | 默认值 | 示例输出1 | 示例输出2 |
|---|---|---|---|---|---|
| `templatingStrategy` | 必需 | 对于您配置的每个文件格式选项，需要添加参数 `templatingStrategy`，可以具有两个值： <br><ul><li>`NONE`：如果您不打算允许用户在配置的不同值之间进行选择，请使用此值。 参见 [此配置](#file-configuration-templating-none) 例如，文件格式选项是固定的。</li><li>`PEBBLE_V1`：如果您希望允许用户在不同的配置值之间进行选择，请使用此值。 在这种情况下，您还必须在以下位置设置相应的客户数据字段： `/destination` 端点配置，用于在UI中向用户显示各种选项。 参见 [此配置](#file-configuration-templating-pebble) 例如，用户可以在不同的值之间为文件格式选项进行选择。</li></ul> | - | - | - |
| `compression.value` | 可选 | 将数据保存到文件时使用的压缩编解码器。 支持的值： `none`， `bzip2`， `gzip`， `lz4`、和 `snappy`. | `none` | - | - |
| `fileType.value` | 可选 | 指定输出文件格式。 支持的值： `csv`， `parquet`、和 `json`. | `csv` | - | - |
| `csvOptions.quote.value` | 可选 | *仅用于`"fileType.value": "csv"`*. 设置用于转义带引号值的单个字符，其中分隔符可以是值的一部分。 | `null` | - | - |
| `csvOptions.quoteAll.value` | 可选 | *仅用于`"fileType.value": "csv"`*. 指示是否始终将所有值括在引号中。 默认为仅转义包含引号字符的值。 | `false` | `quoteAll`：`false` —> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | 可选 | *仅用于`"fileType.value": "csv"`*. 为每个字段和值设置分隔符。 此分隔符可以是一个或多个字符。 | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | 可选 | *仅用于`"fileType.value": "csv"`*. 设置一个用于在已被引号引起的值中将引号转义的字符。 | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | 可选 | *仅用于`"fileType.value": "csv"`*. 指示是否始终将包含引号的值括在引号中。 默认转义包含引号字符的所有值。 | `true` | - | - |
| `csvOptions.header.value` | 可选 | *仅用于`"fileType.value": "csv"`*. 指示是否将列名写入导出文件中的第一行。 | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | 可选 | *仅用于`"fileType.value": "csv"`*. 指示是否从值中修剪前导空格。 | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | 可选 | *仅用于`"fileType.value": "csv"`*. 指示是否从值中修剪尾随空格。 | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | 可选 | *仅用于`"fileType.value": "csv"`*. 设置空值的字符串表示形式。 | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | 可选 | *仅用于`"fileType.value": "csv"`*. 指示日期格式。 | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | 可选 | *仅用于`"fileType.value": "csv"`*. 设置指示时间戳格式的字符串。 | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | 可选 | *仅用于`"fileType.value": "csv"`*. 设置一个用于转义引号字符的转义的字符。 | `\` 当转义字符和引号字符不同时。 `\0` 当转义字符和引号字符相同时。 | - | - |
| `csvOptions.emptyValue.value` | 可选 | *仅用于`"fileType.value": "csv"`*. 设置空值的字符串表示形式。 | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |
| `maxFileRowCount` | 可选 | 指示每个导出文件的最大行数，介于1,000,000和10,000,000行之间。 | 5,000,000 |

{style="table-layout:auto"}

## 后续步骤 {#next-steps}

阅读本文后，您应该更好地了解文件格式在目标服务器配置中的工作方式以及配置方式。

要了解有关其他目标服务器组件的更多信息，请参阅以下文章：

* [使用Destination SDK创建的目标的服务器规范](server-specs.md)
* [模板规范](templating-specs.md)
* [消息格式](message-format.md)
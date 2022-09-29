---
description: 可通过/destination-servers端点在Adobe Experience Platform Destination SDK中配置基于文件的目标的服务器和文件配置规范。
title: 基于文件的目标服务器规范的配置选项
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 9%

---

# 基于文件的目标服务器规范的服务器和文件配置

## 概述 {#overview}

本页详细介绍了基于文件的目标服务器的所有服务器配置选项，并显示如何为用户设置各种文件配置选项，以便将文件从Experience Platform导出到您的目标。

基于文件的目标的服务器和文件配置规范可以通过Adobe Experience Platform Destination SDK `/destination-servers` 端点。 读取 [目标服务器API端点操作](./destination-server-api.md) 有关可对端点执行的操作的完整列表。

以下部分包括特定于Destination SDK中每个受支持的批处理目标类型的目标服务器规范。

## 基于文件的Amazon S3目标服务器规范 {#s3-example}

以下示例显示了Amazon S3目标的正确目标服务器配置。

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于 [!DNL Amazon S3]将设置为 `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字符串 | *必需。* 使用 `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | 字符串 | 的名称 [!DNL Amazon S3] 存储段供此目标使用。 |
| `fileBasedS3Destination.path.templatingStrategy` | 字符串 | *必需。* 使用 `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | 字符串 | 将托管导出文件的目标文件夹的路径。 |
| `fileConfigurations` | 对象 | 请参阅 [文件格式配置](#file-configuration) 以详细了解此部分。 |

{style=&quot;table-layout:auto&quot;}

## 基于文件的SFTP目标服务器规范 {#sftp-example}

以下示例显示了SFTP目标的正确目标服务器配置。

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于 [!DNL SFTP] 目标，将其设置为 `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | 字符串 | *必需。* 使用 `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | 字符串 | 目标存储的根目录。 |
| `fileBasedSftpDestination.hostName.templatingStrategy` | 字符串 | *必需。* 使用 `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | 字符串 | 目标存储的主机名。 |
| `port` | 整数 | SFTP文件服务器端口。 |
| `encryptionMode` | 字符串 | 指示是否使用文件加密。 支持的值： <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | 对象 | 请参阅 [文件格式配置](#file-configuration) 以详细了解此部分。 |

{style=&quot;table-layout:auto&quot;}

## 基于文件 [!DNL Azure Data Lake Storage] ([!DNL ADLS])目标服务器规范 {#adls-example}

以下示例显示了 [!DNL Azure Data Lake Storage] 目标。

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于 [!DNL Azure Data Lake Storage] 目标，将其设置为 `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字符串 | *必需。* 使用 `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | 字符串 | 将托管导出文件的目标文件夹的路径。 |
| `fileConfigurations` | 对象 | 请参阅 [文件格式配置](#file-configuration) 以详细了解此部分。 |

{style=&quot;table-layout:auto&quot;}

## 基于文件 [!DNL Azure Blob Storage] 目标服务器规范 {#blob-example}

以下示例显示了 [!DNL Azure Blob Storage] 目标。

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于 [!DNL Azure Blob Storage] 目标，将其设置为 `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字符串 | *必需。* 使用 `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | 字符串 | 将托管导出文件的目标文件夹的路径。 |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字符串 | *必需。* 使用 `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | 字符串 | 的名称 [!DNL Azure Blob Storage] 容器。 |
| `fileConfigurations` | 对象 | 请参阅 [文件格式配置](#file-configuration) 以详细了解此部分。 |

{style=&quot;table-layout:auto&quot;}

## 基于文件 [!DNL Data Landing Zone] ([!DNL DLZ])目标服务器规范 {#dlz-example}

以下示例显示了 [!DNL Data Landing Zone] ([!DNL DLZ])目标。

```json
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于 [!DNL Data Landing Zone] 目标，将其设置为 `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | 字符串 | *必需。*  使用 `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | 字符串 | 将托管导出文件的目标文件夹的路径。 |
| `fileConfigurations` | 对象 | 请参阅 [文件格式配置](#file-configuration) 以详细了解此部分。 |

{style=&quot;table-layout:auto&quot;}

## 基于文件 [!DNL Google Cloud Storage] 目标服务器规范 {#gcs-example}

以下示例显示了 [!DNL Google Cloud Storage] 目标。

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
   "fileConfigurations":{
      // See the file formatting configuration section further below on this page
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于 [!DNL Google Cloud Storage] 目标，将其设置为 `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字符串 | *必需。*  使用 `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字符串 | 的名称 [!DNL Google Cloud Storage] 存储段供此目标使用。 |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字符串 | *必需。* 使用 `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字符串 | 将托管导出文件的目标文件夹的路径。 |
| `fileConfigurations` | 对象 | 请参阅 [文件格式配置](#file-configuration) 以详细了解此部分。 |

{style=&quot;table-layout:auto&quot;}

## 文件格式配置 {#file-configuration}

本节介绍导出的文件格式设置 `CSV` 文件。 您可以修改导出文件的多个属性，以符合您所在方的文件接收系统的要求，以便以最佳方式读取和解释从Experience Platform接收的文件。

>[!NOTE]
>
>仅在导出CSV文件时支持CSV选项。 的 `fileConfigurations` 设置新的目标服务器时，不强制使用部分。 如果您没有在CSV选项的API调用中传递任何值，则默认值为 [参考表如下](#file-formatting-reference-and-example) 中，将使用。

### 使用CSV选项的文件配置，以及 `templatingStrategy` 设置为 `NONE` {#file-configuration-templating-none}

在以下配置示例中，所有CSV选项均已修复。 在 `csvOptions` 参数是最终参数，用户无法修改它们。

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

### 使用CSV选项的文件配置，以及 `templatingStrategy` 设置为 `PEBBLE_V1` {#file-configuration-templating-pebble}

在以下配置示例中，没有一个CSV选项是固定的。 的 `value` 在 `csvOptions` 参数通过相应的客户数据字段进行配置 `/destinations` 端点(例如 `customerData.quote` 对于 `quote` 文件格式选项)，用户可以使用Experience PlatformUI在您在相应客户数据字段中配置的各种选项之间进行选择。

```json
  "fileConfigurations": {
    "compression": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
    },
    "fileType": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.fileType}}"
    },
    "csvOptions": {
      "sep": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
      },
      "quote": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
      },
      "escape": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
      },
      "nullValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
      },
      "emptyValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
      }
    }
  }
```

### 有关支持的文件格式选项的完整参考和示例 {#file-formatting-reference-and-example}

>[!TIP]
>
>下面描述的CSV文件格式选项也介绍在 [适用于CSV文件的Apache Spark指南](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). 下面使用的说明摘自《Apache Spark指南》。

以下是Destination SDK中所有可用文件格式选项的完整引用，以及每个选项的输出示例。

| 字段 | 必填/可选 | 描述 | 默认值 | 示例输出1 | 示例输出2 |
|---|---|---|---|---|---|
| `templatingStrategy` | 必需 | 对于您配置的每个文件格式选项，需要添加参数 `templatingStrategy`，可以具有两个值： <br><ul><li>`NONE`:如果您不打算允许用户在配置的不同值之间进行选择，请使用此值。 请参阅 [此配置](#file-configuration-templating-none) 例如，文件格式选项是固定的示例。</li><li>`PEBBLE_V1`:如果您希望允许用户在配置的不同值之间进行选择，请使用此值。 在这种情况下，您还必须在 `/destination` 端点配置，以在UI中向用户显示各种选项。 请参阅 [此配置](#file-configuration-templating-pebble) 例如，用户可以为文件格式选项在不同的值之间进行选择。</li></ul> | - | - | - |
| `compression.value` | 可选 | 将数据保存到文件时使用的压缩编解码器。 支持的值： `none`, `bzip2`, `gzip`, `lz4`和 `snappy`. | `none` | - | - |
| `fileType.value` | 可选 | 指定输出文件格式。 支持的值： `csv`, `parquet`和 `json`. | `csv` | - | - |
| `csvOptions.quote.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 设置一个用于转义引号值的字符，其中分隔符可以是值的一部分。 | `null` | - | - |
| `csvOptions.quoteAll.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 指示是否应始终用引号将所有值括起来。 默认值是仅对包含引号字符的转义值进行转义。 | `false` | `quoteAll`:`false` —> `male,John,"TestLastName"` | `quoteAll`:`true` —>`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 为每个字段和值设置分隔符。 此分隔符可以是一个或多个字符。 | `,` | `delimiter`:`,` —> `comma-separated values"` | `delimiter`:`\t` —> `tab-separated values` |
| `csvOptions.escape.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 设置一个用于在已引号值内转义引号的字符。 | `\` | `"escape"`:`"\\"` —> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` —> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 指示包含引号的值是否应始终用引号括起来。 默认值是对包含引号字符的所有值进行转义。 | `true` | - | - |
| `csvOptions.header.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 指示是否将列的名称写入导出文件中的第一行。 | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 指示是否从值中裁切前导空格。 | `true` | `ignoreLeadingWhiteSpace`:`true` —> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`—> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 指示是否从值裁切尾随的空格。 | `true` | `ignoreTrailingWhiteSpace`:`true` —> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`—> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 设置空值的字符串表示形式。 | `""` | `nullvalue`:`""` —> `male,"",TestLastName` | `nullvalue`:`"NULL"` —> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 指示日期格式。 | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` —> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` —> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 设置指示时间戳格式的字符串。 | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 设置用于转义引号字符转义的单个字符。 | `\` 转义和引号字符不同时，指定的值。 `\0` 当转义和引号字符相同时。 | - | - |
| `csvOptions.emptyValue.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 设置空值的字符串表示形式。 | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` —> `male,empty,John` |

{style=&quot;table-layout:auto&quot;}
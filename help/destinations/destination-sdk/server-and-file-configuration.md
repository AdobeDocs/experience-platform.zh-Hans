---
description: 可通过/destination-servers端点在Adobe Experience Platform Destination SDK中配置基于文件的目标的服务器和文件配置规范。
title: （测试版）基于文件的目标服务器规范的配置选项
source-git-commit: bc357e2e93b80edb5f7825bf2dee692f14bd7297
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 10%

---

# （测试版）基于文件的目标服务器规范的服务器和文件配置

## 概述 {#overview}

>[!IMPORTANT]
>
>使用Adobe Experience Platform Destination SDK配置和提交基于文件的目标目前尚处于测试阶段。 文档和功能可能会发生更改。

本页详细介绍了基于文件的目标服务器的所有服务器配置选项，并指示您如何设置各种文件配置选项，以便用户将文件从Experience Platform导出到您的目标。

基于文件的目标的服务器和文件配置规范可以通过Adobe Experience Platform Destination SDK `/destination-servers` 端点。 读取 [目标服务器API端点操作](./destination-server-api.md) 有关可对端点执行的操作的完整列表。

## 基于文件的Amazon S3目标服务器规范 {#s3-example}

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
       // see File-based destinations file configuration
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

## 基于文件的SFTP目标服务器规范 {#sftp-example}

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
       // see File-based destinations file configuration
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

## 基于文件 [!DNL Azure Data Lake Storage] ([!DNL ADLS])目标服务器规范 {#adls-example}

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
       // see File-based destinations file configuration
    }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于 [!DNL Azure Data Lake Storage] 目标，将其设置为 `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字符串 | *必需。* 使用 `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | 字符串 | 将托管导出文件的目标文件夹的路径。 |

## 基于文件 [!DNL Azure Blob Storage] 目标服务器规范 {#blob-example}

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
       // see File-based destinations file configuration
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

## 基于文件 [!DNL Data Landing Zone] ([!DNL DLZ])目标服务器规范 {#dlz-example}

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
       // see File-based destinations file configuration
    }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于 [!DNL Data Landing Zone] 目标，将其设置为 `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | 字符串 | *必需。*  使用 `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | 字符串 | 将托管导出文件的目标文件夹的路径。 |

## 基于文件的目标文件配置 {#file-configuration}

本节介绍导出的文件格式设置 `CSV` 文件。 您可以修改导出文件的多个属性，以符合您所在方的文件接收系统的要求，以便以最佳方式读取和解释从Experience Platform接收的文件。

>[!NOTE]
>
>仅在导出CSV文件时支持CSV选项。 的 `fileConfigurations` 设置新的目标服务器时，不强制使用部分。 如果您没有在CSV选项的API调用中传递任何值，则将使用下表中的默认值。

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
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        }
    }
```

| 字段 | 必填/可选 | 描述 | 默认值 |
|---|---|---|---|
| `compression.value` | 可选 | 将数据保存到文件时使用的压缩编解码器。 支持的值： `none`, `bzip2`, `gzip`, `lz4`和 `snappy`. | `none` |
| `fileType.value` | 可选 | 指定输出文件格式。 支持的值： `csv`, `parquet`和 `json`. | `csv` |
| `csvOptions.quote.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 设置一个用于转义引号值的字符，其中分隔符可以是值的一部分。 | `null` |
| `csvOptions.quoteAll.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 指示是否应始终用引号将所有值括起来。 默认值是仅对包含引号字符的转义值进行转义。 | `false` |
| `csvOptions.escape.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 设置一个用于在已引号值内转义引号的字符。 | `\` |
| `csvOptions.escapeQuotes.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 指示包含引号的值是否应始终用引号括起来。 默认值是对包含引号字符的所有值进行转义。 | `true` |
| `csvOptions.header.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 指示是否将列的名称写入第一行。 | `true` |
| `csvOptions.ignoreLeadingWhiteSpace.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 指示是否从值中裁切前导空格。 | `true` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 指示是否从值中裁切尾随空格。 | `true` |
| `csvOptions.nullValue.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 设置空值的字符串表示形式。 | `""` |
| `csvOptions.dateFormat.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 指示日期格式。 | `yyyy-MM-dd` |
| `csvOptions.timestampFormat.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 设置指示时间戳格式的字符串。 | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` |
| `csvOptions.charToEscapeQuoteEscaping.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 设置用于转义引号字符转义的单个字符。 | `\` 转义和引号字符不同时，指定的值。 `\0` 当转义和引号字符相同时。 |
| `csvOptions.emptyValue.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 设置空值的字符串表示形式。 | `""` |
| `csvOptions.lineSep.value` | 可选 | *仅适用于`"fileType.value": "csv"`*. 定义应用于写入的行分隔符。 最大长度为1个字符。 | `\n` |

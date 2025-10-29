---
keywords: Experience Platform；主页；热门主题；批量摄取；批量摄取；部分摄取；部分摄取；检索错误；检索错误；部分批量摄取；部分批次摄取；部分；摄取；摄取；错误诊断；检索错误诊断；获取错误诊断；获取错误；获取错误；检索错误；
solution: Experience Platform
title: 检索数据摄取错误诊断
description: 本文档提供了有关监控批次摄取、管理部分批次摄取错误的信息，以及部分批次摄取类型的参考。
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 12%

---

# 检索数据摄取错误诊断

Adobe Experience Platform提供两种上传和摄取数据的方法。 您可以使用批量摄取，这允许您使用各种文件类型（如CSV）插入数据；也可以使用流式摄取，这允许您使用流式端点实时将其数据插入到[!DNL Experience Platform]。

本文档提供了有关监控批次摄取、管理部分批次摄取错误的信息，以及部分批次摄取类型的参考。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md)：将数据发送到[!DNL Experience Platform]的方法。

### 正在读取示例 API 调用

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例 API 调用的文档中所用惯例的信息，请参阅故障排除指南中的[如何读取示例 API 调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform]。

### 收集所需标头的值

为调用 [!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Schema Registry]的资源）都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

## 正在下载错误诊断 {#download-diagnostics}

Adobe Experience Platform允许用户下载输入文件的错误诊断。 诊断将在[!DNL Experience Platform]内保留最多30天。

### 列出输入文件 {#list-files}

以下请求检索在最终确定的批次中提供的所有文件的列表。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 要查找的批次的ID。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回JSON对象，该对象详细说明诊断的保存位置。

```json
{
    "_page": {
        "count": 1,
        "limit": 100
    },
    "data": [
        {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### 检索输入文件诊断 {#retrieve-diagnostics}

检索完所有不同输入文件的列表后，可以使用以下请求检索单个文件的诊断。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 要查找的批次的ID。 |
| `{FILE}` | 您正在访问的文件的名称。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回包含`path`个对象的JSON对象，这些对象详细说明诊断的保存位置。 响应将返回`path`JSON行[格式的](https://jsonlines.readthedocs.io/en/latest/)对象。

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## 检索批次摄取错误 {#retrieve-errors}

如果批次包含失败，您应该检索有关这些失败的错误信息，以便重新摄取数据。

### 检查状态 {#check-status}

要检查摄取批次的状态，必须在GET请求的路径中提供批次的ID。 要了解有关使用此API调用的更多信息，请阅读[目录终结点指南](../../catalog/api/list-objects.md)。

**API格式**

```http
GET /catalog/batches/{BATCH_ID}
GET /catalog/batches/{BATCH_ID}?{FILTER}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要检查其状态的批次的`id`值。 |
| `{FILTER}` | 用于筛选响应中返回结果的查询参数。 多个参数由&amp;符号(`&`)分隔。 有关详细信息，请阅读[筛选目录数据](../../catalog/api/filter-data.md)的指南。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**没有错误的响应**

成功的响应将返回，其中包含有关批次状态的详细信息。

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{ORG_ID}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497,
            "failedRecordCount": 0
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `metrics.failedRecordCount` | 由于解析、转换或验证而无法处理的行数。 此值可以通过从`inputRecordCount`中减去`outputRecordCount`而派生。 此值在所有批次中生成，无论是否启用了`errorDiagnostics`。 |

**带有错误的响应**

如果批次具有一个或多个错误并启用了错误诊断，则响应将返回有关错误的更多信息，这些信息既存在于有效负荷中，也存在于可下载的错误文件中。 请注意，包含错误的批次的状态可能仍具有成功状态。

```json
{
    "01E8043CY305K2MTV5ANH9G1GC": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "01E8043CY305K2MTV5ANH9G1GC",
        "externalId": "01E8043CY305K2MTV5ANH9G1GC",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{ORG_ID}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 514,
            "failedRecordCount": 5
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5",
        "errors": [
           {
             "code": "INGEST-1212-400",
             "description": "Encountered 5 errors in the data. Successfully ingested 514 rows. Please review the associated diagnostic files for more details."
           },
           {
             "code": "INGEST-1401-400",
             "description": "The row has corrupted data and cannot be read or parsed. Fix the corrupted data and try again.",
             "recordCount": 2
           },
           {
             "code": "INGEST-1555-400",
             "description": "A required field is either missing or has a value of null. Add the required field to the input row and try again.",
             "recordCount": 3
           }
        ]
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `metrics.failedRecordCount` | 由于解析、转换或验证而无法处理的行数。 此值可以通过从`inputRecordCount`中减去`outputRecordCount`而派生。 此值在所有批次中生成，无论是否启用了`errorDiagnostics`。 |
| `errors.recordCount` | 因指定的错误代码而失败的行数。 如果启用了&#x200B;**，则只生成** 1}值。`errorDiagnostics` |

>[!NOTE]
>
>如果错误诊断不可用，则会显示以下错误消息：
>
>```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## 后续步骤 {#next-steps}

本教程介绍了如何监测部分批次摄取错误。 有关批量摄取的更多信息，请阅读[批量摄取开发人员指南](../batch-ingestion/api-overview.md)。

## 附录 {#appendix}

本节提供有关摄取错误类型的补充信息。

### 部分批次摄取错误类型 {#partial-ingestion-types}

摄取数据时，部分批次摄取具有三种不同的错误类型：

- [无法读取的文件](#unreadable)
- [架构或标头无效](#schemas-headers)
- [无法分析的行](#unparsable)

### 无法读取的文件 {#unreadable}

如果摄取的批次具有不可读的文件，则批次的错误将附加到批次本身。 有关检索失败的批次的详细信息，请参阅[检索失败的批次指南](../quality/retrieve-failed-batches.md)。

### 架构或标头无效 {#schemas-headers}

如果摄取的批次具有无效架构或无效标头，则批次的错误将附加到批次本身。 有关检索失败的批次的详细信息，请参阅[检索失败的批次指南](../quality/retrieve-failed-batches.md)。

### 无法分析的行 {#unparsable}

如果您摄取的批处理包含不可分析的行，则可以使用以下请求查看包含错误的文件列表。

**API格式**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 正在从中检索错误信息的批次的`id`值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含错误的文件列表。

```json
{
    "data": [
        {
            "name": "conversion_errors_0.json",
            "length": "1162",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fconversion_errors_0.json"
                }
            }
        },
        {
            "name": "parsing_errors_0.json",
            "length": "153",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fparsing_errors_0.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

然后，可以使用[诊断检索终结点](#retrieve-diagnostics)检索有关错误的详细信息。

检索错误文件的示例响应如下所示：

```json
{
    "_corrupt_record": "{missingQuotes: 'v1'}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```

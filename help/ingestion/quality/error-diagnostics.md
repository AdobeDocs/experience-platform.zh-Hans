---
keywords: Experience Platform；主页；热门主题；批量摄取；批量摄取；部分摄取；部分摄取；检索错误；检索错误；部分批量摄取；部分批量摄取；部分；摄取；摄取；错误诊断；检索错误诊断；获取错误诊断；获取错误；获取错误；检索错误；
solution: Experience Platform
title: 检索数据摄取错误诊断
topic-legacy: overview
description: 本文档提供了有关监控批量摄取、管理部分批量摄取错误的信息，以及有关部分批量摄取类型的参考。
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 2%

---

# 检索数据摄取错误诊断

Adobe Experience Platform提供了两种上传和摄取数据的方法。 您可以使用批量摄取(允许您使用各种文件类型（如CSV）插入数据)，或使用流式摄取(允许您将其数据插入到 [!DNL Platform] 实时使用流端点。

本文档提供了有关监控批量摄取、管理部分批量摄取错误的信息，以及有关部分批量摄取类型的参考。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md):将数据发送到的方法 [!DNL Experience Platform].

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括属于 [!DNL Schema Registry]，与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

## 下载错误诊断 {#download-diagnostics}

Adobe Experience Platform允许用户下载输入文件的错误诊断程序。 诊断将保留在 [!DNL Platform] 最多30天。

### 列出输入文件 {#list-files}

以下请求将检索完成批处理中提供的所有文件的列表。

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

成功的响应将返回JSON对象，详细说明保存诊断的位置。

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

在检索到所有不同输入文件的列表后，您可以使用以下请求检索单个文件的诊断信息。

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

成功的响应将返回包含 `path` 详细说明保存诊断的位置的对象。 响应将返回 `path` 对象 [JSON行](https://jsonlines.org/) 格式。

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## 检索批量摄取错误 {#retrieve-errors}

如果批量包含失败，则应检索有关这些失败的错误信息，以便可以重新摄取数据。

### 检查状态 {#check-status}

要检查摄取的批的状态，必须在GET请求路径中提供批的ID。 要了解有关使用此API调用的更多信息，请阅读 [catalog endpoint guide](../../catalog/api/list-objects.md).

**API格式**

```http
GET /catalog/batches/{BATCH_ID}
GET /catalog/batches/{BATCH_ID}?{FILTER}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 的 `id` 要检查状态的批的值。 |
| `{FILTER}` | 用于筛选响应中返回的结果的查询参数。 多个参数以与号(`&`)。 有关更多信息，请阅读 [筛选目录数据](../../catalog/api/filter-data.md). |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**无错误响应**

成功的响应会返回有关批处理状态的详细信息。

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
| `metrics.failedRecordCount` | 由于解析、转换或验证而无法处理的行数。 此值可通过减去 `inputRecordCount` 从 `outputRecordCount`. 此值在所有批次上生成，无论 `errorDiagnostics` 启用。 |

**有错误的响应**

如果批处理有一个或多个错误并启用了错误诊断，则响应会返回有关错误的更多信息，包括有效载荷本身以及可下载的错误文件。 请注意，包含错误的批处理的状态可能仍为成功状态。

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
| `metrics.failedRecordCount` | 由于解析、转换或验证而无法处理的行数。 此值可通过减去 `inputRecordCount` 从 `outputRecordCount`. 此值在所有批次上生成，无论 `errorDiagnostics` 启用。 |
| `errors.recordCount` | 指定错误代码失败的行数。 此值为 **仅** 生成条件 `errorDiagnostics` 启用。 |

>[!NOTE]
>
>如果错误诊断不可用，将改为显示以下错误消息：
>
```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## 后续步骤 {#next-steps}

本教程介绍了如何监控部分批量摄取错误。 有关批量摄取的更多信息，请阅读 [批量获取开发人员指南](../batch-ingestion/api-overview.md).

## 附录 {#appendix}

本节提供有关摄取错误类型的补充信息。

### 部分批量摄取错误类型 {#partial-ingestion-types}

部分批量摄取在摄取数据时有三种不同的错误类型：

- [不可读的文件](#unreadable)
- [无效的架构或标头](#schemas-headers)
- [不可解析的行](#unparsable)

### 不可读的文件 {#unreadable}

如果摄取的批处理文件不可读，则该批处理的错误将附加在该批处理本身上。 有关检索失败批的详细信息，请参阅 [检索失败的批量指南](../quality/retrieve-failed-batches.md).

### 无效的架构或标头 {#schemas-headers}

如果摄取的批次具有无效架构或无效标题，则批次的错误将附加到该批次本身。 有关检索失败批的详细信息，请参阅 [检索失败的批量指南](../quality/retrieve-failed-batches.md).

### 不可解析的行 {#unparsable}

如果摄取的批处理具有不可解析的行，您可以使用以下请求查看包含错误的文件列表。

**API格式**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 的 `id` 从中检索错误信息的批的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回有错误的文件列表。

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

然后，您可以使用 [诊断检索端点](#retrieve-diagnostics).

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

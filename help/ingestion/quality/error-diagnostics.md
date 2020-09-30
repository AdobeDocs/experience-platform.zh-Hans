---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;partial ingestion;Partial ingestion;Retrieve error;retrieve error;Partial batch ingestion;partial batch ingestion;partial;ingestion;Ingestion;error diagnostics;retrieve error diagnostics;get error diagnostics;get error;get errors;retrieve errors;
solution: Experience Platform
title: Adobe Experience Platform分批摄取概述
topic: overview
description: 此文档提供有关监视批处理摄取、管理部分批处理摄取错误的信息，以及部分批处理摄取类型的参考。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 2%

---


# 检索错误诊断

Adobe Experience Platform提供两种上传和摄取数据的方法。 您可以使用批处理摄取(允许您使用各种文件类型（如CSV）插入数据)或流式摄取(允许您使用流式端点将数据 [!DNL Platform] 实时插入)。

此文档提供有关监视批处理摄取、管理部分批处理摄取错误的信息，以及部分批处理摄取类型的参考。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

- [[!DNL体验数据模型(XDM)系统]](../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
- [[!DNLAdobe Experience Platform数据摄取]](../home.md):发送数据的方 [!DNL Experience Platform]法

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资源 [!DNL Schema Registry]的资源)都隔离到特定虚拟沙箱。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

## 下载错误诊断 {#download-diagnostics}

Adobe Experience Platform允许用户下载输入文件的错误诊断。 诊断程序将在最 [!DNL Platform] 长30天内保留。

### 列表输入文件 {#list-files}

以下请求检索最终批中提供的所有文件的列表。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 要查找的批的ID。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回详细说明保存诊断的JSON对象。

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

检索到所有不同输入文件的列表后，可以使用以下请求检索单个文件的诊断。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 要查找的批的ID。 |
| `{FILE}` | 要访问的文件的名称。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回包含详细 `path` 说明保存诊断的对象的JSON对象。 响应将返回JSON `path` 行格 [式的对象](https://jsonlines.org/) 。

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## 检索批摄取错误 {#retrieve-errors}

如果批包含失败，则应检索有关这些失败的错误信息，以便重新摄取数据。

### 检查状态 {#check-status}

要检查所摄取批的状态，必须在GET请求的路径中提供批的ID。

**API格式**

```http
GET /catalog/batches/{BATCH_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要 `id` 检查其状态的批的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**无错误响应**

成功的响应会返回，并包含有关批状态的详细信息。

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
        "imsOrg": "{IMS_ORG}",
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
| `metrics.failedRecordCount` | 由于分析、转换或验证而无法处理的行数。 此值可通过从中减去 `inputRecordCount` 来导 `outputRecordCount`出。 无论是否启用，该值都会在所有批 `errorDiagnostics` 上生成。 |

**有错误的响应**

如果批处理有一个或多个错误并启用了错误诊断，则响应将返回有关错误的更多信息，包括有效负荷本身以及可下载的错误文件。 请注意，包含错误的批的状态可能仍为成功状态。

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
        "imsOrg": "{IMS_ORG}",
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
| `metrics.failedRecordCount` | 由于分析、转换或验证而无法处理的行数。 此值可通过从中减去 `inputRecordCount` 来导 `outputRecordCount`出。 无论是否启用，该值都会在所有批 `errorDiagnostics` 上生成。 |
| `errors.recordCount` | 指定错误代码失败的行数。 此值仅在 **启用** 后 `errorDiagnostics` 生成。 |

>[!NOTE]
>
>如果错误诊断不可用，将显示以下错误消息：
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

本教程介绍了如何监视部分批摄取错误。 有关批量摄取的详细信息，请阅读批 [量摄取开发人员指南](../batch-ingestion/api-overview.md)。

## 附录 {#appendix}

本节提供有关摄取错误类型的补充信息。

### 部分批摄取错误类型 {#partial-ingestion-types}

部分批处理摄取在摄取数据时有三种不同的错误类型：

- [不可读文件](#unreadable)
- [模式或标题无效](#schemas-headers)
- [不可分行](#unparsable)

### 不可读文件 {#unreadable}

如果所摄取的批次具有不可读的文件，则批次的错误将附加到该批次本身。 有关检索失败批次的详细信息，请参阅检 [索失败批次指南](../quality/retrieve-failed-batches.md)。

### 模式或标题无效 {#schemas-headers}

如果所摄取的批具有无效的模式或无效的题头，则该批的错误将附加到该批本身。 有关检索失败批次的详细信息，请参阅检 [索失败批次指南](../quality/retrieve-failed-batches.md)。

### 不可分行 {#unparsable}

如果所摄取的批次具有不可分割的行，您可以使用以下请求视图包含错误的一列表文件。

**API格式**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要 `id` 从中检索错误信息的批的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回有错误的文件的列表。

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

然后，您可以使用诊断检索端点检索有关错误 [的详细信息](#retrieve-diagnostics)。

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

---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform分批摄取概述
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 1%

---



# 部分批摄取

部分批量摄取是指能够摄取包含错误的数据，最高可达到某个阈值。 借助此功能，用户可以成功将其所有正确数据引入Adobe Experience Platform，同时单独对其所有错误数据进行分组，并详细说明其无效原因。

此文档提供了管理部分批摄取的教程。

此外，本教程 [的附录](#appendix) ，还提供了部分批量摄取错误类型的参考。

## 入门指南

本教程需要对涉及部分批量摄取的Adobe Experience Platform各项服务有一定的工作知识。 在开始本教程之前，请查看以下服务的相关文档：

- [批量摄取](./overview.md):从数据文 [!DNL Platform] 件（如CSV和Parke）中摄取和存储数据的方法。
- [[!DNL Experience Data Model] (XDM)](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

以下各节提供了成功调用API所需了解的其他信 [!DNL Platform] 息。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

- 授权：承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

## 在API中启用批以进行部分批摄取 {#enable-api}

>[!NOTE]
>
>本节介绍如何使用API启用批处理以进行部分批处理获取。 有关使用UI的说明，请阅读在UI [步骤中启用批以进行部分批摄取](#enable-ui) 。

您可以创建启用了部分摄取的新批。

要创建新批，请按照批摄取开发人员指 [南中的步骤操作](./api-overview.md)。 到达创建批 **[!UICONTROL 处理步骤]** 后，在请求主体中添加以下字段：

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `enableErrorDiagnostics` | 用于生成有关 [!DNL Platform] 批的详细错误消息的标志。 |
| `partialIngestionPercentage` | 整个批处理失败之前可接受错误的百分比。 因此，在本示例中，最多5%的批可能是错误，然后才会失败。 |


## 在UI中启用批以进行部分批摄取 {#enable-ui}

>[!NOTE]
>
>本节介绍如何使用UI启用批以进行部分批摄取。 如果已使用API启用批处理以进行部分批摄取，则可跳到下一节。

要通过UI启用批处理以进行部分 [!DNL Platform] 摄取，您可以通过源连接创建新批处理，在现有数据集中创建新批处理，或通过“将CSV映射到XDM流[!UICONTROL ”创建新批]。

### 创建新源连接 {#new-source}

要创建新的源连接，请按照“源”概述中列出 [的步骤操作](../../sources/home.md)。 进入“数据 **[!UICONTROL 流详细信息]** ”步骤后，请注意“部 **[!UICONTROL 分摄取]** ”和“ **[!UICONTROL 错误诊断]** ”字段。

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

“部 **[!UICONTROL 分摄取]** ”切换允许您启用或禁用部分批摄取。

仅当 **[!UICONTROL “部分摄取]** ”切换关闭时，才 **[!UICONTROL 会显示]** “错误诊断”切换。 此功能允许 [!DNL Platform] 生成有关所摄取批的详细错误消息。 如果打 *[!UICONTROL 开“部分摄取]* ”切换，将自动实施增强的错误诊断。

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

“错 **[!UICONTROL 误阈值]** ”允许您在整个批处理失败之前设置可接受错误的百分比。 默认情况下，此值设置为5%。

### 使用现有数据集 {#existing-dataset}

要使用现有数据集，请通过选择开始集进行。 右侧的提要栏会填充有关数据集的信息。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

“部 **[!UICONTROL 分摄取]** ”切换允许您启用或禁用部分批摄取。

仅当 **[!UICONTROL “部分摄取]** ”切换关闭时，才 **[!UICONTROL 会显示]** “错误诊断”切换。 此功能允许 [!DNL Platform] 生成有关所摄取批的详细错误消息。 如果打 **[!UICONTROL 开“部分摄取]** ”切换，将自动实施增强的错误诊断。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

“错 **[!UICONTROL 误阈值]** ”允许您在整个批处理失败之前设置可接受错误的百分比。 默认情况下，此值设置为5%。

现在，您可以使用“添加数 **据”按钮** ，并且将使用部分摄取来摄取数据。

### 使用“将[!UICONTROL CSV映射到XDM模式]”流 {#map-flow}

要使用“将[!UICONTROL CSV映射到XDM模式]”流程，请按照映射CSV文件教 [程中列出的步骤操作](../tutorials/map-a-csv-file.md)。 进入“添加数 **[!UICONTROL 据]** ”步骤后，请注意“部 **[!UICONTROL 分摄取]** ”和“ **[!UICONTROL 错误诊断]** ”字段。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

“部 **[!UICONTROL 分摄取]** ”切换允许您启用或禁用部分批摄取。

仅当 **[!UICONTROL “部分摄取]** ”切换关闭时，才 **[!UICONTROL 会显示]** “错误诊断”切换。 此功能允许 [!DNL Platform] 生成有关所摄取批的详细错误消息。 如果打 **[!UICONTROL 开“部分摄取]** ”切换，将自动实施增强的错误诊断。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

“错 **[!UICONTROL 误阈值]** ”允许您在整个批处理失败之前设置可接受错误的百分比。 默认情况下，此值设置为5%。

## 下载文件级元数据 {#download-metadata}

Adobe Experience Platform允许用户下载输入文件的元数据。 元数据将在最 [!DNL Platform] 多30天内保留。

### 列表输入文件 {#list-files}

以下请求将允许您视图定稿批次中提供的所有文件的列表。

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回HTTP状态200，其中JSON对象包含详细描述元数据保存位置的路径对象。

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
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### 检索输入文件元数据 {#retrieve-metadata}

检索到所有不同输入文件的列表后，可以使用以下端点检索单个文件的元数据。

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回HTTP状态200，其中JSON对象包含详细描述元数据保存位置的路径对象。

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## 检索部分批摄取错误 {#retrieve-errors}

如果批包含失败，您需要检索有关这些失败的错误信息，以便重新摄取数据。

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
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**无错误响应**

成功的响应返回HTTP状态200，其中包含有关批处理状态的详细信息。

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
| `metrics.failedRecordCount` | 由于分析、转换或验证而无法处理的行数。 此值可通过从中减去 `inputRecordCount` 来导 `outputRecordCount`出。 无论是否启用，都将在所有批上生成 `errorDiagnostics` 此值。 |

**有错误的响应**

如果批处理有一个或多个错误并且启用了错误诊断，则状态将包含有关在响 `success` 应中和可下载的错误文件中提供的错误的更多信息。

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
| `metrics.failedRecordCount` | 由于分析、转换或验证而无法处理的行数。 此值可通过从中减去 `inputRecordCount` 来导 `outputRecordCount`出。 无论是否启用，都将在所有批上生成 `errorDiagnostics` 此值。 |
| `errors.recordCount` | 指定错误代码失败的行数。 此值仅在 **启用** 后 `errorDiagnostics` 生成。 |

>[!NOTE]
>
>如果错误诊断不可用，将显示以下错误消息：
> 
```json
> {
>         "errors": [{
>                 "code": "INGEST-1211-400",
>                 "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>         }]
> }
> ```

## 后续步骤 {#next-steps}

本教程介绍了如何创建或修改数据集以启用部分批量摄取。 有关批量摄取的详细信息，请阅读批 [量摄取开发人员指南](./api-overview.md)。

## 部分批摄取错误类型 {#appendix}

部分批量摄取在摄取数据时有三种不同的错误类型。

- [不可读文件](#unreadable)
- [模式或标题无效](#schemas-headers)
- [不可分行](#unparsable)

### 不可读文件 {#unreadable}

如果所摄取的批次具有不可读的文件，则批次的错误将附加到该批次本身。 有关检索失败批次的详细信息，请参阅检 [索失败批次指南](../quality/retrieve-failed-batches.md)。

### 模式或标题无效 {#schemas-headers}

如果所摄取的批具有无效的模式或无效的题头，则该批的错误将附加到该批本身。 有关检索失败批次的详细信息，请参阅检 [索失败批次指南](../quality/retrieve-failed-batches.md)。

### 不可分行 {#unparsable}

如果所摄取的批次具有不可分割的行，您可以使用以下端点视图包含错误的一列表文件。

**API格式**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要 `id` 从中检索错误信息的批的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200,列表有错误的文件。

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

然后，您可以使用元数据检索端点检索有关错误 [的详细信息](#retrieve-metadata)。

检索错误文件的示例响应如下所示：

```json
{
    "_corrupt_record": "{missingQuotes: "v1"}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```

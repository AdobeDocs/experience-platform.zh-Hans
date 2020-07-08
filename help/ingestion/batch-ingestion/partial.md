---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform部分批摄取概述
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 2%

---



# 部分批摄取（测试版）

部分批量摄取是指能够摄取包含错误的数据，最高可达到某个阈值。 借助此功能，用户可以成功将其所有正确数据引入Adobe Experience Platform，同时单独对其所有错误数据进行批处理，并详细了解其无效原因。

此文档提供了管理部分批摄取的教程。

此外，本教程 [的附录](#appendix) ，还提供了部分批量摄取错误类型的参考。

>[!IMPORTANT]
>
>此功能仅在使用API时存在。 请联系您的团队以获取此功能。

## 入门指南

本教程需要掌握与部分批量摄取相关的各种Adobe Experience Platform服务的相关工作知识。 在开始本教程之前，请查看以下服务的相关文档：

- [批量摄取](./overview.md): 平台从数据文件（如CSV和Parke）中摄取和存储数据的方法。
- [体验数据模型(XDM)](../../xdm/home.md): 平台组织客户体验数据的标准化框架。

以下各节提供了成功调用平台API所需了解的其他信息。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的章节。

### 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

- 授权： 承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都隔离到特定虚拟沙箱。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

## 在API中启用数据集以进行部分批摄取

<!-- >[!NOTE] This section describes enabling a dataset for partial batch ingestion using the API. For instructions on using the UI, please read the [enable a dataset for partial batch ingestion in the UI](#enable-a-dataset-for-partial-batch-ingestion-in-the-ui) step. -->

您可以创建新数据集或修改启用部分摄取的现有数据集。

要创建新数据集，请按照创建数据集教 [程中的步骤操作](../../catalog/api/create-dataset.md)。 到达创建数 *据集步骤后* ，在请求主体中添加以下字段：

```json
{
    ...
    "tags" : {
        "partialBatchIngestion":["errorThresholdPercentage:5"]
    },
    ...
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `errorThresholdPercentage` | 整个批处理失败之前可接受错误的百分比。 |

同样，要修改现有数据集，请按照目录开发人员指 [南中的步骤操作](../../catalog/api/update-object.md)。

在数据集中，您需要添加上述标记。

<!-- ## Enable a dataset for partial batch ingestion in the UI

>[!NOTE]
>
>This section describes enabling a dataset for partial batch ingestion using the UI. If you have already enabled a dataset for partial batch ingestion using the API, you can skip ahead to the next section.

To enable a dataset for partial ingestion through the Platform UI, click **Datasets** in the left navigation. You can either [create a new dataset](#create-a-new-dataset-with-partial-batch-ingestion-enabled) or [modify an existing dataset](#modify-an-existing-dataset-to-enable-partial-batch-ingestion).

### Create a new dataset with partial batch ingestion enabled

To create a new dataset, follow the steps in the [dataset user guide](../../catalog/datasets/user-guide.md). Once you reach the *Configure dataset* step, take note of the *Partial Ingestion* and *Error Diagnostics* fields.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-focus.png)

The *Partial ingestion* toggle allows you to enable or disable the use of partial batch ingestion.

The *Error Diagnostics* toggle only appears when the *Partial Ingestion* toggle is off. This feature allows Platform to generate detailed error messages about your ingested batches. If the *Partial Ingestion* toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-partial-ingestion-focus.png)

The *Error threshold* allows you to set the percentage of acceptable errors before the entire batch will fail. By default, this value is set to 5%.

### Modify an existing dataset to enable partial batch ingestion

To modify an existing dataset, select the dataset you want to modify. The sidebar on the right populates with information about the dataset. 

![](../images/batch-ingestion/partial-ingestion/modify-dataset-focus.png)

The *Partial ingestion* toggle allows you to enable or disable the use of partial batch ingestion.

The *Error threshold* allows you to set the percentage of acceptable errors before the entire batch will fail. By default, this value is set to 5%. -->

## 检索部分批摄取错误

如果批包含失败，您需要检索有关这些失败的错误信息，以便重新摄取数据。

### 检查状态

要检查所摄取批的状态，必须在GET请求的路径中提供该批的ID。

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

**响应**

成功的响应返回HTTP状态200，其中包含有关批处理状态的详细信息。

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            ...
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
            "outputRecordCount": 497
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

如果批处理有错误并启用了错误诊断，状态将“成功”，并在可下载的错误文件中提供更多有关错误的信息。

## 后续步骤

本教程介绍了如何创建或修改数据集以启用部分批量摄取。 有关批量摄取的详细信息，请阅读批 [量摄取开发人员指南](./api-overview.md)。

## 部分批摄取错误类型 {#appendix}

部分批量摄取在摄取数据时有四种不同的错误类型。

- [不可读文件](#unreadable)
- [模式或标题无效](#schemas-headers)
- [不可分行](#unparsable)
- [XDM转换无效](#conversion)

### 不可读文件 {#unreadable}

如果所摄取的批次具有不可读的文件，则批次的错误将附加到该批次本身。 有关检索失败批次的详细信息，请参阅检 [索失败批次指南](../quality/retrieve-failed-batches.md)。

### 模式或标题无效 {#schemas-headers}

如果所摄取的批具有无效的模式或无效的题头，则该批的错误将附加到该批本身。 有关检索失败批次的详细信息，请参阅检 [索失败批次指南](../quality/retrieve-failed-batches.md)。

### 不可分行 {#unparsable}

如果所摄取的批次具有不可分割的行，则该批次的错误将存储在文件中，可使用下面概述的端点进行访问。

**API格式**

```http
GET /export/batches/{BATCH_ID}/failed?path=parse_errors
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要 `id` 从中检索错误信息的批的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=parse_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含不可分行的详细信息。

```json
{
    "_corrupt_record":"{missingQuotes:"v1"}",
    "_errors": [{
         "code":"1401",
         "message":"Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "a1.json"
}
```

### XDM转换无效 {#conversion}

如果所摄取的批处理具有无效的XDM转换，则批处理的错误将存储在文件中，可通过以下端点访问该文件。

**API格式**

```http
GET /export/batches/{BATCH_ID}/failed?path=conversion_errors
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要 `id` 从中检索错误信息的批的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=conversion_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含XDM转换失败的详细信息。

```json
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col3",
        "code":"123",
        "message":"Cannot convert array element from Object to String"
    }],
    "_filename":"a1.json"
},
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col1",
        "code":"100",
        "message":"Cannot convert string to float"
    }],
    "_filename":"a2.json"
}
```

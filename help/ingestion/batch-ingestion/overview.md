---
keywords: Experience Platform；主页；热门主题；数据摄取；批量；启用数据集；批量摄取概述；概述；批量摄取概述；
solution: Experience Platform
title: 批量摄取概述
topic-legacy: overview
description: Adobe Experience Platform数据摄取API允许您将数据作为批处理文件导入到平台中。 摄取的数据可以是CRM系统中平面文件（如Parquet文件）中的配置文件数据，也可以是符合体验数据模型(XDM)注册表中已知架构的数据。
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 3%

---

# 批量摄取概述

Adobe Experience Platform数据摄取API允许您将数据作为批处理文件导入到平台中。 摄取的数据可以是CRM系统中平面文件（如Parquet文件）中的配置文件数据，也可以是符合[!DNL Experience Data Model](XDM)注册表中已知架构的数据。

[数据摄取API引用](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)提供有关这些API调用的其他信息。

下图概述了批量摄取流程：

![](../images/batch-ingestion/overview/batch_ingestion.png)

## 使用 API

[!DNL Data Ingestion] API允许您通过三个基本步骤将数据作为批量（由一个或多个要作为单个单位摄取的文件组成的数据单元）摄取到[!DNL Experience Platform]中：

1. 创建新批。
2. 将文件上传到与数据的XDM架构匹配的指定数据集。
3. 表示批次的结束。


### [!DNL Data Ingestion] 先决条件

- 要上传的数据必须采用Parquet或JSON格式。
- 在[[!DNL Catalog services]](../../catalog/home.md)中创建的数据集。
- Parquet文件的内容必须与要上传到的数据集架构的子集相匹配。
- 验证后拥有您的唯一访问令牌。

### 批量摄取最佳实践

- 建议的批处理大小介于256 MB到100 GB之间。
- 每个批次最多应包含1500个文件。

要上传大于512MB的文件，需要将文件分为较小的块。 在[此处](#large-file-upload---create-file)可找到上载大文件的说明。

### 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅[!DNL Experience Platform]疑难解答指南中[如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程可为所有[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

- 授权：载体`{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

[!DNL Experience Platform]中的所有资源均与特定虚拟沙箱隔离。 对[!DNL Platform] API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

- Content-Type:application/json

### 创建批处理

在将数据添加到数据集之前，必须先将其链接到批次，然后批次才会上传到指定的数据集。

```http
POST /batches
```

**请求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `datasetId` | 要将文件上传到的数据集的ID。 |

**响应**

```JSON
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 刚刚创建的批次的ID（用于后续请求）。 |
| `relatedObjects.id` | 要将文件上传到的数据集的ID。 |

## 文件上传

成功创建新批次以进行上传后，便可以将文件上传到特定数据集。

您可以使用小文件上传API上传文件。 但是，如果文件过大且超出了网关限制（例如，延长超时、超出主体大小请求和其他限制），则可以切换到大文件上传API。 此API以块形式上传文件，并使用大文件上传结束API调用将数据拼合在一起。

>[!NOTE]
>
>以下示例使用[Apache Parquet](https://parquet.apache.org/documentation/latest/)文件格式。 [批量摄取开发人员指南](./api-overview.md)中提供了使用JSON文件格式的示例。

### 小文件上传

创建批处理后，即可将数据上传到预先存在的数据集。  上传的文件必须与其引用的XDM架构匹配。

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 批次的ID。 |
| `{DATASET_ID}` | 要上传文件的数据集的ID。 |
| `{FILE_NAME}` | 数据集中将显示的文件名称。 |

**请求**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 要上传到数据集中的文件的路径和文件名。 |

**响应**

```JSON
#Status 200 OK, with empty response body
```

### 大文件上传 — 创建文件

要上传大文件，必须将文件拆分为较小的块，并一次上传一个。

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 批次的ID。 |
| `{DATASET_ID}` | 摄取文件的数据集的ID。 |
| `{FILE_NAME}` | 数据集中将显示的文件名称。 |

**请求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**响应**

```JSON
#Status 201 CREATED, with empty response body
```

### 大文件上传 — 上传后续部分

创建文件后，可通过发出重复的PATCH请求来上传所有后续区块，该请求对应文件的每个部分一个。

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 批次的ID。 |
| `{DATASET_ID}` | 要将文件上传到的数据集的ID。 |
| `{FILE_NAME}` | 数据集中将显示的文件名称。 |

**请求**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 要上传到数据集中的文件的路径和文件名。 |

**响应**

```JSON
#Status 200 OK, with empty response
```

## 信号批处理完成

将所有文件上传到批处理后，可以发出批处理完成的信号。 这样，[!DNL Catalog] DataSetFile条目就会为已完成的文件创建，并与上面生成的批处理关联。 然后，将[!DNL Catalog]批标记为成功，这会触发下游流以摄取可用数据。

**请求**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 要上传到数据集的批次的ID。 |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**响应**

```JSON
#Status 200 OK, with empty response
```

## 检查批状态

等待文件上传到批处理时，可以检查批处理的状态以查看其进度。

**API格式**

```http
GET /batch/{BATCH_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 正在检查的批处理的ID。 |

**请求**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**响应**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{USER_ID}` | 创建或更新批处理的用户ID。 |

`"status"`字段显示所请求批的当前状态。 批可以具有以下状态之一：

## 批量摄取状态

| 状态 | 描述 |
| ------ | ----------- |
| 已放弃 | 批次未在预期时间范围内完成。 |
| 已中止 | 已为指定的批次（通过批量摄取API）明确调用了&#x200B;****&#x200B;中止操作。 批处理处于“已加载”状态后，将无法中止该批处理。 |
| 活动 | 批已成功提升，可用于下游冲减。 此状态可与“成功”交替使用。 |
| 已删除 | 批次的数据已完全删除。 |
| 失败 | 由配置错误和/或数据错误导致的终端状态。 失败批处理的数据将&#x200B;**不**&#x200B;显示。 此状态可与“失败”交替使用。 |
| 不活动 | 批已成功提升，但已还原或已过期。 批次不再可用于下游冲减。 |
| 已加载 | 批处理的数据已完成，并且批处理已准备好进行升级。 |
| 正在加载 | 正在上载此批的数据，该批当前&#x200B;**尚未**&#x200B;准备提升。 |
| 正在重试 | 正在处理此批的数据。 但是，由于系统或临时错误，批处理失败 — 因此，将重试此批处理。 |
| 暂存 | 批处理提升流程的暂存阶段已完成，并且已运行摄取作业。 |
| 暂存 | 正在处理批处理的数据。 |
| 停止 | 正在处理批处理的数据。 但是，多次重试后，批量升级已停止。 |

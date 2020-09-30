---
keywords: Experience Platform;home;popular topics;data ingestion;batch;Batch;enable dataset;Batch ingestion overview;overview;batch ingestion overview;
solution: Experience Platform
title: 批摄取概述
topic: overview
description: 批处理摄取API允许您将数据作为批处理文件导入到Adobe Experience Platform。 所摄取的用户档案可以是CRM系统中平面文件（如拼花文件）中的模式数据，也可以是与体验数据模型(XDM)注册表中的已知数据相符的数据。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 2%

---


# [!DNL Batch Ingestion]概述

API [!DNL Batch Ingestion] 允许您将数据作为批处理文件引入Adobe Experience Platform。 所摄取的用户档案可以是CRM系统中的平面文件（如拼花文件）中的模式数据，或符合(XDM)注册表中的已知的 [!DNL Experience Data Model] 数据。

数据 [摄取API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) ，提供了有关这些API调用的其他信息。

下图概述了批摄取过程：

![](../images/batch-ingestion/overview/batch_ingestion.png)

## 使用API

API [!DNL Data Ingestion] 允许您通过以下三个基本步骤将数据作为批处理(由一个或多个要作为单个单元摄取的文件组成的数 [!DNL Experience Platform] 据单元)进行：

1. 创建新批。
2. 将文件上传到与数据的XDM模式匹配的指定数据集。
3. 发出批次结束的信号。


### [!DNL Data Ingestion] 先决条件

- 要上传的数据必须采用Parke或JSON格式。
- 在[!DNL Catalog [services]中创建的数据集](../../catalog/home.md)。
- 拼花文件的内容必须与要上传到的数据集的模式的子集匹配。
- 在验证后拥有您的独特访问令牌。

### 批摄取最佳实践

- 建议的批处理大小介于256 MB和100 GB之间。
- 每个批次最多应包含1500个文件。

要上传大于512MB的文件，需要将文件分为较小的块。 此处可找到上传大型文件的 [说明](#large-file-upload---create-file)。

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

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

- 内容类型：application/json

### 创建批

在将数据添加到数据集之前，必须先将其链接到批，然后再将其上传到指定的数据集。

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
| `id` | 刚创建（在后续请求中使用）的批的ID。 |
| `relatedObjects.id` | 要将文件上传到的数据集的ID。 |

## 文件上传

成功创建新批次进行上传后，文件便可上传到特定数据集。

您可以使用“小文件上 **传API”上传文件**。 但是，如果文件太大并且超出网关限制（如延长超时、超出正文大小请求和其他限制），您可以切换到“大文 **件上传API”**。 此API以块为单位上传文件，并使用“大文件上传完 **整API”调用将数据拼** 合到一起。

>[!NOTE]
>
>以下示例使用 [镶木地板](https://parquet.apache.org/documentation/latest/) 文件格式。 使用JSON文件格式的示例可在批量摄取开发人 [员指南中找到](./api-overview.md)。

### 小文件上传

创建批后，数据即可上传到预先存在的数据集。  要上传的文件必须与其引用的XDM模式匹配。

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 批的ID。 |
| `{DATASET_ID}` | 要上传文件的数据集的ID。 |
| `{FILE_NAME}` | 在数据集中看到的文件名称。 |

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
| `{FILE_PATH_AND_NAME}` | 要上载到数据集中的文件的路径和文件名。 |

**响应**

```JSON
#Status 200 OK, with empty response body
```

### 大文件上传——创建文件

要上传大文件，必须将文件拆分为较小的块，并一次上传一个。

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 批的ID。 |
| `{DATASET_ID}` | 摄取文件的数据集的ID。 |
| `{FILE_NAME}` | 在数据集中看到的文件名称。 |

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

### 大文件上传——上传后续部分

创建文件后，可以通过重复的PATCH请求上传所有后续区块，每个区域对应一个请求。

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 批的ID。 |
| `{DATASET_ID}` | 要将文件上传到的数据集的ID。 |
| `{FILE_NAME}` | 在数据集中看到的文件名称。 |

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
| `{FILE_PATH_AND_NAME}` | 要上载到数据集中的文件的路径和文件名。 |

**响应**

```JSON
#Status 200 OK, with empty response
```

## 信号批处理完成

在所有文件都上传到该批后，可以指示该批完成。 通过执行此操作 [!DNL Catalog] ，将为已完 **** 成的文件创建DataSetFile条目，并与上面生成的批关联。 然 [!DNL Catalog] 后将批标记为成功，这会触发下游流以获取可用数据。

**请求**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 要上传到数据集的批的ID。 |

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

在等待文件上传到批时，可以检查批的状态以查看其进度。

**API格式**

```http
GET /batch/{BATCH_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 正在检查的批的ID。 |

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
| `{USER_ID}` | 创建或更新批的用户的ID。 |

字 `"status"` 段显示请求的批的当前状态。 这些批可以具有以下状态之一：

## 批摄取状态

| 状态 | 描述 |
| ------ | ----------- |
| 已放弃 | 批未在预期时间范围内完成。 |
| 已中止 | 已为指定 **批** 显式调用（通过Batch Ingest API）中止操作。 一旦批处理处于“已加 **载** ”状态，就无法中止它。 |
| 活动 | 批已成功提升，可用于下游冲减。 此状态可与“成功”交替 **使用**。 |
| 已删除 | 批处理数据已完全删除。 |
| 失败 | 由错误配置和／或错误数据导致的终端状态。 失败批处理的数 **据将** 不显示。 此状态可与“故障”(Failure)交替 **使用**。 |
| 非活动 | 批已成功提升，但已还原或已过期。 该批不再可用于下游冲减。 |
| 已加载 | 批处理数据已完成，批处理已准备好进行升级。 |
| 正在加载 | 正在上传此批的数据，且该批当前 **未** 准备提升。 |
| 正在重试 | 正在处理此批的数据。 但是，由于系统或临时错误，批处理失败——因此，正在重试此批处理。 |
| 已暂存 | 批处理的升级过程的阶段阶段已完成，并且已运行摄取作业。 |
| 暂存 | 正在处理批的数据。 |
| 停止 | 正在处理批处理的数据。 但是，批次促销已在多个重试后停止。 |
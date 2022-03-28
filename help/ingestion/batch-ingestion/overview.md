---
keywords: Experience Platform；主页；热门主题；数据摄取；批量；启用数据集；批量摄取概述；概述；批量摄取概述；
solution: Experience Platform
title: 批量摄取API概述
topic-legacy: overview
description: Adobe Experience Platform数据摄取API允许您将数据作为批处理文件导入到平台中。 摄取的数据可以是CRM系统中平面文件（如Parquet文件）中的配置文件数据，也可以是符合体验数据模型(XDM)注册表中已知架构的数据。
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: 75426b1ddc16af39eb6c423027fac7d4d0e21c6a
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 6%

---

# 批量摄取API概述

Adobe Experience Platform数据摄取API允许您将数据作为批处理文件导入到平台中。 摄取的数据可以是来自平面文件（如Parquet文件）的配置文件数据，也可以是符合 [!DNL Experience Data Model] (XDM)注册表。

的 [数据摄取API参考](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) 提供了有关这些API调用的其他信息。

下图概述了批量摄取流程：

![](../images/batch-ingestion/overview/batch_ingestion.png)

## 快速入门

本指南中使用的API端点是 [数据摄取API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). 在继续之前，请查看 [入门指南](getting-started.md) 有关相关文档的链接，请参阅本文档中的API调用示例指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

### [!DNL Data Ingestion] 先决条件

- 要上传的数据必须采用Parquet或JSON格式。
- 在 [[!DNL Catalog services]](../../catalog/home.md).
- Parquet文件的内容必须与要上传到的数据集架构的子集相匹配。
- 验证后拥有您的唯一访问令牌。

### 批量摄取最佳实践

- 建议的批处理大小介于256 MB到100 GB之间。
- 每个批次最多应包含1500个文件。

### 批量摄取约束

批量数据摄取具有一些限制：

- 每批文件的最大数量：1500
- 最大批次大小：100 GB
- 每行属性或字段的最大数量：10000
- 每个用户每分钟的最大批数：138

>[!NOTE]
>
>要上传大于512MB的文件，需要将文件分为较小的块。 有关上传大文件的说明，请参阅 [本文档的大文件上传部分](#large-file-upload---create-file).

### 类型

在摄取数据时，了解如何 [!DNL Experience Data Model] (XDM)模式有效。 有关XDM字段类型如何映射到不同格式的更多信息，请阅读 [架构注册开发人员指南](../../xdm/api/getting-started.md).

在摄取数据时具有一定的灵活性 — 如果类型与目标架构中的内容不匹配，则数据将转换为表示的目标类型。 如果不能，则会通过 `TypeCompatibilityException`.

例如，JSON和CSV均没有 `date` 或 `date-time` 类型。 因此，这些值使用 [ISO 8061格式化字符串](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15&quot;:05:59.000-08:00&quot;)或Unix时间（以毫秒为格式）(1531263959000)，在摄取时将转换为目标XDM类型。

下表显示了摄取数据时支持的转化。

| 入站（行）与目标（列） | 字符串 | 字节 | 短 | 整数 | 长 | 双精度 | 日期 | Date-Time | 对象 | 地图 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 字符串 | X | X | X | X | X | X | X | X |  |  |
| 字节 | X | X | X | X | X | X |  |  |  |  |
| 短 | X | X | X | X | X | X |  |  |  |  |
| 整数 | X | X | X | X | X | X |  |  |  |  |
| 长 | X | X | X | X | X | X | X | X |  |  |
| 双精度 | X | X | X | X | X | X |  |  |  |  |
| 日期 |  |  |  |  |  |  | X |  |  |  |
| Date-Time |  |  |  |  |  |  |  | X |  |  |
| 对象 |  |  |  |  |  |  |  |  | X | X |
| 地图 |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>布尔值和数组无法转换为其他类型。

## 使用 API

的 [!DNL Data Ingestion] API允许您将数据作为批量（由一个或多个要作为单个单位摄取的文件组成的数据单元）摄取到中 [!DNL Experience Platform] 三个基本步骤：

1. 创建新批。
2. 将文件上传到与数据的XDM架构匹配的指定数据集。
3. 表示批次的结束。

## 创建批处理

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
  -H "x-api-key: {API_KEY}"
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
>批量摄取可用于以递增方式更新配置文件存储中的数据。 有关更多信息，请参阅 [更新批](#patch-a-batch) 在 [批量获取开发人员指南](api-overview.md).

>[!INFO]
>
>以下示例使用 [Apache Parquet](https://parquet.apache.org/docs/) 文件格式。 在 [批量获取开发人员指南](api-overview.md).

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
  -H "x-api-key: {API_KEY}" \
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

将所有文件上传到批处理后，可以发出批处理完成的信号。 通过执行此操作， [!DNL Catalog] 为已完成的文件创建DataSetFile条目，并与上面生成的批处理关联。 的 [!DNL Catalog] 然后，批次会标记为成功，这会触发下游流以摄取可用数据。

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
-H "x-api-key: {API_KEY}"
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

的 `"status"` 字段，显示所请求批的当前状态。 批可以具有以下状态之一：

## 批量摄取状态

| 状态 | 描述 |
| ------ | ----------- |
| 已放弃 | 批次未在预期时间范围内完成。 |
| 已中止 | 中止操作已 **显式** 已调用（通过批量摄取API）。 批处理处于“已加载”状态后，将无法中止该批处理。 |
| 活动 | 批已成功提升，可用于下游冲减。 此状态可与“成功”交替使用。 |
| 已删除 | 批次的数据已完全删除。 |
| 失败 | 由配置错误和/或数据错误导致的终端状态。 失败批处理的数据将 **not** 出现。 此状态可与“失败”交替使用。 |
| 不活动 | 批已成功提升，但已还原或已过期。 批次不再可用于下游冲减。 |
| 已加载 | 批处理的数据已完成，并且批处理已准备好进行升级。 |
| 正在加载 | 正在上载此批次的数据，并且该批次当前为 **not** 准备升职。 |
| 正在重试 | 正在处理此批的数据。 但是，由于系统或临时错误，批处理失败 — 因此，将重试此批处理。 |
| 暂存 | 批处理提升流程的暂存阶段已完成，并且已运行摄取作业。 |
| 暂存 | 正在处理批处理的数据。 |
| 停止 | 正在处理批处理的数据。 但是，多次重试后，批量升级已停止。 |

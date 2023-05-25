---
keywords: Experience Platform；主页；热门主题；数据摄取；批处理；启用数据集；批量摄取概述；概述；批量摄取概述；
solution: Experience Platform
title: 批量摄取API概述
description: Adobe Experience Platform批量摄取API允许您将数据作为批处理文件摄取到Platform中。 所摄取的数据可以是来自CRM系统中平面文件（如Parquet文件）的配置文件数据，也可以是与Experience Data Model (XDM)注册表中的已知架构相符的数据。
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 6%

---

# 批量摄取API概述

Adobe Experience Platform批量摄取API允许您将数据作为批处理文件摄取到Platform中。 所摄取的数据可以是平面文件（如Parquet文件）中的配置文件数据，也可以是与 [!DNL Experience Data Model] (XDM)注册表。

此 [批量摄取API参考](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) 提供了有关这些API调用的其他信息。

下图概述了批量摄取流程：

![](../images/batch-ingestion/overview/batch_ingestion.png)

## 快速入门

本指南中使用的API端点是 [批量摄取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). 在继续之前，请查看 [快速入门指南](getting-started.md) 有关相关文档的链接，请参阅本文档中的示例API调用指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

### [!DNL Data Ingestion] 先决条件

- 要上传的数据必须为Parquet或JSON格式。
- 在中创建的数据集 [[!DNL Catalog services]](../../catalog/home.md).
- Parquet文件的内容必须与要上传到的数据集架构的子集匹配。
- 在身份验证后拥有您的唯一访问令牌。

### 批量摄取最佳实践

- 建议的批处理大小在256 MB和100 GB之间。
- 每个批次应最多包含1500个文件。

### 批量摄取约束

批量数据摄取有一些限制：

- 每批次的最大文件数： 1500
- 最大批次大小：100 GB
- 每行属性或字段的最大数量：10000
- 每分钟最大批数，每个用户：138

>[!NOTE]
>
>要上载大于512MB的文件，需要将该文件分成较小的块。 有关上载大文件的说明，请参见 [本文档的大型文件上传部分](#large-file-upload---create-file).

### 类型

在摄取数据时，请务必了解如何 [!DNL Experience Data Model] (XDM)架构有效。 有关XDM字段类型如何映射到不同格式的更多信息，请阅读 [Schema Registry开发人员指南](../../xdm/api/getting-started.md).

在摄取数据时有一定的灵活性 — 如果类型与目标架构中的类型不匹配，数据将转换为表示的目标类型。 如果失败，它将使批处理失败 `TypeCompatibilityException`.

例如，JSON和CSV都没有 `date` 或 `date-time` 类型。 因此，这些值使用表示 [ISO 8061格式字符串](https://www.iso.org/iso-8601-date-and-time-format.html) (“2018-07-10T15”:05:59.000-08:00”)或以毫秒(1531263959000)为单位的Unix时间，并在摄取时转换为目标XDM类型。

下表显示了摄取数据时支持的转化。

| 入站（行）与目标（列） | 字符串 | 字节 | 短 | 整数 | 长 | 双精度 | 日期 | 日期时间 | 对象 | 地图 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 字符串 | X | X | X | X | X | X | X | X |  |  |
| 字节 | X | X | X | X | X | X |  |  |  |  |
| 短 | X | X | X | X | X | X |  |  |  |  |
| 整数 | X | X | X | X | X | X |  |  |  |  |
| 长 | X | X | X | X | X | X | X | X |  |  |
| 双精度 | X | X | X | X | X | X |  |  |  |  |
| 日期 |  |  |  |  |  |  | X |  |  |  |
| 日期时间 |  |  |  |  |  |  |  | X |  |  |
| 对象 |  |  |  |  |  |  |  |  | X | X |
| 地图 |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>无法将布尔值和数组转换为其他类型。

## 使用 API

此 [!DNL Data Ingestion] API允许您将数据作为批量（由一个或多个要作为单个单元摄取的文件组成的数据单元）摄取到 [!DNL Experience Platform] 三个基本步骤：

1. 创建新批次。
2. 将文件上传到与数据的XDM架构匹配的指定数据集。
3. 表示批次的结束。

## 创建批次

将数据添加到数据集之前，必须将其链接到批次，该批次稍后将上传到指定的数据集。

```http
POST /batches
```

**请求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
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
    "imsOrg": "{ORG_ID}",
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
| `id` | 刚刚创建的批次ID（在后续请求中使用）。 |
| `relatedObjects.id` | 要将文件上传到的数据集的ID。 |

## 文件上传

成功创建新的上传批次后，可将文件上传到特定数据集。

您可以使用小文件上传API上传文件。 但是，如果文件过大，并且超过了网关限制（例如扩展超时、请求主体大小超过以及其他限制），则可以切换到大型文件上传API。 此API以块形式上传文件，并使用大文件上传完成API调用将数据拼合在一起。

>[!NOTE]
>
>批量摄取可用于以增量方式更新配置文件存储区中的数据。 有关更多信息，请参阅以下部分： [更新批次](#patch-a-batch) 在 [批量摄取开发人员指南](api-overview.md).

>[!INFO]
>
>以下示例使用 [Apache Parquet](https://parquet.apache.org/docs/) 文件格式。 有关使用JSON文件格式的示例，请参阅 [批量摄取开发人员指南](api-overview.md).

### 小文件上传

创建批次后，可将数据上传到预先存在的数据集。  要上传的文件必须与其引用的XDM架构匹配。

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 批次的ID。 |
| `{DATASET_ID}` | 要上传文件的数据集的ID。 |
| `{FILE_NAME}` | 将在数据集中看到的文件的名称。 |

**请求**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 要上传到数据集的文件的路径和文件名。 |

**响应**

```JSON
#Status 200 OK, with empty response body
```

### 大文件上传 — 创建文件

要上载大文件，必须将文件拆分为较小的块，并一次上载一个。

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 批次的ID。 |
| `{DATASET_ID}` | 摄取文件的数据集的ID。 |
| `{FILE_NAME}` | 将在数据集中看到的文件的名称。 |

**请求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**响应**

```JSON
#Status 201 CREATED, with empty response body
```

### 大文件上传 — 上传后续部分

创建文件后，可以通过发出重复的PATCH请求（文件的每个部分各一个）来上传所有后续块。

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 批次的ID。 |
| `{DATASET_ID}` | 要将文件上传到的数据集的ID。 |
| `{FILE_NAME}` | 将在数据集中看到的文件的名称。 |

**请求**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 要上传到数据集的文件的路径和文件名。 |

**响应**

```JSON
#Status 200 OK, with empty response
```

## 信号批次完成

将所有文件上载到批处理之后，可以发出完成该批处理的信号。 这样， [!DNL Catalog] 为已完成的文件创建DataSetFile条目，并与上面生成的批处理相关联。 此 [!DNL Catalog] 然后，将批处理标记为成功，这会触发下游流摄取可用数据。

**请求**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 要上传到数据集的批次ID。 |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**响应**

```JSON
#Status 200 OK, with empty response
```

## 检查批次状态

在等待将文件上传到批次时，可以检查批次的状态以查看其进度。

**API格式**

```http
GET /batch/{BATCH_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 正在检查的批次的ID。 |

**请求**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**响应**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{ORG_ID}",
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
| `{USER_ID}` | 创建或更新批次的用户的ID。 |

此 `"status"` 字段显示所请求批次的当前状态。 批次可以具有以下状态之一：

## 批量摄取状态

| 状态 | 描述 |
| ------ | ----------- |
| 已放弃 | 该批次未在预期时间范围内完成。 |
| 已中止 | 中止操作具有 **明确** 已为指定批次调用（通过批量摄取API）。 批次处于“已加载”状态后，无法中止。 |
| 活动 | 批次已成功提升，可用于下游使用。 此状态可与“Success”互换使用。 |
| 已删除 | 批次的数据已完全删除。 |
| 失败 | 因配置错误和/或数据错误导致的终端状态。 失败批次的数据将 **非** 出现。 此状态可与“失败”互换使用。 |
| 不活动 | 批次已成功提升，但已还原或已过期。 该批次不再可用于下游消耗。 |
| 已加载 | 批次的数据已完成，批次已准备好进行升级。 |
| 正在加载 | 正在上载此批次的数据，批次当前为 **非** 准备提升。 |
| 正在重试 | 正在处理此批次的数据。 但是，由于系统错误或暂时性错误，批次失败 — 因此，将重试此批次。 |
| 已暂存 | 批处理提升流程的暂存阶段已完成，并且引入作业已运行。 |
| 暂存 | 正在处理批次的数据。 |
| 已搁置 | 正在处理批次的数据。 但是，在多次重试后，批次升级已停止。 |

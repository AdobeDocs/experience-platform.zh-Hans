---
keywords: Experience Platform；下载得分；customer ai；热门主题；导出；客户ai下载；customer ai得分
solution: Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: 在Customer AI中下载分数
topic-legacy: Downloading scores
description: Customer AI允许您下载Parquet文件格式的分数。
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---

# 在Customer AI中下载分数

本文档是下载Customer AI得分的指南。

## 快速入门

Customer AI允许您下载Parquet文件格式的分数。 本教程要求您已阅读并完成下载的Customer AI分数部分(位于 [入门](../getting-started.md) 的双曲余切值。

此外，要访问Customer AI的得分，您需要具有运行状态成功的服务实例。 要创建新的服务实例，请访问 [配置Customer AI实例](./configure.md). 如果您最近创建了一个服务实例，但该实例仍在培训和评分，请允许24小时才能完成运行。

目前，有两种方法可下载Customer AI得分：

1. 如果要在单个级别下载分数和/或未启用“实时客户资料”，请首先导航到 [查找数据集ID](#dataset-id).
2. 如果您已启用用户档案，并且想要下载使用Customer AI配置的区段，请导航至 [下载使用Customer AI配置的区段](#segment).

## 查找数据集ID {#dataset-id}

在您的Customer AI分析服务实例中，单击 *更多操作* 右上方导航中的下拉列表，然后选择 **[!UICONTROL 访问分数]**.

![更多操作](../images/insights/more-actions.png)

此时会显示一个新对话框，其中包含指向下载分数文档的链接以及您当前实例的数据集ID。 将数据集ID复制到剪贴板，然后继续执行下一步。

![数据集 ID](../images/download-scores/access-scores.png)

## 检索批处理ID {#retrieve-your-batch-id}

使用上一步中的数据集ID，您需要调用目录API以检索批处理ID。 此API调用使用其他查询参数，以返回最新的成功批次，而不是属于贵组织的批次列表。 要返回其他批，请将限制查询参数的数量增加到您希望返回的所需数量。 有关可用查询参数类型的更多信息，请访问 [使用查询参数筛选目录数据](../../../catalog/api/filter-data.md).

**API格式**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | “访问得分”对话框中可用的数据集ID。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含批处理ID对象的有效负荷。 在此示例中，返回对象的键值是批处理ID `01E5QSWCAASFQ054FNBKYV6TIQ`. 复制批量ID以在下一次API调用中使用。

```json
{
    "01E5QSWCAASFQ054FNBKYV6TIQ": {
        "status": "success",
        "tags": {
            "Tags": [ ... ],
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5cd9146b31dae914b75f654f"
            }
        ],
        "id": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "externalId": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "replay": {
            "predecessors": [
                "01E5N7EDQQP4JHJ93M7C3WM5SP"
            ],
            "reason": "Replacing for 2020-04-09",
            "predecessorListingType": "IMMEDIATE"
        },
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "412657965Y566A4A0A495D4A@AdobeOrg",
        "started": 1586715571808,
        "metrics": {
            "partitionCount": 1,
            "outputByteSize": 2380339,
            "inputFileCount": -1,
            "inputByteSize": 2381007,
            "outputRecordCount": 24340,
            "outputFileCount": 1,
            "inputRecordCount": 24340
        },
        "completed": 1586715582735,
        "created": 1586715571217,
        "createdClient": "acp_foundation_push",
        "createdUser": "sensei_exp_attributionai@AdobeID",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "updated": 1586715583582,
        "version": "1.0.5"
    }
}
```

## 使用您的批处理ID检索下一个API调用 {#retrieve-the-next-api-call-with-your-batch-id}

获得批处理ID后，您便能够向 `/batches`. 该请求会返回用作下一个API请求的链接。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步骤中检索的批ID [检索批ID](#retrieve-your-batch-id). |

**请求**

使用您自己的批处理ID，发出以下请求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回包含 `_links` 对象。 在 `_links` 对象是 `href` 使用新API调用作为其值。 复制此值以继续执行下一步。

```json
{
    "data": [
        {
            "dataSetFileId": "035e2520-5e69-11ea-b624-51ecfeba55d0-1",
            "dataSetViewId": "5e3b2fe3fe4b9f18a8b7a3db",
            "version": "1.0.0",
            "created": "1583361894479",
            "updated": "1583361894479",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

## 检索文件 {#retrieving-your-files}

使用 `href` 作为API调用在上一步中获得的值，请发出新的GET请求以检索您的文件目录。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在 `href` 值 [上一步](#retrieve-the-next-api-call-with-your-batch-id). 也可以在 `data` 对象类型下的数组 `dataSetFileId`. |

**请求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应包含一个数据数组，该数据数组可能具有一个条目，或属于该目录的文件列表。 以下示例包含一个文件列表，为方便阅读，已对其进行了压缩。 在此方案中，您需要遵循每个文件的URL才能访问该文件。

```json
{
    "data": [
        {
            "name": "part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet",
            "length": "16214531",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet"
                }
            }
        },
        {
            "name": "...",
            "length": "16235375",
            "_links": {
                "self": {
                    "href": "..."
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 100
    },
    "_links": {
        "next": {
            "href": "..."
        },
        "page": {
            "href": "...",
            "templated": true
        }
    }
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `_links.self.href` | GET请求URL，用于下载目录中的文件。 |


复制 `href` 值 `data` 数组，然后继续执行下一步。

## 下载文件数据

要下载文件数据，请向 `"href"` 您在上一步中复制的值 [检索文件](#retrieving-your-files).

>[!NOTE]
>
>如果您直接在命令行中发出此请求，则可能会提示您在请求标头之后添加输出。 以下请求示例使用 `--output {FILENAME.FILETYPE}`.

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在 `href` 值 [上一步](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | 文件的名称。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP]
>
>在发出GET请求之前，请确保您位于您希望将文件保存到的正确目录或文件夹中。

**响应**

响应将下载您在当前目录中请求的文件。 在本例中，文件名为“filename.parquet”。

![终端](../images/download-scores/response.png)

## 下载使用Customer AI配置的区段 {#segment}

下载分数数据的另一种方法是将受众导出到数据集。 成功完成分段作业后( `status` 属性为“成功”)，则可以将受众导出到可在其中访问并执行操作的数据集。 要了解有关分段的更多信息，请访问 [分段概述](../../../segmentation/home.md).

>[!IMPORTANT]
>
>要利用这种导出方法，需要为数据集启用实时客户资料。

的 [导出区段](../../../segmentation/tutorials/evaluate-a-segment.md) 区段评估指南中的部分介绍了导出受众数据集所需的步骤。 该指南概述了并提供了以下示例：

- **创建目标数据集：** 创建数据集以保存受众成员。
- **在数据集中生成受众配置文件：** 根据区段作业的结果，使用XDM个人用户档案填充数据集。
- **监视导出进度：** 检查导出过程的当前进度。
- **读取受众数据：** 检索表示受众成员的生成的XDM个人用户档案。

## 后续步骤

本文档概述了下载Customer AI得分所需的步骤。 您现在可以继续浏览另一个 [智能服务](../../home.md) 和提供的指南。

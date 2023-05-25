---
keywords: Experience Platform；下载分数；客户人工智能；热门主题；导出；导出；客户人工智能下载；客户人工智能分数
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 在Customer AI中下载分数
description: 客户人工智能允许您以Parquet文件格式下载分数。
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---

# 在Customer AI中下载分数

本文档用作下载客户人工智能得分的指南。

## 快速入门

客户人工智能允许您以Parquet文件格式下载分数。 本教程要求您已阅读并完成下载客户人工智能得分部分 [快速入门](../getting-started.md) 指南。

此外，要访问客户人工智能的分数，您需要具有可用成功运行状态的服务实例。 要创建新服务实例，请访问 [配置客户人工智能实例](./configure.md). 如果您最近创建了服务实例，但该实例仍在训练和评分中，请等待24小时以使它完成运行。

目前，可通过两种方式下载Customer AI分数：

1. 如果您要下载个人级别的分数和/或没有启用实时客户档案，请从导航到 [查找数据集ID](#dataset-id).
2. 如果您已启用配置文件，并且希望下载已使用Customer AI配置的区段，请导航到 [下载使用Customer AI配置的区段](#segment).

## 查找您的数据集ID {#dataset-id}

在用于客户人工智能分析的服务实例中，单击 *更多操作* 右上方的下拉列表，然后选择 **[!UICONTROL 访问得分]**.

![更多操作](../images/insights/more-actions.png)

此时将显示一个新对话框，其中包含指向下载得分文档的链接以及当前实例的数据集ID。 将数据集ID复制到剪贴板，然后继续执行下一步。

![数据集 ID](../images/download-scores/access-scores.png)

## 检索您的批次ID {#retrieve-your-batch-id}

使用上一步中的数据集ID，您需要调用目录API以检索批次ID。 此API调用使用附加查询参数来返回最新的成功批次，而不是返回属于您组织的批次列表。 要返回附加批，请将限制查询参数的数字增加到您希望返回的所需量。 有关可用查询参数类型的更多信息，请访问以下内容的指南： [使用查询参数筛选目录数据](../../../catalog/api/filter-data.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含批次ID对象的有效负载。 在此示例中，返回对象的键值是批次ID `01E5QSWCAASFQ054FNBKYV6TIQ`. 复制您的批次ID以用于下一个API调用。

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

## 使用您的批次ID检索下一个API调用 {#retrieve-the-next-api-call-with-your-batch-id}

获得批次ID后，您便能够向发出新的GET请求 `/batches`. 该请求返回用作下一个API请求的链接。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 上一步中检索的批次ID [检索您的批次ID](#retrieve-your-batch-id). |

**请求**

使用您自己的批次ID提出以下请求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含 `_links` 对象。 在 `_links` 对象是 `href` 其值为新的API调用。 复制此值以继续执行下一步。

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

使用 `href` 作为一个API调用，发出新的GET请求以检索您的文件目录。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID返回到 `href` 值来自 [上一步](#retrieve-the-next-api-call-with-your-batch-id). 它也可从 `data` 对象类型下的数组 `dataSetFileId`. |

**请求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应包含的数据数组可能只有一个条目，或属于该目录的文件列表。 以下示例包含文件列表并经过压缩以提高可读性。 在此方案中，您需要遵循每个文件的URL才能访问该文件。

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
| `_links.self.href` | 用于下载目录中文件的GET请求URL。 |


复制 `href` 中任何文件对象的值 `data` 数组，然后继续执行下一步。

## 下载您的文件数据

GET要下载文件数据，请向 `"href"` 您在上一步中复制的值 [检索文件](#retrieving-your-files).

>[!NOTE]
>
>如果您直接在命令行中提出此请求，则可能会提示您在请求标头后添加输出。 以下请求示例使用 `--output {FILENAME.FILETYPE}`.

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID返回到 `href` 值来自 [上一步](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | 文件的名称。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP]
>
>在发出GET请求之前，请确保您位于希望将文件保存到的正确目录或文件夹中。

**响应**

响应会将您请求的文件下载到当前目录中。 在此示例中，文件名为“filename.parquet”。

![终端](../images/download-scores/response.png)

## 下载使用客户人工智能配置的区段 {#segment}

下载得分数据的另一种方法是将受众导出到数据集。 成功完成分段作业后( `status` 属性为“SUCCEEDED”)，您可以将受众导出到可在其中进行访问和操作的数据集。 要了解有关分段的更多信息，请访问 [分段概述](../../../segmentation/home.md).

>[!IMPORTANT]
>
>为了利用这种导出方法，需要为数据集启用实时客户档案。

此 [导出区段](../../../segmentation/tutorials/evaluate-a-segment.md) 区段评估指南中的部分介绍了导出受众数据集所需的步骤。 该指南概述了以下内容并提供相关示例：

- **创建目标数据集：** 创建数据集以保存受众成员。
- **在数据集中生成受众配置文件：** 根据区段作业的结果，使用XDM个人资料填充数据集。
- **监视导出进度：** 检查导出过程的当前进度。
- **读取受众数据：** 检索生成的XDM个人资料，这些资料表示受众的成员。

## 后续步骤

本文档概述了下载Customer AI得分所需的步骤。 您现在可以继续浏览其他 [智能服务](../../home.md) 以及提供的指南。

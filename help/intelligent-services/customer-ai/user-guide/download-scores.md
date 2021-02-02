---
keywords: Experience Platform；下载得分；用户ai；热门主题；导出；用户ai下载；用户ai得分
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 在客户AI中下载分数
topic: Downloading scores
description: 客户AI允许您下载Parke文件格式的得分。
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---


# 在客户AI中下载分数

此文档可作为下载客户AI得分的指南。

## 入门指南

客户AI允许您下载Parke文件格式的得分。 本教程要求您已阅读并完成[入门](../getting-started.md)指南中的下载客户AI得分部分。

此外，要访问客户AI的得分，您需要有一个运行状态成功的服务实例可用。 要创建新服务实例，请访问[配置客户AI实例](./configure.md)。 如果您最近创建了一个服务实例，但它仍在培训和评分，请允许24小时，它才能完成运行。

目前，有两种方法可下载客户AI得分：

1. 如果要下载单个级别的得分和／或未启用实时用户档案，请导航至[查找数据集ID](#dataset-id)进行开始。
2. 如果您启用了用户档案并希望下载已使用客户AI配置的区段，请导航至[下载已使用客户AI](#segment)配置的区段。

## 查找数据集ID {#dataset-id}

在您的客户AI洞察服务实例中，单击右上方导航中的&#x200B;*更多操作*&#x200B;下拉框，然后选择&#x200B;**[!UICONTROL 访问分数]**。

![更多操作](../images/insights/more-actions.png)

此时将显示一个新对话框，其中包含一个指向下载得分文档的链接以及当前实例的数据集ID。 将数据集ID复制到剪贴板，然后继续执行下一步。

![数据集ID](../images/download-scores/access-scores.png)

## 检索批ID {#retrieve-your-batch-id}

使用上一步中的数据集ID，您需要调用目录API以检索批处理ID。 此API调用使用其他查询参数，以返回最新的成功批次，而不是属于您组织的列表批次。 要返回附加批，请将限制查询参数的数量增加到您希望返回的所需数量。 有关可用查询参数类型的详细信息，请访问[使用查询参数筛选目录数据的指南](../../../catalog/api/filter-data.md)。

**API格式**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | “Access Scores”对话框中提供的数据集ID。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含批ID对象的有效负荷。 在此示例中，返回对象的键值是批处理ID `01E5QSWCAASFQ054FNBKYV6TIQ`。 复制批ID以用于下一个API调用。

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

## 使用批处理ID {#retrieve-the-next-api-call-with-your-batch-id}检索下一个API调用

获得批ID后，您便能够向`/batches`发出新的GET请求。 该请求返回用作下一个API请求的链接。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步[中检索的批ID检索您的批ID](#retrieve-your-batch-id)。 |

**请求**

使用您自己的批ID，发出以下请求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回包含`_links`对象的有效负荷。 在`_links`对象中是一个`href`，其值为新API调用。 复制此值以继续执行下一步。

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

## 检索文件{#retrieving-your-files}

使用上一步中得到的`href`值作为API调用，发出新的GET请求以检索文件目录。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID以[上一步](#retrieve-the-next-api-call-with-your-batch-id)的`href`值返回。 也可以在`data`数组中对象类型`dataSetFileId`下访问它。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

该响应包含一个列表数组，该数组可能具有一个条目或属于该目录的文件的一个数据。 以下示例包含一列表文件，并经过压缩以便可读。 在此情况下，您需要按照每个文件的URL来访问该文件。

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


复制`data`数组中任何文件对象的`href`值，然后继续执行下一步。

## 下载文件数据

要下载文件数据，请向您在上一步[检索文件](#retrieving-your-files)中复制的`"href"`值发出GET请求。

>[!NOTE]
>
>如果您直接在命令行中发出此请求，可能会提示您在请求标头后添加输出。 以下请求示例使用`--output {FILENAME.FILETYPE}`。

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID从上一步[返回的`href`值中返回。](#retrieve-the-next-api-call-with-your-batch-id) |
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
>在发出GET请求之前，请确保您位于要保存文件的正确目录或文件夹中。

**响应**

响应将下载您在当前目录中请求的文件。 在本示例中，文件名为“filename.parke”。

![终端](../images/download-scores/response.png)

## 下载使用客户AI {#segment}配置的区段

下载得分数据的另一种方法是将受众导出到数据集。 分段作业成功完成后（`status`属性的值为“SUCCEEDED”），您可以将受众导出到数据集，在该数据集中可以访问并执行操作。 要了解有关分段的更多信息，请访问[分段概述](../../../segmentation/home.md)。

>[!IMPORTANT]
>
>要利用此导出方法，需要为数据集启用实时客户用户档案。

区段评估指南中的[导出区段](../../../segmentation/tutorials/evaluate-a-segment.md)部分涵盖导出受众数据集所需的步骤。 本指南概述并提供以下示例：

- **创建目标数据集：** 创建数据集以容纳受众成员。
- **在数据集中生成受众用户档案:** 根据区段作业的结果，用XDM单个用户档案填充数据集。
- **监视导出进** 度：检查导出过程的当前进度。
- **读取受众数** 据：检索表示受众成员的结果XDM单个用户档案。

## 后续步骤

此文档概述了下载客户AI得分所需的步骤。 现在，您可以继续浏览其他提供的[智能服务](../../home.md)和指南。

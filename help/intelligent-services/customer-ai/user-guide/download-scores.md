---
keywords: Experience Platform;download scores;customer ai;popular topics
solution: Experience Platform
title: 在客户人工智能中下载分数
topic: Downloading scores
translation-type: tm+mt
source-git-commit: 1cf1e9c814601bdd4c7198463593be78452004dc

---


# 在客户人工智能中下载分数

此文档可作为下载客户人工智能得分的指南。

## 入门指南

客户AI允许您以镶木地板文件格式下载分数。 本教程要求您已阅读并完成入门指南中的下载客户AI [得分](../getting-started.md) 。

此外，要访问客户AI的得分，您需要有一个运行状态成功的服务实例。 要创建新的服务实例，请访 [问配置客户AI实例](./configure.md)。 如果您最近创建了一个服务实例，但该实例仍在培训和评分中，请允许24小时以便它完成运行。

目前，有两种方法可下载客户AI得分：

1. 如果要在单个级别下载得分和／或未启用实时客户用户档案，请通过导航到查找数据集ID来进行 [开始](#dataset-id)。
2. 如果您启用了用户档案并希望下载已使用客户AI配置的区段，请导航以下 [载已使用客户AI配置的区段](#segment)。

## Find your dataset ID {#dataset-id}

在您的客户人工智能洞察服务实例中，单击右上 *方导航中的* “更多操作”下拉框，然后选择 **[!UICONTROL Access scores]**。

![更多操作](../images/insights/more-actions.png)

此时将显示一个新对话框，其中包含指向下载得分文档的链接以及当前实例的数据集ID。 将数据集ID复制到剪贴板，然后继续执行下一步。

![数据集ID](../images/download-scores/access-scores.png)

## 检索批ID {#retrieve-your-batch-id}

使用上一步中的数据集ID，您需要调用目录API以检索批ID。 此API调用使用其他查询参数，以返回单个批次，而不是属于您组织的列表批次。 有关可用查询参数类型的详细信息，请访问使用查询参数过 [滤目录数据的指南](../../../catalog/api/filter-data.md)。

**API格式**

```http
GET /batches?&dataSet={DATASET_ID}&orderBy=desc:created&limit=1
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | “Access Scores”（访问分数）对话框中提供的数据集ID。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含得分批ID对象的有效负荷。 在此示例中，对象为 `5e602f67c2f39715a87f46b1`。

在得分批ID对象中为数 `relatedObjects` 组。 此数组包含两个对象。 第一个对象的 `type` 值为“batch”，并且还包含ID。 在以下示例响应中，批ID为 `035e2520-5e69-11ea-b624-51evfeba55d1`。 复制您的批ID以用于下一个API调用。

```json
{   
    "5e602f67c2f39715a87f46b1": {
        "imsOrg": "{IMS_ORG}",
        "relatedObjects": [
            {
                "id": "5c01a91863540e14cd3d0432",
                "type": "dataSet"
            },
            {
                "id": "035e2520-5e69-11ea-b624-51evfeba55d1",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsRead": 46721830,
            "recordsWritten": 46721830,
            "avgNumExecutorsPerTask": 33,
            "startTime": 1583362385336,
            "inputSizeInKb": 10242034,
            "endTime": 1583363197517
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    }
}
```

## 使用您的批ID检索下一个API调用 {#retrieve-the-next-api-call-with-your-batch-id}

获得批ID后，您便可以向发出新的GET请求 `/batches`。 该请求返回用作下一个API请求的链接。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步中检索的批ID可检 [索您的批ID](#retrieve-your-batch-id)。 |

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

成功的响应会返回包含对象的有 `_links` 效负荷。 对象 `_links` 中包含 `href` 一个新的API调用作为其值。 复制此值以继续执行下一步。

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

使用上 `href` 一步中获得的值作为API调用，发出新的GET请求以检索文件目录。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID在上一步的值 `href` 中返 [回](#retrieve-the-next-api-call-with-your-batch-id)。 也可在对象类型下 `data` 的数组中访问它 `dataSetFileId`。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应包含一个数据数组，该数组可能具有一个条目或属于该目录的文件列表。 以下示例包含一列表文件，并已压缩以提高可读性。 在此方案中，您需要按照每个文件的URL访问该文件。

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


复制数 `href` 组中任何文件对象的值，然 `data` 后继续执行下一步。

## 下载文件数据

要下载文件数据，请对您在上一步检索文 `"href"` 件时复制的值发出GET [请求](#retrieving-your-files)。

>[!NOTE] 如果您直接在命令行中发出此请求，则可能会提示您在请求标题后添加输出。 以下请求示例使用 `--output {FILENAME.FILETYPE}`。

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID在上一步的值 `href` 中返 [回](#retrieve-the-next-api-call-with-your-batch-id)。 |
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

>[!TIP] 在发出GET请求之前，请确保您位于要将文件保存到的正确目录或文件夹中。

**响应**

响应将下载您在当前目录中请求的文件。 在本示例中，文件名为“filename.parce”。

![终端](../images/download-scores/response.png)

## 下载使用客户AI配置的区段 {#segment}

下载得分数据的另一种方法是将受众导出到数据集。 分段作业成功完成后(属性的值为 `status` “SUCCEEDED”)，您可以将受众导出到可在其中访问和执行操作的数据集。 要了解有关细分的更多信息，请访问分 [段概述](../../../segmentation/home.md)。

>[!IMPORTANT] 要利用此导出方法，需要为数据集启用实时客户用户档案。

区段 [评估指南中的“导出区段](../../../segmentation/tutorials/evaluate-a-segment.md) ”部分涵盖导出受众数据集所需的步骤。 该指南概述并提供了以下示例：

- **创建目标数据集：** 创建数据集以容纳受众成员。
- **在数据集中生成受众用户档案:** 根据区段作业的结果，用XDM单个用户档案填充数据集。
- **监视导出进度：** 检查导出过程的当前进度。
- **读取受众数据：** 检索表示您的用户档案成员的生成的XDM单个受众。

## 后续步骤

本文档概述了下载客户AI得分所需的步骤。 您现在可以继续浏览提供的 [其他智能服务](../../home.md) 和指南。

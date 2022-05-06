---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 导出作业API端点
topic-legacy: guide
type: Documentation
description: 实时客户配置文件允许您通过将来自多个来源的数据（包括属性数据和行为数据）汇总在一起，在Adobe Experience Platform中构建单个客户视图。 然后，可以将配置文件数据导出到数据集以进一步处理。
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1517'
ht-degree: 2%

---

# 导出作业端点

[!DNL Real-time Customer Profile] 通过将来自多个来源的数据（包括属性数据和行为数据）汇总在一起，使您能够构建单个客户视图。 然后，可以将配置文件数据导出到数据集以进一步处理。 例如，受众区段来自 [!DNL Profile] 可以导出数据以进行激活，也可以导出配置文件属性以进行报告。

本文档提供了使用创建和管理导出作业的分步说明 [配置文件API](https://www.adobe.com/go/profile-apis-en).

>[!NOTE]
>
>本指南介绍如何在 [!DNL Profile API]. 有关如何管理Adobe Experience Platform Segmentation Service的导出作业的信息，请参阅 [导出分段API中的作业](../../profile/api/export-jobs.md).

除了创建导出作业外，您还可以访问 [!DNL Profile] 使用 `/entities` 端点，也称为“[!DNL Profile Access]&quot; 请参阅 [entities endpoint指南](./entities.md) 以了解更多信息。 有关如何访问的步骤 [!DNL Profile] 使用UI的数据，请参阅 [用户指南](../ui/user-guide.md).

## 快速入门

本指南中使用的API端点是 [!DNL Real-time Customer Profile] API。 在继续之前，请查看 [入门指南](getting-started.md) 有关相关文档的链接、本文档中的API调用示例指南，以及有关成功调用任何代码所需标头的重要信息 [!DNL Experience Platform] API。

## 创建导出作业

导出 [!DNL Profile] 数据需要先创建一个要将数据导出到的数据集，然后启动新的导出作业。 这两个步骤都可以使用Experience PlatformAPI来实现，前者使用目录服务API，后者使用实时客户资料API。 有关完成每个步骤的详细说明，请参见下面的章节。

### 创建目标数据集

导出时 [!DNL Profile] 数据，必须首先创建目标数据集。 必须正确配置数据集，以确保成功导出。

其中一个关键注意事项是数据集所基于的架构(`schemaRef.id` （在下面的API示例请求中）。 要导出用户档案数据，数据集必须基于 [!DNL XDM Individual Profile] 并集架构(`https://ns.adobe.com/xdm/context/profile__union`)。 并集模式是系统生成的只读模式，用于聚合共享相同类的模式的字段。 在本例中，即 [!DNL XDM Individual Profile] 类。 有关并集视图架构的更多信息，请参阅 [架构组合基础知识指南中的并集部分](../../xdm/schema/composition.md#union).

本教程中遵循的步骤将简要介绍如何创建引用 [!DNL XDM Individual Profile] 并集架构(使用 [!DNL Catalog] API。 您还可以使用 [!DNL Platform] 用于创建引用并集架构的数据集的用户界面。 有关使用UI的步骤，请参见 [此用于导出区段的UI教程](../../segmentation/tutorials/create-dataset-export-segment.md) 但也适用于此处。 完成后，您可以返回到本教程以继续执行 [启动新导出作业](#initiate).

如果您已经有一个兼容的数据集并且知道其ID，则可以直接继续执行的步骤 [启动新导出作业](#initiate).

**API格式**

```http
POST /dataSets
```

**请求**

以下请求会创建一个新数据集，并在有效负载中提供配置参数。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        }
      }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 数据集的描述性名称。 |
| `schemaRef.id` | 数据集将与之关联的并集视图（架构）的ID。 |

**响应**

成功的响应会返回一个数组，其中包含新创建数据集的只读、系统生成的唯一ID。 要成功导出配置文件数据，需要正确配置的数据集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 启动导出作业 {#initiate}

在您拥有具有并集持久保留的数据集后，可以创建一个导出作业，通过向 `/export/jobs` 实时客户资料API中的端点，并提供您希望在请求正文中导出的数据的详细信息。

**API格式**

```http
POST /export/jobs
```

**请求**

以下请求会创建一个新的导出作业，在有效负载中提供配置参数。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields": {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    }
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }' 
```

| 属性 | 描述 |
| -------- | ----------- |
| `fields` | *（可选）* 将要包含在导出中的数据字段限制为仅在此参数中提供的数据字段。 省略此值将导致导出数据中包含所有字段。 |
| `mergePolicy` | *（可选）* 指定用于管理导出数据的合并策略。 当有多个区段要导出时，请包含此参数。 |
| `mergePolicy.id` | 合并策略的ID。 |
| `mergePolicy.version` | 要使用的合并策略的特定版本。 省略此值将默认使用最新版本。 |
| `additionalFields.eventList` | *（可选）* 通过提供以下一个或多个设置，控制为子对象或关联对象导出的时间序列事件字段：<ul><li>`eventList.fields`:控制要导出的字段。</li><li>`eventList.filter`:指定限制关联对象中包含的结果的标准。 预期导出所需的最小值，通常为日期。</li><li>`eventList.filter.fromIngestTimestamp`:将时间系列事件筛选为在提供的时间戳后摄取的事件。 这不是事件时间本身，而是事件的摄取时间。</li></ul> |
| `destination` | **（必需）** 导出数据的目标信息：<ul><li>`destination.datasetId`: **（必需）** 要导出数据的数据集的ID。</li><li>`destination.segmentPerBatch`: *（可选）* 一个布尔值，如果未提供，则默认为 `false`. 值 `false` 将所有区段ID导出为单个批处理ID。 值 `true` 将一个区段ID导出为一个批ID。 请注意，将值设置为 `true` 可能会影响批量导出性能。</li></ul> |
| `schema.name` | **（必需）** 与要导出数据的数据集关联的架构的名称。 |

>[!NOTE]
>
>要仅导出配置文件数据而不包含相关的时序数据，请从请求中删除“additionalFields”对象。

**响应**

成功响应会返回一个数据集，其中填充了请求中指定的配置文件数据。

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

## 列出所有导出作业

您可以通过向 `export/jobs` 端点。 该请求还支持查询参数 `limit` 和 `offset`，如下所示。

**API格式**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
| -------- | ----------- |
| `start` | 根据请求的创建时间，偏移返回的结果页面。 示例: `start=4` |
| `limit` | 限制返回的结果数。 示例: `limit=10` |
| `page` | 根据请求的创建时间返回特定的结果页面。 示例: `page=2` |
| `sort` | 按特定字段对结果进行升序排序( **`asc`** )或降序( **`desc`** )顺序。 返回多个结果页面时，排序参数不起作用。 示例: `sort=updateTime:asc` |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

响应包括 `records` 包含由IMS组织创建的导出作业的对象。

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{ORG_ID}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{ORG_ID}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

## 监视导出进度

要查看特定导出作业的详细信息或在其处理过程中监视其状态，您可以向 `/export/jobs` 端点并包含 `id` 中的导出作业。 导出作业在 `status` 字段会返回值“SUCCEEDED”。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 的 `id` 要访问的导出作业。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `batchId` | 从成功导出创建的批次的标识符，用于读取用户档案数据时的查找目的。 |

## 取消导出作业

Experience Platform允许您取消现有的导出作业，这可能由于多种原因（包括导出作业未完成或在处理阶段卡住）而有用。 要取消导出作业，您可以对 `/export/jobs` 端点并包含 `id` 要取消到请求路径的导出作业。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 的 `id` 要访问的导出作业。 |

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的删除请求会返回HTTP状态204（无内容）和空的响应正文，指示取消操作已成功。

## 后续步骤

成功完成导出后，您的数据即可在数据湖中Experience Platform。 然后，您可以使用 [数据访问API](https://www.adobe.io/experience-platform-apis/references/data-access/) 使用 `batchId` 与导出关联。 根据导出的大小，数据可能以块为单位，并且批处理可能由多个文件组成。

有关如何使用数据访问API访问和下载批处理文件的分步说明，请按照 [数据访问教程](../../data-access/tutorials/dataset-data.md).

您还可以使用Adobe Experience Platform查询服务访问成功导出的实时客户资料数据。 通过使用UI或RESTful API，查询服务允许您对数据湖中的数据写入、验证和运行查询。

有关如何查询受众数据的更多信息，请参阅 [查询服务文档](../../query-service/home.md).

## 附录

以下部分包含有关配置文件API中导出作业的其他信息。

### 其他导出负载示例

API调用示例，如 [启动导出作业](#initiate) 创建同时包含用户档案（记录）和事件（时间系列）数据的作业。 此部分提供了其他请求有效负载示例，以限制您的导出包含一种或另一种数据类型。

以下有效负载会创建一个仅包含用户档案数据（无事件）的导出作业：

```json
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

要创建只包含事件数据（无配置文件属性）的导出作业，有效负载可能类似于以下内容：

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields": {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

### 导出区段

您还可以使用导出作业端点导出受众区段，而不是 [!DNL Profile] 数据。 请参阅 [导出分段API中的作业](../../segmentation/api/export-jobs.md) 以了解更多信息。

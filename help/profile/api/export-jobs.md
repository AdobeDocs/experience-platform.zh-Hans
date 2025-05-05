---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 配置文件导出作业API端点
type: Documentation
description: Real-Time Customer Profile通过将来自多个来源的数据（包括属性数据和行为数据）整合在一起，使您能够在Adobe Experience Platform中构建单个客户视图。 然后，可将用户档案数据导出到数据集以供进一步处理。
role: Developer
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 2%

---

# 配置文件导出作业端点

[!DNL Real-Time Customer Profile]使您能够将来自多个来源的数据（包括属性数据和行为数据）整合在一起，从而构建单个客户的视图。 然后，可将用户档案数据导出到数据集以供进一步处理。 例如，可通过创建受众导出[!DNL Profile]数据以进行激活，并可导出配置文件属性以进行报告。

本文档提供了使用[配置文件API](https://www.adobe.com/go/profile-apis-en)创建和管理导出作业的分步说明。

>[!NOTE]
>
>本指南介绍[!DNL Profile API]中导出作业的使用情况。 有关如何管理Adobe Experience Platform Segmentation Service的导出作业的信息，请参阅关于分段API中的[导出作业的指南](../../profile/api/export-jobs.md)。

除了创建导出作业之外，您还可以使用`/entities`终结点（也称为“[!DNL Profile Access]”）访问[!DNL Profile]数据。 有关详细信息，请参阅[实体终结点指南](./entities.md)。 有关如何使用用户界面访问[!DNL Profile]数据的步骤，请参阅[用户指南](../ui/user-guide.md)。

## 快速入门

本指南中使用的API端点是[!DNL Real-Time Customer Profile] API的一部分。 在继续之前，请查看[快速入门指南](getting-started.md)，以获取相关文档的链接、此文档中示例API调用的阅读指南，以及有关成功调用任何[!DNL Experience Platform] API所需的所需标头的重要信息。

## 创建导出作业

导出[!DNL Profile]数据首先需要创建数据将导出到的数据集，然后启动新的导出作业。 这两个步骤都可以使用Experience Platform API来完成，前者使用目录服务API，后者使用实时客户档案API。 以下各节概述了完成每个步骤的详细说明。

### 创建目标数据集

导出[!DNL Profile]数据时，必须首先创建目标数据集。 请务必正确配置数据集以确保成功导出。

关键注意事项之一是数据集所基于的架构（以下API示例请求中的`schemaRef.id`）。 为了导出配置文件数据，数据集必须基于[!DNL XDM Individual Profile]联合架构(`https://ns.adobe.com/xdm/context/profile__union`)。 合并架构是系统生成的只读架构，它聚合共享相同类的架构的字段。 在这种情况下，它是[!DNL XDM Individual Profile]类。 有关合并视图架构的详细信息，请参阅架构组合基础指南[&#128279;](../../xdm/schema/composition.md#union)中的合并部分。

本教程中接下来的步骤概述了如何使用[!DNL Catalog] API创建引用[!DNL XDM Individual Profile]合并架构的数据集。 您还可以使用[!DNL Experience Platform]用户界面创建引用合并架构的数据集。 此[有关导出受众的UI教程](../../segmentation/tutorials/create-dataset-export-segment.md)中概述了使用UI的步骤，但此处也适用。 完成后，您可以返回本教程以继续执行[启动新导出作业](#initiate)的步骤。

如果您已经具有兼容的数据集并且知道其ID，则可以直接进入[启动新导出作业](#initiate)的步骤。

**API格式**

```http
POST /dataSets
```

**请求**

以下请求创建一个新数据集，在有效负载中提供配置参数。

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
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
| `schemaRef.id` | 数据集将关联的合并视图（架构）的ID。 |

**响应**

成功的响应会返回一个数组，其中包含新创建的数据集的只读、系统生成的唯一ID。 需要正确配置的数据集ID才能成功导出配置文件数据。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 启动导出作业 {#initiate}

拥有合并持久化数据集后，您可以创建一个导出作业以将配置文件数据持久化到数据集，方法是对实时客户配置文件API中的`/export/jobs`端点发出POST请求，并在请求正文中提供要导出的数据的详细信息。

**API格式**

```http
POST /export/jobs
```

**请求**

以下请求创建新的导出作业，在有效负载中提供配置参数。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
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
    },
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
| `fields` | *（可选）*&#x200B;将导出中包含的数据字段限制为仅包含在此参数中提供的那些字段。 省略此值将导致所有字段都包含在导出的数据中。 |
| `mergePolicy` | *（可选）*&#x200B;指定合并策略以管理导出的数据。 当导出多个受众时，包含此参数。 |
| `mergePolicy.id` | 合并策略的ID。 |
| `mergePolicy.version` | 要使用的合并策略的特定版本。 省略此值将默认使用最新版本。 |
| `additionalFields.eventList` | *（可选）*&#x200B;通过提供以下一个或多个设置，控制为子对象或关联对象导出的时间序列事件字段：<ul><li>`eventList.fields`：控制要导出的字段。</li><li>`eventList.filter`：指定限制从关联对象包含结果的条件。 需要导出所需的最小值，通常为日期。</li><li>`eventList.filter.fromIngestTimestamp`：将时间序列事件筛选为提供的时间戳之后摄取的那些事件。 这不是事件时间本身，而是事件的摄取时间。</li></ul> |
| `destination` | **（必需）**&#x200B;导出数据的目标信息：<ul><li>`destination.datasetId`： **（必需）**&#x200B;要导出数据的数据集的ID。</li><li>`destination.segmentPerBatch`： *（可选）*&#x200B;如果未提供，则默认为`false`的布尔值。 值为`false`会将所有区段定义ID导出到单个批次ID中。 值为`true`可将一个区段定义ID导出到一个批次ID中。 请注意，将该值设置为`true`可能会影响批量导出性能。</li></ul> |
| `schema.name` | **（必需）**&#x200B;与要导出数据的数据集关联的架构的名称。 |

>[!NOTE]
>
>要仅导出配置文件数据而不包括相关时间序列数据，请从请求中删除“additionalFields”对象。

**响应**

成功的响应将返回一个使用在请求中指定的配置文件数据填充的数据集。

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

通过向`export/jobs`端点执行GET请求，您可以返回特定组织的所有导出作业列表。 该请求还支持查询参数`limit`和`offset`，如下所示。

**API格式**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
| -------- | ----------- |
| `start` | 根据请求的创建时间，偏移返回的结果页面。 示例：`start=4` |
| `limit` | 限制返回的结果数。 示例：`limit=10` |
| `page` | 根据请求的创建时间，返回结果的特定页面。 示例：`page=2` |
| `sort` | 按特定字段对结果进行升序( **`asc`** )或降序( **`desc`** )排序。 返回多个结果页面时，排序参数不起作用。 示例：`sort=updateTime:asc` |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

响应包含一个`records`对象，其中包含您的组织创建的导出作业。

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

## 监控导出进度

要查看特定导出作业的详细信息，或监视其处理状态，您可以向`/export/jobs`端点发出GET请求，并在路径中包含导出作业的`id`。 一旦`status`字段返回值“SUCCEEDED”，导出作业即完成。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 您要访问的导出作业的`id`。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/24115 \
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
| `batchId` | 成功导出后创建的批次的标识符，在读取配置文件数据时用于查找。 |

## 取消导出作业

Experience Platform允许您取消现有的导出作业，这可能会对许多原因非常有用，包括导出作业未完成或卡在处理阶段。 要取消导出作业，您可以对`/export/jobs`端点执行DELETE请求，并将要取消的导出作业的`id`包含到请求路径。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 您要访问的导出作业的`id`。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的删除请求返回HTTP状态204（无内容）和空响应正文，指示取消操作成功。

## 后续步骤

成功完成导出后，您的数据即可在Experience Platform的数据湖中使用。 然后，您可以使用[数据访问API](https://www.adobe.io/experience-platform-apis/references/data-access/)，通过与导出关联的`batchId`来访问数据。 根据导出的大小，数据可能以块为单位，批量可能包含多个文件。

有关如何使用数据访问API访问和下载批处理文件的分步说明，请按照[数据访问教程](../../data-access/tutorials/dataset-data.md)操作。

您还可以使用Adobe Experience Platform查询服务访问成功导出的实时客户配置文件数据。 查询服务使用UI或RESTful API，允许您编写、验证和运行对数据湖中数据的查询。

有关如何查询受众数据的详细信息，请查阅[查询服务文档](../../query-service/home.md)。

## 附录

以下部分包含有关配置文件API中导出作业的其他信息。

### 其他导出有效负载示例

有关[启动导出作业](#initiate)的部分中显示的示例API调用将创建一个包含配置文件（记录）和事件（时间序列）数据的作业。 此部分提供其他请求有效负载示例，以限制您的导出包含一种数据类型，或包含另一种数据类型。

以下有效负载创建一个仅包含配置文件数据（无事件）的导出作业：

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

要创建仅包含事件数据（无配置文件属性）的导出作业，负载可能类似于以下内容：

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

### 导出受众

您还可以使用导出作业终结点导出受众，而不是[!DNL Profile]数据。 有关详细信息，请参阅分段API[&#128279;](../../segmentation/api/export-jobs.md)中有关导出作业的指南。

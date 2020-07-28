---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 导出作业——实时客户用户档案API
topic: guide
translation-type: tm+mt
source-git-commit: 2c0466bf0534d09e3cad54caef213def122d948b
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 2%

---


# 导出作业端点

[!DNL Real-time Customer Profile] 通过整合来自多个来源的数据（包括属性数据和行为数据），您能够为单个客户构建一个视图。 然后，可以将 [!DNL Profile] 中可用的数据导出到数据集以进一步处理。 例如，可以导出受众 [!DNL Profile] 数据中的用户档案段以进行激活，也可以导出属性以进行报告。

此文档提供使用用户档案API创建和管理导出作业的分步 [说明](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)。

>[!NOTE]
>
>本指南涵盖导出作业在中的使用 [!DNL Profile API]。 有关如何管理Adobe Experience Platform分段服务的导出作业的信息，请参阅分段API中 [的导出作业指南](../../profile/api/export-jobs.md)。

除了创建导出作业外，您还可以使 [!DNL Profile] 用端点 `/entities` (也称为“[!DNL Profile Access]”)访问数据。 See the [entities endpoint guide](./entities.md) for more information. 有关如何使用UI访 [!DNL Profile] 问数据的步骤，请参阅用 [户指南](../ui/user-guide.md)。

## 入门指南

本指南中使用的API端点是API的一 [!DNL Real-time Customer Profile] 部分。 在继续之前，请查 [看入门指南](getting-started.md) ，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何API所需标头的重要信 [!DNL Experience Platform] 息。

## 创建导出作业

导 [!DNL Profile] 出数据需要先创建要将数据导出到的数据集，然后启动新的导出作业。 这两个步骤都可以使用Experience PlatformAPI实现，前者使用目录服务API，后者使用实时客户用户档案API。 有关完成每个步骤的详细说明，请参阅以下各节。

### 创建目标数据集

导出数 [!DNL Profile] 据时，必须先创建目标数据集。 必须正确配置数据集以确保导出成功。

一个主要考虑事项是数据集所基于的模式(在`schemaRef.id` 下面的API示例请求中)。 要导出用户档案数据，数据集必须基于合并 [!DNL XDM Individual Profile] 模式(`https://ns.adobe.com/xdm/context/profile__union`)。 合并模式是系统生成的只读模式，它聚合共享同一类的模式字段。 在这个例子中，这就是 [!DNL XDM Individual Profile] 课。 有关合并视图模式的详细信息，请参 [阅模式合成指南基础知识中的合并部分](../../xdm/schema/composition.md#union)。

本教程中接下来的步骤概述了如何使用API创建引用 [!DNL XDM Individual Profile] 合并模式的 [!DNL Catalog] 数据集。 您还可以使用用 [!DNL Platform] 户界面创建引用合并模式的数据集。 此UI教程中概述了使用UI [的步骤，用于导出区段](../../segmentation/tutorials/create-dataset-export-segment.md) ，但也适用于此处。 完成后，您可以返回本教程，继续执行启动新 [导出作业的步骤](#initiate)。

如果您已经有一个兼容数据集并知道其ID，则可以直接继续执行启动新 [导出作业的步骤](#initiate)。

**API格式**

```http
POST /dataSets
```

**请求**

以下请求将创建新数据集，在有效负荷中提供配置参数。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        },
        "fileDescription": {
          "persisted": true,
          "containerFormat": "parquet",
          "format": "parquet"
        }
      }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 数据集的描述性名称。 |
| `schemaRef.id` | 合并集将与之关联的视图(模式)的ID。 |
| `fileDescription.persisted` | 一个布尔值，当设置为 `true`时，它使数据集在合并视图中保持。 |

**响应**

成功的响应会返回一个数组，其中包含新创建数据集的只读、系统生成的唯一ID。 要成功导出用户档案数据，需要正确配置的数据集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 启动导出作业 {#initiate}

一旦有合并持久数据集，您就可以创建一个导出作业，通过在实时用户档案API中向端点发出POST请求并在请求主体中提供要导出的数据的详细信息，将用户档案数据保留到数据集。 `/export/jobs`

**API格式**

```http
POST /export/jobs
```

**请求**

以下请求将创建新的导出作业，在有效负荷中提供配置参数。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
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
| `fields` | *（可选）* 将要包含在导出中的数据字段限制为仅包含在此参数中的字段。 忽略此值将导致导出数据中包含所有字段。 |
| `mergePolicy` | *（可选）* 指定用于管理导出数据的合并策略。 当导出多个段时，请包含此参数。 |
| `mergePolicy.id` | 合并策略的ID。 |
| `mergePolicy.version` | 要使用的合并策略的特定版本。 忽略此值将默认为最新版本。 |
| `additionalFields.eventList` | *（可选）通过* 提供以下一个或多个设置，控制为子对象或关联对象导出的时间序列事件字段：<ul><li>`eventList.fields`: 控制要导出的字段。</li><li>`eventList.filter`: 指定限制关联对象中包含的结果的条件。 需要导出所需的最小值，通常为日期。</li><li>`eventList.filter.fromIngestTimestamp`: 过滤器时间序列事件到在提供的时间戳后摄取的时间序列。 这不是事件本身，而是事件的摄取时间。</li></ul> |
| `destination` | **（必需）导出** 数据的目标信息：<ul><li>`destination.datasetId`: **(必需** )要导出数据的数据集的ID。</li><li>`destination.segmentPerBatch`: *(可选* )布尔值，如果未提供，则默认为 `false`。 值将所 `false` 有段ID导出为单个批ID。 值将一个 `true` 段ID导出为一个批ID。 请注意，将值设置为可能 `true` 会影响批量导出性能。</li></ul> |
| `schema.name` | **(必需** )与要导出数据的数据集关联的模式的名称。 |

>[!NOTE] 要仅导出用户档案数据而不包括相关的时间序列数据，请从请求中删除“additionalFields”对象。

**响应**

成功的响应会返回一个数据集，其中填充了请求中指定的用户档案数据。

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
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

## 列表所有导出作业

通过向端点执行列表请求，可以返回特定IMS组织的所有导出作业的GET `export/jobs` 符。 该请求还支持查询参 `limit` 数 `offset`和，如下所示。

**API格式**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
| -------- | ----------- |
| `start` | 根据请求的创建时间，偏移返回的结果页面。 示例: `start=4` |
| `limit` | 限制返回的结果数。 示例: `limit=10` |
| `page` | 按照请求的创建时间返回特定的结果页面。 示例: `page=2` |
| `sort` | 按特定字段按升序()或降序() **`asc`** 顺序对结果 **`desc`** 进行排序。 返回多页结果时，排序参数不起作用。 示例: `sort=updateTime:asc` |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

该响应包含 `records` 一个对象，其中包含由IMS组织创建的导出作业。

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
      "imsOrgId": "{IMS_ORG}",
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
      "imsOrgId": "{IMS_ORG}",
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

要视图特定导出作业的详细信息，或在其处理过程中监视其状态，您可以向端点发出GET请求，并 `/export/jobs` 将导出作 `id` 业的详细信息包括在路径中。 一旦字段返回值“SUCCEEDED”, `status` 导出作业即完成。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 要 `id` 访问的导出作业。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `batchId` | 从成功导出创建的批的标识符，用于读取用户档案数据时的查找目的。 |

## 取消导出作业

Experience Platform允许您取消现有的导出作业，这可能有多种原因，包括导出作业未完成或在处理阶段卡住。 要取消导出作业，您可以对终结点执行DELETE `/export/jobs` 请求，并将要 `id` 取消的导出作业包含到请求路径中。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 要 `id` 访问的导出作业。 |

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功删除请求将返回HTTP状态204（无内容）和空的响应主体，表示取消操作成功。

## 后续步骤

成功完成导出后，您的数据即可在Experience Platform的数据湖中使用。 然后，您可以使用 [数据访问](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) API，使用与导出 `batchId` 关联的数据访问数据。 根据导出的大小，数据可能以块为单位，而批可能由多个文件组成。

有关如何使用数据访问API访问和下载批处理文件的分步说明，请遵循数据 [访问教程](../../data-access/tutorials/dataset-data.md)。

您还可以使用Adobe Experience Platform用户档案服务访问成功导出的实时客户查询数据。 查询服务使用UI或RESTful API，允许您对数据湖中的数据编写、验证和运行查询。

有关如何查询受众数据的更多信息，请查阅 [查询服务文档](../../query-service/home.md)。

## 附录

以下部分包含有关用户档案API中导出作业的其他信息。

### 其他导出有效负荷示例

启动导出作业一节中显示的 [示例API调用](#initiate) ，创建一个同时包含用户档案（记录）和事件（时间序列）数据的作业。 本节提供其他请求有效负荷示例，以限制导出包含一种或另一种数据类型。

以下有效负荷创建的导出作业只包含用户档案数据(无事件):

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

要创建只包含事件数据(无用户档案属性)的导出作业，有效负荷的外观可能与以下内容类似：

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
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

您还可以使用导出作业端点导出受众段而非 [!DNL Profile] 数据。 有关详细信息， [请参阅分段API中的](../../segmentation/api/export-jobs.md) “导出作业”指南。
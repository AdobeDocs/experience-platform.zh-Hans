---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用API导出数据
topic: tutorial
translation-type: tm+mt
source-git-commit: 409d98818888f2758258441ea2d993ced48caf9a

---


# 使用API导出用户档案数据

实时客户用户档案使您能够通过整合来自多个来源的数据（包括属性数据和行为数据）来构建单个客户视图。 然后，可将用户档案中可用的数据导出到数据集以进一步处理。 本教程提供了使用分段API创建和管理导出作业的分步 [说明](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)。

除了创建导出作业外，您还可以使用用户档案访问API和通过预测访问用户档案数据。 有关这些其 [他访问模式的详细信息](../../profile/api/entities.md) ，请参阅 [用户档案访问API教程或配置边缘目](../../profile/api/edge-projections.md) 标和预测的教程。

## 入门指南

本教程需要对处理用户档案数据时涉及的各种Adobe Experience Platform服务进行有效的了解。 在开始本教程之前，请查看以下服务的相关文档：

- [实时客户用户档案](../../profile/home.md):根据来自多个来源的汇总数据实时提供统一的客户用户档案。
- [Adobe Experience Platform Segmentation Service](../home.md):允许您根据实时客户用户档案数据构建受众细分。
- [体验数据模型(XDM)](../../xdm/home.md):平台通过标准化框架组织客户体验数据。
- [沙箱](../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

### 必需的标题

本教程还要求您完成身份验证教 [程](../../tutorials/authentication.md) ，以便成功调用平台API。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权：承载人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的请求需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有POST、PUT和PATCH请求都需要额外的标题：

- 内容类型：application/json

## 创建导出作业

导出用户档案数据需要先创建要将数据导出到的数据集，然后启动新的导出作业。 这两个步骤都可以使用Experience Platform API(前者使用Catalog Service API，后者使用实时客户用户档案API)来实现。 有关完成每个步骤的详细说明，请参阅以下各节。

- [创建目标数据集](#create-a-target-dataset) -创建数据集以保存导出的数据。
- [启动新的导出作业](#initiate-export-job) -用XDM单个用户档案数据填充数据集。

### 创建目标数据集

导出用户档案数据时，必须先创建目标数据集。 必须正确配置数据集以确保导出成功。

一个关键注意事项是数据集所基于的模式(在`schemaRef.id` 下面的API示例请求中)。 要导出区段，数据集必须基于XDM单个用户档案合并模式(`https://ns.adobe.com/xdm/context/profile__union`)。 合并模式是系统生成的只读模式，它聚合共享同一类的模式的字段，在本例中为XDM单个用户档案类。 有关合并视图模式的更多信息，请参 [阅模式注册开发人员指南的实时客户用户档案部分](../../xdm/schema/composition.md#union)。

本教程中接下来的步骤概述了如何使用目录API创建引用XDM单个用户档案合并模式的数据集。 您还可以使用Adobe Experience Platform用户界面创建引用合并模式的数据集。 此UI教程介绍了使用UI的 [步骤以导出区段](./create-dataset-export-segment.md) ，但也适用于此处。 完成后，您可以返回本教程，继续执行启动新导 [出作业的步骤](#initiate-export-job)。

如果您已经有一个兼容的数据集并且知道其ID，则可以直接继续执行启动新导 [出作业的步骤](#initiate-export-job)。

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
| `schemaRef.id` | 数据集将与合并视图(模式)关联的ID。 |
| `fileDescription.persisted` | 一个布尔值，当设置为时， `true`它使数据集能够在合并视图中持续存在。 |

**响应**

成功的响应会返回一个数组，其中包含新创建的数据集的只读、系统生成的唯一ID。 要成功导出用户档案数据，需要正确配置的数据集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 启动导出作业

一旦有持续合并数据集，您便可以创建一个导出作业，以将用户档案数据保留到数据集，方法是在实时客户用户档案API中向端点发出POST请求，并在请求正文中提供要导出的数据的详细信息。 `/export/jobs`

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
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
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
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `fields` | *（可选）* 将要包含在导出中的数据字段限制为仅包含在此参数中提供的数据字段。 创建区段时也可以使用相同的参数，因此区段中的字段可能已过滤。 忽略此值将导致导出的数据中包含所有字段。 |
| `mergePolicy` | *（可选）* 指定用于管理导出数据的合并策略。 当导出多个区段时，请包含此参数。 忽略此值将导致导出服务使用区段提供的合并策略。 |
| `mergePolicy.id` | 合并策略的ID。 |
| `mergePolicy.version` | 要使用的合并策略的特定版本。 省略此值将默认为最新版本。 |
| `filter` | *（可选）* 指定在导出之前应用于区段的以下一个或多个过滤器。 |
| `filter.segments` | *（可选）* 指定要导出的区段。 忽略此值将导致导出所有用户档案的所有数据。 接受段对象的数组，每个对象都包含以下字段：<ul><li>`segmentId`:( **使用时需要`segments`** )要导出的用户档案的区段ID。</li><li>`segmentNs` (可 *选)* ，给定的区段命名空间 `segmentID`。</li><li>`status` (可 *选)* ，提供状态过滤器的字符串数组 `segmentID`。 默认情况下， `status` 该值将表示 `["realized", "existing"]` 当前时间属于该区段的所有用户档案。 可能的值包括： `"realized"`、 `"existing"`和 `"exited"`。</br></br>有关详细信息，请参阅创 [建区段教程](./create-a-segment.md)。</li></ul> |
| `filter.segmentQualificationTime` | *（可选）* Filter based on segment qualification time. 可以提供开始时间和／或结束时间。 |
| `filter.segmentQualificationTime.startTime` | *（可选）* ，给定状态的区段ID的区段资格开始时间。 未提供，将不对区段ID资格的开始时间进行筛选。 时间戳必须以 [RFC 3339格式提供](https://tools.ietf.org/html/rfc3339) 。 |
| `filter.segmentQualificationTime.endTime` | *（可选）* ，给定状态的区段ID的区段资格结束时间。 它未提供，在区段ID资格的结束时间上不会有过滤器。 时间戳必须以 [RFC 3339格式提供](https://tools.ietf.org/html/rfc3339) 。 |
| `filter.fromIngestTimestamp ` | *（可选）* 将导出的用户档案限制为仅包括在此时间戳后更新的那些。 时间戳必须以 [RFC 3339格式提供](https://tools.ietf.org/html/rfc3339) 。 <ul><li>`fromIngestTimestamp` **用户档案**，如果提供：包括所有合并的用户档案，其中合并的更新时间戳大于给定时间戳。 支持操 `greater_than` 作数。</li><li>`fromTimestamp` 对于 **事件**:在此时间戳之后摄取的所有事件将与生成的用户档案结果相对应地导出。 这不是事件时间本身，而是事件的摄取时间。</li> |
| `filter.emptyProfiles` | *（可选）* Boolean。 用户档案可以包含用户档案记录和／或ExperienceEvent记录。 没有用户档案记录且只有ExperienceEvent记录的用户档案称为“emptyProfiles”。 要导出用户档案商店中的所有用户档案（包括“emptyProfiles”），请将值设 `emptyProfiles` 置为 `true`。 如果 `emptyProfiles` 设置为， `false`则只导出存储中具有用户档案记录的用户档案。 默认情况下，如 `emptyProfiles` 果不包括属性，则只导出包含用户档案记录的用户档案。 |
| `additionalFields.eventList` | *（可选）* 通过提供以下一个或多个设置，控制为子对象或关联对象导出的时间序列事件字段：<ul><li>`eventList.fields`:控制要导出的字段。</li><li>`eventList.filter`:指定限制关联对象中包含的结果的条件。 需要导出所需的最小值，通常为日期。</li><li>`eventList.filter.fromIngestTimestamp`:过滤器时间序列事件到在提供时间戳后摄取的时间序列。 这不是事件时间本身，而是事件的摄取时间。</li></ul> |
| `destination` | **（必需）** “导出的数据”的目标信息：<ul><li>`destination.datasetId`:(必 **需)** ，要导出数据的数据集的ID。</li><li>`destination.segmentPerBatch`:(可 *选)* Boolean值，如果未提供，则默认为 `false`。 值将所 `false` 有区段ID导出为单个批ID。 值将一个 `true` 段ID导出为一个批ID。 请注意，将值设置为可能 `true` 会影响批导出性能。</li></ul> |
| `schema.name` | **（必需）** ，与要导出数据的数据集关联的模式的名称。 |

>[!NOTE] 要仅导出用户档案数据而不包括相关的ExperienceEvent数据，请从请求中删除“additionalFields”对象。

**响应**

成功的响应会返回一个数据集，其中填充了请求中指定的用户档案数据。

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

如 `destination.segmentPerBatch` 果请求中未包括(如果不存在，则默认为 `false`)或将值设置为 `false`，则上述响应中的对象将没有数组，而只包括一个 `destination``batches``batchId`，如下所示。 该单个批将包括所有区段ID，而上述响应显示每个批ID的单个区段ID。

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

## 列表所有导出作业

您可以通过向端点执行GET请求，为特定IMS组织返回所有导出作业的列表 `export/jobs` 信息。 该请求还支持查询参 `limit` 数 `offset`和，如下所示。

**API格式**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| 属性 | 描述 |
| -------- | ----------- |
| `limit` | 指定要返回的记录数。 |
| `offset` | 将返回的结果页偏移所提供的数字。 |

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

响应包括一个对 `records` 象，其中包含由IMS组织创建的导出作业。

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
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

要视图特定导出作业的详细信息，或在其处理过程中监视其状态，您可以向端点发出GET请求，并在路径中包 `/export/jobs``id` 含导出作业的内容。 在字段返回值“SUCCEEDED” `status` 后，导出作业即完成。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 要 `id` 访问的导出作业的值。 |

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
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
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

Experience Platform允许您取消现有的导出作业，这可能由于许多原因（包括导出作业未完成或在处理阶段卡住）而有用。 要取消导出作业，您可以对端点执行DELETE请求，并将要取消的导出作业 `/export/jobs``id` 包含到请求路径中。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 要 `id` 访问的导出作业的值。 |

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

如果删除请求成功，则返回HTTP状态204（无内容）和空的响应主体，表示取消操作成功。

## 后续步骤

成功完成导出后，您的数据即可在Experience Platform的数据湖中使用。 然后，您可以使用 [Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) ，使用与导出相关 `batchId` 的访问数据。 根据导出的大小，数据可能以块为单位，而批可能由多个文件组成。

有关如何使用Data Access API访问和下载批处理文件的分步说明，请遵循数据访 [问教程](../../data-access/tutorials/dataset-data.md)。

您还可以使用Adobe Experience Platform用户档案服务访问成功导出的实时客户查询数据。 使用UI或RESTful API,查询服务允许您在数据湖中编写、验证和运行查询。

有关如何查询受众数据的更多信息，请查阅 [查询服务文档](../../query-service/home.md)。
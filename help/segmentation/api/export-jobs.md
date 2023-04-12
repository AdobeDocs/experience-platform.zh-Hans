---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；导出作业；API;
solution: Experience Platform
title: 区段导出作业API端点
description: 导出作业是用于将受众区段成员保留到数据集的异步进程。 您可以在Adobe Experience Platform Segmentation Service API中使用/export/jobs端点，该端点允许您以编程方式检索、创建和取消导出作业。
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 2%

---

# 区段导出作业端点

导出作业是用于将受众区段成员保留到数据集的异步进程。 您可以使用 `/export/jobs` Adobe Experience Platform分段API中的端点，它允许您以编程方式检索、创建和取消导出作业。

>[!NOTE]
>
>本指南介绍如何在 [!DNL Segmentation API]. 有关如何管理的导出作业的信息 [!DNL Real-Time Customer Profile] 数据，请参阅 [导出配置文件API中的作业](../../profile/api/export-jobs.md)

## 快速入门

本指南中使用的端点是 [!DNL Adobe Experience Platform Segmentation Service] API。 在继续之前，请查看 [入门指南](./getting-started.md) 有关成功调用API所需的重要信息，包括所需的标头以及如何读取示例API调用。

## 检索导出作业列表 {#retrieve-list}

通过向 `/export/jobs` 端点。

**API格式**

的 `/export/jobs` 端点支持多个查询参数来帮助筛选结果。 虽然这些参数是可选的，但强烈建议使用这些参数，以帮助减少昂贵的开销。 对此端点进行无参数调用将检索适用于贵组织的所有导出作业。 可以包含多个参数，这些参数之间用与号(`&`)。

```http
GET /export/jobs
GET /export/jobs?limit={LIMIT}
GET /export/jobs?offset={OFFSET}
GET /export/jobs?status={STATUS}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{LIMIT}` | 指定返回的导出作业数。 |
| `{OFFSET}` | 指定结果页的偏移。 |
| `{STATUS}` | 根据状态筛选结果。 支持的值为“NEW”、“SUCCEEDED”和“FAILED”。 |

**请求**

以下请求将检索您组织内的最后两个导出作业。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

以下响应会根据请求路径中提供的查询参数，返回包含已成功完成导出作业列表的HTTP状态200。

```json
{
    "records": [
        {
            "id": 100,
            "jobType": "BATCH",
            "destination": {
                "datasetId": "5b7c86968f7b6501e21ba9df",
                "segmentPerBatch": false,
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
            },
            "fields": "identities.id,personalEmail.address",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "status": "SUCCEEDED",
            "filter": {
                "segments": [
                    {
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "ups",
                        "status": [
                            "realized"
                        ]
                    }
                ]
            },
            "mergePolicy": {
                "id": "timestampOrdered-none-mp",
                "version": 1
            },
            "profileInstanceId": "ups",
            "errors": [
                {
                    "code": "0100000003",
                    "msg": "Error in Export Job",
                    "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger"
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "profileExportTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "totalExportedProfileCounter": 20,
                "exportedProfileByNamespaceCounter": {
                    "namespace1": 10,
                    "namespace2": 5
                }
            },
            "computeGatewayJobId": {
                "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
            },
            "creationTime": 1538615973895,
            "updateTime": 1538616233239,
            "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
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
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "AAM",
                        "status": ["realized"]
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
                "segmentPerBatch": false,
                "batchId": "IWEQ6920712f9475762D"
            },
            "updateTime": 1538573922551,
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "creationTime": 1538573416687
        }
    ],
    "page":{
        "sortField": "createdTime",
        "sort": "desc",
        "pageOffset": "1540974701302_96",
        "pageSize": 2
    },
    "link":{
        "next": "/export/jobs/?limit=2&offset=1538573416687_722"
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `destination` | 导出数据的目标信息：<ul><li>`datasetId`:导出数据的数据集的ID。</li><li>`segmentPerBatch`:一个布尔值，用于显示区段ID是否已合并。 值“false”表示所有区段ID都导出为单个批量ID。 值“true”表示将一个区段ID导出为一个批量ID。 **注意：** 将值设置为true可能会影响批量导出性能。</li></ul> |
| `fields` | 导出字段的列表，用逗号分隔。 |
| `schema.name` | 与要导出数据的数据集关联的架构的名称。 |
| `filter.segments` | 导出的区段。 包括以下字段：<ul><li>`segmentId`:将用户档案导出到的区段ID。</li><li>`segmentNs`:给定的区段命名空间 `segmentID`.</li><li>`status`:字符串数组，为 `segmentID`. 默认情况下， `status` 将具有值 `["realized"]` 表示当前属于该区段的所有用户档案。 可能的值包括： `realized` 和 `exited`. 值 `realized` 表示用户档案符合区段的条件。 值 `exiting` 表示用户档案正在退出区段。</li></ul> |
| `mergePolicy` | 导出数据的合并策略信息。 |
| `metrics.totalTime` | 一个字段，用于指示导出作业运行所用的总时间。 |
| `metrics.profileExportTime` | 一个字段，用于指示用户档案导出所用的时间。 |
| `page` | 有关所请求导出作业分页的信息。 |
| `link.next` | 指向导出作业下一页的链接。 |

## 创建新导出作业 {#create}

您可以通过向 `/export/jobs` 端点。

**API格式**

```http
POST /export/jobs
```

**请求**

以下请求会创建一个新的导出作业，该作业由有效负载中提供的参数进行配置。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "string",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z",
                "toIngestTimestamp": "2020-01-01T00:00:00Z"
            }
        }
    },
    "destination":{
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false
    },
    "schema":{
        "name": "_xdm.context.profile"
    },
    "evaluationInfo": {
        "segmentation": true
    }
}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `fields` | 导出字段的列表，用逗号分隔。 如果留空，则将导出所有字段。 |
| `mergePolicy` | 指定用于管理导出数据的合并策略。 当有多个区段要导出时，请包含此参数。 如果未提供，则导出将采用与给定区段相同的合并策略。 |
| `filter` | 一个对象，根据下面列出的子属性，指定将按ID、鉴别时间或摄取时间包含在导出作业中的区段。 如果留空，则会导出所有数据。 |
| `filter.segments` | 指定要导出的区段。 省略此值将导致导出所有用户档案的所有数据。 接受区段对象的数组，每个数组都包含以下字段：<ul><li>`segmentId`: **(使用时需要 `segments`)** 要导出的用户档案的区段ID。</li><li>`segmentNs` *（可选）* 给定的区段命名空间 `segmentID`.</li><li>`status` *（可选）* 字符串数组，为 `segmentID`. 默认情况下， `status` 将具有值 `["realized"]` 表示当前属于该区段的所有用户档案。 可能的值包括： `realized` 和 `exited`.  值 `realized` 表示用户档案符合区段的条件。 值 `exiting` 表示用户档案正在退出区段。</li></ul> |
| `filter.segmentQualificationTime` | 根据区段鉴别时间进行筛选。 可以提供开始时间和/或结束时间。 |
| `filter.segmentQualificationTime.startTime` | 给定状态的区段ID的区段鉴别开始时间。 未提供，将不会对区段ID鉴别的开始时间进行过滤。 必须在 [RFC 3339](https://tools.ietf.org/html/rfc3339) 格式。 |
| `filter.segmentQualificationTime.endTime` | 给定状态的区段ID的区段鉴别结束时间。 如果未提供，则不会对区段ID鉴别的结束时间进行过滤。 必须在 [RFC 3339](https://tools.ietf.org/html/rfc3339) 格式。 |
| `filter.fromIngestTimestamp ` | 将导出的用户档案限制为仅包含在此时间戳后更新的用户档案。 必须在 [RFC 3339](https://tools.ietf.org/html/rfc3339) 格式。 <ul><li>`fromIngestTimestamp` 表示 **用户档案**，如果提供：包括所有合并的用户档案，其中合并的更新时间戳大于给定的时间戳。 支持 `greater_than` 操作数。</li><li>`fromIngestTimestamp` 表示 **事件**:在此时间戳之后摄取的所有事件都将导出与结果用户档案结果对应的事件。 这不是事件时间本身，而是事件的摄取时间。</li> |
| `filter.emptyProfiles` | 一个布尔值，指示是否过滤空配置文件。 配置文件可以包含配置文件记录和/或ExperienceEvent记录。 没有用户档案记录且只有ExperienceEvent记录的用户档案称为“emptyProfiles”。 要导出配置文件存储中的所有配置文件（包括“emptyProfiles”），请将 `emptyProfiles` to `true`. 如果 `emptyProfiles` 设置为 `false`，则只会导出存储中具有用户档案记录的用户档案。 默认情况下，如果 `emptyProfiles` 属性时，只会导出包含用户档案记录的用户档案。 |
| `additionalFields.eventList` | 通过提供以下一个或多个设置，控制为子对象或关联对象导出的时间序列事件字段：<ul><li>`fields`:控制要导出的字段。</li><li>`filter`:指定限制关联对象中包含的结果的标准。 预期导出所需的最小值，通常为日期。</li><li>`filter.fromIngestTimestamp`:将时间系列事件筛选为在提供的时间戳后摄取的事件。 这不是事件时间本身，而是事件的摄取时间。</li><li>`filter.toIngestTimestamp`:将时间戳过滤为在提供的时间戳之前摄取的时间戳。 这不是事件时间本身，而是事件的摄取时间。</li></ul> |
| `destination` | **（必需）** 有关导出数据的信息：<ul><li>`datasetId`: **（必需）** 要导出数据的数据集的ID。</li><li>`segmentPerBatch`: *（可选）* 一个布尔值，如果未提供，则默认为“false”。 值“false”会将所有区段ID导出为单个批量ID。 值“true”会将一个区段ID导出为一个批量ID。 请注意，将值设置为“true”可能会影响批量导出性能。</li></ul> |
| `schema.name` | **（必需）** 与要导出数据的数据集关联的架构的名称。 |
| `evaluationInfo.segmentation` | *（可选）* 一个布尔值，如果未提供，则默认为 `false`. 值 `true` 表示需要在导出作业中完成分段。 |

**响应**

成功响应会返回HTTP状态200，其中包含新创建的导出作业的详细信息。

```json
{
    "id": 100,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
    "status": "NEW",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "_id, _experience",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z"
            }
        }
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
        }
    },
    "computeGatewayJobId": {
        "exportJob": ""    
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 系统生成的只读值，用于标识刚刚创建的导出作业。 |

或者，如果 `destination.segmentPerBatch` 已设置为 `true`, `destination` 上面的对象将具有 `batches` 数组，如下所示：

```json
    "destination": {
        "dataSetId": "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches": [
            {
                "segmentId": "segment1",
                "segmentNs": "ups",
                "status": ["realized"],
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
            },
            {
                "segmentId": "segment2",
                "segmentNs": "AdCloud",
                "status": "exited",
                "batchId": "df4gssdfb93a09f7e37fa53ad52"
            }
        ]
    }
```

## 检索特定导出作业 {#get}

您可以通过向 `/export/jobs` 端点和提供您希望在请求路径中检索的导出作业的ID。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 的 `id` 要访问的导出作业。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关指定导出作业的详细信息。

```json
{
    "id": 11037,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
    "status": "SUCCEEDED",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status":[
                    "realized"
                ]
            }
        ]
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "profileExportTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "totalExportedProfileCounter": 20,
        "exportedProfileByNamespaceCounter": {
            "namespace1": 10,
            "namespace2": 5
        }
    },
    "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `destination` | 导出数据的目标信息：<ul><li>`datasetId`:导出数据的数据集的ID。</li><li>`segmentPerBatch`:一个布尔值，用于显示区段ID是否已合并。 值 `false` 表示所有区段ID都归为一个批处理ID。 值 `true` 表示将一个区段ID导出为一个批量ID。</li></ul> |
| `fields` | 导出字段的列表，用逗号分隔。 |
| `schema.name` | 与要导出数据的数据集关联的架构的名称。 |
| `filter.segments` | 导出的区段。 包括以下字段：<ul><li>`segmentId`:要导出的用户档案的区段ID。</li><li>`segmentNs`:给定的区段命名空间 `segmentID`.</li><li>`status`:字符串数组，为 `segmentID`. 默认情况下， `status` 将具有值 `["realized"]` 表示当前属于该区段的所有用户档案。 可能的值包括： `realized` 和 `exited`.  值 `realized` 表示用户档案符合区段的条件。 值 `exiting` 表示用户档案正在退出区段。</li></ul> |
| `mergePolicy` | 导出数据的合并策略信息。 |
| `metrics.totalTime` | 一个字段，用于指示导出作业运行所用的总时间。 |
| `metrics.profileExportTime` | 一个字段，用于指示用户档案导出所用的时间。 |
| `totalExportedProfileCounter` | 所有批次中导出的配置文件总数。 |

## 取消或删除特定导出作业 {#delete}

您可以通过向 `/export/jobs` 端点和提供您希望在请求路径中删除的导出作业的ID。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 的 `id` 要删除的导出作业。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态204，并显示以下消息：

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## 后续步骤

阅读本指南后，您现在可以更好地了解导出作业的工作方式。

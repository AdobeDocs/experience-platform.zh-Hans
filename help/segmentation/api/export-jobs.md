---
solution: Experience Platform
title: 区段导出作业API端点
description: 导出作业是异步流程，用于将受众区段成员保留到数据集。 您可以使用Adobe Experience Platform Segmentation Service API中的/export/jobs端点，它允许您以编程方式检索、创建和取消导出作业。
role: Developer
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 1%

---

# 区段导出作业端点

导出作业是异步流程，用于将受众区段成员保留到数据集。 您可以使用Adobe Experience Platform Segmentation API中的`/export/jobs`端点，它允许您以编程方式检索、创建和取消导出作业。

>[!NOTE]
>
>本指南介绍[!DNL Segmentation API]中导出作业的使用情况。 有关如何管理[!DNL Real-Time Customer Profile]数据的导出作业的信息，请参阅配置文件API[中有关](../../profile/api/export-jobs.md)导出作业的指南

## 快速入门

本指南中使用的端点是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)以了解成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

## 检索导出作业列表 {#retrieve-list}

您可以通过向`/export/jobs`端点发出GET请求来检索组织的所有导出作业的列表。

**API格式**

`/export/jobs`端点支持多个查询参数以帮助筛选结果。 虽然这些参数是可选的，但强烈建议使用这些参数以帮助减少昂贵的开销。 在不使用参数的情况下调用此端点将检索您的组织可用的所有导出作业。 可以包含多个参数，以&amp;符号(`&`)分隔。

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

**查询参数**

+++ 可用查询参数的列表。

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `limit` | 指定返回的导出作业数。 | `limit=10` |
| `offset` | 指定结果页面的偏移量。 | `offset=1540974701302_96` |
| `status` | 根据状态筛选结果。 支持的值为“NEW”、“SUCCEEDED”和“FAILED”。 | `status=NEW` |

+++

**请求**

以下请求将检索组织内的最后两个导出作业。

+++ 用于检索导出作业的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

以下响应根据请求路径中提供的查询参数，返回HTTP状态200，其中包含已成功完成的导出作业列表。

+++ 检索导出作业时的示例响应。

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
| `destination` | 导出数据的目标信息：<ul><li>`datasetId`：导出数据的数据集的ID。</li><li>`segmentPerBatch`：一个布尔值，它显示区段ID是否已合并。 值为“false”表示所有区段ID都将导出到单个批次ID中。 值为“true”表示将一个区段ID导出到一个批次ID中。 **注意：**&#x200B;将该值设置为true可能会影响批量导出性能。</li></ul> |
| `fields` | 导出的字段列表，以逗号分隔。 |
| `schema.name` | 与要导出数据的数据集关联的架构的名称。 |
| `filter.segments` | 导出的区段。 包括以下字段：<ul><li>`segmentId`：配置文件将导出到的区段ID。</li><li>`segmentNs`：给定`segmentID`的区段命名空间。</li><li>`status`：为`segmentID`提供状态筛选器的字符串数组。 默认情况下，`status`将具有值`["realized"]`，该值表示当前时间属于该区段的所有用户档案。 可能的值包括： `realized`和`exited`。 值为`realized`表示配置文件符合该区段的条件。 值为`exiting`表示配置文件正在退出区段。</li></ul> |
| `mergePolicy` | 合并导出数据的策略信息。 |
| `metrics.totalTime` | 指示导出作业运行总时间的字段。 |
| `metrics.profileExportTime` | 指示导出用户档案所用时间的字段。 |
| `page` | 有关所请求的导出作业的分页的信息。 |
| `link.next` | 指向导出作业下一页的链接。 |

+++

## 创建新的导出作业 {#create}

您可以通过向`/export/jobs`端点发出POST请求来创建新的导出作业。

**API格式**

```http
POST /export/jobs
```

**请求**

以下请求创建新的导出作业，该作业由有效负载中提供的参数配置。

+++ 创建导出作业的示例请求。

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
| `fields` | 导出的字段列表，以逗号分隔。 如果留空，将导出所有字段。 |
| `mergePolicy` | 指定用于管理导出数据的合并策略。 有多个区段要导出时包含此参数。 如果未提供，导出将采用与给定区段相同的合并策略。 |
| `filter` | 一个对象，它根据下面列出的子属性，按ID、限定时间或摄取时间指定要包含在导出作业中的区段。 如果留空，将导出所有数据。 |
| `filter.segments` | 指定要导出的区段。 忽略此值将导致导出所有用户档案中的所有数据。 接受区段对象的数组，每个对象包含以下字段：<ul><li>`segmentId`： **（如果使用`segments`）**&#x200B;区段ID导出用户档案，则此为必填字段。</li><li>`segmentNs` *（可选）*&#x200B;给定`segmentID`的区段命名空间。</li><li>`status` *（可选）*&#x200B;为`segmentID`提供状态筛选器的字符串数组。 默认情况下，`status`将具有值`["realized"]`，该值表示当前时间属于该区段的所有用户档案。 可能的值包括： `realized`和`exited`。  值为`realized`表示配置文件符合该区段的条件。 值为`exiting`表示配置文件正在退出区段。</li></ul> |
| `filter.segmentQualificationTime` | 根据区段鉴别时间进行筛选。 可以提供开始时间和/或结束时间。 |
| `filter.segmentQualificationTime.startTime` | 给定状态的区段ID的区段资格开始时间。 如果未提供，则区段ID鉴别的开始时间将不存在过滤器。 时间戳必须以[RFC 3339](https://tools.ietf.org/html/rfc3339)格式提供。 |
| `filter.segmentQualificationTime.endTime` | 给定状态的区段ID的区段资格结束时间。 如果未提供，则区段ID鉴别的结束时间将没有过滤器。 时间戳必须以[RFC 3339](https://tools.ietf.org/html/rfc3339)格式提供。 |
| `filter.fromIngestTimestamp` | 限制导出的配置文件仅包括在此时间戳之后更新的配置文件。 时间戳必须以[RFC 3339](https://tools.ietf.org/html/rfc3339)格式提供。 <ul><li>`fromIngestTimestamp`配置文件&#x200B;**的**（如果提供）：包括合并的更新时间戳大于给定时间戳的所有合并配置文件。 支持`greater_than`操作数。</li><li>`fromIngestTimestamp`个事件&#x200B;**的**：将导出在此时间戳之后摄取的所有事件，以对应于生成的配置文件结果。 这不是事件时间本身，而是事件的摄取时间。</li> |
| `filter.emptyProfiles` | 一个布尔值，指示是否筛选空配置文件。 配置文件可以包含配置文件记录、ExperienceEvent记录，或同时包含两者。 没有配置文件记录且只有ExperienceEvent记录的配置文件称为“emptyProfiles”。 要导出配置文件存储中的所有配置文件，包括“emptyProfiles”，请将`emptyProfiles`的值设置为`true`。 如果`emptyProfiles`设置为`false`，则仅导出存储中具有配置文件记录的配置文件。 默认情况下，如果不包括`emptyProfiles`属性，则只导出包含配置文件记录的配置文件。 |
| `additionalFields.eventList` | 通过提供以下一个或多个设置，控制为子对象或关联对象导出的时间序列事件字段：<ul><li>`fields`：控制要导出的字段。</li><li>`filter`：指定限制从关联对象包含结果的条件。 需要导出所需的最小值，通常为日期。</li><li>`filter.fromIngestTimestamp`：将时间序列事件筛选为提供的时间戳之后摄取的那些事件。 这不是事件时间本身，而是事件的摄取时间。</li><li>`filter.toIngestTimestamp`：将时间戳过滤为提供的时间戳之前摄取的那些时间戳。 这不是事件时间本身，而是事件的摄取时间。</li></ul> |
| `destination` | **（必需）**&#x200B;有关导出数据的信息：<ul><li>`datasetId`： **（必需）**&#x200B;要导出数据的数据集的ID。</li><li>`segmentPerBatch`： *（可选）*&#x200B;布尔值，如果未提供，则默认为“false”。 如果值为“false”，则会将所有区段ID导出到单个批次ID中。 值为“true”会将一个区段ID导出到一个批次ID中。 请注意，将该值设置为“true”可能会影响批量导出性能。</li></ul> |
| `schema.name` | **（必需）**&#x200B;与要导出数据的数据集关联的架构的名称。 |
| `evaluationInfo.segmentation` | *（可选）*&#x200B;布尔值，如果未提供，则默认为`false`。 值为`true`表示需要对导出作业进行分段。 |

+++

**响应**

成功的响应返回HTTP状态200以及新创建的导出作业的详细信息。

+++ 创建导出作业时的示例响应。

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
| `id` | 系统生成的只读值，用于标识刚创建的导出作业。 |

或者，如果将`destination.segmentPerBatch`设置为`true`，则上述`destination`对象将具有`batches`数组，如下所示：

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

+++

## 检索特定导出作业 {#get}

您可以通过向`/export/jobs`端点发出GET请求并在请求路径中提供要检索的导出作业的ID，来检索有关特定导出作业的详细信息。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 您要访问的导出作业的`id`。 |

**请求**

+++ 用于检索导出作业的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关指定导出作业的详细信息。

+++ 检索导出作业时的示例响应。

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
| `destination` | 导出数据的目标信息：<ul><li>`datasetId`：导出数据的数据集的ID。</li><li>`segmentPerBatch`：一个布尔值，它显示区段ID是否已合并。 值为`false`表示所有区段ID都位于单个批次ID中。 值为`true`表示将一个区段ID导出到一个批次ID中。</li></ul> |
| `fields` | 导出的字段列表，以逗号分隔。 |
| `schema.name` | 与要导出数据的数据集关联的架构的名称。 |
| `filter.segments` | 导出的区段。 包括以下字段：<ul><li>`segmentId`：要导出的配置文件的区段ID。</li><li>`segmentNs`：给定`segmentID`的区段命名空间。</li><li>`status`：为`segmentID`提供状态筛选器的字符串数组。 默认情况下，`status`将具有值`["realized"]`，该值表示当前时间属于该区段的所有用户档案。 可能的值包括： `realized`和`exited`。  值为`realized`表示配置文件符合该区段的条件。 值为`exiting`表示配置文件正在退出区段。</li></ul> |
| `mergePolicy` | 合并导出数据的策略信息。 |
| `metrics.totalTime` | 指示导出作业运行总时间的字段。 |
| `metrics.profileExportTime` | 指示导出用户档案所用时间的字段。 |
| `totalExportedProfileCounter` | 跨所有批次导出的配置文件总数。 |

+++

## 取消或删除特定导出作业 {#delete}

您可以通过向`/export/jobs`端点发出DELETE请求并在请求路径中提供要删除的导出作业的ID来请求删除指定的导出作业。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 要删除的导出作业的`id`。 |

**请求**

+++ 删除导出作业的示例请求。

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态204，并显示以下消息：

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## 后续步骤

阅读本指南后，您现在可以更好地了解导出作业的工作方式。

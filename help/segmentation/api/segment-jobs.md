---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；分段作业；分段作业；段作业；API;api;
solution: Experience Platform
title: 区段作业API端点
topic-legacy: developer guide
description: Adobe Experience Platform Segmentation Service API中的区段作业端点允许您以编程方式管理组织的区段作业。
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 2%

---

# 段作业端点

段作业是创建新受众段的异步进程。 它引用[区段定义](./segment-definitions.md)以及任何[合并策略](../../profile/api/merge-policies.md)，控制[!DNL Real-time Customer Profile]如何合并您用户档案片段中的重叠属性。 当区段作业成功完成时，您可以收集有关区段的各种信息，例如在处理过程中可能发生的任何错误以及受众的最终大小。

本指南提供相关信息，帮助您更好地了解细分作业，并包含使用API执行基本操作的示例API调用。

## 入门指南

本指南中使用的端点是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)以了解成功调用API所需的重要信息，包括必需的标头以及如何读取示例API调用。

## 检索区段作业{#retrieve-list}的列表

您可以通过向`/segment/jobs`端点发出列表请求，为IMS组织检索所有区段作业的GET。

**API格式**

`/segment/jobs`端点支持多个查询参数，以帮助筛选结果。 尽管这些参数是可选的，但强烈建议使用这些参数以帮助降低昂贵的开销。 调用不带参数的此端点将检索组织可用的所有导出作业。 可以包含多个参数，用&amp;符号(`&`)分隔。

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**查询参数**

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `start` | 指定返回的段作业的起始偏移。 | `start=1` |
| `limit` | 指定每页返回的区段作业数。 | `limit=20` |
| `status` | 过滤器基于状态的结果。 支持的值为NEW、QUEUED、PROCESSING、SUCCEEDED、FAILED、CANCELLED、CANCELLED | `status=NEW` |
| `sort` | 订购已退回的区段作业。 以`[attributeName]:[desc|asc]`格式写入。 | `sort=creationTime:desc` |
| `property` | 过滤器对作业进行细分，并获取给定过滤器的精确匹配。 它可以采用以下任一格式编写： <ul><li>`[jsonObjectPath]==[value]`  — 对对象键进行筛选</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]`  — 在数组内过滤</li></ul> | `property=segments~segmentId==workInUS` |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，并将指定IMS组织的区段作业列表为JSON。 以下响应返回IMS组织所有成功的区段作业的列表。

>[!NOTE]
>
>以下响应已被截断为空格，并将仅显示第一个返回的作业。

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                        "mergePolicy": {
                            "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                            "version": 1
                        }
                    }
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles":13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "existing":10,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 区段作业的系统生成的只读标识符。 |
| `status` | 区段作业的当前状态。 状态的潜在值包括“NEW”、“PROCESSING”、“CANCELLING”、“CANCELLED”、“FAILED”和“SUCCEEDED”。 |
| `segments` | 一个对象，其中包含有关在区段作业中返回的区段定义的信息。 |
| `segments.segment.id` | 区段定义的ID。 |
| `segments.segment.expression` | 一个对象，其中包含有关段定义表达式的信息，以PQL编写。 |
| `metrics` | 包含有关区段作业的诊断信息的对象。 |
| `metrics.totalTime` | 包含分段作业开始和结束的时间以及所花费的总时间信息的对象。 |
| `metrics.profileSegmentationTime` | 包含分段评估开始和结束的时间以及所花费的总时间的信息的对象。 |
| `metrics.segmentProfileCounter` | 每个细分的合格用户档案数。 |
| `metrics.segmentedProfileByNamespaceCounter` | 每个区段的每个身份命名空间的合格用户档案数。 |
| `metrics.segmentProfileByStatusCounter` | 每个状态的用户档案计数。 支持以下三种状态： <ul><li>“已实现” — 进入区段的新用户档案数。</li><li>“existing” — 区段中继续存在的用户档案数。</li><li>“退出” — 区段中不再存在的用户档案区段数。</li></ul> |
| `metrics.totalProfilesByMergePolicy` | 每个合并策略基础上的合并用户档案总数。 |

## 创建新区段作业{#create}

您可以通过向`/segment/jobs`端点发出POST请求并在主体中包含要从中创建新受众的区段定义的ID来创建新区段作业。

**API格式**

```http
POST /segment/jobs
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
[
  {
    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
  }
]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `segmentId` | 要为其创建区段作业的区段定义的ID。 这些区段定义可以属于不同的合并策略。 有关区段定义的详细信息，请参阅[区段定义端点指南](./segment-definitions.md)。 |

**响应**

成功的响应会返回HTTP状态200，其中包含您新创建的区段作业的详细信息。

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "NEW",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304260000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304260
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 系统为新创建的区段作业生成的只读标识符。 |
| `status` | 区段作业的当前状态。 由于区段作业是新创建的，因此状态将始终为“NEW”。 |
| `segments` | 一个对象，其中包含有关此区段作业正在运行的区段定义的信息。 |
| `segments.segment.id` | 您提供的区段定义的ID。 |
| `segments.segment.expression` | 一个对象，其中包含有关段定义表达式的信息，以PQL编写。 |

## 检索特定区段作业{#get}

您可以通过向`/segment/jobs`端点发出GET请求并提供您希望在请求路径中检索的区段作业的ID来检索有关特定区段作业的详细信息。

**API格式**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| 属性 | 描述 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 要检索的区段作业的`id`值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关指定区段作业的详细信息。

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "651fc109-3963-48d2-aa98-9e3cc2003bac",
    "computeJobId": 39312,
    "computeGatewayJobId": "a0099ab6-11ab-4c2b-a0ea-6162e16806bd",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 区段作业的系统生成的只读标识符。 |
| `status` | 区段作业的当前状态。 状态的潜在值包括“NEW”、“PROCESSING”、“CANCELLING”、“CANCELLED”、“FAILED”和“SUCCEEDED”。 |
| `segments` | 一个对象，其中包含有关在区段作业中返回的区段定义的信息。 |
| `segments.segment.id` | 区段定义的ID。 |
| `segments.segment.expression` | 一个对象，其中包含有关段定义表达式的信息，以PQL编写。 |
| `metrics` | 包含有关区段作业的诊断信息的对象。 |

## 批量检索区段作业{#bulk-get}

您可以通过向`/segment/jobs/bulk-get`端点发出POST请求并在请求主体中提供段作业的`id`值，检索有关多个段作业的详细信息。

**API格式**

```http
POST /segment/jobs/bulk-get
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "cc3419d3-0389-47f1-b174-fead6b3c830d"
            },
            {
                "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8"
            }
        ]
    }'
```

**响应**

成功的响应会返回请求的区段作业的HTTP状态207。

>[!NOTE]
>
>以下响应已被截断，仅显示每个区段作业的部分详细信息。 完整响应将列表所请求区段作业的完整详细信息。

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        },
        "c527dc3f-07fe-4b96-be4e-23f38e734ff8": {
            "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                    "segment": {
                        "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 区段作业的系统生成的只读标识符。 |
| `status` | 区段作业的当前状态。 状态的潜在值包括“NEW”、“PROCESSING”、“CANCELLING”、“CANCELLED”、“FAILED”和“SUCCEEDED”。 |
| `segments` | 一个对象，其中包含有关在区段作业中返回的区段定义的信息。 |
| `segments.segment.id` | 区段定义的ID。 |
| `segments.segment.expression` | 一个对象，其中包含有关段定义表达式的信息，以PQL编写。 |

## 取消或删除特定区段作业{#delete}

您可以通过向`/segment/jobs`端点发出DELETE请求并在请求路径中提供要删除的区段作业的ID来删除特定区段作业。

>[!NOTE]
>
>对删除请求的API响应是即时的。 但是，实际删除区段作业是异步的。 换句话说，对区段作业发出删除请求和应用删除请求之间存在时间差。

**API格式**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| 属性 | 描述 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 要删除的区段作业的`id`值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回包含以下信息的HTTP状态204。

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## 后续步骤

阅读本指南后，您现在可以更好地了解细分作业的工作方式。

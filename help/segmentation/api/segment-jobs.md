---
solution: Experience Platform
title: 区段作业API端点
description: Adobe Experience Platform Segmentation Service API中的区段作业端点允许您以编程方式管理组织的区段作业。
role: Developer
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
source-git-commit: 83a249daddbee1ec264b6e505517325c76ac9b09
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 2%

---

# 区段作业端点

区段作业是一个异步过程，可按需创建受众区段。 它引用了[区段定义](./segment-definitions.md)以及任何[合并策略](../../profile/api/merge-policies.md)，这些策略控制[!DNL Real-Time Customer Profile]如何在您的配置文件片段中合并重叠属性。 成功完成区段作业后，您可以收集有关该区段的各种信息，例如处理期间可能发生的任何错误以及最终的受众规模。

本指南提供的信息可帮助您更好地了解区段作业，包括用于使用API执行基本操作的示例API调用。

## 快速入门

本指南中使用的端点是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)以了解成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

## 检索区段作业列表 {#retrieve-list}

您可以通过向`/segment/jobs`端点发出GET请求来检索组织的所有区段作业的列表。

**API格式**

`/segment/jobs`端点支持多个查询参数以帮助筛选结果。 虽然这些参数是可选的，但强烈建议使用这些参数以帮助减少昂贵的开销。 在不使用参数的情况下调用此端点将检索您的组织可用的所有导出作业。 可以包含多个参数，以&amp;符号(`&`)分隔。

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**查询参数**

+++ 可用查询参数的列表。

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `start` | 为返回的区段作业指定起始偏移。 | `start=1` |
| `limit` | 指定每页返回的区段作业数。 | `limit=20` |
| `status` | 根据状态筛选结果。 支持的值为NEW、QUEUED、PROCESSING、SUCCEEDED、FAILED、CANCELING、CANCELED | `status=NEW` |
| `sort` | 区段作业返回的订单。 | 以`[attributeName]:[desc\|asc]`格式编写。`sort=creationTime:desc` |
| `property` | 过滤区段作业，并获取给定过滤器的精确匹配项。 可采用以下任一格式编写： <ul><li>`[jsonObjectPath]==[value]` — 在对象键上筛选</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` — 在数组中筛选</li></ul> | `property=segments~segmentId==workInUS` |

+++

**请求**

+++ 查看区段作业列表的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200，并将指定组织的区段作业列表作为JSON。 所有区段定义的完整列表将显示在`children.segments`属性中。

>[!NOTE]
>
>以下响应已截断空格，将仅显示返回的第一个作业。

+++ 检索区段作业列表时的示例响应。 

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
| `status` | 区段作业的当前状态。 状态的潜在值包括“NEW”、“PROCESSING”、“CANCELING”、“CANCELLED”、“FAILED”和“SUCCEEDED”。 |
| `segments` | 一个对象，其中包含有关区段作业中返回的区段定义的信息。 |
| `segments.segment.id` | 区段定义的ID。 |
| `segments.segment.expression` | 一个对象，其中包含有关在PQL中编写的区段定义表达式的信息。 |
| `metrics` | 包含有关区段作业的诊断信息的对象。 |
| `metrics.totalTime` | 一个对象，其中包含有关分段作业开始和结束的时间以及所用总时间的信息。 |
| `metrics.profileSegmentationTime` | 一个对象，其中包含有关分段评估开始和结束的时间以及所用总时间的信息。 |
| `metrics.segmentProfileCounter` | 每个区段符合条件的配置文件数。 |
| `metrics.segmentedProfileByNamespaceCounter` | 每个区段定义中每个身份命名空间限定的配置文件数。 |
| `metrics.segmentProfileByStatusCounter` | 每个状态的配置文件数。 支持以下三种状态： <ul><li>“已实现” — 符合区段定义资格的用户档案数。</li><li>“已退出” — 区段定义中不再存在的配置文件数。</li></ul> |
| `metrics.totalProfilesByMergePolicy` | 基于每个合并策略的合并配置文件总数。 |

+++

## 创建新的区段作业 {#create}

您可以通过向`/segment/jobs`端点发出POST请求并在请求正文中包含区段定义的ID来创建新的区段作业。

**API格式**

```http
POST /segment/jobs
```

**请求**

+++用于创建新区段作业的示例请求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    },
    {
        "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85"
    }
 ]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `segmentId` | 要评估的区段定义的ID。 这些区段定义可以属于不同的合并策略。 有关区段定义的详细信息，请参阅[区段定义终结点指南](./segment-definitions.md)。 |

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关新创建的区段作业的信息。

+++ 创建新区段作业时的示例响应。

```json
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
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
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
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
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
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 系统为新创建的区段作业生成的只读标识符。 |
| `status` | 区段作业的当前状态。 由于区段作业是新创建的，因此状态将始终为“NEW”。 |
| `segments` | 一个对象，其中包含有关运行此区段作业的区段定义的信息。 |
| `segments.segment.id` | 您提供的区段定义的ID。 |
| `segments.segment.expression` | 一个对象，其中包含有关在PQL中编写的区段定义表达式的信息。 |

+++

## 检索特定区段作业 {#get}

您可以通过向`/segment/jobs`端点发出GET请求并在请求路径中提供要检索的区段作业的ID，来检索有关特定区段作业的详细信息。

**API格式**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| 属性 | 描述 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 要检索的区段作业的`id`值。 |

**请求**

+++ 用于检索区段作业的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关指定区段作业的详细信息。 所有区段定义的完整列表将显示在`children.segments`属性中。

+++ 用于检索区段作业的示例响应。

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{ORG_ID}",
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
| `status` | 区段作业的当前状态。 状态的潜在值包括“NEW”、“PROCESSING”、“CANCELING”、“CANCELLED”、“FAILED”和“SUCCEEDED”。 |
| `segments` | 一个对象，其中包含有关区段作业中返回的区段定义的信息。 |
| `segments.segment.id` | 区段定义的ID。 |
| `segments.segment.expression` | 一个对象，其中包含有关在PQL中编写的区段定义表达式的信息。 |
| `metrics` | 包含有关区段作业的诊断信息的对象。 |

+++

>[!ENDTABS]

## 批量检索区段作业 {#bulk-get}

通过向`/segment/jobs/bulk-get`端点发出POST请求并在请求正文中提供区段作业的`id`值，可以检索有关多个区段作业的详细信息。

**API格式**

```http
POST /segment/jobs/bulk-get
```

**请求**

+++ 使用批量检索端点的示例请求。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

+++

**响应**

成功的响应会返回包含所请求区段作业的HTTP状态207。

>[!NOTE]
>
>以下响应已因空间而被截断，仅显示每个区段作业的部分详细信息。 完整响应将列出所请求区段作业的完整详细信息。

+++ 使用批量获取响应时的示例响应。

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-d78c-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-d78c-48ad-8012-c5563a007069",
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
| `status` | 区段作业的当前状态。 状态的潜在值包括“NEW”、“PROCESSING”、“CANCELING”、“CANCELLED”、“FAILED”和“SUCCEEDED”。 |
| `segments` | 一个对象，其中包含有关区段作业中返回的区段定义的信息。 |
| `segments.segment.id` | 区段定义的ID。 |
| `segments.segment.expression` | 一个对象，其中包含有关在PQL中编写的区段定义表达式的信息。 |

+++

## 取消或删除特定区段作业 {#delete}

您可以通过向`/segment/jobs`端点发出DELETE请求并在请求路径中提供要删除的区段作业的ID来删除特定区段作业。

>[!NOTE]
>
>API会立即响应删除请求。 但是，实际删除区段作业是异步执行的。 换句话说，对区段作业发出删除请求的时间与应用该请求的时间之间存在时间差。

**API格式**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| 属性 | 描述 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 要删除的区段作业的`id`值。 |

**请求**

+++ 删除区段作业的示例请求。

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回带有空响应正文的HTTP状态204。

## 后续步骤

阅读本指南后，您现在可以更好地了解区段作业的工作方式。

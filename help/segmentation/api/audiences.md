---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；受众；API;API;
title: 受众API端点
description: Adobe Experience Platform Segmentation Service API中的受众端点允许您以编程方式管理贵组织的受众。
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
hide: true
hidefromtoc: true
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 4%

---

# 受众端点

>[!IMPORTANT]
>
>受众端点当前为测试版，并非所有用户都可用。 文档和功能可能会发生变化。

受众是具有相似行为和/或特征的人员的集合。 这些人员集合可通过使用Adobe Experience Platform或从外部源生成。 您可以使用 `/audiences` 分段API中的端点，它允许您以编程方式检索、创建、更新和删除受众。

## 快速入门

本指南中使用的端点是 [!DNL Adobe Experience Platform Segmentation Service] API。 在继续之前，请查看 [入门指南](./getting-started.md) 有关成功调用API所需的重要信息，包括所需的标头以及如何读取示例API调用。

## 检索受众列表 {#list}

您可以通过向 `/audiences` 端点。

**API格式**

的 `/audiences` 端点支持多个查询参数来帮助筛选结果。 虽然这些参数是可选的，但强烈建议使用这些参数，以帮助在列出资源时减少昂贵的开销。 如果您对此端点进行无参数调用，则将检索您组织的所有可用受众。 可以包含多个参数，这些参数之间用与号(`&`)。

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

在检索受众列表时，可以使用以下查询参数：

| 查询参数 | 描述 | 示例 |
| --------------- | ----------- | ------- |
| `start` | 指定返回的受众的起始偏移。 | `start=5` |
| `limit` | 指定每页返回的最大受众数。 | `limit=10` |
| `sort` | 指定对结果进行排序的顺序。 该文件采用格式编写 `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | 用于指定受众的过滤器 **完全** 匹配属性的值。 该文件采用格式编写 `property=` | `property=audienceId==test-audience-id` |
| `name` | 一种过滤器，用于指定名称为 **contain** 提供的值。 此值不区分大小写。 | `name=Sample` |
| `description` | 过滤器允许您指定其描述的受众 **contain** 提供的值。 此值不区分大小写。 | `description=Test Description` |
| `withMetrics` | 除受众之外，还可返回量度的过滤器。 | `property=withMetrics==true` |

>[!IMPORTANT]
>
>对于受众，量度会在 `metrics` 属性，并包含有关配置文件计数、创建和更新时间戳的信息。

**无量度**

在 `withMetrics` 查询参数不存在。

**请求**

以下请求会检索在您的组织中创建的最后五个受众。

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=5 \
 -H 'Authorization:  Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id:  {IMS_ORG}' \
 -H 'x-api-key:  {API_KEY}' \
 -H 'x-sandbox-name:  {SANDBOX_NAME}'
```

**响应** {#no-metrics}

成功响应会返回HTTP状态200，其中包含在您的组织中以JSON形式创建的受众列表。

>[!NOTE]
>
>以下响应已因空间而被截断，仅显示返回的第一个受众。

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
    ]
}
```

| 属性 | 受众类型 | 描述 |
| -------- | ------------- | ----------- | 
| `id` | 两者兼有 | 系统生成的受众只读标识符。 |
| `audienceId` | 两者兼有 | 如果受众是平台生成的受众，则该值与 `id`. 如果受众是外部生成的，则此值由客户提供。 |
| `schema` | 两者兼有 | 受众的体验数据模型(XDM)架构。 |
| `imsOrgId` | 两者兼有 | 受众所属的组织的ID。 |
| `sandbox` | 两者兼有 | 有关受众所属的沙盒的信息。 有关沙箱的更多信息，请参阅 [沙箱概述](../../sandboxes/home.md). |
| `name` | 两者兼有 | 受众的名称。 |
| `description` | 两者兼有 | 受众的描述。 |
| `expression` | 平台生成 | 受众的配置文件查询语言(PQL)表达式。 有关PQL表达式的更多信息，请参阅 [PQL表达式指南](../pql/overview.md). |
| `mergePolicyId` | 平台生成 | 与受众关联的合并策略的ID。 有关合并策略的更多信息，请参阅 [合并策略指南](../../profile/api/merge-policies.md). |
| `evaluationInfo` | 平台生成 | 显示如何评估受众。 可能的评估方法包括批量、流或边缘。 有关评估方法的更多信息，请参阅 [分段概述](../home.md) |
| `dependents` | 两者兼有 | 依赖于当前受众的受众ID数组。 如果您创建的受众是区段的区段，则会使用此功能。 |
| `dependencies` | 两者兼有 | 受众所依赖的受众ID数组。 如果您创建的受众是区段的区段，则会使用此功能。 |
| `type` | 两者兼有 | 系统生成的字段，用于显示受众是平台生成的还是外部生成的受众。 可能的值包括 `SegmentDefinition` 和 `ExternalAudience`. A `SegmentDefinition` 是指在Platform中生成的受众，而 `ExternalAudience` 是指未在Platform中生成的受众。 |
| `createdBy` | 两者兼有 | 创建受众的用户ID。 |
| `labels` | 两者兼有 | 与受众相关的对象级别数据使用情况和基于属性的访问控制标签。 |
| `namespace` | 两者兼有 | 受众所属的命名空间。 可能的值包括 `AAM`, `AAMSegments`, `AAMTraits`和 `AEPSegments`. |
| `audienceMeta` | 外部 | 来自外部创建受众的外部创建元数据。 |

**包含量度**

在 `withMetrics` 查询参数存在。

**请求**

以下请求会检索在您的组织中创建的最近五个受众（包含量度）。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?propoerty=withMetrics==true&limit=5&sort=totalProfiles:desc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含指定组织的受众列表（包含量度），并将其返回为JSON。

>[!NOTE]
>
>以下响应已因空间而被截断，仅显示返回的第一个受众。

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "metrics": {
                "type": "export",
                "jobId": "test-job-id",
                "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
                "data": {
                    "totalProfiles": 11200769,
                    "totalProfilesByNamespace": {
                        "crmid": 11400769
                    },
                    "totalProfilesByStatus": {
                        "existing": 11400769
                    }
                },
                "createEpoch": 1653583927,
                "updateEpoch": 1653583927
            },
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
   ],
   "_page": {
      "totalCount": 111,
      "pageSize": 5,
      "next": "1"
   },
   "_links": {
      "next": {
         "href": "@/audiences?start=1&limit=5&totalCount=111"
      }
   }
}
```

下面列出了属性 **排他** 到 `withMetrics` 响应。 如果您想了解标准受众属性，请阅读 [上一部分](#no-metrics).

| 属性 | 描述 |
| -------- | ----------- |
| `metrics.imsOrgId` | 受众的组织ID。 |
| `metrics.sandbox` | 与受众相关的沙盒信息。 |
| `metrics.jobId` | 处理受众的区段作业的ID。 |
| `metrics.type` | 区段作业类型。 这可以是 `export` 或 `batch_segmentation`. |
| `metrics.id` | 受众的ID。 |
| `metrics.data` | 与受众相关的量度。 这包括以下信息：受众中包含的用户档案总数、基于每个命名空间的用户档案总数以及基于每个状态的用户档案总数。 |
| `metrics.createEpoch` | 显示受众创建时间的时间戳。 |
| `metrics.updateEpoch` | 显示受众上次更新时间的时间戳。 |

## 创建新受众 {#create}

您可以通过向 `/audiences` 端点。

**API格式**

```http
POST /audiences
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ]
    }'
```

| 属性 | 描述 |
| -------- | ----------- | 
| `name` | 受众的名称。 |
| `description` | 受众的描述。 |
| `type` | 一个字段，用于显示受众是平台生成的受众，还是外部生成的受众。 可能的值包括 `SegmentDefinition` 和 `ExternalAudience`. A `SegmentDefinition` 是指在Platform中生成的受众，而 `ExternalAudience` 是指未在Platform中生成的受众。 |
| `expression` | 受众的配置文件查询语言(PQL)表达式。 有关PQL表达式的更多信息，请参阅 [PQL表达式指南](../pql/overview.md). |
| `schema` | 受众的体验数据模型(XDM)架构。 |
| `labels` | 与受众相关的对象级别数据使用情况和基于属性的访问控制标签。 |

**响应**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## 查找指定的受众 {#get}

您可以通过向发出GET请求，查找有关特定受众的详细信息 `/audiences` 端点和提供您希望在请求路径中检索的受众的ID。

**API格式**

```http
GET /audiences/{AUDIENCE_ID}
GET /audiences/{AUDIENCE_ID}?property=withmetrics==true
```

| 参数 | 描述 |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | 您尝试检索的受众的ID。 |
| `property=withmetrics==true` | 一个可选查询参数，如果要使用受众量度检索指定的受众，可使用该参数。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关指定受众的信息。 响应将因受众是使用Adobe Experience Platform还是外部源生成而异。

**平台生成**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

**外部生成**

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "externalSegment1",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## 更新受众中的字段 {#update-field}

您可以通过向 `/audiences` 端点和提供您希望在请求路径中更新的受众的ID。

**API格式**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 要更新的受众的ID。 |

**请求**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `op` | 要更新受众，此值始终为 `add`. |
| `path` | 要更新的字段的路径。 |
| `value` | 要将字段更新为的值。 |

**响应**

成功响应会返回HTTP状态200，其中包含有关新更新受众的信息。

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## 更新受众 {#put}

您可以通过向 `/audiences` 端点和提供您希望在请求路径中更新的受众的ID。

**API格式**

```http
PUT /audiences/{AUDIENCE_ID}
```

**请求**

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId":"test-external-audience-id",
    "name":"new externalSegment",
    "namespace":"aam",
    "description":"Last 30 days",
    "type":"ExternalSegment",
    "lifecycle":"published",
    "datasetId":"6254cf3c97f8e31b639fb14d",
    "labels":[
        "core/C1"
    ]
}' 
```

| 属性 | 描述 |
| -------- | ----------- | 
| `audienceId` | 受众的ID。 外部受众使用此功能 |
| `name` | 受众的名称。 |
| `namespace` |  |
| `description` | 受众的描述。 |
| `type` | 系统生成的字段，用于显示受众是平台生成的还是外部生成的受众。 可能的值包括 `SegmentDefinition` 和 `ExternalAudience`. A `SegmentDefinition` 是指在Platform中生成的受众，而 `ExternalAudience` 是指未在Platform中生成的受众。 |
| `lifecycle` | 受众的状态。 可能的值包括 `draft`, `published`, `inactive`和 `archived`. `draft` 表示创建受众的时间， `published` 发布受众时， `inactive` 当受众不再处于活动状态时，以及 `archived` 受众。 |
| `datasetId` | 可找到受众数据的数据集的ID。 |
| `labels` | 与受众相关的对象级别数据使用情况和基于属性的访问控制标签。 |

**响应**

成功响应会返回HTTP状态200，其中包含您新更新的受众的详细信息。 请注意，受众的详细信息将因平台生成的受众或外部生成的受众而异。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "new externalSegment",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## 删除受众 {#delete}

您可以通过向 `/audiences` 端点和提供您希望在请求路径中删除的受众的ID。

**API格式**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 要删除的受众的ID。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态204，且没有消息。

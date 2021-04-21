---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；分段定义；段定义；api;API;
solution: Experience Platform
title: 区段定义API端点
topic-legacy: developer guide
description: Adobe Experience Platform Segmentation Service API中的区段定义端点允许您以编程方式管理组织的区段定义。
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 3%

---

# 段定义端点

Adobe Experience Platform允许您创建区段，这些区段从一组用户档案中定义一组特定属性或行为。 段定义是封装写入[!DNL Profile Query Language](PQL)中的查询的对象。 此对象也称为PQL谓词。 PQL谓词根据与提供给[!DNL Real-time Customer Profile]的任何记录或时间序列数据相关的条件定义区段规则。 有关编写PQL查询的详细信息，请参阅[ PQL指南](../pql/overview.md)。

本指南提供相关信息，帮助您更好地了解细分定义，并包含使用API执行基本操作的示例API调用。

## 入门指南

本指南中使用的端点是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)以了解成功调用API所需的重要信息，包括必需的标头以及如何读取示例API调用。

## 检索区段定义{#list}的列表

您可以通过向`/segment/definitions`端点发出列表请求，检索IMS组织的所有区段定义的GET。

**API格式**

`/segment/definitions`端点支持多个查询参数，以帮助筛选结果。 尽管这些参数是可选的，但强烈建议使用这些参数以帮助降低昂贵的开销。 调用此端点时不含参数将检索组织可用的所有区段定义。 可以包含多个参数，用&amp;符号(`&`)分隔。

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**查询参数**

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `start` | 为返回的段定义指定起始偏移。 | `start=4` |
| `limit` | 指定每页返回的区段定义数。 | `limit=20` |
| `page` | 指定段定义结果将从哪个页开始。 | `page=5` |
| `sort` | 指定将结果排序依据的字段。 以下格式编写：`[attributeName]:[desc|asc]`。 | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | 指定段定义是否启用流。 | `evaluationInfo.continuous.enabled=true` |

**请求**

以下请求将检索发布在您的IMS组织内的最后两个区段定义。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，并列表指定IMS组织的段定义为JSON。

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1573253640000,
            "baselineTime": 1574327114,
            "updateEpoch": 1575588309,
            "updateTime": 1575588309000
        },
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG}",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1561073779000,
            "baselineTime": 1574327114,
            "updateEpoch": 1574327114,
            "updateTime": 1574327114000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## 创建新的区段定义{#create}

可以通过向`/segment/definitions`端点发出POST请求来创建新的段定义。

**API格式**

```http
POST /segment/definitions
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | **必需。** 引用区段的唯一名称。 |
| `schema` | **必需。** 与区段中的实体关联的模式。由`id`或`name`字段组成。 |
| `expression` | **必需。** 包含有关区段定义的字段信息的实体。 |
| `expression.type` | 指定表达式类型。 目前，仅支持“PQL”。 |
| `expression.format` | 以值表示表达式的结构。 目前，支持以下格式： <ul><li>`pql/text`:根据已发布的PQL语法的段定义的文本表示。例如：`workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合`expression.format`中指示的类型的表达式。 |
| `description` | 定义的用户可读描述。 |

>[!NOTE]
>
>段定义表达式也可以引用计算的属性。 要了解更多信息，请参阅[计算属性API端点指南](../../profile/computed-attributes/ca-api.md)
>
>计算的属性功能位于alpha中，并且不适用于所有用户。 文档和功能可能会更改。

**响应**

成功的响应会返回HTTP状态200，其中包含您新创建的区段定义的详细信息。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 您新创建的区段定义的系统生成的ID。 |
| `evaluationInfo` | 系统生成的对象，用于告知区段定义将进行的评估类型。 它可以是批量、连续（也称为流）或同步分段。 |

## 检索特定的段定义{#get}

您可以通过向`/segment/definitions`端点发出GET请求并提供您希望在请求路径中检索的区段定义的ID，来检索有关特定区段定义的详细信息。

**API格式**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 要检索的区段定义的`id`值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关指定区段定义的详细信息。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 区段定义的系统生成的只读ID。 |
| `name` | 引用区段的唯一名称。 |
| `schema` | 与区段中的实体关联的模式。 由`id`或`name`字段组成。 |
| `expression` | 包含有关区段定义的字段信息的实体。 |
| `expression.type` | 指定表达式类型。 目前，仅支持“PQL”。 |
| `expression.format` | 以值表示表达式的结构。 目前，支持以下格式： <ul><li>`pql/text`:根据已发布的PQL语法的段定义的文本表示。例如：`workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合`expression.format`中指示的类型的表达式。 |
| `description` | 定义的可读描述。 |
| `evaluationInfo` | 系统生成的对象，它告诉将要进行的评估、批处理、连续（也称为流）或同步的区段定义。 |

## 批量检索段定义{#bulk-get}

您可以通过向`/segment/definitions/bulk-get`端点发出POST请求并在请求主体中提供段定义的`id`值，检索有关多个指定段定义的详细信息。

**API格式**

```http
POST /segment/definitions/bulk-get
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "54669488-03ab-4e0d-a694-37fe49e32be8"
            },
            {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05"
            }
        ]
    }'
```

**响应**

成功的响应会返回HTTP状态207，并返回请求的区段定义。

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        },
        "4afe34ae-8c98-4513-8a1d-67ccaa54bc05": {
            "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        }

    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 区段定义的系统生成的只读ID。 |
| `name` | 引用区段的唯一名称。 |
| `schema` | 与区段中的实体关联的模式。 由`id`或`name`字段组成。 |
| `expression` | 包含有关区段定义的字段信息的实体。 |
| `expression.type` | 指定表达式类型。 目前，仅支持“PQL”。 |
| `expression.format` | 以值表示表达式的结构。 目前，支持以下格式： <ul><li>`pql/text`:根据已发布的PQL语法的段定义的文本表示。例如：`workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合`expression.format`中指示的类型的表达式。 |
| `description` | 定义的可读描述。 |
| `evaluationInfo` | 系统生成的对象，它告诉将要进行的评估、批处理、连续（也称为流）或同步的区段定义。 |

## 删除特定区段定义{#delete}

您可以请求删除特定区段定义，方法是向`/segment/definitions`端点发出DELETE请求，并提供您希望在请求路径中删除的区段定义的ID。

**API格式**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 要删除的区段定义的`id`值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，无消息。

## 更新特定区段定义

您可以通过向`/segment/definitions`端点发出PATCH请求并提供您希望在请求路径中更新的区段定义的ID来更新特定的区段定义。

**API格式**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 要更新的区段定义的`id`值。 |

**请求**

以下请求将将工作地址国家/地区从美国更新至加拿大。

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "name": "Updated people who ordered in the last 30 days",
    "profileInstanceId": "ups",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

**响应**

成功的响应会返回HTTP状态200，其中包含您最近更新的区段定义的详细信息。 请注意，工作地址国家/地区已如何从美国（美国）更新至加拿大(CA)。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "Updated people who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579295340,
    "updateTime": 1579295340000
}
```

## 转换区段定义

可以通过向`/segment/conversion`端点发出POST请求，将`pql/text`和`pql/json`或`pql/json`之间的段定义转换为`pql/text`。

**API格式**

```http
POST /segment/conversion
```

**请求**

以下请求会将区段定义的格式从`pql/text`更改为`pql/json`。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

**响应**

成功的响应会返回HTTP状态200，其中包含您新转换的区段定义的详细信息。

```json
{
    "ttlInDays": 60,
    "imsOrgId": "6A29340459CA8D350A49413A@AdobeOrg",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## 后续步骤

阅读本指南后，您现在可以更好地了解细分定义的工作方式。 有关创建区段的详细信息，请阅读[创建区段](../tutorials/create-a-segment.md)教程。

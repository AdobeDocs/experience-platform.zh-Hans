---
solution: Experience Platform
title: 区段定义API端点
description: Adobe Experience Platform分段服务API中的区段定义端点允许您以编程方式管理组织的区段定义。
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 3%

---

# 区段定义端点

Adobe Experience Platform允许您根据一组配置文件创建区段定义，以定义一组特定属性或行为。 区段定义是一个对象，它封装了写入的查询 [!DNL Profile Query Language] (PQL)。 区段定义应用于用户档案以创建受众。 此对象（区段定义）也称为PQL谓词。 PQL谓词根据与您提供到的任何记录或时间序列数据相关的条件定义区段定义的规则 [!DNL Real-Time Customer Profile]. 请参阅 [PQL指南](../pql/overview.md) 有关编写PQL查询的更多信息。

本指南提供的信息可帮助您更好地了解区段定义，包括用于使用API执行基本操作的示例API调用。

## 快速入门

本指南中使用的端点是 [!DNL Adobe Experience Platform Segmentation Service] API。 在继续之前，请查看 [快速入门指南](./getting-started.md) 有关成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

## 检索区段定义列表 {#list}

您可以通过对以下网站发出GET请求，检索贵组织所有区段定义的列表： `/segment/definitions` 端点。

**API格式**

此 `/segment/definitions` 端点支持多个查询参数以帮助筛选结果。 虽然这些参数是可选的，但强烈建议使用这些参数以帮助减少昂贵的开销。 在不使用参数的情况下对此端点进行调用将检索可用于您的组织的所有区段定义。 可以包含多个参数，以&amp;符号(`&`)。

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**查询参数**

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `start` | 为返回的区段定义指定起始偏移。 | `start=4` |
| `limit` | 指定每页返回的区段定义数。 | `limit=20` |
| `page` | 指定区段定义结果将从哪个页面开始。 | `page=5` |
| `sort` | 指定排序结果所依据的字段。 按以下格式编写： `[attributeName]:[desc|asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | 指定区段定义是否启用流式处理。 | `evaluationInfo.continuous.enabled=true` |

**请求**

以下请求将检索组织中发布的最后两个区段定义。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含以JSON格式表示的指定组织的区段定义列表。

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

## 创建新的区段定义 {#create}

您可以通过向以下对象发出POST请求来创建新的区段定义： `/segment/definitions` 端点。

**API格式**

```http
POST /segment/definitions
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 用于引用区段定义的唯一名称。 |
| `description` | (可选.) 正在创建的区段定义的描述。 |
| `evaluationInfo` | (可选.) 正在创建的区段定义的类型。 如果要创建批处理客户细分，请设置 `evaluationInfo.batch.enabled` 是真的。 如果要创建流区段，请设置 `evaluationInfo.continuous.enabled` 是真的。 如果要创建边段，请设置 `evaluationInfo.synchronous.enabled` 是真的。 如果留空，区段定义将创建为 **批次** 区段。 |
| `schema` | 与区段中的实体关联的架构。 由以下任一项组成 `id` 或 `name` 字段。 |
| `expression` | 包含有关区段定义的字段信息的实体。 |
| `expression.type` | 指定表达式类型。 目前，仅支持“PQL”。 |
| `expression.format` | 指示值中表达式的结构。 目前，支持以下格式： <ul><li>`pql/text`：根据发布的PQL语法，区段定义的文本表示形式。  例如：`workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合中指定的类型的表达式 `expression.format`. |

<!-- >[!NOTE]
>
>A segment definition expression may also reference a computed attribute. To learn more, please refer to the [computed attribute API endpoint guide](../../profile/computed-attributes/ca-api.md)
>
>Computed attribute functionality is in alpha and is not available to all users. Documentation and functionality are subject to change. -->

**响应**

成功的响应会返回HTTP状态200以及新创建的区段定义的详细信息。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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
| `id` | 新创建的区段定义的系统生成的ID。 |
| `evaluationInfo` | 一个对象，指明区段定义将进行何种类型的评估。 它可以是批处理、流（也称为连续）或边缘（也称为同步）分段。 |

## 检索特定区段定义 {#get}

通过向GET请求，您可以检索有关特定区段定义的详细信息。 `/segment/definitions` 端点并提供要在请求路径中检索的区段定义的ID。

**API格式**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 此 `id` 要检索的区段定义的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，其中包含有关指定区段定义的详细信息。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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
| `id` | 系统生成的区段定义的只读ID。 |
| `name` | 用于引用区段定义的唯一名称。 |
| `schema` | 与区段中的实体关联的架构。 由以下任一项组成 `id` 或 `name` 字段。 |
| `expression` | 包含有关区段定义的字段信息的实体。 |
| `expression.type` | 指定表达式类型。 目前，仅支持“PQL”。 |
| `expression.format` | 指示值中表达式的结构。 目前，支持以下格式： <ul><li>`pql/text`：根据发布的PQL语法，区段定义的文本表示形式。  例如：`workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合中指定的类型的表达式 `expression.format`. |
| `description` | 易于用户识别的定义描述。 |
| `evaluationInfo` | 一个对象，指示将接受区段定义的评估类型：批处理、流（也称为连续）或边缘（也称为同步）。 |

## 批量检索区段定义 {#bulk-get}

您可以通过对以下对象发出POST请求，检索有关多个指定区段定义的详细信息： `/segment/definitions/bulk-get` 端点并提供 `id` 请求正文中的区段定义的值。

**API格式**

```http
POST /segment/definitions/bulk-get
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的响应会返回包含所请求区段定义的HTTP状态207。

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
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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
| `id` | 系统生成的区段定义的只读ID。 |
| `name` | 用于引用区段定义的唯一名称。 |
| `schema` | 与区段中的实体关联的架构。 由以下任一项组成 `id` 或 `name` 字段。 |
| `expression` | 包含有关区段定义的字段信息的实体。 |
| `expression.type` | 指定表达式类型。 目前，仅支持“PQL”。 |
| `expression.format` | 指示值中表达式的结构。 目前，支持以下格式： <ul><li>`pql/text`：根据发布的PQL语法，区段定义的文本表示形式。  例如：`workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合中指定的类型的表达式 `expression.format`. |
| `description` | 易于用户识别的定义描述。 |
| `evaluationInfo` | 一个对象，指示将接受区段定义的评估类型：批处理、流（也称为连续）或边缘（也称为同步）。 |

## 删除特定区段定义 {#delete}

您可以通过对以下网站发出DELETE请求，请求删除特定区段定义： `/segment/definitions` 端点并在请求路径中提供要删除的区段定义的ID。

>[!NOTE]
>
> 在目标激活中使用的区段定义 **无法** 将被删除。

**API格式**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 此 `id` 要删除的区段定义的值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，但不返回消息。

## 更新特定区段定义

您可以通过向以下网站发出PATCH请求来更新特定区段定义： `/segment/definitions` 端点并提供要在请求路径中更新的区段定义的ID。

**API格式**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 此 `id` 要更新的区段定义的值。 |

**请求**

以下请求会将工作地址所在国家/地区从美国更新为加拿大。

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功响应会返回HTTP状态200，其中包含新更新的区段定义的详细信息。 请注意工作地址国家/地区如何从美国（美国）更新为加拿大(CA)。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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

可在以下位置转换区段定义： `pql/text` 和 `pql/json` 或 `pql/json` 到 `pql/text` 向发出POST请求 `/segment/conversion` 端点。

**API格式**

```http
POST /segment/conversion
```

**请求**

以下请求会将区段定义的格式从 `pql/text` 到 `pql/json`.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功响应会返回HTTP状态200以及新转换的区段定义的详细信息。

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

阅读本指南后，您现在可以更好地了解区段定义的工作方式。 有关创建区段的更多信息，请阅读 [创建区段](../tutorials/create-a-segment.md) 教程。

---
solution: Experience Platform
title: 区段定义API端点
description: Adobe Experience Platform分段服务API中的区段定义端点允许您以编程方式管理组织的区段定义。
role: Developer
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: 5f19bd0601770115cae859fd6dc85bd9c9f6e92c
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 2%

---

# 区段定义端点

>[!WARNING]
>
>不建议使用分段服务API通过B2B实体创建受众。 不能再使用以下B2B实体创建受众：帐户、帐户 — 人员关系、营销活动、营销活动成员、营销列表成员、机会和机会 — 人员关系。 有关详细信息，请阅读[Real-Time CDP B2B edition架构升级](../../rtcdp/b2b-architecture-upgrade.md)指南。

Adobe Experience Platform允许您创建区段定义，以从一组配置文件中定义一组特定属性或行为。 区段定义是一个对象，它封装在[!DNL Profile Query Language] (PQL)中编写的查询。 区段定义会应用到用户档案以创建受众。 此对象（区段定义）也称为PQL谓词。 PQL谓词根据与您提供给[!DNL Real-Time Customer Profile]的任何记录或时间序列数据相关的条件定义区段定义的规则。 有关编写PQL查询的更多信息，请参阅[PQL指南](../pql/overview.md)。

本指南提供的信息可帮助您更好地了解区段定义，包括用于使用API执行基本操作的示例API调用。

## 快速入门

本指南中使用的端点是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)以了解成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

## 检索区段定义列表 {#list}

您可以通过向`/segment/definitions`端点发出GET请求来检索贵组织的所有区段定义的列表。

**API格式**

`/segment/definitions`端点支持多个查询参数以帮助筛选结果。 虽然这些参数是可选的，但强烈建议使用这些参数以帮助减少昂贵的开销。 在不使用参数的情况下调用此端点将检索您的组织可用的所有区段定义。 可以包含多个参数，以&amp;符号(`&`)分隔。

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**查询参数**

+++ 可用查询参数的列表。

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `start` | 为返回的段定义指定起始偏移。 | `start=4` |
| `limit` | 指定每页返回的区段定义数。 | `limit=20` |
| `page` | 指定区段定义的结果将从哪一页开始。 | `page=5` |
| `sort` | 指定排序结果所依据的字段。 使用以下格式编写： `[attributeName]:[desc/asc]`。 | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | 指定区段定义是否启用流式处理。 | `evaluationInfo.continuous.enabled=true` |

+++

**请求**

以下请求将检索组织中发布的最后两个区段定义。

+++ 用于检索区段定义列表的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200，其中包含指定组织的区段定义列表(JSON)。

+++ 检索区段定义列表时的示例响应。

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
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

+++

## 创建新的区段定义 {#create}

您可以通过向`/segment/definitions`端点发出POST请求来创建新的区段定义。

>[!IMPORTANT]
>
>通过API **创建的区段定义无法使用区段生成器编辑**。

**API格式**

```http
POST /segment/definitions
```

**请求**

创建新区段定义时，您可以采用`pql/text`或`pql/json`格式创建它。

>[!BEGINTABS]

>[!TAB 使用pql/文本]

+++ 创建区段定义的示例请求。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
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
        "schema": {
            "name": "_xdm.context.profile"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 用于引用区段定义的唯一名称。 |
| `description` | （可选）正在创建的区段定义的描述。 |
| `expression` | 包含有关区段定义的字段信息的实体。 |
| `expression.type` | 指定表达式类型。 目前，仅支持“PQL”。 |
| `expression.format` | 指示值中表达式的结构。 支持的值包括`pql/text`和`pql/json`。 |
| `expression.value` | 符合`expression.format`中指示的类型的表达式。 |
| `evaluationInfo` | （可选）要创建的区段定义的类型。 如果要创建批次区段，请将`evaluationInfo.batch.enabled`设置为true。 如果要创建流区段，请将`evaluationInfo.continuous.enabled`设置为true。 如果要创建边缘区段，请将`evaluationInfo.synchronous.enabled`设置为true。 如果留空，区段定义将创建为&#x200B;**批次**&#x200B;区段。 |
| `schema` | 与区段中的实体关联的架构。 由`id`或`name`字段组成。 |

+++

>[!TAB 使用pql/json]

+++ 创建区段定义的示例请求。

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
            "format": "pql/json",
            "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"a\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}},{\"nodeType\":\"fieldLookup\",\"fieldName\":\"b\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}]}"
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
        "payloadSchema": "string"
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 用于引用区段定义的唯一名称。 |
| `description` | （可选）正在创建的区段定义的描述。 |
| `evaluationInfo` | （可选）要创建的区段定义的类型。 如果要创建批次区段，请将`evaluationInfo.batch.enabled`设置为true。 如果要创建流区段，请将`evaluationInfo.continuous.enabled`设置为true。 如果要创建边缘区段，请将`evaluationInfo.synchronous.enabled`设置为true。 如果留空，区段定义将创建为&#x200B;**批次**&#x200B;区段。 |
| `schema` | 与区段中的实体关联的架构。 由`id`或`name`字段组成。 |
| `expression` | 包含有关区段定义的字段信息的实体。 |
| `expression.type` | 指定表达式类型。 目前，仅支持“PQL”。 |
| `expression.format` | 指示值中表达式的结构。 |
| `expression.value` | 符合`expression.format`中指示的类型的表达式。 |

+++

>[!ENDTABS]

**响应**

成功的响应会返回HTTP状态200以及新创建的区段定义的详细信息。

+++ 创建区段定义时的示例响应。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
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
| `evaluationInfo` | 一个对象，指明区段定义将进行的评估类型。 它可以是批处理、流（也称为连续）或边缘（也称为同步）分段。 |

+++

## 检索特定区段定义 {#get}

通过向`/segment/definitions`端点发出GET请求并提供要在请求路径中检索的区段定义的ID，您可以检索有关特定区段定义的详细信息。

**API格式**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 要检索的区段定义的`id`值。 |

**请求**

+++ 用于检索区段定义的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关指定区段定义的详细信息。

+++ 检索区段定义时的示例响应。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
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
| `schema` | 与区段中的实体关联的架构。 由`id`或`name`字段组成。 |
| `expression` | 包含有关区段定义的字段信息的实体。 |
| `expression.type` | 指定表达式类型。 目前，仅支持“PQL”。 |
| `expression.format` | 指示值中表达式的结构。 目前，支持以下格式： <ul><li>`pql/text`：区段定义的文本表示形式，根据发布的PQL语法。  例如：`workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合`expression.format`中指示的类型的表达式。 |
| `description` | 易于用户识别的定义描述。 |
| `evaluationInfo` | 一个对象，可指示将接受区段定义的评估类型、批处理、流式处理（也称为连续）或边缘（也称为同步）。 |

+++

## 批量检索区段定义 {#bulk-get}

通过向`/segment/definitions/bulk-get`端点发出POST请求并在请求正文中提供区段定义的`id`值，您可以检索有关多个指定区段定义的详细信息。

**API格式**

```http
POST /segment/definitions/bulk-get
```

**请求**

+++ 使用批量获取端点时的示例请求。

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

| 属性 | 描述 |
| -------- | ----------- |
| `ids` | 一个数组，其中包含说明要检索的区段定义ID的对象。 |

+++

**响应**

成功的响应会返回包含所请求区段定义的HTTP状态207。

+++ 使用批量获取端点时的示例响应。

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
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
| `schema` | 与区段中的实体关联的架构。 由`id`或`name`字段组成。 |
| `expression` | 包含有关区段定义的字段信息的实体。 |
| `expression.type` | 指定表达式类型。 目前，仅支持“PQL”。 |
| `expression.format` | 指示值中表达式的结构。 目前，支持以下格式： <ul><li>`pql/text`：区段定义的文本表示形式，根据发布的PQL语法。  例如：`workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合`expression.format`中指示的类型的表达式。 |
| `description` | 易于用户识别的定义描述。 |
| `evaluationInfo` | 一个对象，可指示将接受区段定义的评估类型、批处理、流式处理（也称为连续）或边缘（也称为同步）。 |

+++

## 删除特定区段定义 {#delete}

您可以通过向`/segment/definitions`端点发出DELETE请求并在请求路径中提供要删除的区段定义的ID，来请求删除特定区段定义。

>[!NOTE]
>
> 无法删除目标激活&#x200B;**中使用的区段定义**。

**API格式**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 要删除的区段定义的`id`值。 |

**请求**

+++ 删除区段定义的示例请求。

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200，但不返回消息。

## 更新特定区段定义

您可以更新特定的区段定义，方法是向`/segment/definitions`端点发出PATCH请求，并在请求路径中提供要更新的区段定义的ID。

**API格式**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 要更新的区段定义的`id`值。 |

**请求**

以下请求会将工作地址所在国家/地区从美国更新为加拿大。

>[!NOTE]
>
>由于此API调用&#x200B;**替换了**&#x200B;区段定义的内容，请确保&#x200B;**所有**&#x200B;要保留的字段都包含在请求正文中。

+++ 更新区段定义的示例请求。

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
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

+++

**响应**

成功的响应会返回HTTP状态200以及新更新的区段定义的详细信息。

+++ 更新区段定义时的示例响应。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
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

+++

## 转换区段定义

您可以通过向`pql/text`终结点发出POST请求，将`pql/json`和`pql/json`之间的区段定义或`pql/text`转换为`/segment/conversion`。

**API格式**

```http
POST /segment/conversion
```

**请求**

以下请求会将区段定义的格式从`pql/text`更改为`pql/json`。

+++ 转换区段定义的示例请求。

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
        "payloadSchema": "string"
    }'
```

+++

**响应**

成功的响应会返回HTTP状态200以及新转换的区段定义的详细信息。

+++ 转换区段定义时的示例响应。

```json
{
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

+++

## 后续步骤

阅读本指南后，您现在可以更好地了解区段定义的工作方式。 有关创建区段的更多信息，请参阅[创建区段](../tutorials/create-a-segment.md)教程。

---
keywords: Experience Platform；主页；热门主题；策略执行；基于API的执行；数据管理
solution: Experience Platform
title: 数据使用策略API端点
topic-legacy: developer guide
description: 数据使用策略是贵组织采用的规则，用于描述您允许或限制对Experience Platform内数据执行的营销操作类型。 /policys端点用于与查看、创建、更新或删除数据使用策略相关的所有API调用。
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: 05e63064dc8eb3f070a383f508cc4a86d4f5e9cc
workflow-type: tm+mt
source-wordcount: '1840'
ht-degree: 2%

---

# 数据使用策略端点

数据使用策略是描述您允许或限制对内数据执行的营销操作类型的规则 [!DNL Experience Platform]. 的 `/policies` 的端点 [!DNL Policy Service API] 允许您以编程方式管理贵组织的数据使用策略。

>[!IMPORTANT]
>
>不要将此端点与 `/policies` 的端点 [访问控制API](../../access-control/abac/api/policies.md)，用于管理访问控制策略。

## 快速入门

本指南中使用的API端点是 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 在继续之前，请查看 [入门指南](getting-started.md) 有关相关文档的链接、本文档中的API调用示例指南，以及有关成功调用任何代码所需标头的重要信息 [!DNL Experience Platform] API。

## 检索策略列表 {#list}

您可以列出所有 `core` 或 `custom` 策略，方法是向 `/policies/core` 或 `/policies/custom`，分别为。

**API格式**

```http
GET /policies/core
GET /policies/custom
```

**请求**

以下请求可检索由您的组织定义的自定义策略列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包括 `children` 列出每个检索到的策略(包括其 `id` 值。 您可以使用 `id` 要执行的特定策略的字段 [对照](#lookup), [更新](#update)和 [删除](#delete) 要求执行该政策。

```JSON
{
    "_page": {
        "start": "5c6dacdf685a4913dc48937c",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/policies/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "Export Data to Third Party",
            "status": "DRAFT",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
                        "operands": [
                            {
                                "label": "C3"
                            },
                            {
                                "label": "C7"
                            }
                        ]
                    }
                ]
            },
            "imsOrg": "{ORG_ID}",
            "created": 1550691551888,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550701472910,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
                }
            },
            "id": "5c6dacdf685a4913dc48937c"
        },
        {
            "name": "Combine Data",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
            ],
            "description": "Data that meets these conditions cannot be combined.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "I1"
                    }
                ]
            },
            "imsOrg": "{ORG_ID}",
            "created": 1550703519823,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550714340335,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `_page.count` | 检索到的策略总数。 |
| `name` | 策略的显示名称。 |
| `status` | 策略的当前状态。 有三种可能的状态： `DRAFT`, `ENABLED`或 `DISABLED`. 默认情况下，仅 `ENABLED` 政策参与评价。 请参阅 [政策评价](../enforcement/overview.md) 以了解更多信息。 |
| `marketingActionRefs` | 列出策略所有适用营销操作的URI的数组。 |
| `description` | 可选描述，提供了策略用例的进一步上下文。 |
| `deny` | 描述特定数据使用标签的对象，策略的关联营销操作被限制在其上执行。 请参阅 [创建策略](#create-policy) 以了解有关此属性的详细信息。 |

## 查找策略 {#look-up}

您可以通过将 `id` 属性。

**API格式**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 的 `id` 你想查的政策。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回策略的详细信息。

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "C7"
                    }
                ]
            }
        ]
    },
    "imsOrg": "{ORG_ID}",
    "created": 1550703519823,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550714340335,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

| 属性 | 描述 |
| --- | --- |
| `name` | 策略的显示名称。 |
| `status` | 策略的当前状态。 有三种可能的状态： `DRAFT`, `ENABLED`或 `DISABLED`. 默认情况下，仅 `ENABLED` 政策参与评价。 请参阅 [政策评价](../enforcement/overview.md) 以了解更多信息。 |
| `marketingActionRefs` | 一个数组，其中列出了策略所有适用营销操作的URI。 |
| `description` | 可选描述，提供了策略用例的进一步上下文。 |
| `deny` | 描述特定数据使用标签的对象，策略的关联营销操作被限制为不执行。 请参阅 [创建策略](#create-policy) 以了解有关此属性的详细信息。 |

## 创建自定义策略 {#create-policy}

在 [!DNL Policy Service] API，策略由以下内容定义：

* 对特定营销操作的引用
* 描述限制对其执行营销操作的数据使用标签的表达式

要满足后一要求，策略定义必须包含有关存在数据使用标签的布尔表达式。 此表达式称为策略表达式。

策略表达式以 `deny` 属性。 简单的示例 `deny` 仅检查单个标签是否存在的对象将如下所示：

```json
"deny": {
    "label": "C1"
}
```

但是，许多策略指定了关于存在数据使用标签的更复杂的条件。 要支持这些用例，您还可以包含布尔运算来描述策略表达式。 策略表达式对象必须包含标签或运算符和操作数，但不能同时包含这两者。 反过来，每个操作数也是策略表达式对象。

例如，为了定义一项策略，该策略禁止对 `C1 OR (C3 AND C7)` 标签存在，策略 `deny` 属性将指定为：

```JSON
"deny": {
  "operator": "OR",
  "operands": [
    {"label": "C1"},
    {
      "operator": "AND",
      "operands": [
        {"label": "C3"},
        {"label": "C7"}
      ]
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `operator` | 指示同级中提供的标签之间的条件关系 `operands` 数组。 接受的值包括： <ul><li>`OR`:如果 `operands` 数组存在。</li><li>`AND`:仅当 `operands` 数组存在。</li></ul> |
| `operands` | 对象数组，每个对象表示单个标签或附加对 `operator` 和 `operands` 属性。 在 `operands` 数组根据其同级数组的值解析为true或false `operator` 属性。 |
| `label` | 应用于策略的单个数据使用标签的名称。 |

您可以通过向 `/policies/custom` 端点。

**API格式**

```http
POST /policies/custom
```

**请求**

以下请求会创建一个新策略，以限制营销操作 `exportToThirdParty` 对包含标签的数据执行 `C1 OR (C3 AND C7)`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "OR",
          "operands": [
            {"label": "C1"},
            {
              "operator": "AND",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 策略的显示名称。 |
| `status` | 策略的当前状态。 有三种可能的状态： `DRAFT`, `ENABLED`或 `DISABLED`. 默认情况下，仅 `ENABLED` 政策参与评价。 请参阅 [政策评价](../enforcement/overview.md) 以了解更多信息。 |
| `marketingActionRefs` | 一个数组，其中列出了策略所有适用营销操作的URI。 营销操作的URI在 `_links.self.href` 的 [查找营销操作](./marketing-actions.md#look-up). |
| `description` | 可选描述，提供了策略用例的进一步上下文。 |
| `deny` | 描述特定数据使用情况的策略表达式会限制不对其执行策略关联的营销操作。 |

**响应**

成功的响应会返回新创建策略的详细信息，包括其 `id`. 此值为只读，在创建策略时自动分配。

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "OR",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "C7"
                    }
                ]
            }
        ]
    },
    "imsOrg": "{ORG_ID}",
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550691551888,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 更新自定义策略 {#update}

>[!IMPORTANT]
>
>您只能更新自定义策略。 如果要启用或禁用核心策略，请参阅 [更新已启用的核心策略列表](#update-enabled-core).

您可以更新现有的自定义策略，方法是在PUT请求的路径中提供其ID，其有效负载包含完整策略的更新形式。 换句话说，PUT请求实际上会重写策略。

>[!NOTE]
>
>请参阅 [更新自定义策略的一部分](#patch) 如果您只想更新策略的一个或多个字段，而不是覆盖策略。

**API格式**

```http
PUT /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 的 `id` 要更新的策略。 |

**请求**

在此示例中，将数据导出到第三方的条件已发生更改，现在，您需要创建的策略才能在 `C1 AND C5` 数据标签存在。

以下请求会更新现有策略以包含新策略表达式。 请注意，由于此请求实质上重写了策略，因此所有字段都必须包含在有效负载中，即使其某些值未更新也是如此。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "../marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "AND",
          "operands": [
            {"label": "C1"},
            {"label": "C5"}
          ]
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 策略的显示名称。 |
| `status` | 策略的当前状态。 有三种可能的状态： `DRAFT`, `ENABLED`或 `DISABLED`. 默认情况下，仅 `ENABLED` 政策参与评价。 请参阅 [政策评价](../enforcement/overview.md) 以了解更多信息。 |
| `marketingActionRefs` | 一个数组，其中列出了策略所有适用营销操作的URI。 营销操作的URI在 `_links.self.href` 的 [查找营销操作](./marketing-actions.md#look-up). |
| `description` | 可选描述，提供了策略用例的进一步上下文。 |
| `deny` | 描述特定数据使用情况的策略表达式会限制不对其执行策略关联的营销操作。 请参阅 [创建策略](#create-policy) 以了解有关此属性的详细信息。 |

**响应**

成功的响应会返回更新策略的详细信息。

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/core/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "label": "C5"
            }
        ]
    },
    "imsOrg": "{ORG_ID}",
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550701472910,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 更新自定义策略的一部分 {#patch}

>[!IMPORTANT]
>
>您只能更新自定义策略。 如果要启用或禁用核心策略，请参阅 [更新已启用的核心策略列表](#update-enabled-core).

可以使用PATCH请求来更新策略的特定部分。 与重写策略的PUT请求不同，PATCH请求仅更新请求正文中指定的属性。 当您想要启用或禁用策略时，这特别有用，因为您只需提供相应属性的路径(`/status`)及其值(`ENABLED` 或 `DISABLED`)。

>[!NOTE]
>
>PATCH请求的负载遵循JSON修补程序格式。 请参阅 [API基础知识指南](../../landing/api-fundamentals.md) 以了解有关已接受语法的更多信息。

的 [!DNL Policy Service] API支持JSON修补程序操作 `add`, `remove`和 `replace`，和允许您将多个更新合并到一个调用中，如以下示例所示。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 的 `id` 要更新其属性的策略的。 |

**请求**

以下请求使用两个 `replace` 操作将策略状态从 `DRAFT` to `ENABLED`，以及更新 `description` 字段。

>[!IMPORTANT]
>
>在单个请求中发送多个PATCH操作时，将按它们在数组中的显示顺序进行处理。 确保在必要时按正确的顺序发送请求。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' [
          {
            "op": "replace",
            "path": "/status",
            "value": "ENABLED"
          },
          {
            "op": "replace",
            "path": "/description",
            "value": "New policy description."
          }
        ]'
```

**响应**

成功的响应会返回更新策略的详细信息。


```JSON
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "New policy description.",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "C7"
                    }
                ]
            }
        ]
    },
    "imsOrg": "{ORG_ID}",
    "created": 1550703519823,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550712163182,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 删除自定义策略 {#delete}

您可以通过将 `id` 在DELETE请求的路径中。

>[!WARNING]
>
>删除后，将无法恢复策略。 最佳做法是 [执行查找(GET)请求](#lookup) 首先查看策略，并确认它是您希望删除的正确策略。

**API格式**

```http
DELETE /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 要删除的策略的ID。 |

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200(OK)，并带有空白正文。

您可以再次尝试查找(GET)策略以确认删除。 如果策略已成功删除，您应会收到HTTP 404（未找到）错误。

## 检索已启用的核心策略列表 {#list-enabled-core}

默认情况下，只有启用的数据使用策略才会参与评估。 您可以通过向 `/enabledCorePolicies` 端点。

**API格式**

```http
GET /enabledCorePolicies
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回 `policyIds` 数组。

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0003",
    "corepolicy_0004",
    "corepolicy_0005",
    "corepolicy_0006",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## 更新已启用的核心策略列表 {#update-enabled-core}

默认情况下，只有启用的数据使用策略才会参与评估。 通过向 `/enabledCorePolicies` 端点，您可以使用一次调用来更新贵组织已启用的核心策略列表。

>[!NOTE]
>
>此端点只能启用或禁用核心策略。 要启用或禁用自定义策略，请参阅 [更新策略的一部分](#patch).

**API格式**

```http
PUT /enabledCorePolicies
```

**请求**

以下请求会根据有效负载中提供的ID更新已启用的核心策略列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "policyIds": [
          "corepolicy_0001",
          "corepolicy_0002",
          "corepolicy_0007",
          "corepolicy_0008"
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `policyIds` | 要启用的核心策略ID列表。 未包含的任何核心策略均设置为 `DISABLED` 状态和将不参与评估。 |

**响应**

成功响应会返回 `policyIds` 数组。

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{ORG_ID}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1595876052649,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## 后续步骤

定义新策略或更新现有策略后，即可使用 [!DNL Policy Service] 用于测试针对特定标签或数据集的营销操作的API，并查看您的策略是否按预期引发违规。 请参阅 [策略评估端点](./evaluation.md) 以了解更多信息。

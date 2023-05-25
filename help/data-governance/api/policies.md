---
keywords: Experience Platform；主页；热门主题；策略实施；基于API的实施；数据治理
solution: Experience Platform
title: 数据管理策略API端点
description: 数据治理策略是您的组织采用的规则，用于描述允许或限制您对Experience Platform中的数据执行的营销操作类型。 /policies端点用于与查看、创建、更新或删除数据治理策略相关的所有API调用。
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 2%

---

# 数据治理策略端点

数据治理策略是描述允许或限制您对内数据执行的营销操作类型的规则 [!DNL Experience Platform]. 此 `/policies` 中的端点 [!DNL Policy Service API] 允许您以编程方式管理组织的数据治理策略。

>[!IMPORTANT]
>
>不应将治理策略与访问控制策略混淆，访问控制策略确定组织中的某些Platform用户可以访问的特定数据属性。 请参阅 `/policies` 的端点指南 [访问控制API](../../access-control/abac/api/policies.md) 有关如何以编程方式管理访问控制策略的详细信息。

## 快速入门

本指南中使用的API端点是 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 在继续之前，请查看 [快速入门指南](getting-started.md) 有关相关文档的链接，请参阅本文档中的示例API调用指南，以及有关成功调用任何组件所需的所需标头的重要信息 [!DNL Experience Platform] API。

## 检索策略列表 {#list}

您可以列出所有 `core` 或 `custom` 向以下机构发出GET请求以制定政策 `/policies/core` 或 `/policies/custom`，则不会显示任何内容。

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

成功的响应包括 `children` 数组，其中列出了每个检索到的策略的详细信息，包括其 `id` 值。 您可以使用 `id` 要执行的特定策略的字段 [查找](#lookup)， [更新](#update)、和 [delete](#delete) 请求该策略。

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
| `status` | 策略的当前状态。 可能的状态有三种： `DRAFT`， `ENABLED`，或 `DISABLED`. 默认情况下，仅限 `ENABLED` 政策参与评价。 请参阅概述，位于 [策略评估](../enforcement/overview.md) 了解更多信息。 |
| `marketingActionRefs` | 一个数组，列出策略的所有适用营销操作的URI。 |
| `description` | 可选描述，为策略用例提供进一步的上下文。 |
| `deny` | 描述策略的相关营销操作被限制无法执行的特定数据使用标签的对象。 请参阅以下部分： [创建策略](#create-policy) 以了解有关此属性的更多信息。 |

## 查找策略 {#look-up}

您可以通过包含特定策略的 `id` 属性(在GET请求的路径中)。

**API格式**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 要查找的策略的URL。 |

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

成功响应将返回策略的详细信息。

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
| `status` | 策略的当前状态。 可能的状态有三种： `DRAFT`， `ENABLED`，或 `DISABLED`. 默认情况下，仅限 `ENABLED` 政策参与评价。 请参阅概述，位于 [策略评估](../enforcement/overview.md) 了解更多信息。 |
| `marketingActionRefs` | 一个数组，列出策略的所有适用营销操作的URI。 |
| `description` | 可选描述，为策略用例提供进一步的上下文。 |
| `deny` | 描述策略的相关营销操作被限制无法执行的特定数据使用标签的对象。 请参阅以下部分： [创建策略](#create-policy) 以了解有关此属性的更多信息。 |

## 创建自定义策略 {#create-policy}

在 [!DNL Policy Service] API中，策略通过以下方式定义：

* 对特定营销操作的引用
* 描述限制执行营销操作的数据使用标签的表达式

为了满足后一种要求，策略定义必须包括关于数据使用标签存在的布尔表达式。 此表达式称为策略表达式。

策略表达式的形式为 `deny` 属性。 简单示例 `deny` 仅检查单个标签是否存在的对象如下所示：

```json
"deny": {
    "label": "C1"
}
```

但是，许多策略会针对数据使用标签的存在指定更复杂的条件。 要支持这些用例，您还可以包含布尔操作来描述策略表达式。 策略表达式对象必须包含标签或运算符和操作数，但不能同时包含两者。 反过来，每个操作数也是策略表达式对象。

例如，为了定义禁止对以下位置的数据执行营销操作的策略 `C1 OR (C3 AND C7)` 标签存在，策略的 `deny` 属性将指定为：

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
| `operator` | 指示同级中提供的标签之间的条件关系 `operands` 数组。 接受的值包括： <ul><li>`OR`：如果中的任何标签，则表达式解析为true `operands` 数组存在。</li><li>`AND`：仅当所有标签都位于以下条件时，表达式才会解析为true `operands` 数组存在。</li></ul> |
| `operands` | 一个对象数组，每个对象表示一个标签或另外的一对 `operator` 和 `operands` 属性。 标签和/或操作在 `operands` 数组根据其同级值的解析为true或false `operator` 属性。 |
| `label` | 应用于策略的单个数据使用标签的名称。 |

您可以通过向以下对象发出POST请求来创建新的自定义策略： `/policies/custom` 端点。

**API格式**

```http
POST /policies/custom
```

**请求**

以下请求将创建一个限制营销操作的新策略 `exportToThirdParty` 对包含标签的数据执行 `C1 OR (C3 AND C7)`.

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
| `status` | 策略的当前状态。 可能的状态有三种： `DRAFT`， `ENABLED`，或 `DISABLED`. 默认情况下，仅限 `ENABLED` 政策参与评价。 请参阅概述，位于 [策略评估](../enforcement/overview.md) 了解更多信息。 |
| `marketingActionRefs` | 一个数组，列出策略的所有适用营销操作的URI。 营销活动的URI在下提供 `_links.self.href` 在的响应中 [查找营销操作](./marketing-actions.md#look-up). |
| `description` | 可选描述，为策略用例提供进一步的上下文。 |
| `deny` | 描述特定数据使用标签的策略表达式，限制执行策略的关联营销操作。 |

**响应**

成功响应将返回新创建的策略的详细信息，包括其 `id`. 此值为只读值，在创建策略时自动分配。

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
>您只能更新自定义策略。 如果要启用或禁用核心策略，请参阅 [更新已启用的核心策略的列表](#update-enabled-core).

您可以通过在PUT请求的路径中提供其ID来更新现有的自定义策略，有效负载包括完整的已更新策略形式。 换句话说，PUT请求实际上重写了策略。

>[!NOTE]
>
>请参阅以下部分： [更新自定义策略的一部分](#patch) 只想更新策略的一个或多个字段，而不想覆盖它。

**API格式**

```http
PUT /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 要更新的策略的ID。 |

**请求**

在此示例中，将数据导出到第三方的条件已更改，现在，您需要创建的策略来拒绝此营销操作，如果 `C1 AND C5` 存在数据标签。

以下请求更新现有策略以包含新的策略表达式。 请注意，由于此请求实际上重写了策略，因此所有字段都必须包含在有效负载中，即使它们的某些值未更新也是如此。

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
| `status` | 策略的当前状态。 可能的状态有三种： `DRAFT`， `ENABLED`，或 `DISABLED`. 默认情况下，仅限 `ENABLED` 政策参与评价。 请参阅概述，位于 [策略评估](../enforcement/overview.md) 了解更多信息。 |
| `marketingActionRefs` | 一个数组，列出策略的所有适用营销操作的URI。 营销活动的URI在下提供 `_links.self.href` 在的响应中 [查找营销操作](./marketing-actions.md#look-up). |
| `description` | 可选描述，为策略用例提供进一步的上下文。 |
| `deny` | 描述特定数据使用标签的策略表达式，限制执行策略的关联营销操作。 请参阅以下部分： [创建策略](#create-policy) 以了解有关此属性的更多信息。 |

**响应**

成功响应将返回已更新策略的详细信息。

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
>您只能更新自定义策略。 如果要启用或禁用核心策略，请参阅 [更新已启用的核心策略的列表](#update-enabled-core).

可以使用PATCH请求更新策略的特定部分。 与重写策略的PUT请求不同，PATCH请求仅更新请求正文中指定的属性。 当您希望启用或禁用策略时，此选项特别有用，因为您只需提供相应属性的路径(`/status`)及其值(`ENABLED` 或 `DISABLED`)。

>[!NOTE]
>
>PATCH请求的有效负载遵循JSON修补程序格式。 请参阅 [API基础知识指南](../../landing/api-fundamentals.md) 有关接受的语法的更多信息。

此 [!DNL Policy Service] API支持JSON修补程序操作 `add`， `remove`、和 `replace`，并用于将多个更新组合到单个调用中，如以下示例所示。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 此 `id` 要更新其属性的策略的。 |

**请求**

以下请求使用两个 `replace` 更改策略状态的操作 `DRAFT` 到 `ENABLED`，并更新 `description` 字段，其中包含新描述。

>[!IMPORTANT]
>
>在单个请求中发送多个PATCH操作时，将按照它们在数组中的显示顺序进行处理。 确保在必要时按正确的顺序发送请求。

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

成功响应将返回已更新策略的详细信息。


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

您可以通过包含某个自定义策略的 `id` 在DELETE请求的路径中。

>[!WARNING]
>
>一旦删除，策略将无法恢复。 最佳做法是 [执行查找(GET)请求](#lookup) 首先查看策略，并确认它是您要删除的正确策略。

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

成功的响应返回带有空白正文的HTTP状态200 （确定）。

您可以通过再次尝试查找(GET)策略来确认删除。 如果已成功删除策略，您应会收到HTTP 404 （未找到）错误。

## 检索已启用的核心策略的列表 {#list-enabled-core}

默认情况下，只有启用的数据治理策略会参与评估。 您可以通过对以下网站发出GET请求，检索贵组织当前启用的核心策略的列表： `/enabledCorePolicies` 端点。

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

成功的响应会返回下启用的核心策略列表。 `policyIds` 数组。

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

## 更新已启用的核心策略的列表 {#update-enabled-core}

默认情况下，只有启用的数据治理策略会参与评估。 向发出PUT请求 `/enabledCorePolicies` 端点，您可以使用单个调用更新贵组织的已启用核心策略的列表。

>[!NOTE]
>
>此端点只能启用或禁用核心策略。 要启用或禁用自定义策略，请参阅 [更新策略的一部分](#patch).

**API格式**

```http
PUT /enabledCorePolicies
```

**请求**

以下请求根据有效负载中提供的ID更新已启用的核心策略的列表。

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
| `policyIds` | 要启用的核心策略ID列表。 任何未包含的核心策略均设置为 `DISABLED` 状态，不参与评估。 |

**响应**

成功的响应会返回下启用的核心策略的更新列表。 `policyIds` 数组。

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

定义新策略或更新现有策略后，您可以使用 [!DNL Policy Service] 此API用于针对特定标签或数据集测试营销操作，并查看您的策略是否按预期引发违规。 请参阅 [策略评估端点](./evaluation.md) 了解更多信息。

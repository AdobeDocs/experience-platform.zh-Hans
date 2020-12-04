---
keywords: Experience Platform;home;popular topics;Policy enforcement;API-based enforcement;data governance
solution: Experience Platform
title: 策略
topic: developer guide
description: 数据使用策略是贵组织采用的规则，用于描述您允许或限制您对Experience Platform内数据执行的营销操作类型。 /policies端点用于与查看、创建、更新或删除数据使用策略相关的所有API调用。
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 2%

---


# 策略端点

数据使用策略是描述允许或限制您对中的数据执行的营销操作种类的规则 [!DNL Experience Platform]。 中的 `/policies` 端点允许您 [!DNL Policy Service API] 以编程方式管理组织的数据使用策略。

## 入门指南

本指南中使用的API端点是API的一 [[!DNL Policy Service] 部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)。 在继续之前，请查 [看入门指南](getting-started.md) ，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何API所需标头的重要信 [!DNL Experience Platform] 息。

## 检索一列表策略 {#list}

您可以通过分别 `core` 向或 `custom` 者发出列表请求来GET `/policies/core` 所有或 `/policies/custom`策略。

**API格式**

```http
GET /policies/core
GET /policies/custom
```

**请求**

以下请求检索由您的组织定义的一列表自定义策略。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包括一个 `children` 数组，它列表每个检索到的策略的详细信息，包括其 `id` 值。 您可以使用特 `id` 定策略的字段来执行 [查找](#lookup)、更 [新和删](#update)除该策 [略的请求](#delete) 。

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
| `_page.count` | 检索的策略总数。 |
| `name` | 策略的显示名称。 |
| `status` | 策略的当前状态。 有三种可能的状态： `DRAFT`、 `ENABLED`或 `DISABLED`。 默认情况下，只 `ENABLED` 有策略参与评估。 See the overview on [policy evaluation](../enforcement/overview.md) for more information. |
| `marketingActionRefs` | 列表策略所有适用营销操作的URI的数组。 |
| `description` | 可选描述，它提供策略用例的进一步上下文。 |
| `deny` | 一个对象，它描述策略的关联营销操作被限制在其上执行的特定数据使用标签。 有关此属性的 [详细信息](#create-policy) ，请参阅创建策略一节。 |

## 查找策略 {#look-up}

通过在GET请求路径中包含该策略的属 `id` 性，可以查找特定策略。

**API格式**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 要 `id` 查看的策略。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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
| `status` | 策略的当前状态。 有三种可能的状态： `DRAFT`、 `ENABLED`或 `DISABLED`。 默认情况下，只 `ENABLED` 有策略参与评估。 See the overview on [policy evaluation](../enforcement/overview.md) for more information. |
| `marketingActionRefs` | 列表策略所有适用营销操作的URI的数组。 |
| `description` | 可选描述，它提供策略用例的进一步上下文。 |
| `deny` | 一个对象，它描述策略的关联营销操作被限制在其上执行的特定数据使用标签。 有关此属性的 [详细信息](#create-policy) ，请参阅创建策略一节。 |

## Create a custom policy {#create-policy}

在API [!DNL Policy Service] 中，策略由以下各项定义：

* 对特定营销活动的引用
* 描述限制市场营销活动的数据使用标签的表达式

要满足后一要求，策略定义必须包含与存在数据使用标签有关的布尔表达式。 此表达式称为策略表达式。

策略表达式以属性的形式在每个 `deny` 策略定义中提供。 仅检查单个标 `deny` 签是否存在的简单对象示例如下所示：

```json
"deny": {
    "label": "C1"
}
```

但是，许多策略指定了与存在数据使用标签有关的更复杂条件。 要支持这些用例，您还可以包含布尔运算来描述策略表达式。 策略表达式对象必须包含标签或操作符和操作数，但不能同时包含这两者。 反过来，每个操作数也是策略表达式对象。

例如，为了定义禁止对存在标签的数据执行营销 `C1 OR (C3 AND C7)` 操作的策略，策略的 `deny` 属性将指定为：

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
| `operator` | 指示在同级数组中提供的标签之间的条件 `operands` 关系。 接受的值为： <ul><li>`OR`:如果数组中存在任何标签，表达式解 `operands` 析为true。</li><li>`AND`:仅当数组中的所有标签都存在时，表达式 `operands` 才解析为true。</li></ul> |
| `operands` | 对象的数组，每个对象表示单个标签或另一对和属 `operator` 性 `operands` 。 数组中存在的标签和／或操 `operands` 作会根据其同级属性的值解析为true或false `operator` 。 |
| `label` | 应用于策略的单个数据使用标签的名称。 |

可以通过向端点发出POST请求来创建新的自定义 `/policies/custom` 策略。

**API格式**

```http
POST /policies/custom
```

**请求**

以下请求会创建新策略，限制对包含标签 `exportToThirdParty` 的数据执行营销操作 `C1 OR (C3 AND C7)`。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `status` | 策略的当前状态。 有三种可能的状态： `DRAFT`、 `ENABLED`或 `DISABLED`。 默认情况下，只 `ENABLED` 有策略参与评估。 See the overview on [policy evaluation](../enforcement/overview.md) for more information. |
| `marketingActionRefs` | 列表策略所有适用营销操作的URI的数组。 市场营销操作的URI在响应中 `_links.self.href` 提供，用 [于查找营销操作](./marketing-actions.md#look-up)。 |
| `description` | 可选描述，它提供策略用例的进一步上下文。 |
| `deny` | 描述策略的关联营销操作的特定数据使用标签的策略表达式被限制为不能执行。 |

**响应**

成功的响应会返回新创建策略的详细信息，包括其详细信息 `id`。 此值是只读的，在创建策略时自动分配。

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
    "imsOrg": "{IMS_ORG}",
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
>您只能更新自定义策略。 如果要启用或禁用核心策略，请参阅更新已启 [用核心策略的列表部分](#update-enabled-core)。

您可以通过在PUT请求路径中提供现有自定义策略的ID来更新其现有自定义策略，该ID包含完整策略的更新形式的有效负荷。 换言之，PUT请求实质上重写了策略。

>[!NOTE]
>
>如果您只想更 [新策略的一个或多个字段](#patch) ，而不是覆盖策略，请参阅更新自定义策略的一部分部分。

**API格式**

```http
PUT /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 要 `id` 更新的策略的名称。 |

**请求**

在此示例中，将数据导出到第三方的条件已发生更改，现在您需要创建的策略才能在数据标签存在时拒绝 `C1 AND C5` 此营销操作。

以下请求将更新现有策略以包含新策略表达式。 请注意，由于此请求实质上重写了策略，因此所有字段都必须包含在有效负荷中，即使某些字段的值未更新也是如此。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `status` | 策略的当前状态。 有三种可能的状态： `DRAFT`、 `ENABLED`或 `DISABLED`。 默认情况下，只 `ENABLED` 有策略参与评估。 See the overview on [policy evaluation](../enforcement/overview.md) for more information. |
| `marketingActionRefs` | 列表策略所有适用营销操作的URI的数组。 市场营销操作的URI在响应中 `_links.self.href` 提供，用 [于查找营销操作](./marketing-actions.md#look-up)。 |
| `description` | 可选描述，它提供策略用例的进一步上下文。 |
| `deny` | 描述策略的关联营销操作的特定数据使用标签的策略表达式被限制为不能执行。 有关此属性的 [详细信息](#create-policy) ，请参阅创建策略一节。 |

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
    "imsOrg": "{IMS_ORG}",
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
>您只能更新自定义策略。 如果要启用或禁用核心策略，请参阅更新已启 [用核心策略的列表部分](#update-enabled-core)。

可以使用PATCH请求更新策略的特定部分。 与重写策略的PUT请求不同，PATCH请求只更新请求主体中指定的属性。 当您要启用或禁用策略时，这特别有用，因为您只需提供相应属性()及其值(`/status`或)的路`ENABLED` 径 `DISABLED`即可。

>[!NOTE]
>
>PATCH请求的有效负载遵循JSON修补程序格式。 有关已接 [受的语法的更多信息](../../landing/api-fundamentals.md) ，请参阅API基础知识指南。

API [!DNL Policy Service] 支持JSON修补 `add`操 `remove`作和， `replace`并允许您将多个更新组合到单个调用中，如以下示例所示。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 要更 `id` 新其属性的策略的名称。 |

**请求**

以下请求使用两 `replace` 个操作将策略状态 `DRAFT` 从更 `ENABLED`改为，并使用新 `description` 描述更新字段。

>[!IMPORTANT]
>
>在单个请求中发送多个PATCH操作时，将按它们在数组中的显示顺序处理它们。 确保在必要时按正确顺序发送请求。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

通过将自定义策略包含在DELETE请 `id` 求的路径中，可以删除该策略。

>[!WARNING]
>
>删除策略后，无法恢复策略。 最好先执行查 [找(GET)请求](#lookup) ，以视图策略并确认它是您要删除的正确策略。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200(OK)，且正文为空。

您可以通过再次尝试查找(GET)策略来确认删除。 如果策略已成功删除，您应收到HTTP 404（未找到）错误。

## 检索已启用的核心策略列表 {#list-enabled-core}

默认情况下，只有启用的数据使用策略才会参与评估。 您可以通过向端点发出列表请求来检索当前由您的组织启用的核心策略 `/enabledCorePolicies` GET。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回阵列下启用的核心策略的 `policyIds` 列表。

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
  "imsOrg": "{IMS_ORG}",
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

## 更新已启用核心策略的列表 {#update-enabled-core}

默认情况下，只有启用的数据使用策略才会参与评估。 通过向端点发出PUT请 `/enabledCorePolicies` 求，您可以使用一次调用来更新组织已启用核心策略的列表。

>[!NOTE]
>
>此端点只能启用或禁用核心策略。 要启用或禁用自定义策略，请参阅更新 [策略的一部分部分](#patch)。

**API格式**

```http
PUT /enabledCorePolicies
```

**请求**

以下请求根据有效负荷中提供的ID更新已启用核心策略的列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `policyIds` | 要启用的核心策略ID的列表。 未包含的任何核心策略均设置为 `DISABLED` 状态，且不会参与评估。 |

**响应**

成功的响应会返回阵列下已启用核心策略的更新 `policyIds` 列表。

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
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

定义新策略或更新现有策略后，您可以使用 [!DNL Policy Service] API测试针对特定标签或数据集的营销操作，并查看您的策略是否会按预期引发违规。 有关详细信息，请 [参阅策略评估](./evaluation.md) 端点指南。
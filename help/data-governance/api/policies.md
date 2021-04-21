---
keywords: Experience Platform；主页；热门主题；策略实施；基于API的实施；数据治理
solution: Experience Platform
title: 策略API端点
topic-legacy: developer guide
description: 数据使用策略是贵组织采用的规则，用于描述您允许或限制对Experience Platform内数据执行的营销操作的类型。 /policies端点用于与查看、创建、更新或删除数据使用策略相关的所有API调用。
exl-id: 62a6f15b-4c12-4269-bf90-aaa04c147053
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 2%

---

# 策略端点

数据使用策略是描述允许或限制您对[!DNL Experience Platform]内的数据执行的营销操作类型的规则。 [!DNL Policy Service API]中的`/policies`端点允许您以编程方式管理组织的数据使用策略。

## 入门指南

本指南中使用的API端点是[[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)的一部分。 在继续之前，请查阅[快速入门指南](getting-started.md)，了解相关文档的链接、阅读此文档中示例API调用的指南以及成功调用任何[!DNL Experience Platform] API所需标头的重要信息。

## 检索策略列表{#list}

您可以通过分别向`/policies/core`或`/policies/custom`发出GET请求来列表所有`core`或`custom`策略。

**API格式**

```http
GET /policies/core
GET /policies/custom
```

**请求**

以下请求检索由您的组织定义的自定义策略列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包括一个`children`数组，用于列表每个检索到的策略的详细信息，包括其`id`值。 您可以使用特定策略的`id`字段执行[查找](#lookup)、[update](#update)和[delete](#delete)请求。

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
| `status` | 策略的当前状态。 有三种可能的状态：`DRAFT`、`ENABLED`或`DISABLED`。 默认情况下，只有`ENABLED`策略参与评估。 有关详细信息，请参阅[策略评估](../enforcement/overview.md)的概述。 |
| `marketingActionRefs` | 一个数组，用于列表策略所有适用营销操作的URI。 |
| `description` | 提供策略用例的进一步上下文的可选描述。 |
| `deny` | 描述特定数据使用标签的对象，策略的关联营销操作被限制在其上执行。 有关此属性的详细信息，请参见[创建策略](#create-policy)一节。 |

## 查找策略{#look-up}

通过在GET请求的路径中包含该策略的`id`属性，可以查找特定策略。

**API格式**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 要查找的策略的`id`。 |

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
| `status` | 策略的当前状态。 有三种可能的状态：`DRAFT`、`ENABLED`或`DISABLED`。 默认情况下，只有`ENABLED`策略参与评估。 有关详细信息，请参阅[策略评估](../enforcement/overview.md)的概述。 |
| `marketingActionRefs` | 一个数组，用于列表策略所有适用营销操作的URI。 |
| `description` | 提供策略用例的进一步上下文的可选描述。 |
| `deny` | 描述特定数据使用标签的对象，其中策略的关联营销操作被限制在其上执行。 有关此属性的详细信息，请参见[创建策略](#create-policy)一节。 |

## 创建自定义策略{#create-policy}

在[!DNL Policy Service] API中，策略由以下内容定义：

* 对特定营销操作的引用
* 表达式，用于描述禁止对其执行营销操作的数据使用标签

为满足后一要求，策略定义必须包含关于存在数据使用标签的布尔表达式。 此表达式称为策略表达式。

策略表达式以`deny`属性的形式在每个策略定义中提供。 仅检查单个标签是否存在的简单`deny`对象的示例如下所示：

```json
"deny": {
    "label": "C1"
}
```

但是，许多策略指定了关于存在数据使用标签的更复杂的条件。 要支持这些用例，您还可以包含用于描述策略表达式的布尔运算。 策略表达式对象必须包含标签或操作符和操作数，但不能同时包含这两者。 反过来，每个操作数也是策略表达式对象。

例如，为了定义一个策略，禁止对存在`C1 OR (C3 AND C7)`标签的数据执行营销操作，策略的`deny`属性将指定为：

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
| `operator` | 指示在同级`operands`数组中提供的标签之间的条件关系。 接受的值为： <ul><li>`OR`:如果数组中存在任何标签，表达式会解 `operands` 析为true。</li><li>`AND`:该表达式仅解析为true(如果数组中的所有标 `operands` 签都存在)。</li></ul> |
| `operands` | 对象的数组，每个对象表示单个标签或`operator`和`operands`属性的额外对。 `operands`数组中存在标签和/或操作将根据其同级`operator`属性的值解析为true或false。 |
| `label` | 应用于策略的单个数据使用标签的名称。 |

可以通过向`/policies/custom`端点发出POST请求来创建新的自定义策略。

**API格式**

```http
POST /policies/custom
```

**请求**

以下请求创建了新策略，该策略限制对包含标签`C1 OR (C3 AND C7)`的数据执行营销操作`exportToThirdParty`。

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
| `status` | 策略的当前状态。 有三种可能的状态：`DRAFT`、`ENABLED`或`DISABLED`。 默认情况下，只有`ENABLED`策略参与评估。 有关详细信息，请参阅[策略评估](../enforcement/overview.md)的概述。 |
| `marketingActionRefs` | 一个数组，用于列表策略所有适用营销操作的URI。 市场营销操作的URI在[响应中的`_links.self.href`下提供，以查找营销操作](./marketing-actions.md#look-up)。 |
| `description` | 提供策略用例的进一步上下文的可选描述。 |
| `deny` | 描述策略关联营销操作的特定数据使用标签的策略表达式被限制不能对其执行。 |

**响应**

成功的响应返回新创建的策略的详细信息，包括其`id`。 此值为只读，在创建策略时自动分配。

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

## 更新自定义策略{#update}

>[!IMPORTANT]
>
>您只能更新自定义策略。 如果要启用或禁用核心策略，请参阅[更新已启用核心策略的列表的部分](#update-enabled-core)。

您可以通过在PUT请求路径中提供现有自定义策略的ID来更新现有自定义策略，该ID包含完整策略的更新形式的有效负荷。 换句话说，PUT请求实质上会重写策略。

>[!NOTE]
>
>如果您只想更新策略的一个或多个字段，而不是覆盖策略，请参阅[更新自定义策略](#patch)的一部分部分。

**API格式**

```http
PUT /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 要更新的策略的`id`。 |

**请求**

在此示例中，将数据导出到第三方的条件已更改，现在您需要创建的策略以在存在`C1 AND C5`数据标签时拒绝此营销操作。

以下请求将更新现有策略以包含新策略表达式。 请注意，由于此请求实质上会重写策略，因此所有字段都必须包含在负载中，即使某些值未更新也是如此。

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
| `status` | 策略的当前状态。 有三种可能的状态：`DRAFT`、`ENABLED`或`DISABLED`。 默认情况下，只有`ENABLED`策略参与评估。 有关详细信息，请参阅[策略评估](../enforcement/overview.md)的概述。 |
| `marketingActionRefs` | 一个数组，用于列表策略所有适用营销操作的URI。 市场营销操作的URI在[响应中的`_links.self.href`下提供，以查找营销操作](./marketing-actions.md#look-up)。 |
| `description` | 提供策略用例的进一步上下文的可选描述。 |
| `deny` | 描述策略关联营销操作的特定数据使用标签的策略表达式被限制不能对其执行。 有关此属性的详细信息，请参见[创建策略](#create-policy)一节。 |

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

## 更新自定义策略{#patch}的一部分

>[!IMPORTANT]
>
>您只能更新自定义策略。 如果要启用或禁用核心策略，请参阅[更新已启用核心策略的列表的部分](#update-enabled-core)。

可以使用PATCH请求更新策略的特定部分。 与重写策略的PUT请求不同，PATCH请求只更新在请求主体中指定的属性。 当您希望启用或禁用策略时，这特别有用，因为您只需提供相应属性(`/status`)及其值（`ENABLED`或`DISABLED`）的路径。

>[!NOTE]
>
>PATCH请求的负载遵循JSON修补程序格式。 有关已接受语法的详细信息，请参阅[API基础指南](../../landing/api-fundamentals.md)。

[!DNL Policy Service] API支持JSON修补程序操作`add`、`remove`和`replace`，并允许您将多个更新组合到单个调用中，如下例所示。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 要更新其属性的策略的`id`。 |

**请求**

以下请求使用两个`replace`操作将策略状态从`DRAFT`更改为`ENABLED`，并使用新说明更新`description`字段。

>[!IMPORTANT]
>
>在单个请求中发送多个PATCH操作时，将按它们在数组中的显示顺序进行处理。 请确保您在必要时以正确的顺序发送请求。

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

## 删除自定义策略{#delete}

可以通过将自定义策略`id`包含在DELETE请求的路径中来删除该策略。

>[!WARNING]
>
>删除后，无法恢复策略。 最好先[执行查找(GET)请求](#lookup)以视图策略并确认其是您要删除的正确策略。

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

成功的响应返回HTTP状态200(OK)，正文为空。

您可以通过尝试再次查找(GET)策略来确认删除。 如果策略已成功删除，您应收到HTTP 404（未找到）错误。

## 检索已启用核心策略{#list-enabled-core}的列表

默认情况下，只有启用的数据使用策略才会参与评估。 通过向`/enabledCorePolicies`端点发出GET请求，可以检索当前由您的组织启用的核心策略列表。

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

成功的响应返回`policyIds`阵列下启用的核心策略的列表。

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

## 更新已启用核心策略{#update-enabled-core}的列表

默认情况下，只有启用的数据使用策略才会参与评估。 通过向`/enabledCorePolicies`端点发出PUT请求，您可以使用一次调用来更新组织已启用核心策略的列表。

>[!NOTE]
>
>此端点只能启用或禁用核心策略。 要启用或禁用自定义策略，请参阅[更新策略](#patch)的一部分。

**API格式**

```http
PUT /enabledCorePolicies
```

**请求**

以下请求根据在有效负荷中提供的ID更新已启用核心策略的列表。

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
| `policyIds` | 要启用的核心策略ID的列表。 未包含的任何核心策略均设置为`DISABLED`状态，且不会参与评估。 |

**响应**

成功的响应返回`policyIds`阵列下已启用核心策略的更新列表。

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

定义新策略或更新现有策略后，您可以使用[!DNL Policy Service] API测试针对特定标签或数据集的营销操作，并查看您的策略是否按预期引发违规。 有关详细信息，请参阅[策略评估端点](./evaluation.md)上的指南。

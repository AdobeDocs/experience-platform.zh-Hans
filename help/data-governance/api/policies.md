---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 策略
topic: developer guide
translation-type: tm+mt
source-git-commit: ba9d4b31cfc3b7924879a91bd125f72159e55fc4
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 1%

---


# 策略

数据使用策略是贵组织采用的规则，用于描述您允许或限制对Experience Platform内数据执行的营销操作类型。

端点 `/policies` 用于与查看、创建、更新或删除数据使用策略相关的所有API调用。

## 列表所有策略

要视图策略列表，可以向指定发出GET请 `/policies/core` 求或 `/policies/custom` 返回指定容器的所有策略。

**API格式**

```http
GET /policies/core
GET /policies/custom
```

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

该响应包括一个“计数”，显示指定容器内策略的总数以及每个策略的详细信息(包括其 `id`)。 该字 `id` 段用于执行查找请求以视图特定策略，以及执行更新和删除操作。

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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550701472910,
            "updatedClient": "string",
            "updatedUser": "string",
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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714340335,
            "updatedClient": "string",
            "updatedUser": "string",
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

## 查找策略

每个策略都包 `id` 含一个字段，可用于请求特定策略的详细信息。 如果策 `id` 略未知，则可以使用列表(GET)请求列表特定容器（或）内的所有策略，如上`core` 一 `custom`步所示。

**API格式**

```http
GET /policies/core/{id}
GET /policies/custom/{id}
```

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应包含策略的详细信息，包括关键字段( `id` 此字段应与请求中发送的 `id` 字段相匹配)、 `name`、 `status`和 `description`，以及指向策略所基于的营销操作的引用链接(`marketingActionRefs`)。

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
    "created": 1550691551888,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 创建策略 {#create-policy}

要创建策略，必须包含包含禁止该营销操作的DULE标签表达式的营销操作。 策略定义必须包 `deny` 括属性，该属性是与DULE标签存在相关的布尔表达式。

此表达式称为 `PolicyExpression` ，是一个对象， _它包含标_ 签或 _操作符_ 和操作数，但不同时包含这两个。 反过来，每个操作数也是一个 `PolicyExpression` 对象。 例如，如果存在标签，则可能禁止向第三方导出数 `C1 OR (C3 AND C7)` 据的策略。 此表达式将指定为：

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

**API格式**

```http
POST /policies/custom
```

**请求**

```SHELL
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
          "../marketingActions/custom/exportToThirdParty"
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

**响应**

如果成功创建，您将收到HTTP状态201（已创建），响应主体将包含新创建策略的详细信息，包括其详细信 `id`息。 此值是只读的，在创建策略时自动分配。

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550691551888,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 更新策略

您可能会发现，您需要在数据使用策略创建后更新它。 这是通过对策略的PUT请求完 `id` 成的，有效负荷包括策略的更新形式。 换言之，PUT请求实质上是 _重写_ 该策略，因此机构必须包括以下示例所示的所有必需信息。

**API格式**

```http
PUT /policies/custom/{id}
```

**请求**

在此示例中，将数据导出到第三方的条件已发生更改，现在您需要创建的策略才能在数据标签存在时拒绝 `C1 AND (C3 OR C7)` 此营销操作。 您可以使用以下调用来更新现有策略。

```SHELL
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
            {
              "operator": "OR",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

**响应**

成功的更新请求返回HTTP状态200（确定），响应主体将显示更新的策略。 应 `id` 与请求 `id` 中发送的匹配。

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 更新策略的一部分

可以使用PATCH请求更新策略的特定部分。 与重写策略 _的PUT_ 请求不同，PATCH请求只更新请求主体中指定的路径。 当您要启用或禁用策略时，这特别有用，因为您只需发送要更新()的特定路径`/status`及其值(`ENABLE` 或 `DISABLE`)。

策略服务API当前支持“添加”、“替换”和“删除”PATCH操作，并允许您通过将多个更新作为对象添加到阵列中，将它们组合到单个调用中，如以下示例所示。

**API格式**

```http
PATCH /policies/custom/{id}
```

**请求**

在此示例中，我们使用“替换”操作将策略状态从“DRAFT”更改为“ENABLED”，并使用新描述更新描述字段。 我们还可以使用“delete”操作删除策略描述，然后使用“add”操作添加新的一次，从而更新描述字段，如：

```SHELL
[
    {
        "op": "remove",
        "path": "/description"
    },
    {
        "op": "add",
        "path": "/description",
        "value": "New policy description."
    }
]
```

在单个请求中发送多个PATCH操作时，请记住，这些操作将按照它们在阵列中的显示顺序进行处理，以确保在必要时按正确的顺序发送请求。

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

成功的更新请求将返回HTTP状态200（确定），响应主体将显示更新的策略（“状态”现在为“已启用”，且“描述”已更改）。 策略应 `id` 与请求中 `id` 发送的策略匹配。


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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550712163182,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## 删除策略

如果需要删除已创建的策略，可以通过向要删除的策略发出DELETE `id` 请求来执行此操作。 最好先执行查找(GET)请求，以视图策略并确认它是您要删除的正确策略。 **删除策略后，无法恢复策略。**

**API格式**

```http
DELETE /policies/custom/{id}
```

**请求**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

如果策略已成功删除，则响应正文将为空，并且HTTP状态为200（确定）。

您可以再次尝试查找(GET)策略以确认删除。 您应收到HTTP状态404（未找到）和“找不到”错误消息，因为该策略已被删除。

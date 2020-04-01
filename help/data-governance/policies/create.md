---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建数据使用策略
topic: policies
translation-type: tm+mt
source-git-commit: 04b2e07ba39df9f530c9c93c4bf1af9e2cf30169

---


# 创建数据使用策略

数据使用标签和强制执行(DULE)是Adobe Experience Platform数据管理的核心机制。 通过 [DULE Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) ，您可以创建和管理DULE策略，以确定可以对包含某些DULE标签的数据执行哪些营销操作。

本文档提供了使用策略服务API创建DULE策略的分步教程。 有关API中可用的不同操作的更全面的指南，请参阅策略服务开 [发人员指南](../api/getting-started.md)。

## 入门指南

本教程需要对创建和评估DULE策略时涉及的下列主要概念有充分的了解：

* [数据管理](../home.md):平台执行数据使用合规性的框架。
* [数据使用标签](../labels/overview.md):数据使用标签应用于XDM数据字段，为访问该数据的方式指定限制。
* [体验数据模型(XDM)](../../xdm/home.md):平台通过标准化框架组织客户体验数据。
* [沙箱](../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

在开始本教程之前，请查看开发人员指 [南](../api/getting-started.md) ，了解成功调用DULE Policy Service API需要了解的重要信息，包括必需的标题以及如何读取示例API调用。

## 定义营销活动 {#define-action}

在数据管理框架中，营销操作是Experience Platform数据消费者采取的操作，需要检查是否存在违反数据使用策略的情况。

创建DULE策略的第一步是确定策略将评估的营销操作。 可以使用以下选项之一执行此操作：

* [查找现有营销活动](#look-up)
* [创建新的营销操作](#create-new)

### 查找现有营销活动 {#look-up}

您可以通过向其中一个端点发出GET请求来查找要由DULE策略评估的现有营销 `/marketingActions` 操作。

**API格式**

根据您查找的是Experience Platform提供的营销活动还是组织创建的自定义营销活动，请分别使 `marketingActions/core` 用或 `marketingActions/custom` 端点。

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**请求**

以下请求使用端 `marketingActions/custom` 点，端点可获取由IMS组织定义的所有营销操作的列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回找到(`count`)的营销操作总数，并列表阵列中营销操作本身的详细 `children` 信息。

```json
{
    "_page": {
        "start": "sampleMarketingAction",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550714012088,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714012088,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550793833224,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `_links.self.href` | 数组中的每个项 `children` 目都包含列出的营销操作的URI ID。 |

当您找到要使用的营销活动时，请记录其属性的 `href` 值。 此值将在创建DULE策略的下 [一步中使用](#create-policy)。

### 创建新的营销操作 {#create-new}

您可以通过向端点发出PUT请求并在请求路径的末尾 `/marketingActions/custom/` 提供营销操作的名称来创建新的营销操作。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要创建的新营销操作的名称。 此名称用作营销活动的主要标识符，因此必须是唯一的。 最佳实践是为营销操作提供一个描述性但简明的名称。 |

**请求**

以下请求创建一个名为“exportToThirdParty”的新自定义营销操作。 请注意，请 `name` 求有效负荷中的名称与请求路径中提供的名称相同。

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 要创建的营销操作的名称。 此名称必须与请求路径中提供的名称匹配，否则将发生400（错误请求）错误。 |
| `description` | 营销操作的可读描述。 |

**响应**

成功的响应会返回HTTP状态201（已创建）和新创建的营销操作的详细信息。

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1550713856390,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        }
    }
}
```

| 属性 | 描述 |
| --- | --- |
| `_links.self.href` | 营销操作的URI ID。 |

记录新创建的营销操作的URI ID，就像在创建DULE策略的下一步中使用它一样。

## 创建DULE策略 {#create-policy}

创建新策略要求您提供营销操作的URI ID，并表达式禁止该营销操作的DULE标签。

此表达式称为策 **略表达式** ，是包含(A)DULE标签或(B)操作符和操作数的对象，但不同时包含两者。 反过来，每个操作数也是策略表达式对象。 例如，如果存在标签，则可能禁止向第三方导出数 `C1 OR (C3 AND C7)` 据的策略。 此表达式将指定为：

```json
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
}
```

>[!NOTE] 仅支持OR和AND运算符。

配置策略表达式后，您可以通过向端点发出POST请求来创建新的DULE策 `/policies/custom` 略。

**API格式**

```http
POST /policies/custom
```

**请求**

以下请求通过在请求有效负荷中提供营销操作和策略表达式来创建名为“将数据导出到第三方”的DULE策略。

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

| 属性 | 描述 |
| --- | --- |
| `marketingActionRefs` | 包含在上一步 `href` 中获取的营销操作值的数 [组](#define-action)。 虽然上述示例仅列表一个营销操作，但也可以提供多个操作。 |
| `deny` | 策略表达式对象。 定义DULE标签和条件，它们会导致策略拒绝中引用的营销操作 `marketingActionRefs`。 |

**响应**

成功的响应会返回HTTP状态201（已创建）和新创建策略的详细信息。

```json
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1565651746693,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 唯一标识DULE策略的只读、系统生成的值。 |

记录新创建的DULE策略的URI ID，就像在下一步中用于启用策略一样。

## 启用DULE策略

>[!NOTE] 如果您希望将DULE策略保留为状态，则此步骤是可选的，但请注意，默认情况下，策略必须将其状态设置为 `DRAFT``ENABLED` ，才能参与评估。 有关如何为处于状 [态的策略设置例外](../enforcement/api-enforcement.md) ，请参阅有关强制实施DULE策略的教程 `DRAFT` 。

默认情况下，将其属性设置为 `status` 不参与评 `DRAFT` 估的DULE策略。 您可以通过向端点发出PATCH请求并在请求路径的末尾提供策略的唯一标识符来启用策略 `/policies/custom/` 以进行评估。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 要 `id` 启用的策略的值。 |

**请求**

以下请求对DULE策略的属性执 `status` 行PATCH操作，将其值从更改为 `DRAFT` 值 `ENABLED`。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    {
      "op": "replace",
      "path": "/status",
      "value": "ENABLED"
    }
  ]'
```

| 属性 | 描述 |
| --- | --- |
| `op` | 要执行的PATCH操作的类型。 此请求执行“替换”操作。 |
| `path` | 要更新的字段的路径。 启用策略时，必须将值设置为“/status”。 |
| `value` | 要分配给中指定属性的新值 `path`。 此请求将策略的属 `status` 性设置为“ENABLED”。 |

**响应**

成功的响应会返回HTTP状态200(OK)和更新策略的详细信息，其现 `status` 在设置为 `ENABLED`。

```json
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
    "created": 1565651746693,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER}",
    "updated": 1565723012139,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

## 后续步骤

通过遵循本教程，您已成功为营销操作创建了DULE策略。 您现在可以继续阅读关于强制 [实施DULE策略的教程](../enforcement/api-enforcement.md) ，了解如何检查策略违规并在体验应用程序中处理这些违规。

有关Policy Service API中不同可用操作的详细信息，请参阅 [Policy Service开发人员指南](../api/getting-started.md)。 有关如何为实时客户用户档案数据实施DULE策略的信息，请参阅关于为受众细分强制实 [施数据使用合规性的教程](../../segmentation/tutorials/governance.md)。
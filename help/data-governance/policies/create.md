---
keywords: Experience Platform；主页；热门主题；数据管理；数据使用策略
solution: Experience Platform
title: 在API中创建数据管理策略
type: Tutorial
description: 了解如何使用策略服务API创建数据管理策略。
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 2%

---

# 在API中创建数据治理策略

[策略服务API](https://www.adobe.io/experience-platform-apis/references/policy-service/)允许您创建和管理数据治理策略，以确定可以对包含特定数据使用标签的数据执行哪些营销操作。

此文档提供了使用[!DNL Policy Service] API创建治理策略的分步教程。

>[!NOTE]
>
>有关如何创建访问控制策略的步骤，请参阅[访问控制API](../../access-control/abac/api/policies.md)的`/policies`端点指南。 要了解如何创建同意策略，请参阅[策略UI指南](./user-guide.md#consent-policy)。

## 快速入门

本教程需要对创建和评估策略所涉及的以下关键概念有一定的了解：

* [Adobe Experience Platform数据管理](../home.md)： [!DNL Experience Platform]强制数据使用合规性的框架。
   * [数据使用标签](../labels/overview.md)：数据使用标签应用于XDM数据字段，指定访问数据的方式限制。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
* [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

在开始本教程之前，请查看[开发人员指南](../api/getting-started.md)以了解成功调用[!DNL Policy Service] API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

## 定义营销活动 {#define-action}

在数据管理框架中，营销操作是[!DNL Experience Platform]数据使用者采取的操作，需要检查是否存在违反数据使用策略的操作。

创建数据使用策略的第一步是确定策略将评估什么营销操作。 可以使用以下选项之一完成此操作：

* [查找现有营销操作](#look-up)
* [创建新的营销操作](#create-new)

### 查找现有营销操作 {#look-up}

通过向`/marketingActions`个端点之一发出GET请求，您可以查找要由策略评估的现有营销操作。

**API格式**

根据您要查找由[!DNL Experience Platform]提供的营销操作还是由您的组织创建的自定义营销操作，分别使用`marketingActions/core`或`marketingActions/custom`端点。

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**请求**

以下请求使用`marketingActions/custom`端点，该端点获取由您的组织定义的所有营销操作的列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回找到的营销操作总数(`count`)，并列出`children`数组中营销操作本身的详细信息。

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `_links.self.href` | `children`数组中的每一项都包含所列出营销操作的URI ID。 |

找到要使用的营销操作后，记录其`href`属性的值。 此值在[创建策略](#create-policy)的下一个步骤中使用。

### 创建新的营销操作 {#create-new}

您可以通过向`/marketingActions/custom/`端点发出PUT请求并在请求路径末尾提供营销操作的名称来创建新的营销操作。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要创建的新营销操作的名称。 此名称用作营销操作的主要标识符，因此必须是唯一的。 最佳实践是为营销操作提供一个描述性但简洁的名称。 |

**请求**

以下请求创建新的自定义营销操作，称为“exportToThirdParty”。 请注意，请求有效负载中的`name`与请求路径中提供的名称相同。

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `description` | 易于用户识别的营销操作描述。 |

**响应**

成功的响应会返回HTTP状态201（已创建）以及新创建的营销操作的详细信息。

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{ORG_ID}",
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
| `_links.self.href` | 营销活动的URI ID。 |

记录新创建的营销操作的URI ID，因为它将在创建策略的下一个步骤中使用。

## 创建策略 {#create-policy}

创建新策略需要您提供营销活动的URI ID，以及禁止该营销活动的使用标签的表达式。

此表达式称为策略表达式，它是包含(A)标签或(B)运算符和操作数的对象，但不能同时包含两者。 反过来，每个操作数也是策略表达式对象。 例如，如果存在`C1 OR (C3 AND C7)`标签，则可能禁止将数据导出到第三方的策略。 此表达式将指定为：

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

>[!NOTE]
>
>仅支持OR和AND运算符。

配置策略表达式后，您可以通过向`/policies/custom`端点发出POST请求来创建新策略。

**API格式**

```http
POST /policies/custom
```

**请求**

以下请求通过在请求有效负荷中提供营销操作和策略表达式，创建名为“将数据导出到第三方”的策略。

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
| `marketingActionRefs` | 一个数组，其中包含在[上一步](#define-action)中获取的营销操作的`href`值。 虽然上述示例仅列出一个营销操作，但也可以提供多个操作。 |
| `deny` | 策略表达式对象。 定义将导致策略拒绝`marketingActionRefs`中引用的营销操作的使用标签和条件。 |

**响应**

成功的响应返回HTTP状态201（已创建）和新创建策略的详细信息。

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
    "imsOrg": "{ORG_ID}",
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
| `id` | 系统生成的只读值，用于唯一标识策略。 |

记录新创建策略的URI ID，以便在下一个步骤中启用该策略。

## 启用策略

>[!NOTE]
>
>虽然如果您希望将策略保留为`DRAFT`状态，则此步骤是可选的，但请注意，默认情况下，策略必须将其状态设置为`ENABLED`才能参与评估。 有关如何为处于`DRAFT`状态的策略创建异常的信息，请参阅[策略实施](../enforcement/api-enforcement.md)指南。

默认情况下，`status`属性设置为`DRAFT`的策略不参与评估。 您可以通过向`/policies/custom/`端点发出PATCH请求并在请求路径末尾提供策略的唯一标识符来启用策略以供评估。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 要启用的策略的`id`值。 |

**请求**

以下请求对策略的`status`属性执行PATCH操作，将其值从`DRAFT`更改为`ENABLED`。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | 要更新的字段的路径。 启用策略时，必须将该值设置为“/status”。 |
| `value` | 要分配给`path`中指定的属性的新值。 此请求将策略的`status`属性设置为“ENABLED”。 |

**响应**

成功的响应返回HTTP状态200 （正常）以及已更新策略的详细信息，其`status`现在设置为`ENABLED`。

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
    "imsOrg": "{ORG_ID}",
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

通过学习本教程，您已成功为营销操作创建了数据使用策略。 您现在可以继续学习有关[实施数据使用策略](../enforcement/api-enforcement.md)的教程，以了解如何检查策略违规并在体验应用程序中处理这些违规。

有关[!DNL Policy Service] API中不同可用操作的详细信息，请参阅[策略服务开发人员指南](../api/getting-started.md)。 有关如何实施[!DNL Real-Time Customer Profile]数据策略的信息，请参阅有关[实施受众区段的数据使用合规性的教程](../../segmentation/tutorials/governance.md)。

要了解如何在[!DNL Experience Platform]用户界面中管理使用策略，请参阅[策略用户指南](user-guide.md)。

---
keywords: Experience Platform；主页；热门主题；数据管理；数据使用策略
solution: Experience Platform
title: 在API中创建数据使用策略
topic-legacy: policies
type: Tutorial
description: 策略服务API允许您创建和管理数据使用策略，以确定可以对包含某些数据使用标签的数据执行哪些营销操作。 本文档提供了使用策略服务API创建策略的分步教程。
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 2%

---

# 在API中创建数据使用策略

的 [策略服务API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 允许您创建和管理数据使用策略，以确定可以对包含某些数据使用标签的数据执行哪些营销操作。

本文档提供了使用 [!DNL Policy Service] API。 有关API中可用的不同操作的更全面指南，请参阅 [策略服务开发人员指南](../api/getting-started.md).

## 快速入门

本教程需要对创建和评估策略时涉及的以下关键概念有一定的了解：

* [Adobe Experience Platform数据管理](../home.md):框架 [!DNL Platform] 强制实施数据使用合规性。
   * [数据使用标签](../labels/overview.md):数据使用标签会应用于XDM数据字段，从而指定如何访问该数据的限制。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

在启动本教程之前，请查看 [开发人员指南](../api/getting-started.md) 以了解成功调用 [!DNL Policy Service] API，包括所需的标头以及如何读取示例API调用。

## 定义营销操作 {#define-action}

在“数据管理”框架中，营销操作是指 [!DNL Experience Platform] 数据使用者，需要检查其是否违反了数据使用策略。

创建数据使用策略的第一步是确定该策略将评估的营销操作。 可以使用以下选项之一完成此操作：

* [查找现有营销操作](#look-up)
* [创建新营销操作](#create-new)

### 查找现有营销操作 {#look-up}

您可以通过向 `/marketingActions` 端点。

**API格式**

根据您是否查找 [!DNL Experience Platform] 或您的组织创建的自定义营销操作，请使用 `marketingActions/core` 或 `marketingActions/custom` 端点。

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**请求**

以下请求使用 `marketingActions/custom` 端点，可获取由IMS组织定义的所有营销操作的列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回找到的营销操作总数(`count`)，并列出 `children` 数组。

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
| `_links.self.href` | 中的每个项目 `children` 数组包含列出的营销操作的URI ID。 |

当您找到要使用的营销操作时，记录其值 `href` 属性。 此值将在 [创建策略](#create-policy).

### 创建新营销操作 {#create-new}

您可以通过向 `/marketingActions/custom/` 端点，并在请求路径的末尾为营销操作提供名称。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要创建的新营销操作的名称。 此名称用作营销操作的主要标识符，因此必须是唯一的。 最佳实践是为营销操作提供一个描述性但简洁的名称。 |

**请求**

以下请求会创建一个名为“exportToThirdParty”的新自定义营销操作。 请注意， `name` 请求有效负载中的名称与请求路径中提供的名称相同。

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
| `name` | 要创建的营销操作的名称。 此名称必须与请求路径中提供的名称匹配，否则将发生400（请求错误）错误。 |
| `description` | 可供用户读取的营销操作描述。 |

**响应**

成功响应会返回HTTP状态201（已创建）以及新创建营销操作的详细信息。

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
| `_links.self.href` | 营销操作的URI ID。 |

记录新创建营销操作的URI ID，因为它将在创建策略的下一步中使用。

## 创建策略 {#create-policy}

创建新策略要求您提供营销操作的URI ID以及禁止该营销操作的使用标签的表达式。

此表达式称为策略表达式，是包含(A)标签或(B)运算符和操作数（但不同时包含这两者）的对象。 反过来，每个操作数也是策略表达式对象。 例如，在以下情况下，可能会禁止有关向第三方出口数据的政策 `C1 OR (C3 AND C7)` 标签存在。 此表达式将指定为：

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

配置策略表达式后，您可以通过向 `/policies/custom` 端点。

**API格式**

```http
POST /policies/custom
```

**请求**

以下请求通过在请求有效负载中提供营销操作和策略表达式，创建一个名为“将数据导出到第三方”的策略。

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
| `marketingActionRefs` | 包含 `href` 营销操作的值，在 [上一步](#define-action). 虽然上例仅列出一个营销操作，但也可以提供多个操作。 |
| `deny` | 策略表达式对象。 定义导致策略拒绝 `marketingActionRefs`. |

**响应**

成功响应会返回HTTP状态201（已创建）以及新创建策略的详细信息。

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
| `id` | 唯一标识策略的只读、系统生成的值。 |

记录新创建策略的URI ID，因为该ID将在下一步中用于启用策略。

## 启用策略

>[!NOTE]
>
>如果您希望在 `DRAFT` 状态，请注意，默认情况下，策略的状态必须设置为 `ENABLED` 以参与评价。 请参阅 [策略实施](../enforcement/api-enforcement.md) 有关如何在 `DRAFT` 状态。

默认情况下， `status` 属性设置为 `DRAFT` 不参与评价。 您可以通过向 `/policies/custom/` 端点和在请求路径末尾提供策略的唯一标识符。

**API格式**

```http
PATCH /policies/custom/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{POLICY_ID}` | 的 `id` 要启用的策略的值。 |

**请求**

以下请求对 `status` 属性，从 `DRAFT` to `ENABLED`.

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
| `path` | 要更新的字段的路径。 启用策略时，必须将值设置为“/status”。 |
| `value` | 要分配给中指定属性的新值 `path`. 此请求将设置策略的 `status` 属性更改为“ENABLED”。 |

**响应**

成功响应会返回HTTP状态200(OK)以及更新策略的详细信息，以及 `status` 现在设置为 `ENABLED`.

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

通过阅读本教程，您已成功为营销操作创建了数据使用策略。 您现在可以继续阅读 [强制实施数据使用策略](../enforcement/api-enforcement.md) 了解如何检查是否存在策略违规，并在您的体验应用程序中处理这些违规。

有关 [!DNL Policy Service] API，请参阅 [策略服务开发人员指南](../api/getting-started.md). 有关如何执行 [!DNL Real-time Customer Profile] 数据，请参阅 [为受众区段强制实施数据使用合规性](../../segmentation/tutorials/governance.md).

了解如何在 [!DNL Experience Platform] 用户界面，请参阅 [策略用户指南](user-guide.md).

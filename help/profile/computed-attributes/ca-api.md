---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 计算属性API端点
topic-legacy: guide
type: Documentation
description: 在Adobe Experience Platform中，计算属性是用于将事件级别数据聚合到配置文件级别属性中的函数。 这些函数会自动计算，以便在分段、激活和个性化期间使用。 本指南演示了如何使用实时客户配置文件API创建、查看、更新和删除计算属性。
exl-id: 6b35ff63-590b-4ef5-ab39-c36c39ab1d58
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2275'
ht-degree: 2%

---

# (Alpha)计算属性API端点

>[!IMPORTANT]
>
>本文档中概述的计算属性功能当前位于alpha中，并非所有用户都可用。 文档和功能可能会发生变化。

计算属性是用于将事件级别数据聚合到配置文件级别属性中的函数。 这些函数会自动计算，以便在分段、激活和个性化期间使用。 本指南包含使用执行基本CRUD操作的示例API调用 `/computedAttributes` 端点。

要了解有关计算属性的更多信息，请首先阅读 [计算属性概述](overview.md).

## 快速入门

本指南中使用的API端点是 [实时客户资料API](https://www.adobe.com/go/profile-apis-en).

在继续之前，请查看 [配置文件API快速入门指南](../api/getting-started.md) 有关推荐文档的链接，请参阅本文档中显示的示例API调用指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

## 配置计算属性字段

要创建计算属性，您首先需要在架构中标识将包含计算属性值的字段。

请参阅 [配置计算属性](configure-api.md) 有关在架构中创建计算属性字段的完整端到端指南。

>[!WARNING]
>
>要继续阅读API指南，您必须配置一个计算属性字段。

## 创建计算属性 {#create-a-computed-attribute}

现在，通过在启用配置文件的架构中定义计算属性字段，可以配置计算属性。 如果您尚未执行此操作，请按照 [配置计算属性](configure-api.md) 文档。

要创建计算属性，请首先向 `/config/computedAttributes` 终结点，其请求正文包含您要创建的计算属性的详细信息。

**API格式**

```http
POST /config/computedAttributes
```

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "birthdayCurrentMonth",
        "path": "_{TENANT_ID}",
        "description": "Computed attribute to capture if the customer birthday is in the current month.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| 属性 | 描述 |
|---|---|
| `name` | 作为字符串的计算属性字段的名称。 |
| `path` | 包含计算属性的字段的路径。 此路径可在 `properties` 属性，且不应在路径中包含字段名称。 写入路径时，请忽略 `properties` 属性。 |
| `{TENANT_ID}` | 如果您不熟悉租户ID，请参阅 [架构注册开发人员指南](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | 计算属性的描述。 在定义了多个计算属性后，此功能特别有用，因为它将帮助IMS组织内的其他人确定要使用的正确计算属性。 |
| `expression.value` | 有效 [!DNL Profile Query Language] (PQL)表达式。 计算属性当前支持以下函数：sum、count、min、max和boolean。 有关示例表达式的列表，请参阅 [示例PQL表达式](expressions.md) 文档。 |
| `schema.name` | 包含计算属性字段的架构所基于的类。 示例： `_xdm.context.experienceevent` ，用于基于XDM ExperienceEvent类的架构。 |

**响应**

成功创建的计算属性会返回HTTP状态200（确定）和包含新创建计算属性详细信息的响应主体。 这些详细信息包括系统生成的唯一只读 `id` ，可用于在其他API操作期间引用计算属性。

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| 属性 | 描述 |
|---|---|
| `id` | 唯一的只读系统生成的ID，可用于在其他API操作期间引用计算的属性。 |
| `imsOrgId` | 与计算属性相关的IMS组织应与请求中发送的值匹配。 |
| `sandbox` | 沙盒对象包含在其中配置计算属性的沙盒的详细信息。 此信息来自请求中发送的沙盒标头。 有关详细信息，请参阅 [沙箱概述](../../sandboxes/home.md). |
| `positionPath` | 包含被解构的数组 `path` 到请求中发送的字段。 |
| `returnSchema.meta:xdmType` | 存储计算属性的字段类型。 |
| `definedOn` | 一个数组，用于显示已定义计算属性的并集架构。 每个并集架构包含一个对象，这意味着如果计算的属性已基于不同类添加到多个架构，则数组中可能有多个对象。 |
| `active` | 一个布尔值，用于显示计算的属性当前是否处于活动状态。 默认情况下，值为 `true`. |
| `type` | 创建的资源类型，在此例中，“ComputedAttribute”是默认值。 |
| `createEpoch` 和 `updateEpoch` | 分别创建和上次更新计算属性的时间。 |

## 创建引用现有计算属性的计算属性

也可以创建引用现有计算属性的计算属性。 为此，请首先向 `/config/computedAttributes` 端点。 请求正文将包含对 `expression.value` 字段，如以下示例中所示。

**API格式**

```http
POST /config/computedAttributes
```

**请求**

在此示例中，已创建两个计算属性，将用于定义第三个属性。 现有的计算属性包括：

* **`totalSpend`:** 捕获客户已花费的总美元金额。
* **`countPurchases`:** 计算客户的购买次数。

以下请求引用两个现有的计算属性，使用有效的PQL进行除以计算新属性 `averageSpend` 计算属性。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "averageSpend",
        "path": "_{TENANT_ID}.purchaseSummary",
        "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| 属性 | 描述 |
|---|---|
| `name` | 作为字符串的计算属性字段的名称。 |
| `path` | 包含计算属性的字段的路径。 此路径可在 `properties` 属性，且不应在路径中包含字段名称。 写入路径时，请忽略 `properties` 属性。 |
| `{TENANT_ID}` | 如果您不熟悉租户ID，请参阅 [架构注册开发人员指南](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | 计算属性的描述。 在定义了多个计算属性后，此功能特别有用，因为它将帮助IMS组织内的其他人确定要使用的正确计算属性。 |
| `expression.value` | 有效的PQL表达式。 计算属性当前支持以下函数：sum、count、min、max和boolean。 有关示例表达式的列表，请参阅 [示例PQL表达式](expressions.md) 文档。<br/><br/>在此示例中，表达式引用了两个现有的计算属性。 属性使用 `path` 和 `name` 中显示的计算属性，在其中定义了计算属性的架构中。 例如， `path` 第一个引用的计算属性的 `_{TENANT_ID}.purchaseSummary` 和 `name` is `totalSpend`. |
| `schema.name` | 包含计算属性字段的架构所基于的类。 示例： `_xdm.context.experienceevent` ，用于基于XDM ExperienceEvent类的架构。 |

**响应**

成功创建的计算属性会返回HTTP状态200（确定）和包含新创建计算属性详细信息的响应主体。 这些详细信息包括系统生成的唯一只读 `id` ，可用于在其他API操作期间引用计算属性。

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "averageSpend",
    "path": "_{TENANT_ID}.purchaseSummary",
    "positionPath": [
        "_{TENANT_ID}",
        "purchaseSummary"
    ],
    "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
    "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "number"
    },
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"\bVR)JMSR())(+KLOJKկHO+I(/(OI/S8{E:",
    "dependencies": [
        "c08a92f3-2418-4a3d-89d0-96f15fda3e5d",
        "4ed9e3aa-57ae-4705-9e8a-7fba9a6a7010"
    ],
    "dependents": [],
    "active": true,
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
      },
    "type": "ComputedAttribute",
    "createEpoch": 1613696592,
    "updateEpoch": 1613696593
}
```

| 属性 | 描述 |
|---|---|
| `id` | 唯一的只读系统生成的ID，可用于在其他API操作期间引用计算的属性。 |
| `imsOrgId` | 与计算属性相关的IMS组织应与请求中发送的值匹配。 |
| `sandbox` | 沙盒对象包含在其中配置计算属性的沙盒的详细信息。 此信息来自请求中发送的沙盒标头。 有关详细信息，请参阅 [沙箱概述](../../sandboxes/home.md). |
| `positionPath` | 包含被解构的数组 `path` 到请求中发送的字段。 |
| `returnSchema.meta:xdmType` | 存储计算属性的字段类型。 |
| `definedOn` | 一个数组，用于显示已定义计算属性的并集架构。 每个并集架构包含一个对象，这意味着如果计算的属性已基于不同类添加到多个架构，则数组中可能有多个对象。 |
| `active` | 一个布尔值，用于显示计算的属性当前是否处于活动状态。 默认情况下，值为 `true`. |
| `type` | 创建的资源类型，在此例中，“ComputedAttribute”是默认值。 |
| `createEpoch` 和 `updateEpoch` | 分别创建和上次更新计算属性的时间。 |

## 访问计算属性

使用API处理计算属性时，有两个选项可用于访问您的组织已定义的计算属性。 第一个是列出所有计算属性，第二个是通过其唯一性查看特定计算属性 `id`.

本文档概述了两种访问模式的步骤。 选择以下选项之一开始：

* **[列出所有现有的计算属性](#list-all-computed-attributes):** 返回您的组织已创建的所有现有计算属性的列表。
* **[查看特定的计算属性](#view-a-computed-attribute):** 在请求期间通过指定单个计算属性的ID来返回其详细信息。

### 列出所有计算属性 {#list-all-computed-attributes}

您的IMS组织可以创建多个计算属性，并对 `/config/computedAttributes` 端点允许您列出组织的所有现有计算属性。

**API格式**

```http
GET /config/computedAttributes
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应包括 `_page` 提供计算属性总数的属性(`totalCount`)以及页面上计算属性的数量(`pageSize`)。

响应还包括 `children` 由一个或多个对象组成的数组，每个对象包含一个计算属性的详细信息。 如果贵组织没有任何计算属性，则 `totalCount` 和 `pageSize` 将为0（零），并且 `children` 数组将为空。

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type": "PQL", 
                "format": "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| 属性 | 描述 |
|---|---|
| `_page.totalCount` | 由IMS组织定义的计算属性总数。 |
| `_page.pageSize` | 在此结果页面上返回的计算属性数。 如果 `pageSize` 等于 `totalCount`，这意味着只有一个结果页且返回了所有计算属性。 如果不等于，则可以访问其他的结果页面。 请参阅 `_links.next` 以了解详细信息。 |
| `children` | 由一个或多个对象组成的数组，每个对象包含单个计算属性的详细信息。 如果尚未定义计算属性，则 `children` 数组为空。 |
| `id` | 创建时自动分配给计算属性的唯一只读系统生成值。 有关计算属性对象的组件的更多信息，请参阅 [创建计算属性](#create-a-computed-attribute) 在本教程的前面部分。 |
| `_links.next` | 如果返回单页计算属性， `_links.next` 是空对象，如上面的示例响应中所示。 如果贵组织具有许多计算属性，则会在多个页面上返回这些属性，您可以通过向发出GET请求来访问这些属性 `_links.next` 值。 |

### 查看计算属性 {#view-a-computed-attribute}

您可以通过向 `/config/computedAttributes` 端点，并在请求路径中包含计算的属性ID。

**API格式**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| 参数 | 描述 |
|---|---|
| `{ATTRIBUTE_ID}` | 要查看的计算属性的ID。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## 更新计算属性

如果您发现需要更新现有的计算属性，可以通过向 `/config/computedAttributes` 端点，并包括您希望在请求路径中更新的计算归因的ID。

**API格式**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| 参数 | 描述 |
|---|---|
| `{ATTRIBUTE_ID}` | 要更新的计算属性的ID。 |

**请求**

此请求使用 [JSON修补程序格式](https://datatracker.ietf.org/doc/html/rfc6902) 更新“expression”字段的“value”。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type": "PQL", 
            "format": "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| 属性 | 描述 |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | 有效 [!DNL Profile Query Language] (PQL)表达式。 计算属性当前支持以下函数：sum、count、min、max和boolean。 有关示例表达式的列表，请参阅 [示例PQL表达式](expressions.md) 文档。 |

**响应**

成功的更新会返回HTTP状态204（无内容）和空的响应正文。 如果要确认更新成功，可以执行GET请求以按其ID查看计算的属性。

## 删除计算属性

也可以使用API删除计算的属性。 这是通过向 `/config/computedAttributes` 端点，包括您希望在请求路径中删除的计算属性的ID。

>[!NOTE]
>
>删除计算属性时请务必谨慎，因为该属性可能正在多个架构中使用，并且DELETE操作无法撤消。

**API格式**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| 参数 | 描述 |
|---|---|
| `{ATTRIBUTE_ID}` | 要删除的计算属性的ID。 |

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**响应**

成功的删除请求会返回HTTP状态200（确定）和空的响应正文。 要确认删除成功，您可以执行GET请求以按其ID查找计算的属性。 如果删除了属性，您将收到“HTTP状态404（未找到）”错误。

## 创建引用计算属性的区段定义

Adobe Experience Platform允许您从一组用户档案创建用于定义一组特定属性或行为的区段。 区段定义包括封装在PQL中写入的查询的表达式。 这些表达式还可以引用计算属性。

以下示例创建引用现有计算属性的区段定义。 要详细了解区段定义以及如何在分段服务API中使用这些定义，请参阅 [区段定义API端点指南](../../segmentation/api/segment-definitions.md).

要开始，请向 `/segment/definitions` 端点，在请求正文中提供计算属性。

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
        "name": "downloadedInLast7Days",
        "description": "Has product been downloaded in last 7 days?",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "ttlInDays": 30,
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "_{TENANT_ID}.downloadsLast7Days > 0",
            "meta": "m"
        },
        "dataGovernancePolicy": {
            "excludeOptOut": true
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 区段的唯一名称，以字符串形式表示。 |
| `description` | 定义的人类可读描述。 |
| `schema.name` | 与区段中的实体关联的架构。 由 `id` 或 `name` 字段。 |
| `expression` | 包含字段的对象，其中包含有关区段定义的信息。 |
| `expression.type` | 指定表达式类型。 目前仅支持“PQL”。 |
| `expression.format` | 指示值中表达式的结构。 目前，仅 `pql/text` 支持。 |
| `expression.value` | 有效的PQL表达式，在此示例中，它包括对现有计算属性的引用。 |

有关架构定义属性的更多信息，请参阅 [区段定义API端点指南](../../segmentation/api/segment-definitions.md).

**响应**

成功响应会返回HTTP状态200，其中包含新创建的区段定义的详细信息。 要了解有关区段定义响应对象的更多信息，请参阅 [区段定义API端点指南](../../segmentation/api/segment-definitions.md).

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "segment-downloadedInLast7Days",
    "description": "Has product been downloaded in last 7 days?",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "_{TENANT_ID}.downloadsLast7Days > 0",
        "meta": "m"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1602016581000,
    "updateEpoch": 1610609459,
    "updateTime": 1610609459000,
    "createEpoch": 1602016554,
    "_etag": "\"8b01611a-0000-0200-0000-5ffff3330000\"",
    "dependents": [
        "023d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [
    "103d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "type": "SegmentDefinition"
}
```

## 后续步骤

现在，您已学习了计算属性的基础知识，接下来便可以开始为您的组织定义这些属性。

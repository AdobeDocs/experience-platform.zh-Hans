---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API
title: 计算属性API端点
topic: 指南
type: 文档
description: 在Adobe Experience Platform中，计算属性是用于将事件级数据聚合为用户档案级属性的函数。 这些函数会自动计算，以便能够跨细分、激活和个性化使用。 本指南说明如何使用实时客户用户档案API创建、视图、更新和删除计算属性。
translation-type: tm+mt
source-git-commit: 6ae96ab25bd7992fe93d15bfc16b58a2fe7b4b7c
workflow-type: tm+mt
source-wordcount: '2279'
ht-degree: 2%

---


# (Alpha)计算属性API端点

>[!IMPORTANT]
>
>此文档中概述的计算属性功能当前位于alpha中，并非所有用户都可用。 文档和功能可能会发生变化。

计算属性是用于将事件级数据聚合为用户档案级属性的函数。 这些函数会自动计算，以便能够跨细分、激活和个性化使用。 本指南包含使用`/computedAttributes`端点执行基本CRUD操作的示例API调用。

要了解有关计算属性的详细信息，请首先阅读[计算属性概述](overview.md)。

## 入门指南

本指南中使用的API端点是[实时客户用户档案API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)的一部分。

在继续之前，请查看[用户档案 API快速入门指南](../api/getting-started.md)，了解指向推荐文档的链接、阅读此文档中显示的示例API调用的指南以及成功调用任何Experience Platform API所需标头的重要信息。

## 配置计算属性字段

要创建计算属性，您首先需要在包含计算属性值的模式中标识字段。

有关在模式中创建计算属性字段的完整端到端指南，请参阅有关[配置计算属性](configure-api.md)的文档。

>[!WARNING]
>
>要继续使用API指南，您必须配置了计算属性字段。

## 创建计算属性{#create-a-computed-attribute}

在启用用户档案的模式中定义计算属性字段后，您现在可以配置计算属性。 如果尚未执行此操作，请按照[配置计算属性](configure-api.md)文档中概述的工作流进行操作。

要创建计算属性，首先向`/config/computedAttributes`端点发出POST请求，请求主体包含要创建的计算属性的详细信息。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| 属性 | 描述 |
|---|---|
| `name` | 计算的属性字段的名称，作为字符串。 |
| `path` | 包含计算属性的字段的路径。 此路径位于模式的`properties`属性中，路径中不应包含字段名称。 编写路径时，忽略`properties`属性的多个级别。 |
| `{TENANT_ID}` | 如果您不熟悉您的租户ID，请参阅[模式注册表开发人员指南](../../xdm/api/getting-started.md#know-your-tenant_id)中有关查找您的租户ID的步骤。 |
| `description` | 计算属性的描述。 一旦定义了多个计算属性，这特别有用，因为它将帮助IMS组织中的其他人员确定要使用的正确计算属性。 |
| `expression.value` | 有效的[!DNL Profile Query Language](PQL)表达式。 计算属性当前支持以下函数：sum、count、min、max和boolean。 有关示例表达式的列表，请参阅[示例PQL表达式](expressions.md)文档。 |
| `schema.name` | 包含计算属性字段的模式所基于的类。 示例：`_xdm.context.experienceevent`，用于基于XDM ExperienceEvent类的模式。 |

**响应**

成功创建的计算属性返回HTTP状态200(OK)和包含新创建计算属性详细信息的响应主体。 这些详细信息包括系统生成的唯一只读`id`，可用于在其他API操作期间引用计算属性。

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
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

| 属性 | 描述 |
|---|---|
| `id` | 唯一的只读系统生成的ID，可用于在其他API操作期间引用计算的属性。 |
| `imsOrgId` | 与计算属性相关的IMS组织应与请求中发送的值匹配。 |
| `sandbox` | 沙箱对象包含在其中配置了计算属性的沙箱的详细信息。 此信息从请求中发送的沙箱标头中提取。 有关详细信息，请参阅[沙箱概述](../../sandboxes/home.md)。 |
| `positionPath` | 一个数组，包含已解构`path`到请求中发送的字段。 |
| `returnSchema.meta:xdmType` | 存储计算属性的字段的类型。 |
| `definedOn` | 一个数组，显示已定义计算属性的合并模式。 每个合并模式包含一个对象，这意味着如果计算的属性已添加到基于不同类的多个模式，则数组中可能有多个对象。 |
| `active` | 一个布尔值，显示计算的属性当前是否处于活动状态。 默认情况下，值为`true`。 |
| `type` | 创建的资源类型（在本例中为“ComputedAttribute”）是默认值。 |
| `createEpoch` 和 `updateEpoch` | 分别创建和上次更新计算属性的时间。 |

## 创建引用现有计算属性的计算属性

还可以创建引用现有计算属性的计算属性。 为此，首先向`/config/computedAttributes`端点发出POST请求。 请求主体将包含对`expression.value`字段中计算属性的引用，如下例所示。

**API格式**

```http
POST /config/computedAttributes
```

**请求**

在此示例中，已创建了两个计算属性，并将用于定义第三个属性。 现有的计算属性有：

* **`totalSpend`:** 捕获客户已支出的总美元金额。
* **`countPurchases`:** 计算客户已购买的数量。

以下请求引用两个现有的计算属性，使用有效的PQL进行划分以计算新的`averageSpend`计算属性。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "averageSpend",
        "path" : "_{TENANT_ID}.purchaseSummary",
        "description" : "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| 属性 | 描述 |
|---|---|
| `name` | 计算的属性字段的名称，作为字符串。 |
| `path` | 包含计算属性的字段的路径。 此路径位于模式的`properties`属性中，路径中不应包含字段名称。 编写路径时，忽略`properties`属性的多个级别。 |
| `{TENANT_ID}` | 如果您不熟悉您的租户ID，请参阅[模式注册表开发人员指南](../../xdm/api/getting-started.md#know-your-tenant_id)中有关查找您的租户ID的步骤。 |
| `description` | 计算属性的描述。 一旦定义了多个计算属性，这特别有用，因为它将帮助IMS组织中的其他人员确定要使用的正确计算属性。 |
| `expression.value` | 有效的PQL表达式。 计算属性当前支持以下函数：sum、count、min、max和boolean。 有关示例表达式的列表，请参阅[示例PQL表达式](expressions.md)文档。<br/><br/>在此示例中，表达式引用两个现有的计算属性。这些属性使用计算属性的`path`和`name`进行引用，它们显示在定义计算属性的模式中。 例如，第一个引用的计算属性的`path`为`_{TENANT_ID}.purchaseSummary`，而`name`为`totalSpend`。 |
| `schema.name` | 包含计算属性字段的模式所基于的类。 示例：`_xdm.context.experienceevent`，用于基于XDM ExperienceEvent类的模式。 |

**响应**

成功创建的计算属性返回HTTP状态200(OK)和包含新创建计算属性详细信息的响应主体。 这些详细信息包括系统生成的唯一只读`id`，可用于在其他API操作期间引用计算属性。

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
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
    "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
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
| `sandbox` | 沙箱对象包含在其中配置了计算属性的沙箱的详细信息。 此信息从请求中发送的沙箱标头中提取。 有关详细信息，请参阅[沙箱概述](../../sandboxes/home.md)。 |
| `positionPath` | 一个数组，包含已解构`path`到请求中发送的字段。 |
| `returnSchema.meta:xdmType` | 存储计算属性的字段的类型。 |
| `definedOn` | 一个数组，显示已定义计算属性的合并模式。 每个合并模式包含一个对象，这意味着如果计算的属性已添加到基于不同类的多个模式，则数组中可能有多个对象。 |
| `active` | 一个布尔值，显示计算的属性当前是否处于活动状态。 默认情况下，值为`true`。 |
| `type` | 创建的资源类型（在本例中为“ComputedAttribute”）是默认值。 |
| `createEpoch` 和 `updateEpoch` | 分别创建和上次更新计算属性的时间。 |

## 访问计算属性

使用API处理计算属性时，有两个选项用于访问您的组织定义的计算属性。 第一种是列表所有计算属性，第二种是视图特定计算属性的唯一`id`。

本文档概述了两种访问模式的步骤。 选择以下选项之一开始：

* **[列表所有现有计算属性](#list-all-computed-attributes):** 返回您的组织已创建的所有现有计算属性的列表。
* **[视图特定的计算属性](#view-a-computed-attribute):** 通过在请求期间指定单个计算属性的ID来返回其详细信息。

### 列表所有计算属性{#list-all-computed-attributes}

您的IMS组织可以创建多个计算属性，并且对`/config/computedAttributes`终结点执行GET请求允许您列表组织的所有现有计算属性。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功响应包括`_page`属性，该属性提供计算属性(`totalCount`)的总数和页面(`pageSize`)上计算属性的数量。

响应还包括由一个或多个对象组成的`children`数组，每个对象包含一个计算属性的详细信息。 如果您的组织没有任何计算属性，则`totalCount`和`pageSize`将为0（零），而`children`数组将为空。

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
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
            "imsOrgId": "{IMS_ORG}",
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
                "type" : "PQL", 
                "format" : "pql/text", 
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
| `_page.totalCount` | IMS组织定义的计算属性总数。 |
| `_page.pageSize` | 在结果页上返回的计算属性数。 如果`pageSize`等于`totalCount`，则表示只有一页结果，且已返回所有计算属性。 如果它们不相等，则可以访问其他页面的结果。 有关详细信息，请参阅`_links.next`。 |
| `children` | 由一个或多个对象组成的数组，每个对象都包含单个计算属性的详细信息。 如果未定义计算属性，则`children`数组为空。 |
| `id` | 在创建计算属性时自动分配给该属性的唯一、只读的、系统生成的值。 有关计算属性对象的组件的详细信息，请参阅本教程前面有关创建计算属性](#create-a-computed-attribute)的部分。[ |
| `_links.next` | 如果返回计算属性的单页，则`_links.next`是空对象，如上面的示例响应所示。 如果您的组织有许多计算属性，您可以通过向`_links.next`值发出GET请求访问的多个页面上将返回这些属性。 |

### 视图计算属性{#view-a-computed-attribute}

可以通过向`/config/computedAttributes`端点发出GET请求并在请求路径中包含计算属性ID来视图特定计算属性。

**API格式**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| 参数 | 描述 |
|---|---|
| `{ATTRIBUTE_ID}` | 要视图的计算属性的ID。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
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

如果您发现需要更新现有计算属性，可通过向`/config/computedAttributes`端点发出PATCH请求并在请求路径中包含要更新的计算属性的ID来完成此操作。

**API格式**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| 参数 | 描述 |
|---|---|
| `{ATTRIBUTE_ID}` | 要更新的计算属性的ID。 |

**请求**

此请求使用[JSON修补程序格式](http://jsonpatch.com/)更新“表达式”字段的“value”。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| 属性 | 描述 |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | 有效的[!DNL Profile Query Language](PQL)表达式。 计算属性当前支持以下函数：sum、count、min、max和boolean。 有关示例表达式的列表，请参阅[示例PQL表达式](expressions.md)文档。 |

**响应**

成功的更新会返回HTTP状态204（无内容）和空的响应体。 如果您希望确认更新成功，则可以执行GET请求，以按计算属性的ID视图该属性。

## 删除计算属性

也可以使用API删除计算属性。 这是通过向`/config/computedAttributes`端点发出DELETE请求并在请求路径中包括要删除的计算属性的ID来完成的。

>[!NOTE]
>
>删除计算属性时请务必小心，因为该属性可能正在多个模式中使用，并且DELETE操作无法撤消。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**响应**

成功的删除请求返回HTTP状态200(OK)和空的响应体。 要确认删除成功，您可以执行GET请求以按计算属性的ID查找该属性。 如果删除了该属性，您将收到HTTP状态404（找不到）错误。

## 创建引用计算属性的区段定义

Adobe Experience Platform允许您创建区段，这些区段从一组用户档案中定义一组特定属性或行为。 段定义包括封装在PQL中写入的查询的表达式。 这些表达式还可以引用计算属性。

下面的示例创建引用现有计算属性的段定义。 要进一步了解区段定义以及如何在分段服务API中使用它们，请参阅[区段定义API端点指南](../../segmentation/api/segment-definitions.md)。

要开始，向`/segment/definitions`端点发出POST请求，在请求体中提供计算的属性。

**API格式**

```http
POST /segment/definitions
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 区段的唯一名称，作为字符串。 |
| `description` | 定义的用户可读描述。 |
| `schema.name` | 与区段中的实体关联的模式。 由`id`或`name`字段组成。 |
| `expression` | 包含字段的对象，其中包含有关区段定义的信息。 |
| `expression.type` | 指定表达式类型。 目前，仅支持“PQL”。 |
| `expression.format` | 以值表示表达式的结构。 当前仅支持`pql/text`。 |
| `expression.value` | 有效的PQL表达式，在此示例中包括对现有计算属性的引用。 |

有关模式定义属性的详细信息，请参阅[段定义API端点指南](../../segmentation/api/segment-definitions.md)中提供的示例。

**响应**

成功的响应会返回HTTP状态200，其中包含您新创建的区段定义的详细信息。 要了解有关区段定义响应对象的更多信息，请参阅[区段定义API端点指南](../../segmentation/api/segment-definitions.md)。

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{IMS_ORG}",
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

现在，您已经学习了计算属性的基础知识，可以开始为组织定义这些属性了。
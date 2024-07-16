---
title: 计算属性API端点
description: 了解如何使用实时客户个人资料API创建、查看、更新和删除计算属性。
exl-id: f217891c-574d-4a64-9d04-afc436cf16a9
source-git-commit: 94c94b8a3757aca1a04ff4ffc3c62e84602805cc
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 1%

---

# 计算属性API端点

>[!IMPORTANT]
>
>对API的访问受到限制。 要了解如何获取对计算属性API的访问权限，请联系Adobe支持。

计算属性是用于将事件级数据聚合到配置文件级属性的函数。 这些函数是自动计算的，以便在分段、激活和个性化中使用它们。 本指南包含使用`/attributes`端点执行基本CRUD操作的示例API调用。

若要了解有关计算属性的更多信息，请先阅读[计算属性概述](overview.md)。

## 快速入门

本指南中使用的API端点是[实时客户个人资料API](https://www.adobe.com/go/profile-apis-en)的一部分。

在继续之前，请查看[配置文件API快速入门指南](../api/getting-started.md)，以获取推荐文档的链接、阅读此文档中显示的示例API调用的指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

此外，请查看以下服务的文档：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   - [架构注册表快速入门指南](../../xdm/api/getting-started.md#know-your-tenant_id)：提供了有关本指南的响应中显示的`{TENANT_ID}`的信息。

## 检索计算属性列表 {#list}

您可以通过向`/attributes`端点发出GET请求来检索组织的所有计算属性的列表。

**API格式**

`/attributes`端点支持多个查询参数以帮助筛选结果。 虽然这些参数是可选的，但强烈建议使用这些参数，以帮助在列出资源时减少昂贵的开销。 如果您在不使用参数的情况下调用此端点，则将检索对您的组织可用的所有计算属性。 可以包含多个参数，以&amp;符号(`&`)分隔。

```http
GET /attributes
GET /attributes?{QUERY_PARAMETERS}
```

在检索计算属性列表时，可以使用以下查询参数：

| 查询参数 | 描述 | 示例 |
| --------------- | ----------- | ------- |
| `limit` | 指定作为响应的一部分返回的最大项数的参数。 此参数的最小值为1，最大值为40。 如果不包含此参数，则默认情况下将返回20项。 | `limit=20` |
| `offset` | 一个参数，指定在返回项目之前跳过的项目数。 | `offset=5` |
| `sortBy` | 一个参数，指定返回项的排序顺序。 可用选项包括`name`、`status`、`updateEpoch`和`createEpoch`。 您还可以通过在排序选项前面不包含或包含`-`来选择是按升序排序还是按降序排序。 默认情况下，这些项将按`updateEpoch`降序排序。 | `sortBy=name` |
| `property` | 一个参数，可让您筛选各种计算属性字段。 支持的属性包括`name`、`createEpoch`、`mergeFunction.value`、`updateEpoch`和`status`。 支持的操作取决于列出的属性。 <ul><li>`name`： `EQUAL` (=)，`NOT_EQUAL` (！=)， `CONTAINS` (=contains())， `NOT_CONTAINS` (=!contains())</li><li>`createEpoch`： `GREATER_THAN_OR_EQUALS` (&lt;=)， `LESS_THAN_OR_EQUALS` (>=) </li><li>`mergeFunction.value`： `EQUAL` (=)，`NOT_EQUAL` (！=)， `CONTAINS` (=contains())， `NOT_CONTAINS` (=!contains())</li><li>`updateEpoch`： `GREATER_THAN_OR_EQUALS` (&lt;=)， `LESS_THAN_OR_EQUALS` (>=)</li><li>`status`： `EQUAL` (=)，`NOT_EQUAL` (！=)， `CONTAINS` (=contains())， `NOT_CONTAINS` (=!contains())</li></ul> | `property=updateEpoch>=1683669114845`<br/>`property=name!=testingrelease`<br/>`property=status=contains(new,processing,disabled)` |

**请求**

以下请求检索组织中更新的最后三个计算属性。

+++ 用于检索计算属性列表的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ca/attributes?limit=3 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200，其中包含属于您的组织和沙盒的最后3个已更新计算属性的列表。

+++ 用于检索计算属性列表的示例响应。

```json
{
    "_links": {
        "last": {
            "href": "/attributes?offset=3&limit=1"
        },
        "next": {
            "href": "/attributes?offset=20&limit=20"
        },
        "prev": {
            "href": "/attributes?offset=0&limit=20"
        },
        "self": {
            "href": "/attributes?offset=0&limit=20"
        }
    },
    "computedAttributes": [
        {
            "id": "2e3bf98c-5840-4eb5-98c9-fcd7bde82188",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses19",
            "displayName": "Multiple Filter Clauses 19",
            "description": "Multiple Filter Clauses 19",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": false,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223530322,
            "updateEpoch": 1673043640946,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "d9fbbd3d-049a-4561-b826-adc162511950",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses20",
            "displayName": "Multiple Filter Clauses 20",
            "description": "Multiple Filter Clauses 20",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": true,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[eventType.equals(\"commerce.backofficeOrderPlaced\", false)].topN(timestamp, 1).map({\"timestamp\": timestamp, \"value\": producedBy}).head()"
            },
            "mergeFunction": {
                "value": "MOST_RECENT"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223586455,
            "updateEpoch": 1671223586455,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "afedff07-9d15-4385-b181-49708229d73b",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses18",
            "displayName": "Multiple Filter Clauses 18",
            "description": "Multiple Filter Clauses 18",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "PROCESSED",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "2023-08-27T00:14:55.028",
            "createEpoch": 1671220358902,
            "updateEpoch": 1671220358902,
            "createdBy": "{USER_ID}"
        }
    ],
    "_page": {
        "offset": 0,
        "limit": 20,
        "count": 3,
        "totalCount": 3
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `_links` | 一个对象，其中包含访问最后一页结果、下一页结果、上一页结果或当前页结果所需的分页信息。 |
| `computedAttributes` | 一个数组，其中包含基于查询参数的计算属性。 有关计算属性数组的详细信息，请参阅[检索特定的计算属性节](#get)。 |
| `_page` | 包含有关返回结果的元数据的对象。 其中包括有关当前偏移、返回的计算属性的计数、计算属性的总计数以及返回的计算属性的限制的信息。 |

+++

## 创建计算属性 {#create}

要创建计算属性，首先向`/attributes`端点发出POST请求，请求正文包含要创建的计算属性的详细信息。

**API格式**

```http
POST /attributes
```

**请求**

+++ 用于创建新的计算属性的示例请求。

```shell
curl -X POST https://platform.adobe.io/data/core/ca/attributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "testing",
        "displayName": "Sample Display Name",
        "description": "Sample Description",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)"
        },
        "keepCurrent": false,
        "duration": {
            "count": 4,
            "unit": "DAYS"
        },
        "status": "DRAFT"
      }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 计算属性字段的名称（以字符串形式）。 计算属性的名称只能由字母数字字符组成，不能有任何空格或下划线。 此值&#x200B;**在所有计算属性中必须**&#x200B;是唯一的。 作为最佳实践，此名称应该是`displayName`的camelCase版本。 |
| `description` | 计算属性的描述。 定义多个计算属性后，此功能会特别有用，因为它有助于组织内的其他人确定要使用的正确计算属性。 |
| `displayName` | 计算属性的显示名称。 这是在Adobe Experience Platform UI中列出计算属性时将显示的名称。 |
| `expression` | 一个对象，表示您尝试创建的计算属性的查询表达式。 |
| `expression.type` | 表达式的类型。 目前，仅支持PQL。 |
| `expression.format` | 表达式的格式。 当前仅支持`pql/text`。 |
| `expression.value` | 表达式的值。 |
| `keepCurrent` | 一个布尔值，用于确定使用快速刷新使计算属性的值保持最新。 目前，此值应设置为`false`。 |
| `duration` | 表示计算属性的回顾期间的对象。 回顾时间范围表示计算计算属性时回顾的时间范围。 |
| `duration.count` | 表示回顾期间的持续时间的数字。 可能的值取决于`duration.unit`字段的值。 <ul><li>`HOURS`： 1-24</li><li>`DAYS`： 1-7</li><li>`WEEKS`： 1-4</li><li>`MONTHS`： 1-6</li></ul> |
| `duration.unit` | 一个字符串，表示将用于回顾期间的时间单位。 可能的值包括： `HOURS`、`DAYS`、`WEEKS`和`MONTHS`。 |
| `status` | 计算属性的状态。 可能的值包括`DRAFT`和`NEW`。 |

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关新创建的计算属性的信息。

+++ 创建新计算属性时的示例响应。

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 新创建的计算属性的系统生成的ID。 |
| `status` | 计算属性的状态。 这可以是`DRAFT`或`NEW`。 |
| `createEpoch` | 计算属性的创建时间（以秒为单位）。 |
| `updateEpoch` | 上次更新计算属性的时间（以秒为单位）。 |
| `createdBy` | 创建计算属性的用户的ID。 |

+++

## 检索特定的计算属性 {#get}

通过向`/attributes`端点发出GET请求并提供要在请求路径中检索的计算属性的ID，可以检索有关特定计算属性的详细信息。

**API格式**

```http
GET /attributes/{ATTRIBUTE_ID}
```

**请求**

+++ 用于检索特定计算属性的示例请求。

```shell
curl -X GET 'https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关指定计算属性的详细信息。

+++ 检索特定计算属性时的示例响应。

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 系统生成的唯一只读ID，可用于在其他API操作期间引用计算属性。 |
| `type` | 一个字符串，它表明返回的对象是计算属性。 |
| `name` | 计算属性的名称。 |
| `displayName` | 计算属性的显示名称。 这是在Adobe Experience Platform UI中列出计算属性时将显示的名称。 |
| `description` | 计算属性的描述。 定义多个计算属性后，此功能会特别有用，因为它有助于组织内的其他人确定要使用的正确计算属性。 |
| `imsOrgId` | 计算属性所属的组织的ID。 |
| `sandbox` | 沙盒对象包含在其中配置计算属性的沙盒的详细信息。 此信息摘自在请求中发送的沙盒标头。 有关详细信息，请参阅[沙盒概述](../../sandboxes/home.md)。 |
| `path` | 计算属性的`path`。 |
| `keepCurrent` | 一个布尔值，用于确定使用快速刷新使计算属性的值保持最新。 |
| `expression` | 包含计算属性的表达式的对象。 |
| `mergeFunction` | 包含计算属性的合并函数的对象。 此值基于计算属性的表达式中对应的聚合参数。 可能的值包括`SUM`、`MIN`、`MAX`和`MOST_RECENT`。 |
| `status` | 计算属性的状态。 此值可以是以下值之一：`DRAFT`、`NEW`、`INITIALIZING`、`PROCESSING`、`PROCESSED`、`FAILED`或`DISABLED`。 |
| `schema` | 一个对象，其中包含有关在其中计算表达式的方案的信息。 当前仅支持`_xdm.context.profile`。 |
| `lastEvaluationTs` | 表示计算属性的上次评估时间的时间戳。 |
| `createEpoch` | 计算属性的创建时间（以秒为单位）。 |
| `updateEpoch` | 上次更新计算属性的时间（以秒为单位）。 |
| `createdBy` | 创建计算属性的用户的ID。 |

+++

## 删除特定的计算属性 {#delete}

通过向`/attributes`端点发出DELETE请求并在请求路径中提供要删除的计算属性的ID，可以删除特定的计算属性。

>[!IMPORTANT]
>
>删除请求只能用于删除状态为&#x200B;**草稿** (`DRAFT`)的计算属性。 此终结点&#x200B;**不能**&#x200B;用于删除处于任何其他状态的计算属性。

**API格式**

```http
DELETE /attributes/{ATTRIBUTE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | 要删除的计算属性的`id`值。 |

**请求**

+++ 删除计算属性的示例请求。

```shell
curl -X DELETE https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态202，其中包含已删除计算属性的详细信息。

+++ 删除计算属性时的示例响应。

```json
{
    "id": "03ae581b-5f7b-48da-a9eb-4ef0daf4bc3c",
    "type": "ComputedAttribute",
    "name": "testdemopd2",
    "displayName": "testdemopd2",
    "description": "testdemopd2",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.shipping.shipDate occurs <= 1 days before now) and (timestamp occurs <= 1 days before now)].min(commerce.shipping.shipDate)"
    },
    "mergeFunction": {
        "value": "MIN"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1681365690928,
    "updateEpoch": 1681365690928,
    "createdBy": "{USER_ID}"
}
```

+++

## 更新特定的计算属性

您可以通过向`/attributes`端点发出PATCH请求并在请求路径中提供要更新的计算属性的ID来更新特定的计算属性。

>[!IMPORTANT]
>
>更新计算属性时，只能更新以下字段：
>
>- 如果当前状态为`NEW`，则状态只能更改为`DISABLED`。
>- 如果当前状态为`DRAFT`，则可以更改以下字段的值： `name`、`description`、`keepCurrent`、`expression`和`duration`。 您还可以将状态从`DRAFT`更改为`NEW`。 对系统生成的字段（如`mergeFunction`或`path`）所做的任何更改都将返回错误。
>- 如果当前状态为`PROCESSING`或`PROCESSED`，则状态只能更改为`DISABLED`。

**API格式**

```http
PATCH /attributes/{ATTRIBUTE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | 要更新的计算属性的`id`值。 |

**请求**

以下请求会将计算属性的状态从`DRAFT`更新为`NEW`。

+++ 更新计算属性的示例请求。

```shell
curl -X PATCH https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "description": "Sample Description",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "status": "NEW"
 }'
```

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关新更新的计算属性的信息。

+++ 更新计算属性时的示例响应。

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing123",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "NEW",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680071726825,
    "updateEpoch": 1680074429192,
    "createdBy": "{USER_ID}"
}
```

+++

## 后续步骤

现在，您已了解计算属性的基础知识，可以开始为组织定义这些属性了。 要了解如何在Experience PlatformUI中使用计算属性，请阅读[计算属性UI指南](./ui.md)。

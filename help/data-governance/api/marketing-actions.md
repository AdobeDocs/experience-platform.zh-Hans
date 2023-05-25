---
keywords: Experience Platform；主页；热门主题；策略实施；营销操作API；基于API的实施；数据管理
solution: Experience Platform
title: 营销操作API端点
description: 在Adobe Experience Platform数据管理上下文中，营销操作是Experience Platform数据使用者执行的操作，需要检查是否存在违反数据使用策略的行为。
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 2%

---

# 营销活动端点

在Adobe Experience Platform数据管理上下文中，营销操作是一个 [!DNL Experience Platform] 数据使用者需要使用，为此，需要检查是否存在违反数据使用策略的情况。

您可以使用管理组织的营销操作 `/marketingActions` 策略服务API中的端点。

## 快速入门

本指南中使用的API端点是 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 在继续之前，请查看 [快速入门指南](./getting-started.md) 有关相关文档的链接，请参阅本文档中的示例API调用指南，以及有关成功调用任何组件所需的所需标头的重要信息 [!DNL Experience Platform] API。

## 检索营销操作列表 {#list}

您可以通过向以下用户发出GET请求来检索核心或自定义营销操作的列表： `/marketingActions/core` 或 `/marketingActions/custom`，则不会显示任何内容。

**API格式**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**请求**

以下请求可检索由您的组织维护的自定义营销操作列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回每个检索到的营销操作的详细信息，包括其 `name` 和 `href`. 此 `href` 值用于标识营销活动，当 [创建数据使用策略](policies.md#create-policy).

```json
{
    "_page": {
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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714012088,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{ORG_ID}",
            "created": 1550793833224,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550793833224,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `_page.count` | 返回的营销操作总数。 |
| `children` | 一个对象数组，其中包含检索到的营销操作的详细信息。 |
| `name` | 营销活动的名称，在下列情况下充当其唯一标识符： [查找特定的营销操作](#lookup). |
| `_links.self.href` | 营销活动的URI引用，可用于完成 `marketingActionsRefs` 数组： [创建数据使用策略](policies.md#create-policy). |

## 查找特定的营销操作 {#lookup}

通过包含营销操作的，您可以查找特定营销操作的详细信息 `name` 属性(在GET请求的路径中)。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 此 `name` 要查找的营销操作的属性。 |

**请求**

以下请求检索名为的自定义营销操作 `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应对象包含营销操作的详细信息，包括路径(`_links.self.href`)需要在以下情况下引用营销操作 [定义数据使用策略](policies.md#create-policy) (`marketingActionsRefs`)。

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{ORG_ID}",
    "created": 1550793805590,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550793805590,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
        }
    }
}
```

## 创建或更新自定义营销操作 {#create-update}

您可以创建新的自定义营销操作，也可以通过在PUT请求的路径中包含营销操作的现有名称或预期名称来更新现有营销操作。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要创建或更新的营销操作的名称。 如果系统中已存在具有所提供名称的营销操作，则会更新该营销操作。 如果不存在，则会为提供的名称创建新的营销操作。 |

**请求**

以下请求将创建一个名为的新营销操作 `crossSiteTargeting`，前提是系统中不存在同名的营销操作。 如果 `crossSiteTargeting` 营销操作确实存在，此调用会根据有效负载中提供的属性更新该营销操作。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 要创建或更新的营销操作的名称。 <br><br>**重要**：此属性必须匹配 `{MARKETING_ACTION_NAME}` 路径中，否则将发生HTTP 400（错误请求）错误。 换言之，一旦创建了营销操作，其 `name` 属性无法更改。 |
| `description` | 为营销操作提供进一步上下文的可选描述。 |

**响应**

成功响应将返回营销操作的详细信息。 如果更新了现有营销操作，则响应会返回HTTP状态200 （确定）。 如果创建了新营销操作，则响应会返回HTTP状态201（已创建）。

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{ORG_ID}",
    "created": 1550713341915,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550713856390,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
        }
    }
}
```

## 删除自定义营销操作 {#delete}

您可以通过在DELETE请求的路径中包含自定义营销操作的名称来删除该营销操作。

>[!NOTE]
>
>无法删除由现有策略引用的营销操作。 尝试删除其中一个营销操作将导致HTTP 400（错误请求）错误以及包含引用营销操作的所有策略ID的消息。

**API格式**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要删除的营销操作的名称。 |

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回带有空白响应正文的HTTP状态200 （确定）。

您可以通过尝试确认删除 [查找营销操作](#look-up). 如果已从系统中删除营销操作，您应会收到HTTP 404（未找到）错误。

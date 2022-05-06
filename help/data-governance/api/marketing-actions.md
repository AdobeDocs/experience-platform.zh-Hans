---
keywords: Experience Platform；主页；热门主题；策略实施；营销操作API；基于API的实施；数据管理
solution: Experience Platform
title: 营销操作API端点
topic-legacy: developer guide
description: 在“Adobe Experience Platform数据管理”中，营销操作是Experience Platform数据使用者采取的一项操作，需要检查其是否违反了数据使用策略。
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 2%

---

# 营销操作端点

在“Adobe Experience Platform数据管理”范围内，营销行动是指 [!DNL Experience Platform] 数据使用者，需要检查其是否违反了数据使用策略。

您可以使用 `/marketingActions` 策略服务API中的端点。

## 快速入门

本指南中使用的API端点是 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 在继续之前，请查看 [入门指南](./getting-started.md) 有关相关文档的链接、本文档中的API调用示例指南，以及有关成功调用任何代码所需标头的重要信息 [!DNL Experience Platform] API。

## 检索营销操作列表 {#list}

您可以通过向 `/marketingActions/core` 或 `/marketingActions/custom`，分别为。

**API格式**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**请求**

以下请求可检索由贵组织维护的自定义营销操作列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回每个检索到的营销操作的详细信息，包括其 `name` 和 `href`. 的 `href` 值用于识别营销操作，当 [创建数据使用策略](policies.md#create-policy).

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
| `children` | 包含检索到的营销操作详细信息的对象数组。 |
| `name` | 营销操作的名称，在 [查找特定营销操作](#lookup). |
| `_links.self.href` | 营销操作的URI引用，可用于完成 `marketingActionsRefs` 数组 [创建数据使用策略](policies.md#create-policy). |

## 查找特定营销操作 {#lookup}

通过将 `name` 属性。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 的 `name` 要查找的营销操作的属性。 |

**请求**

以下请求将检索名为 `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应对象包含营销操作的详细信息，包括路径(`_links.self.href`)需要在 [定义数据使用策略](policies.md#create-policy) (`marketingActionsRefs`)。

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

您可以创建新的自定义营销操作，或通过在PUT请求的路径中包含营销操作的现有或预期名称来更新现有的自定义营销操作。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要创建或更新的营销操作的名称。 如果系统中已存在具有提供名称的营销操作，则会更新该营销操作。 如果不存在，则会为提供的名称创建新的营销操作。 |

**请求**

以下请求会创建一个名为 `crossSiteTargeting`，前提是系统中不存在同名的营销操作。 如果 `crossSiteTargeting` 营销操作确实存在，但此调用会根据有效负载中提供的属性来更新营销操作。

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
| `name` | 要创建或更新的营销操作的名称。 <br><br>**重要信息**:此属性必须匹配 `{MARKETING_ACTION_NAME}` 在路径中，否则将发生HTTP 400（错误请求）错误。 换句话说，一旦创建了营销操作， `name` 属性。 |
| `description` | 可选描述，用于为营销操作提供更多上下文。 |

**响应**

成功的响应会返回营销操作的详细信息。 如果更新了现有的营销操作，则响应会返回HTTP状态200（确定）。 如果创建了新的营销操作，则响应会返回HTTP状态201（已创建）。

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

您可以通过在自定义营销请求的路径中包含其名称来删除DELETE操作。

>[!NOTE]
>
>无法删除现有策略引用的营销操作。 尝试删除其中一个营销操作时，将导致HTTP 400（错误请求）错误，并出现一则消息，其中包含引用营销操作的所有策略的ID。

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

成功的响应会返回HTTP状态200(OK)，并且返回一个空白的响应正文。

您可以通过尝试 [查找营销操作](#look-up). 如果营销操作已从系统中删除，您应会收到HTTP 404（未找到）错误。

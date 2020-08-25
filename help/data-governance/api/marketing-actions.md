---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 营销操作
topic: developer guide
translation-type: tm+mt
source-git-commit: 12c53122d84e145a699a2a86631dc37ee0073578
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 2%

---


# 营销活动端点

在Adobe Experience Platform的背景下，营销行 [!DNL Data Governance]动是数据消费者 [!DNL Experience Platform] 采取的行动，需要检查是否存在违反数据使用策略的情况。

您可以使用策略服务API中的端点来管 `/marketingActions` 理组织的营销操作。

## 入门指南

本指南中使用的API端点是API的一 [[!DNL Policy Service] 部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)。 在继续之前，请查 [看入门指南](./getting-started.md) ，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何API所需标头的重要信 [!DNL Experience Platform] 息。

## 检索营销操作列表 {#list}

您可以通过分别向或发出列表请求来检索核心或自定义 `/marketingActions/core` 营销 `/marketingActions/custom`操作的GET。

**API格式**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**请求**

以下请求检索由您的组织维护的列表自定义营销活动。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回每个检索到的营销操作（包括其和）的详细 `name` 信息 `href`。 该值 `href` 用于在创建数据使用策略时 [标识营销操作](policies.md#create-policy)。

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
| `_page.count` | 返回的营销活动总数。 |
| `children` | 一组对象，其中包含检索到的营销操作的详细信息。 |
| `name` | 营销活动的名称，在查找特定营销活动时充当 [其唯一标识符](#lookup)。 |
| `_links.self.href` | 市场营销操作的URI引用，在创建数据使用策 `marketingActionsRefs` 略时 [可用于完成阵列](policies.md#create-policy)。 |

## 查找特定的营销活动 {#lookup}

通过在GET请求路径中包含营销活动的属性，您可 `name` 以查找特定营销活动的详细信息。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要 `name` 查找的营销操作的属性。 |

**请求**

以下请求检索名为的自定义营销活动 `combineData`。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应对象包含市场营销操作的详细信息，包括定义数据使`_links.self.href`用策略()时引用营销 [操作所需的路径](policies.md#create-policy) (`marketingActionsRefs`)。

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{IMS_ORG}",
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

您可以创建新的自定义营销活动，或通过在PUT请求路径中包含该营销活动的现有或预期名称来更新现有的自定义营销活动。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要创建或更新的营销操作的名称。 如果系统中已存在具有提供名称的营销操作，则会更新该营销操作。 如果不存在，则会为提供的名称创建新的营销操作。 |

**请求**

以下请求将创建一个名为的 `crossSiteTargeting`新营销活动，前提是系统中尚不存在同名的营销活动。 如果某 `crossSiteTargeting` 个营销活动确实存在，此调用会根据有效负荷中提供的属性更新该营销活动。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 要创建或更新的营销操作的名称。 <br><br>**重要说明**:此属性必须与路 `{MARKETING_ACTION_NAME}` 径中的匹配，否则将发生HTTP 400（错误请求）错误。 换言之，一旦创建了营销操作，其属 `name` 性便无法更改。 |
| `description` | 可选描述，用于为营销操作提供更多上下文。 |

**响应**

成功的响应会返回营销操作的详细信息。 如果更新了现有的营销操作，则响应将返回HTTP状态200（确定）。 如果创建了新的营销操作，则响应将返回HTTP状态201（已创建）。

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{IMS_ORG}",
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

您可以通过在DELETE请求路径中包含自定义营销操作的名称来删除该操作。

>[!NOTE]
>
>无法删除现有策略引用的营销活动。 尝试删除其中一个营销操作将导致HTTP 400（错误请求）错误，并显示一条消息，其中包含引用该营销操作的所有策略的ID。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200(OK)，并返回一个空的响应体。

您可以通过尝试查找营销 [操作来确认删除](#look-up)。 如果营销操作已从系统中删除，您应会收到HTTP 404（未找到）错误。

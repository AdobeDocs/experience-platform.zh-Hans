---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 营销操作
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---


# 营销操作

在Adobe Experience Platform数据治理的环境中，营销行为是消费者采取的行 [!DNL Experience Platform] 为，需要检查是否存在违反数据使用策略的情况。

在API中处理营销操作需要您使用终 `/marketingActions` 点。

## 列表所有营销行动

要视图所有营销活动的列表，可以向指定发出GET请求， `/marketingActions/core` 或者 `/marketingActions/custom` 返回指定容器的所有策略。

**API格式**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**请求**

以下请求将返回由IMS组织定义的所有自定义营销操作的列表。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应对象提供容器()中的营销操作`count`总数，并且 `children` 数组包含每个营销操作的详细信息，包括 `name` 营销 `href` 操作的详细信息。 此路径(`_links.self.href`)用于在创建数据 `marketingActionsRefs` 使用 [策略时完成阵列](policies.md#create-policy)。

```JSON
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

## 查找特定的营销活动

您还可以执行查找(GET)请求，以视图特定营销操作的详细信息。 这是使用营销 `name` 操作完成的。 如果名称未知，则可使用以前显示的列表(GET)请求找到该名称。

**API格式**

```http
GET /marketingActions/core/{marketingActionName}
GET /marketingActions/custom/{marketingActionName}
```

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应对象包含市场营销操作的详细信息，包括定义数据使`_links.self.href`用策略时引用营销操作所需的路径(`marketingActionsRefs`)。

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

## 创建或更新营销活动

API [!DNL Policy Service] 允许您定义自己的营销操作，并更新现有的营销操作。 创建和更新操作均使用PUT操作完成，并将其用于营销操作的名称。

**API格式**

```http
PUT /marketingActions/custom/{marketingActionName}
```

**请求**

在随后的请求中，请注 `name` 意请求有效负荷中的与API调 `{marketingActionName}` 用中的相同。 与只 `id` 读策略和系统生成的策略不同，创建营销操作需要您在创建 _时_ 提供营销操作的预期名称。

>[!NOTE]
>
>无法在调 `{marketingActionName}` 用中提供，将导致405错误（不允许使用方法），因为不允许您直接对端点执行 `/marketingActions/custom` PUT。 此外，如 `name` 果有效负荷中的与路径 `{marketingActionName}` 中的不匹配，您将收到400错误（错误请求）。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

**响应**

如果成功创建，您将收到HTTP状态201（已创建），并且响应主体将包含新创建营销操作的详细信息。 响 `name` 应中的值应与请求中发送的内容匹配。

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

## 删除营销操作

您可以通过向要删除的营销活动发送DELETE请 `{marketingActionName}` 求来删除营销活动。

>[!NOTE]
>
>您无法删除由现有策略引用的营销操作。 尝试执行此操作将导致400错误（错误请求）和错误消息，该错误消息包括任何策略(或 `id` 策略)的（或多个ID），其中包含对您尝试删除的营销操作的引用。

**API格式**

```http
DELETE /marketingActions/custom/{marketingActionName}
```

**请求**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

如果营销操作已成功删除，则响应正文将为空，并显示HTTP状态200（确定）。

您可以通过尝试查找(GET)营销操作来确认删除。 您应会收到HTTP状态404（未找到）和“找不到”错误消息，因为营销操作已被删除。

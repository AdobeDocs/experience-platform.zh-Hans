---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 营销操作
topic: developer guide
translation-type: tm+mt
source-git-commit: 08d02e7323f75c450e7a250835f26a569685cdd1

---


# 营销操作

在Adobe Experience Platform数据管理环境中的营销操作是Experience Platform数据消费者采取的操作，需要检查是否存在违反数据使用策略的情况。

在API中使用营销操作需要您使用端 `/marketingActions` 点。

## 列表所有营销操作

要视图所有营销操作的列表，可向指定发出GET请求， `/marketingActions/core` 或者 `/marketingActions/custom` 向指定容器返回所有策略。

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

响应对象提供容器(`count`)中的营销操作总数，并且该数组包含每个营销操作的详细信息，包括 `children` 营 `name``href` 销操作的和。 此路径(`_links.self.href`)用于在创建数据使 `marketingActionsRefs` 用策 [略时完成阵列](policies.md#create-policy)。

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

您还可以执行查找(GET)请求以视图特定营销活动的详细信息。 这是使用营销 `name` 操作完成的。 如果名称未知，则可使用以前显示的列表(GET)请求找到该名称。

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

响应对象包含营销操作的详细信息，包括定义数据使用策略(`_links.self.href`)时引用营销操作所需的路径(`marketingActionsRefs`)。

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

## 创建或更新营销操作

策略服务API允许您定义自己的营销操作，并更新现有的营销操作。 创建和更新操作均使用PUT操作完成，并且操作名称为营销操作。

**API格式**

```http
PUT /marketingActions/custom/{marketingActionName}
```

**请求**

在随后的请求中，请注意请 `name` 求有效负荷中的值与API调 `{marketingActionName}` 用中的值相同。 与只 `id` 读和系统生成的策略不同，创建营销操作需要您在创建营销操作时提供 _其预期名称_ 。

>[!NOTE] 由于不允许 `{marketingActionName}` 您直接对端点执行PUT，因此在调用中提供失败将导致405错误(不允许使用方 `/marketingActions/custom` 法)。 此外，如果有 `name` 效负荷中的与路径中的不匹配， `{marketingActionName}` 您将收到400错误（错误请求）。

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

如果成功创建，您将收到HTTP状态201（已创建），响应主体将包含新创建的营销操作的详细信息。 响 `name` 应中的值应与请求中发送的内容匹配。

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

可以通过向要删除的营销操作发送DELETE请求来 `{marketingActionName}` 删除营销操作。

>[!NOTE] 您无法删除现有策略引用的营销操作。 如果尝试这样做，将导致400错误（错误请求）和错误消息，其中包括任何策略（或策略）的 `id` （或多个ID），这些策略（或策略）包含对您尝试删除的营销操作的引用。

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

您可以通过尝试查找(GET)营销操作来确认删除。 您应该会收到HTTP状态404（未找到）和“找不到”错误消息，因为营销操作已被删除。

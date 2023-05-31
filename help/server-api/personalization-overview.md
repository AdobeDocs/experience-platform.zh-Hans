---
title: 个性化概述
description: 了解如何使用Adobe Experience Platform Edge Network Server API从Adobe个性化解决方案中检索个性化内容。
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: 378f222b5c673632ce5792c52fc32410106def37
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 9%

---

# 个性化概述

使用 [!DNL Server API]，您可以从Adobe个性化解决方案中检索个性化内容，包括 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) 和 [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=en).

此外， [!DNL Server API] 通过Adobe Experience Platform个性化目标(例如 [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定义个性化连接](../destinations/catalog/personalization/custom-personalization.md). 要了解如何为同页和下一页个性化配置Experience Platform，请参阅 [专用指南](../destinations/ui/activate-edge-personalization-destinations.md).

在使用服务器API时，您必须将个性化引擎提供的响应与用于呈现网站上的内容的逻辑集成。 不像 [Web SDK](../edge/home.md)，则 [!DNL Server API] 没有自动应用返回内容的机制 [!DNL Adobe Target] 和 [!DNL Offer Decisioning].

## 术语 {#terminology}

在使用Adobe个性化解决方案之前，请确保了解以下概念：

* **优惠**：优惠是营销消息，其中可能包含与其关联的规则，用于指定有资格查看优惠的人员。
* **决策**：决策（以前称为优惠活动）会通知优惠选择。
* **架构**：决策的架构通知返回的优惠类型。
* **范围**：决定的范围。
   * 在Adobe Target中，这是 [!DNL mbox]. 此 [!DNL global mbox] 是 `__view__` 范围
   * 对象 [!DNL Offer Decisioning]，这些是JSON的Base64编码字符串，其中包含您希望offer decisioning服务用来建议选件的活动和版面ID。

## 此 `query` 对象 {#query-object}

检索个性化内容需要请求示例的显式请求查询对象。 查询对象具有以下格式：

```json
{
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "alloyStore",
            "siteWide",
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}
```

| 属性 | 类型 | 必填/可选 | 描述 |
| --- | --- | --- | ---|
| `schemas` | `String[]` | 对于Target个性化是必需的。 对于Offer decisioning而言，它是可选项。 | 决策中使用的架构列表，用于选择返回的优惠类型。 |
| `scopes` | `String[]` | 可选 | 决策范围列表。 每个请求最多30个。 |

## 句柄对象 {#handle}

从个性化解决方案中检索到的个性化内容显示在中 `personalization:decisions` 句柄，其有效负载具有以下格式：

```json
{
   "type":"personalization:decisions",
   "payload":[
      {
         "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
         "scope":"__view__",
         "scopeDetails":{
            "decisionProvider":"TGT",
            "activity":{
               "id":"131010"
            },
            "experience":{
               "id":"0"
            },
            "strategies":[
               {
                  "algorithmID":"0",
                  "trafficType":"0"
               }
            ]
         },
         "items":[
            {
               "id":"0",
               "schema":"https://ns.adobe.com/personalization/dom-action",
               "meta":{
                  "offer.name":"Default Content",
                  "experience.id":"0",
                  "activity.name":"Luma target reporting",
                  "activity.id":"131010",
                  "experience.name":"Experience A",
                  "option.id":"2",
                  "offer.id":"0"
               },
               "data":{
                  "type":"setHtml",
                  "format":"application/vnd.adobe.target.dom-action",
                  "content":"Customer Service not chrome",
                  "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                  "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
               }
            }
         ]
      }
   ]
}
```

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| `payload.id` | 字符串 | 决策ID。 |
| `payload.scope` | 字符串 | 导致建议优惠的决策范围。 |
| `payload.scopeDetails.decisionProvider` | 字符串 | 设置为 `TGT` 使用Adobe Target时。 |
| `payload.scopeDetails.activity.id` | 字符串 | 优惠活动的唯一ID。 |
| `payload.scopeDetails.experience.id` | 字符串 | 优惠投放的唯一ID。 |
| `items[].id` | 字符串 | 优惠投放的唯一ID。 |
| `items[].data.id` | 字符串 | 建议优惠的ID。 |
| `items[].data.schema` | 字符串 | 与建议选件关联的内容的架构。 |
| `items[].data.format` | 字符串 | 与建议选件关联的内容的格式。 |
| `items[].data.language` | 字符串 | 与建议选件中的内容关联的一系列语言。 |
| `items[].data.content` | 字符串 | 以字符串格式与建议选件关联的内容。 |
| `items[].data.selector` | 字符串 | HTML选择器，用于为DOM操作选件标识目标DOM元素。 |
| `items[].data.prehidingSelector` | 字符串 | HTML选择器，用于标识在处理DOM操作选件时要隐藏的DOM元素。 |
| `items[].data.deliveryUrl` | 字符串 | 以URL格式显示的与建议选件关联的图像内容。 |
| `items[].data.characteristics` | 字符串 | 与JSON对象格式中提议的选件关联的特性。 |

## 示例API调用 {#sample-call}

**API格式**

```http
POST /ee/v2/interact
```

### 请求 {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event":{
      "xdm":{
         "identityMap":{
            "Email_LC_SHA256":[
               {
                  "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary":true
               }
            ]
         },
         "eventType":"web.webpagedetails.pageViews",
         "web":{
            "webPageDetails":{
               "URL":"https://alloystore.dev/",
               "name":"home-demo-Home Page"
            }
         },
         "timestamp":"2021-08-09T14:09:20.859Z"
      }
   },
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}'
```

| 参数 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| `configId` | 字符串 | 是 | 数据流ID。 |
| `requestId` | 字符串 | 否 | 提供外部请求跟踪ID。 如果未提供任何内容，Edge Network将为您生成一个，并将其返回至响应正文/标头。 |

### 响应 {#response}

返回 `200 OK` 状态和一个或多个 `Handle` 对象，具体取决于在数据流配置中启用的边缘服务。

```json
{
   "requestId":"da20d11d-adac-458c-91ac-15bf4e420a15",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"__view__",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"131010"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ]
               },
               "items":[
                  {
                     "id":"0",
                     "schema":"https://ns.adobe.com/personalization/dom-action",
                     "meta":{
                        "offer.name":"Default Content",
                        "experience.id":"0",
                        "activity.name":"Luma target reporting",
                        "activity.id":"131010",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"0"
                     },
                     "data":{
                        "type":"setHtml",
                        "format":"application/vnd.adobe.target.dom-action",
                        "content":"Customer Service not chrome",
                        "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                        "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions"
      }
   ]
}
```

## 通知 {#notifications}

在已访问预获取的内容或视图或已将预获取的内容或视图呈现给最终用户时，应触发通知。 为了能够在正确的范围内触发通知，请确保跟踪相应的 `id` 每个作用域。

带有右侧的通知 `id` 要正确反映报表，需要触发相应的范围。

**API格式**

```http
POST /ee/v2/collect
```

### 请求 {#notifications-request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "events":[
      {
         "xdm":{
            "identityMap":{
               "Email_LC_SHA256":[
                  {
                     "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                     "primary":true
                  }
               ]
            },
            "eventType":"web.webpagedetails.pageViews",
            "web":{
               "webPageDetails":{
                  "URL":"https://alloystore.dev/",
                  "name":"home-demo-Home Page"
               }
            },
            "timestamp":"2021-08-09T14:09:20.859Z",
            "_experience":{
               "decisioning":{
                  "propositions":[
                     {
                        "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                        "scope":"__view__",
                        "items":[
                           {
                              "id":"0"
                           }
                        ]
                     }
                  ]
               }
            }
         }
      }
   ]
}'
```

| 参数 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 是 | 数据收集端点使用的数据流的ID。 |
| `requestId` | `String` | 否 | 外部外部请求跟踪ID。 如果未提供任何内容，Edge Network将为您生成一个，并将其返回至响应正文/标头。 |
| `silent` | `Boolean` | 否 | 可选布尔参数，指示Edge Network是否应返回 `204 No Content` 响应时有效负载为空。 使用相应的HTTP状态代码和有效负载报告严重错误。 |

### 响应 {#notifications-response}

成功响应将返回以下状态之一，并且 `requestID` 请求中没有提供该请求的话。

* `202 Accepted` 成功处理请求时；
* `204 No Content` 成功处理请求后，以及 `silent` 参数已设置为 `true`；
* `400 Bad Request` 请求格式不正确（例如，未找到强制的主标识）时。

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```

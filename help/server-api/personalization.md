---
title: 从其他Adobe解决方案中检索个性化内容
description: 了解如何使用Adobe Experience Platform Edge Network Server API从Adobe个性化解决方案中检索个性化内容
seo-description: Learn how to use the Adobe Experience Platform Edge Network Server API to retrieve personalized content from Adobe personalization solutions
keywords: 个性化；服务器api;Adobe Experience Platform边缘网络；检索个性化
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 9%

---


# 从Adobe解决方案中检索个性化内容

使用 [!DNL Server API]，您可以从Adobe个性化解决方案中检索个性化内容，包括 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) 和 [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=en).

## 术语 {#terminology}

在使用Adobe个性化解决方案之前，请确保了解以下概念：

* **优惠**：优惠是营销消息，其中可能包含与其关联的规则，用于指定有资格查看优惠的人员。
* **决策**:决策（以前称为选件活动）会通知选件的选择。
* **架构**:决策架构会通知返回的选件类型。
* **范围**:决定的范围。
   * 在Adobe Target，这是 [!DNL mbox]. 的 [!DNL global mbox] 是 `__view__` 范围
   * 对于 [!DNL Offer Decisioning]，这些是JSON的Base64编码字符串，其中包含您希望offer decisioning服务用于建议选件的活动和版面ID。

## `query` 对象 {#query}

检索个性化内容时，需要为请求示例提供一个明确的请求查询对象。 查询对象具有以下格式：

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

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| `schemas` | `String[]` | *可选*. 决策中使用的架构列表，用于选择返回的选件类型。 |
| `scopes` | `String[]` | *可选*. 决策范围列表。 每个请求最多30个。 |

## 手柄 {#handle}

从个性化解决方案检索到的个性化内容显示在 `personalization:decisions` handle，其有效负载具有以下格式：

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
| `payload.scope` | 字符串 | 产生建议报价的决定范围。 |
| `payload.scopeDetails.decisionProvider` | 字符串 | 这要么是 `TGT` 如果使用Adobe Target或 `ODE` 如果使用 [!DNL Offer Decisioning]. |
| `payload.scopeDetails.activity.id` | 字符串 | 选件活动的唯一ID。 |
| `payload.scopeDetails.experience.id` | 字符串 | 选件版面的唯一ID。 |
| `items[].id` | 字符串 | 选件版面的唯一ID。 |
| `items[].data.id` | 字符串 | 建议的选件的ID。 |
| `items[].data.schema` | 字符串 | 与建议的选件关联的内容的架构。 |
| `items[].data.format` | 字符串 | 与建议的选件关联的内容格式。 |
| `items[].data.language` | 字符串 | 与建议选件中的内容关联的语言数组。 |
| `items[].data.content` | 字符串 | 与建议的选件关联的内容（以字符串格式）。 |
| `items[].data.selector` | 字符串 | HTML选择器，用于标识DOM操作选件的目标DOM元素。 |
| `items[].data.prehidingSelector` | 字符串 | HTML选择器，用于识别在处理DOM操作选件时要隐藏的DOM元素。 |
| `items[].data.deliveryUrl` | 字符串 | 与建议的选件关联的图像内容采用URL格式。 |
| `items[].data.characteristics` | 字符串 | 与JSON对象格式的建议选件关联的特性。 |

## 检索内容 {#retrieve-content}

### API格式 {#api-format}

```http
POST /ee/v2/interact
```

### 请求 {#request}

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {IMS_ORG_ID}"
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
| `requestId` | 字符串 | 否 | 提供外部请求跟踪ID。 如果未提供任何内容，边缘网络将为您生成一个，并将其返回到响应主体/标头中。 |

### 响应 {#response}

返回 `200 OK` 状态和一个或多个 `Handle` 对象，具体取决于数据流配置中启用的边缘服务。

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

## 通知

预取的内容或视图被访问或呈现给最终用户后，应触发通知。 为了在正确的范围内触发通知，请确保跟踪相应的 `id` 每个范围。

右侧通知 `id` ，以便正确反映报表，需要触发相应的作用域。

### API格式

```http
POST /v2/collect
```

### 请求

```shell
url -X POST "https://server.adobedc.net/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {IMS_ORG_ID}" 
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
| `requestId` | `String` | 否 | 外部请求跟踪ID。 如果未提供任何内容，边缘网络将为您生成一个，并将其返回到响应主体/标头中。 |
| `silent` | `Boolean` | 否 | 可选布尔参数，指示边缘网络是否应返回 `204 No Content` 具有空有效负载的响应。 使用相应的HTTP状态代码和负载报告严重错误。 |

### 响应

成功的响应会返回以下状态之一，并返回 `requestID` 如果请求中未提供任何内容。

* `202 Accepted` 请求成功处理时；
* `204 No Content` 成功处理请求和 `silent` 参数设置为 `true`;
* `400 Bad Request` 请求格式不正确时（例如，找不到强制主标识）。

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```

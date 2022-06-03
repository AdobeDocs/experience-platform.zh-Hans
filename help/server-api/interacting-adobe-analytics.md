---
title: 与Adobe Analytics交互
description: 了解如何使用边缘网络服务器API与Adobe Analytics交互
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Analytics
keywords: 数据收集；出口；analytics;Adobe Experience Platform Edge Network API;Analytics
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: 4fd5b5eebdeca065582365343b605a5b9ee695bb
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 1%

---

# 与Adobe Analytics交互

## 概述 {#overview}

Adobe Analytics数据收集是通过将XDM数据转换为Adobe Analytics可以理解的格式来进行的。 几个XDM字段包括 [自动映射](../edge/data-collection/adobe-analytics/automatically-mapped-vars.md) 到Analytics变量。

您还可以 [手动映射XDM值](../edge/data-collection/adobe-analytics/manually-mapping-variables.md) 到旧版Analytics变量。

要使Adobe Analytics能够从服务器API接收数据，您需要 [配置数据流](../edge/datastreams/overview.md#adobe-analytics-settings) 要将事件转发到Adobe Analytics，请在数据流配置页面中输入报表包ID。

![Adobe Analytics数据流配置](assets/analytics-datastream.png)

## 与Adobe Analytics交互 {#interacting-analytics}

### API格式 {#format}

```http
POST /ee/v2/interact?dataStreamId={DATASTREAM_ID}
```

### 请求 {#request}

以下示例包括 `_experience.analytics` 字段组。 它还包含基于JSON的数据层。 虽然这些数据层无法自动映射，但可以使用 [为数据收集准备数据](../edge/datastreams/data-prep.md) 将这些值映射到包含上述字段组的架构。

用户映射到这些字段的所有值都将自动映射到相应的Analytics值，就像它们包含在API请求中一样。

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" \
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" \
-d '{
   "event": {
      "xdm": {
         "eventType": "web.webpagedetails.pageViews",
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev",
               "name": "Home Page"
            },
            "webReferrer": {
               "URL": ""
            }
         },
         "device": {
            "screenHeight": 1440,
            "screenWidth": 3440,
            "screenOrientation": "landscape"
         },
         "environment": {
            "type": "browser",
            "browserDetails": {
               "viewportWidth": 3440,
               "viewportHeight": 1440
            }
         },
         "placeContext": {
            "localTime": "2022-03-22T22:45:21.193-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-23T04:45:21.193Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "2.8.0+2.9.0",
            "environment": "browser"
         },
         "_experience": {
            "analytics": {
               "customDimensions": {
                  "eVars": {
                     "eVar14": "eVar14"
                  }
               },
               "event1to100": {
                  "event13": {
                     "value": 1
                  },
                  "event14": {
                     "value": 2
                  }
               }
            }
         }
      }
   },
   "data": {
      "page": {
         "pageInfo": {
            "pageName": "Promotions",
            "siteSection": "Home"
         },
         "promos": {
            "heroPromos": "purse,shoes,sunglasses"
         },
         "customVariables": {
            "testGroup": "orange/black theme"
         },
         "events": {
            "homePage": true
         },
         "products": [
            {
               "productSKU": "abc123",
               "productName": "shirt"
            }
         ]
      }
   }
}'
```

### 响应 {#response}

```json
{
   "requestId": "d2ad6364-5675-4a86-ba41-50e7a4c4a299",
   "handle": []
}
```

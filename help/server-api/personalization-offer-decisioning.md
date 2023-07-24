---
title: 通过Offer decisioning进行个性化
description: 了解如何使用服务器API通过Offer decisioning交付和呈现个性化体验。
exl-id: 5348cd3e-08db-4778-b413-3339cb56b35a
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 4%

---

# 通过Offer decisioning进行个性化

## 概述 {#overview}

Edge Network Server API可以提供在中管理的个性化体验 [offer decisioning](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en) 到Web渠道。

[!DNL Offer Decisioning] 支持使用非可视化界面创建、激活和交付您的活动和个性化体验。

## 先决条件 {#prerequisites}

通过以下方式实现个性化 [!DNL Offer Decisioning] 要求您有权访问 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=en) ，然后再配置集成。

## 配置数据流 {#configure-your-datastream}

在将Server API与Offer decisioning结合使用之前，必须在数据流配置上启用Adobe Experience Platform个性化，并启用 **[!UICONTROL offer decisioning]** 选项。

请参阅 [有关向数据流添加服务的指南](../datastreams/overview.md#adobe-experience-platform-settings)，以了解有关如何启用Offer decisioning的详细信息。

![显示“数据流服务配置”屏幕(已选择Offer decisioning)的UI图像](assets/aep-od-datastream.png)

## 受众创建 {#audience-creation}

[!DNL Offer Decisioning] 依靠Adobe Experience Platform分段服务来创建受众。 您可以找到相关文档 [!DNL Segmentation Service] [此处](../segmentation/home.md).

## 定义决策范围 {#creating-decision-scopes}

此 [!DNL Offer Decision Engine] 使用Adobe Experience Platform数据和 [实时客户档案](../profile/home.md)，以及 [!DNL Offer Library]，以便在适当的时间将优惠提供给适当的客户和渠道。

要了解有关 [!DNL Offer Decisioning Engine]，请参阅专用的 [文档](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=zh-Hans).

晚于 [配置数据流](#configure-your-datastream)中，您必须定义要在个性化营销活动中使用的决策范围。

[决策范围](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html?lang=en#add-decision-scopes) 是经过Base64编码的JSON字符串，其中包含您所需的活动和版面ID。 [!DNL Offer Decisioning Service] 以在建议优惠时使用。

**决策范围JSON**

```json
{
   "activityId":"xcore:offer-activity:11cfb1fa93381aca",
   "placementId":"xcore:offer-placement:1175009612b0100c"
}
```

**决策范围Base64编码的字符串**

```shell
"eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
```

创建优惠和收藏集后，您需要定义 [决策范围](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html?lang=en#add-decision-scopes).

复制Base64编码的决策范围。 您将在以下位置使用它 `query` 服务器API请求的对象。

![显示Offer decisioningUI的UI图像，突出显示决策范围。](assets/decision-scope.png)

```json
"query":{
   "personalization":{
      "decisionScopes":[
         "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
      ]
   }
}
```

## API调用示例 {#api-example}

**API格式**

```http
POST /ee/v2/interact
```

### 请求 {#request}

下面概述了包含完整XDM对象、数据对象和Offer decisioning查询的完整请求。

>[!NOTE]
>
>此 `xdm` 和 `data` 对象是可选的，只有当您创建的区段满足条件时，才需要Offer decisioning这些对象，条件是在这些对象的任何一个中使用字段。

```shell
curl -X POST 'https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org: {ORG_ID}' \
--header 'Authorization: Bearer {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "event": {
        "xdm": {
            "eventType": "web.webpagedetails.pageViews",
            "identityMap": {
                "ECID": [
                    {
                        "id": "05907638112924484241029082405297151763",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
            },
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
                "version": "1.0",
                "environment": "serverapi"
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
            },
            "__adobe.target": {
                "profile.eyeColor": "brown",
                "profile.hairColor": "brown"
            }
        }
    },
    "query": {
        "personalization": {
            "decisionScopes": [
                "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
            ]
        }
    }
}'
```

### 响应 {#response}

Edge Network将返回类似于下面的响应。

```json
{
   "requestId":"b375077d-7e1d-4c18-b7d3-e4da0fb4fbc5",
   "handle":[
      {
         "payload":[
            
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "id":"120d5db7-181c-42c5-8653-88b3cd3e1e69",
               "scope":"eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9",
               "activity":{
                  "id":"xcore:offer-activity:14efca8941895181",
                  "etag":"1"
               },
               "placement":{
                  "id":"xcore:offer-placement:12d544ae54e7e7db",
                  "etag":"1"
               },
               "items":[
                  {
                     "id":"xcore:personalized-offer:14efc848a3577d92",
                     "etag":"2",
                     "schema":"https://ns.adobe.com/experience/offer-management/content-component-json",
                     "data":{
                        "id":"xcore:personalized-offer:14efc848a3577d92",
                        "format":"application/json",
                        "language":[
                           "en-us"
                        ],
                        "content":"{\n\t\"ODEFirstTest\" : \"Personalizaton Content\"\n}",
                        "characteristics":{
                           "reporting":"testRequest"
                        }
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCLr6xb39LxgBKgNPUjLwAbr6xb39Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

如果访客根据发送给的数据符合个性化活动的条件 [!DNL Offer Decisioning]，相关活动内容将位于 `handle` 对象，其中类型为 `personalization:decisions`.

其他内容将返回到 `handle` 个对象。 其他内容类型与 [!DNL Offer Decisioning] 个性化。 如果访客符合多个活动的条件，则这些活动将包含在数组中。

下表说明了响应中该部分的关键要素。

| 属性 | 描述 | 示例 |
|---|---|---|
| `scope` | 与返回的建议优惠关联的决策范围。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 优惠活动的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | 优惠投放的唯一ID。 | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | 建议优惠的唯一ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 与建议选件关联的内容的架构。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 建议优惠的唯一ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 与建议选件关联的内容的格式。 | `"format": "text/html"` |
| `language` | 与建议选件中的内容关联的一系列语言。 | `"language": [ "en-US" ]` |
| `content` | 以字符串格式与建议选件关联的内容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式显示的与建议选件关联的图像内容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 包含与建议选件关联的特性的JSON对象。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

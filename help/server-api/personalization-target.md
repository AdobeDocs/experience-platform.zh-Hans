---
title: 通过Adobe Target进行个性化
description: 了解如何使用服务器API来交付和渲染在Adobe Target中创建的个性化体验。
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---

# 通过Adobe Target进行个性化

## 概述 {#overview}

Edge Network Server API可以投放和渲染在Adobe Target中创建的个性化体验，这要借助 [基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

>[!IMPORTANT]
>
>通过创建的个性化体验 [Target可视化体验编辑器(VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) 服务器API不完全支持。 服务器API可以 **retrieve** 由VEC创建的活动，但服务器API无法 **渲染** VEC创建的活动。 如果要渲染由VEC创建的活动，请实施 [混合个性化](../edge/personalization/hybrid-personalization.md) 使用Web SDK和Edge Network服务器API。

## 配置数据流 {#configure-your-datastream}

在将Server API与Adobe Target结合使用之前，必须对数据流配置启用Adobe Target个性化。

请参阅 [有关向数据流添加服务的指南](../datastreams/overview.md#adobe-target-settings)，以了解有关如何启用Adobe Target的详细信息。

配置数据流时，您可以（可选）提供以下值： [!DNL Property Token]， [!DNL Target Environment ID]、和 [!DNL Target Third Party ID Namespace].

![显示“数据流服务配置”屏幕(已选择Adobe Target)的用户界面图像](assets/target-datastream.png)


## 自定义参数 {#custom-parameters}

中的大多数字段 [!DNL XDM] 每个请求的一部分被序列化为点表示法，然后作为自定义或发送到Target [!DNL mbox] 参数。


### 示例 {#custom-parameters-example}

给定以下XDM示例：

```json
"xdm":{
   "marketing":{
      "campaignGroup":"winter22",
      "campaignName":"homeOwnerPromo22",
      "trackingCode":"hop22"
   }
}
```

在Target中创建受众时，以下值可用作自定义参数：

* `marketing.campaignGroup`
* `marketing.campaignName`
* `marketing.trackingCode`

## Target配置文件更新 {#profile-update}

此 [!DNL Server API] 允许更新Target配置文件。 要更新Target配置文件，请确保配置文件数据在 `data` 部分请求，格式如下：

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## 查询Target活动 {#querying-target-activities}

### 架构 {#schemas}

请求的查询部分确定Target返回的内容。 在 `personalization` 对象， `schemas` 确定Target返回的内容类型。

如果不确定将检索哪类选件，则应将所有四个架构都包含在对边缘网络的个性化查询中：

* **基于HTML的优惠：**
https://ns.adobe.com/personalization/html-content-item
* **基于JSON的选件：**
https://ns.adobe.com/personalization/json-content-item
* **Target重定向优惠**
https://ns.adobe.com/personalization/redirect-item
* **定位DOM操作选件**
https://ns.adobe.com/personalization/dom-action

### 决策范围 {#decision-scopes}

Adobe Target [!DNL mbox] 名称应包含在 `decisionScopes` 数组，以返回相应的内容。

#### 示例 {#decision-scopes-example}

在以下示例中，将请求所有四种选件类型以及一个名为的Target活动 `serverapimbox`.

```json
"query":{
   "personalization":{
      "schemas":[
         "https://ns.adobe.com/personalization/html-content-item",
         "https://ns.adobe.com/personalization/json-content-item",
         "https://ns.adobe.com/personalization/redirect-item",
         "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes":[
         "serverapimbox"
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

下面概述了包含完整XDM对象、配置文件参数以及相应Target查询的完整请求。

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
            },
            "data": {
                "__adobe": {
                    "target": {
                        "profile.eyeColor": "brown",
                        "profile.hairColor": "brown",
                        "profile.shoeColor": "black"
                    }
                }
            }
        }
    },
    "query": {
        "personalization": {
            "schemas": [
                "https://ns.adobe.com/personalization/html-content-item",
                "https://ns.adobe.com/personalization/json-content-item",
                "https://ns.adobe.com/personalization/redirect-item",
                "https://ns.adobe.com/personalization/dom-action"
            ],
            "decisionScopes": [
                "serverapimbox"
            ]
        }
    }
}'
```

### 响应 {#response}

Edge Network将返回类似于下面的响应。

```json
{
   "requestId":"10959bbf-f83d-40e1-9521-d9145f19cdc5",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTQwMjgxIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"serverapimbox",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"140281"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ],
                  "characteristics":{
                     "eventToken":"xycjBJlZhwVV5MN0kMkmoGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
                  }
               },
               "items":[
                  {
                     "id":"282484",
                     "schema":"https://ns.adobe.com/personalization/json-content-item",
                     "meta":{
                        "offer.name":"/server_apiform/experiences/0/pages/0/zones/0/1648103551041",
                        "experience.id":"0",
                        "activity.name":"Server API Form",
                        "activity.id":"140281",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"282484"
                     },
                     "data":{
                        "id":"282484",
                        "format":"application/json",
                        "content":{
                           "value":"a/b json experience a",
                           "platform":"server"
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
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCL-pwpv9LxgBKgNPUjLwAb-pwpv9Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

如果访客根据发送到Adobe Target的数据符合个性化活动的资格，则相关活动内容将位于 `handle` 对象，其中类型为 `personalization:decisions`.

其他内容有时将返回到 `handle` 也是。 其他内容类型与Target个性化无关。 如果访客符合多个活动的条件，则每个活动将是一个单独的 `personalization` 数组中的对象。

下表说明了响应中该部分的关键要素。

| 属性 | 描述 | 示例 |
|---|---|---|
| `scope` | 导致建议优惠的Target mbox名称。 | `"scope": "serverapimbox"` |
| `items[].schema` | 与建议选件关联的内容的架构。 这将与您在创建个性化活动时选择的活动类型相关。 | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | 优惠活动的唯一ID。 通常为6位数。 | `"activity.id": "140281"` |
| `items[].meta.activity.name` | 用户指定的选件活动的名称。 这是在活动创建步骤中提供的。 | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | 个性化体验的唯一ID。 | `"experience.id": "0"` |
| `items[].meta.experience.name` | 个性化体验的唯一名称。 | `"experience.name": "Experience A"` |
| `items[].data.id` | 建议优惠的ID。 | `"id": "282484"` |
| `items[].data.format` | 与建议选件关联的内容的格式。 | `"format: "application/json` |
| `items[].data.content` | 与建议选件关联的内容。 这将用于个性化调用应用程序的内容。 | `"content": "<CONTENT CONFIGURED IN TARGET>"` |

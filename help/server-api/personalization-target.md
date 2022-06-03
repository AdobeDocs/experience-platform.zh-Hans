---
title: 通过Adobe Target进行个性化
description: 了解如何使用服务器API来提供和渲染在Adobe Target中创建的个性化体验
keywords: 个性化；服务器api;Adobe Experience Platform边缘网络；检索个性化；Target;Adobe Target
source-git-commit: 59cb43007c4a7ff125738c21064381cf833063b2
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---


# 通过Adobe Target进行个性化

## 概述 {#overview}

边缘网络服务器API可以借助 [基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

>[!IMPORTANT]
>
>通过 [Target可视化体验编辑器(VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) 服务器API不支持。

## 配置数据流 {#configure-your-datastream}

在将服务器API与Adobe Target结合使用之前，必须对数据流配置启用Adobe Target个性化。

请参阅 [向数据流添加服务的指南](../edge/datastreams/overview.md#adobe-target-settings)，以了解有关如何启用Adobe Target的详细信息。

在配置数据流时，您可以（可选）为 [!DNL Property Token], [!DNL Target Environment ID]和 [!DNL Target Third Party ID Namespace].

![显示数据流服务配置屏幕的UI图像，并选择Adobe Target](assets/target-datastream.png)

您可以在以下选项中进行选择 [!DNL Analytics Logging] 选项：

* **[!DNL Server Side]**:这是 [[!DNL A4T]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=zh-Hans). 选择此选项后，每次Target返回个性化内容时，相关 [!DNL A4T] 数据会根据来自Target个性化引擎的响应自动发送到Analytics。
* **[!DNL Client Side]**:选择此选项后，每次Target返回个性化内容时，相关 [!DNL A4T] 数据将返回给调用应用程序。 如果您打算在Analytics中记录此数据，则需要确保在后续调用中报告此数据 [!DNL Analytics].

   >[!IMPORTANT]
   >
   >除了选择 **[!UICONTROL 客户端]** 在Target配置中，您还必须禁用Analytics，以便边缘网络返回 [!DNL A4T] 返回响应的信息。


## 自定义参数 {#custom-parameters}

中的大多数字段 [!DNL XDM] 每个请求的一部分序列化为点符号，然后作为自定义或 [!DNL mbox] 参数。


### 示例 {#custom-parameters-example}

提供以下XDM示例：

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

* `xdm.marketing.campaignGroup`
* `xdm.marketing.campaignName`
* `xdm.marketing.trackingCode`

## Target配置文件更新 {#profile-update}

的 [!DNL Server API] 用于更新Target配置文件。 要更新Target配置文件，请确保在 `data` 请求的一部分，格式如下：

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

请求的查询部分可确定Target返回的内容。 在 `personalization` 对象， `schemas` 确定Target要返回的内容类型。

如果您不确定将检索哪种选件，则应在对边缘网络的个性化查询中包含所有四个架构：

* **基于HTML的选件：**
https://ns.adobe.com/personalization/html-content-item
* **基于JSON的选件：**
https://ns.adobe.com/personalization/json-content-item
* **Target重定向选件**
https://ns.adobe.com/personalization/redirect-item
* **Target DOM操作选件**
https://ns.adobe.com/personalization/dom-action

### 决策范围 {#decision-scopes}

Adobe Target [!DNL mbox] 名称应包含在 `decisionScopes` 数组来返回相应的内容。

#### 示例 {#decision-scopes-example}

在以下示例中，请求所有四种选件类型以及一个名为 `serverapimbox`.

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

下面概述了一个完整请求，其中包括一个完整的XDM对象、配置文件参数以及相应的Target查询。

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

边缘网络将返回与下面类似的响应。

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

如果访客根据发送到Adobe Target的数据有资格参加个性化活动，则相关活动内容将在 `handle` 对象，其中类型为 `personalization:decisions`.

有时，会在 `handle` 也是。 其他内容类型与Target个性化无关。 如果访客符合多个活动的条件，则每个活动将是一个单独的活动 `personalization` 对象。

下表说明了响应中该部分的关键元素。

| 属性 | 描述 | 示例 |
|---|---|---|
| `scope` | 产生建议选件的Target mbox名称。 | `"scope": "serverapimbox"` |
| `items[].schema` | 与建议的选件关联的内容的架构。 这将与您在创建个性化活动时选择的活动类型相关。 | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | 选件活动的唯一ID。 通常为6位数。 | `"activity.id": "140281"` |
| `items[].meta.activity.name` | 用户指定的选件活动的名称。 在活动创建步骤中提供了此信息。 | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | 个性化体验的唯一ID。 | `"experience.id": "0"` |
| `items[].meta.experience.name` | 个性化体验的唯一名称。 | `"experience.name": "Experience A"` |
| `items[].data.id` | 建议的选件的ID。 | `"id": "282484"` |
| `items[].data.format` | 与建议的选件关联的内容格式。 | `"format: "application/json` |
| `items[].data.content` | 与建议的选件关联的内容。 这将用于个性化调用应用程序的内容。 | `"content": "<CONTENT CONFIGURED IN TARGET>"` |

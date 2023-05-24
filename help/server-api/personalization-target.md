---
title: 透過Adobe Target個人化
description: 瞭解如何使用伺服器API來傳遞和轉譯在Adobe Target中建立的個人化體驗。
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: 091d5440d7346861b7c882fa0a17bd03d528e438
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---

# 透過Adobe Target個人化

## 概述 {#overview}

Edge Network Server API可協助提供和轉譯在Adobe Target中建立的個人化體驗。 [表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

>[!IMPORTANT]
>
>透過建立的個人化體驗 [Target視覺化體驗撰寫器(VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) 伺服器API不完全支援。 伺服器API可以 **retrieve** 由VEC建立的活動，但伺服器API無法 **轉譯** VEC建立的活動。 如果您想要轉譯VEC建立的活動，請實作 [混合個人化](../edge/personalization/hybrid-personalization.md) 使用Web SDK和Edge Network Server API。

## 設定您的資料串流 {#configure-your-datastream}

您必須先在資料流設定上啟用Adobe Target個人化，才能將伺服器API與Adobe Target搭配使用。

請參閱 [新增服務至資料流的指南](../edge/datastreams/overview.md#adobe-target-settings)，以取得如何啟用Adobe Target的詳細資訊。

設定資料流時，您可以（選擇性）提供以下專案的值： [!DNL Property Token]， [!DNL Target Environment ID]、和 [!DNL Target Third Party ID Namespace].

![顯示資料流服務設定畫面的UI影像，其中選取Adobe Target](assets/target-datastream.png)


## 自定义参数 {#custom-parameters}

中的大部分欄位 [!DNL XDM] 每個請求的部分都會序列化為點標籤法，然後以自訂或的形式傳送至Target [!DNL mbox] 引數。


### 示例 {#custom-parameters-example}

提供以下XDM範例：

```json
"xdm":{
   "marketing":{
      "campaignGroup":"winter22",
      "campaignName":"homeOwnerPromo22",
      "trackingCode":"hop22"
   }
}
```

在Target中建立受眾時，下列值將可作為自訂引數使用：

* `xdm.marketing.campaignGroup`
* `xdm.marketing.campaignName`
* `xdm.marketing.trackingCode`

## Target設定檔更新 {#profile-update}

此 [!DNL Server API] 允許更新Target設定檔。 若要更新Target設定檔，請確定設定檔資料已傳入 `data` 請求部分，格式如下：

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## 查詢Target活動 {#querying-target-activities}

### 架构 {#schemas}

請求的查詢部分決定Target傳回的內容。 在 `personalization` 物件， `schemas` 決定Target要傳回的內容型別。

若您不確定要擷取哪一種優惠方案，應在Edge Network的個人化查詢中納入全部四個結構描述：

* **HTML型優惠方案：**
https://ns.adobe.com/personalization/html-content-item
* **JSON型選件：**
https://ns.adobe.com/personalization/json-content-item
* **Target重新導向選件**
https://ns.adobe.com/personalization/redirect-item
* **目標DOM操作選件**
https://ns.adobe.com/personalization/dom-action

### 決定範圍 {#decision-scopes}

Adobe Target [!DNL mbox] 名稱應包含在 `decisionScopes` 陣列，傳回適當的內容。

#### 示例 {#decision-scopes-example}

在以下範例中，會請求所有四種選件型別以及一個名為的Target活動 `serverapimbox`.

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

## API呼叫範例 {#api-example}

**API格式**

```http
POST /ee/v2/interact
```

### 请求 {#request}

包含完整XDM物件、設定檔引數以及適當Target查詢的完整請求概述如下。

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

Edge Network會傳回類似下列的回應。

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

如果訪客根據傳送至Adobe Target的資料符合個人化活動的資格，相關活動內容將會位於 `handle` 物件，其中型別為 `personalization:decisions`.

其他內容有時會傳回到 `handle` 以及。 其他內容型別與Target個人化無關。 如果訪客符合多個活動的資格，則每個活動將是一個單獨的 `personalization` 物件。

下表說明該部分回應的主要元素。

| 属性 | 描述 | 示例 |
|---|---|---|
| `scope` | 產生建議優惠方案的Target mbox名稱。 | `"scope": "serverapimbox"` |
| `items[].schema` | 與建議選件相關聯的內容結構描述。 這會與您建立個人化活動時選取的活動型別相關。 | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | 優惠活動的唯一ID。 通常是6位數的數字。 | `"activity.id": "140281"` |
| `items[].meta.activity.name` | 使用者指定的優惠方案活動的名稱。 這會在活動建立步驟期間提供。 | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | 個人化體驗的唯一識別碼。 | `"experience.id": "0"` |
| `items[].meta.experience.name` | 個人化體驗的唯一名稱。 | `"experience.name": "Experience A"` |
| `items[].data.id` | 建議優惠方案的ID。 | `"id": "282484"` |
| `items[].data.format` | 與建議選件相關聯的內容格式。 | `"format: "application/json` |
| `items[].data.content` | 與建議優惠方案相關的內容。 這將用於呼叫應用程式內容的個人化。 | `"content": "<CONTENT CONFIGURED IN TARGET>"` |

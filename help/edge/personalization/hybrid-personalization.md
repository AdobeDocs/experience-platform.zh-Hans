---
title: 使用Web SDK和Edge Network Server API的混合個人化
description: 本文示範如何搭配使用Web SDK與伺服器API，在Web屬性上部署混合式個人化。
keywords: 個人化；混合；伺服器api；伺服器端；混合實作；
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 3%

---

# 使用Web SDK和Edge Network Server API的混合個人化

## 概述 {#overview}

Hybdrid個人化會說明在伺服器端擷取個人化內容的程式，使用 [Edge Network Server API](../..//server-api/overview.md)，並在使用者端轉譯，使用 [Web SDK](../home.md).

您可以將混合式個人化與Adobe Target或Offer Decisioning等個人化解決方案搭配使用，兩者的差異在於其內容 [!UICONTROL 伺服器API] 裝載。

## 先决条件 {#prerequisites}

在您的Web屬性上實作混合個人化之前，請確定您符合下列條件：

* 您已決定要使用的個人化解決方案。 這會對「 」的內容產生影響 [!UICONTROL 伺服器API] 裝載。
* 您有應用程式伺服器的存取權，您可以使用該應用程式伺服器來 [!UICONTROL 伺服器API] 呼叫。
* 您有權存取 [Edge Network Server API](../../server-api/authentication.md).
* 您已正確 [已設定和部署](../fundamentals/configuring-the-sdk.md) 您想要個人化的頁面上的Web SDK。

## 流程圖 {#flow-diagram}

以下流程圖說明傳遞混合式個人化的步驟順序。

![顯示傳遞混合式個人化步驟順序的視覺流程圖。](assets/hybrid-personalization-diagram.png)

1. 之前由瀏覽器儲存的任何現有Cookie，都會加上前置詞 `kndctr_`，已包含在瀏覽器請求中。
1. 使用者端網頁瀏覽器會向您的應用程式伺服器要求網頁。
1. 應用程式伺服器收到頁面請求時，會發出 `POST` 向以下專案提出的請求： [伺服器API互動式資料收集端點](../../server-api/interactive-data-collection.md) 以擷取個人化內容。 此 `POST` 請求包含 `event` 和 `query`. 上一步的Cookie （如果有的話）會包含在 `meta>state>entries` 陣列。
1. 伺服器API會將個人化內容傳回至您的應用程式伺服器。
1. 應用程式伺服器會傳回HTML回應給使用者端瀏覽器，其中包含 [身分和叢集Cookie](#cookies).
1. 在使用者端頁面上， [!DNL Web SDK] `applyResponse` 命令稱為，傳入的標題和內文中 [!UICONTROL 伺服器API] 上一步的回應。
1. 此 [!DNL Web SDK] 轉譯頁面載入 [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) 會自動選件，因為 `renderDecisions` 標幟已設定為 `true`.
1. 表單式 [!DNL JSON] 優惠方案是透過以下方式手動套用： `applyPersonalization` 方法，更新 [!DNL DOM] 根據個人化選件而定。
1. 對於表單式活動，必須手動傳送顯示事件，以指出何時已顯示選件。 這是透過 `sendEvent` 命令。

## Cookie {#cookies}

Cookie可用來儲存使用者身分和叢集資訊。  使用混合實作時，Web應用程式伺服器會在請求生命週期期間處理這些Cookie的儲存和傳送。

| Cookie | 用途 | 儲存者 | 傳送者 |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | 包含使用者身分詳細資訊。 | 应用程序服务器 | 应用程序服务器 |
| `kndctr_AdobeOrg_cluster` | 指出應使用哪一個Edge Network叢集來執行要求。 | 应用程序服务器 | 应用程序服务器 |

## 請求位置 {#request-placement}

需要伺服器API請求才能取得主張並傳送顯示通知。 使用混合實作時，應用程式伺服器會向伺服器API提出這些要求。

| 请求 | 製作者 |
|---|---|
| 擷取主張的互動請求 | 应用程序服务器 |
| 傳送顯示通知的Interact請求 | 应用程序服务器 |

## 分析影響 {#analytics}

實作混合個人化時，您必須特別注意，才不會在Analytics中多次計算頁面點選。

當您 [設定資料串流](../datastreams/overview.md) 對於Analytics，會自動轉送事件，以便擷取頁面點選。

此實作的範例使用兩個不同的資料串流：

* 為Analytics設定的資料串流。 此資料流用於Web SDK互動。
* 沒有Analytics設定的第二個資料串流。 此資料流用於伺服器API請求。

如此一來，伺服器端要求不會註冊任何Analytics事件，但使用者端要求會註冊。 如此一來，便能正確計算Analytics請求。


## 伺服器端要求 {#server-side-request}

以下範例請求說明您的應用程式伺服器可用來擷取個人化內容的伺服器API請求。

>[!IMPORTANT]
>
>此範例請求使用Adobe Target作為個人化解決方案。 您的請求可能會因您選擇的個人化解決方案而異。


**API格式**

```http
POST /ee/v2/interact
```

### 请求 {#request}

```shell
curl -X POST "https://edge.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Content-Type: text/plain" 
-d '{
   "event":{
      "xdm":{
         "web":{
            "webPageDetails":{
               "URL":"http://localhost/"
            },
            "webReferrer":{
               "URL":""
            }
         },
         "identityMap":{
            "FPID":[
               {
                  "id":"xyz",
                  "authenticatedState":"ambiguous",
                  "primary":true
               }
            ]
         },
         "timestamp":"2022-06-23T22:21:00.878Z"
      },
      "data":{
         
      }
   },
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      },
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/default-content-item",
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "sample-json-offer"
         ]
      }
   },
   "meta":{
      "state":{
         "domain":"localhost",
         "cookiesEnabled":true,
         "entries":[
            {
               "key":"kndctr_XXX_AdobeOrg_identity",
               "value":"abc123"
            },
            {
               "key":"kndctr_XXX_AdobeOrg_cluster",
               "value":"or2"
            }
         ]
      }
   }
}'
```

| 参数 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 可以。 | 用來傳遞互動至Edge Network的資料串流的ID。 請參閱 [資料串流概觀](../datastreams/overview.md) 以瞭解如何設定資料串流。 |
| `requestId` | `String` | 否 | 用於關聯內部伺服器請求的隨機ID。 如果未提供，Edge Network將會產生一個，並在回應中傳回。 |

### 伺服器端回應 {#server-response}

以下範例回應顯示伺服器API回應的外觀。


```json
{
   "requestId":"5c539bd0-33bf-43b6-a054-2924ac58038b",
   "handle":[
      {
         "payload":[
            {
               "id":"XXX",
               "namespace":{
                  "code":"ECID"
               }
            }
         ],
         "type":"identity:result"
      },
      {
         "payload":[
            {
               "..."
            },
            {
               "..."
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      }
   ]
}
```

## 使用者端請求 {#client-request}

在使用者端頁面上， [!DNL Web SDK] `applyResponse` 會呼叫命令，傳入伺服器端回應的標頭和內文。

```js
   alloy("applyResponse", {
      "renderDecisions": true,
      "responseHeaders": {
         "cache-control": "no-cache, no-store, max-age=0, no-transform, private",
         "connection": "close",
         "content-encoding": "deflate",
         "content-type": "application/json;charset=utf-8",
         "date": "Mon, 11 Jul 2022 19:42:01 GMT",
         "server": "jag",
         "strict-transport-security": "max-age=31536000; includeSubDomains",
         "transfer-encoding": "chunked",
         "vary": "Origin",
         "x-adobe-edge": "OR2;9",
         "x-content-type-options": "nosniff",
         "x-konductor": "22.6.78-BLACKOUTSERVERDOMAINS:7fa23f82",
         "x-rate-limit-remaining": "599",
         "x-request-id": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "x-xss-protection": "1; mode=block"
      },
      "responseBody": {
         "requestId": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "handle": [
         {
            "payload": [
               {
               "id": "XXX",
               "namespace": {
                  "code": "ECID"
               }
               }
            ],
            "type": "identity:result"
         },
         {
            "payload": [
               {...}, 
               {...}
            ],
            "type": "personalization:decisions",
            "eventIndex": 0
         }
         ]
      }
   }
   ).then(applyPersonalization("sample-json-offer"));
```

表單式 [!DNL JSON] 優惠方案是透過以下方式手動套用： `applyPersonalization` 方法，更新 [!DNL DOM] 根據個人化選件而定。 對於表單式活動，必須手動傳送顯示事件，以指出何時已顯示選件。 這是透過 `sendEvent` 命令。

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        xdm: {
            eventType: "decisioning.propositionDisplay",
            _experience: {
                decisioning: {
                    propositions: [
                        {
                            id: id,
                            scope: scope,
                            scopeDetails: scopeDetails,
                        },
                    ],
                },
            },
        },
    });
}
```

## 範例應用程式 {#sample-app}

為了協助您實驗並深入瞭解這類個人化，我們提供一個範例應用程式，您可下載並使用它進行測試。 您可以從這裡下載應用程式，以及有關如何使用的詳細說明 [GitHub存放庫](https://github.com/adobe/alloy-samples).

---
title: Platform Web SDK中A4T資料的使用者端記錄
description: 瞭解如何使用Experience PlatformWeb SDK為Adobe Analytics for Target (A4T)啟用使用者端記錄。
seo-title: Client-side logging for A4T data in the Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: target；a4t；記錄；web sdk；體驗；平台；
exl-id: 7071d7e4-66e0-4ab5-a51a-1387bbff1a6d
source-git-commit: de420d3bbf35968fdff59b403a0f2b18110f3c17
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 4%

---

# Platform Web SDK中A4T資料的使用者端記錄

## 概述 {#overview}

Adobe Experience Platform Web SDK可讓您收集 [Adobe Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) 網頁應用程式使用者端的資料。

使用者端記錄表示相關 [!DNL Target] 資料會在使用者端傳回，讓您收集資料並與Analytics共用。 如果您想使用手動將資料傳送至Analytics，則應啟用此選項 [資料插入API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).

>[!NOTE]
>
>使用執行此動作的方法 [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html) 目前正在開發中，將於不久的將來提供。

本文介紹為Web SDK設定使用者端A4T記錄的步驟，並提供常見使用案例的一些實施範例。

## 先决条件 {#prerequisites}

本教學課程假設您熟悉與將Web SDK用於個人化目的相關的基本概念和流程。 如果您需要簡介，請檢閱下列檔案：

* [設定Web SDK](../../../fundamentals/configuring-the-sdk.md)
* [傳送事件](../../../fundamentals/tracking-events.md)
* [呈現個人化內容](../../rendering-personalization-content.md)

## 設定Analytics使用者端記錄 {#set-up-client-side-logging}

以下小節概述如何為您的Web SDK實作啟用Analytics使用者端記錄。

### 啟用Analytics使用者端記錄 {#enable-analytics-client-side-logging}

若要考慮為實作啟用Analytics使用者端記錄，您必須在以下專案中停用Adobe Analytics設定： [資料串流](../../../datastreams/overview.md).

![Analytics資料流設定已停用](../assets/disable-analytics-datastream.png)

### 擷取 [!DNL A4T] 來自SDK的資料並將其傳送到Analytics {#a4t-to-analytics}

為了讓此報告方法正常運作，您必須傳送 [!DNL A4T] 從擷取的相關資料 [`sendEvent`](../../../fundamentals/tracking-events.md) Analytics點選中的命令。

Target Edge計算主張回應時，會檢查是否啟用Analytics使用者端記錄（亦即是否在資料流中停用Analytics）。 如果啟用了使用者端記錄，則系統會在回應中為每個主張新增Analytics代號。

流量看起來類似這樣：

![使用者端記錄流程](../assets/analytics-client-side-logging.png)

以下範例為 `interact` 啟用Analytics使用者端記錄時的回應。 如果主張適用於具有Analytics報告的活動，則會有 `scopeDetails.characteristics.analyticsToken` 屬性。

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            }
          ]
        },
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
            }
          },
          "items": [
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

表單式體驗撰寫器活動的主張可包含相同主張下的內容和點選量度專案。 因此，與其讓單一Analytics Token在中顯示內容， `scopeDetails.characteristics.analyticsToken` 屬性，這些屬性中可以同時指定顯示和點按analytics代號 `scopeDetails.characteristics.analyticsDisplayToken` 和 `scopeDetails.characteristics.analyticsClickToken` 屬性（對應）。

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            },
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

所有值來自 `scopeDetails.characteristics.analyticsToken`以及 `scopeDetails.characteristics.analyticsDisplayToken` （適用於顯示的內容）和 `scopeDetails.characteristics.analyticsClickToken` （用於點選量度）是需要收集並納入的A4T裝載 `tnta` 標籤中的變數 [資料插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) 呼叫。

>[!IMPORTANT]
>
>此 `analyticsToken`， `analyticsDisplayToken`， `analyticsClickToken` 屬性可包含多個Token，串連為以逗號分隔的單一字串。
>
>在下節提供的實施範例中，會反複收集多個Analytics Token。 若要串連Analytics權杖陣列，請使用類似下列的函式：
>
>
```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## 實作範例 {#implementation-examples}

以下小節示範如何針對常見使用案例實作Analytics使用者端記錄。

### 表單式體驗撰寫器活動 {#form-based-composer}

您可以使用Web SDK從以下位置控制主張的執行 [Adobe Target表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 活動。

當您請求特定決定範圍的建議時，傳回的建議包含其適當的Analytics代號。 最佳實務建議鏈結Platform Web SDK `sendEvent` 命令並逐一檢視傳回的主張，以便在同時收集Analytics權杖時執行這些建議。

您可以觸發 `sendEvent` 表單式體驗撰寫器活動範圍的命令，如下所示：

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

從這裡，您必須實作程式碼以執行主張並建構最終將傳送至Analytics的裝載。 以下範例說明 `results.propositions` 可能包含：

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

若要從包含內容專案的主張中擷取Analytics Token，您可以實作類似於以下內容的函式：

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

主張可以有不同型別的專案，如 `schema` 相關專案的屬性。 表單式體驗撰寫器活動支援四種主張專案結構描述：

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` 和 `JSON_SCHEMA` 是反映選件型別的結構描述，而 `MEASUREMENT_SCHEMA` 反映應附加至DOM元素的量度。

訪客實際點按先前顯示內容時，點選量度的Analytics裝載應加以收集，並與內容專案分開傳送至Analytics。

在此情況下，以下用於取得點選量度A4T裝載的協助程式函式將很實用：

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### 實作摘要 {#implementation-summary}

總而言之，透過Platform Web SDK套用表單式體驗撰寫器活動時，必須執行下列步驟：

1. 傳送擷取表單式體驗撰寫器活動選件的事件；
1. 將內容變更套用至頁面；
1. 傳送 `decisioning.propositionDisplay` 通知事件；
1. 從SDK回應中收集Analytics顯示Token，並建構用於Analytics點選的裝載；
1. 使用將裝載傳送至Analytics [資料插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)；
1. 如果在已傳遞的建議中有任何點按量度，則應設定點按接聽程式，以便執行點按時，它會傳送 `decisioning.propositionInteract` 通知事件。 此 `onBeforeEventSend` 應設定處理常式，以便在攔截時 `decisioning.propositionInteract` 事件時，會發生下列動作：
   1. 收集點選Analytics Token來源 `xdm._experience.decisioning.propositions`
   1. 透過將收集的Analytics裝載傳送至Analytics點選 [資料插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)；

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### 視覺化體驗撰寫器活動 {#visual-experience-composer-acitivties}

Web SDK可讓您處理使用編寫的選件 [視覺化體驗撰寫器(VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).

>[!NOTE]
>
>實施此使用案例的步驟非常類似於 [表單式體驗撰寫器活動](#form-based-composer). 如需更多詳細資訊，請參閱上一節。

啟用自動呈現時，您可以從頁面上執行的建議中收集Analytics權杖。 最佳實務建議鏈結Platform Web SDK `sendEvent` 命令並逐一檢視傳回的主張，以篩選Web SDK嘗試呈現的主張。

**示例**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  
  for (var i = 0; i < results.propositions.length; i++) {
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### 使用 `onBeforeEventSend` 處理頁面量度的方式 {#using-onbeforeeventsend}

您可以使用Adobe Target活動在頁面上設定不同的量度，手動附加至DOM或自動附加至DOM （VEC編寫的活動）。 這兩種型別都是延遲的一般使用者在網頁上的互動。

若想解決此問題，最佳作法是使用 `onBeforeEventSend` Adobe Experience Platform Web SDK鉤點。 此 `onBeforeEventSend` 應該使用來設定鉤點 `configure` 命令，和將會反映在透過資料流傳送的所有事件中。

以下範例說明如何 `onBeforeEventSent` 可設定為觸發Analytics點選：

```javascript
alloy("configure", {
  edgeConfigId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## 后续步骤 {#next-steps}

本指南涵蓋Web SDK中A4T資料的使用者端記錄。 請參閱指南： [伺服器端記錄](server-side.md) 以取得如何在Edge Network上處理A4T資料的詳細資訊。

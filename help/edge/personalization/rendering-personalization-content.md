---
title: 使用Adobe Experience Platform Web SDK演算個人化內容
description: 瞭解如何使用Adobe Experience Platform Web SDK呈現個人化內容。
keywords: 個人化；renderDecisions；sendEvent；decisionScopes；主張；
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: c75a8bdeaba67259b5f4b4ce025d5e128d763040
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# 呈現個人化內容

Adobe Experience Platform Web SDK支援從Adobe個人化解決方案擷取個人化內容，包括 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html)， [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=zh-Hans) 和 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=zh-Hans).

此外，Web SDK也透過Adobe Experience Platform個人化目的地(例如 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自訂個人化連線](../../destinations/catalog/personalization/custom-personalization.md). 若要瞭解如何為同頁和下一頁個人化設定Experience Platform，請參閱 [專用指南](../../destinations/ui/configure-personalization-destinations.md).

在Adobe Target中建立的內容 [視覺化體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) 以及Adobe Journey Optimizer [網站行銷活動UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) 可由SDK自動擷取及轉譯。 在Adobe Target中建立的內容 [表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 或Offer decisioning無法由SDK自動轉譯。 相反地，您必須使用SDK請求此內容，然後自行手動轉譯內容。

## 自動呈現內容

將事件傳送至伺服器時，您可以設定 `renderDecisions` 選項至 `true`. 這麼做會強制SDK自動轉譯任何符合自動轉譯資格的個人化內容。

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

個人化內容的呈現是非同步的，因此您不應就特定內容片段何時完成呈現做出假設。

## 手動呈現內容

若要存取任何個人化內容，您可以提供回呼函式，SDK收到來自伺服器的成功回應後，就會呼叫此函式。 您的回撥會獲得 `result` 物件，其中可能包含 `propositions` 包含任何傳回的個人化內容的屬性。 以下是在傳送事件時如何提供回呼函式的範例。

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

在此範例中， `result.propositions`，如果存在的話，是包含與事件相關之個人化主張的陣列。 依預設，它僅包含符合自動演算資格的主張。

此 `propositions` 陣列看起來可能類似於此範例：

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  }
]
```

在此範例中， `renderDecisions` 選項未設定為 `true` 當 `sendEvent` 命令已執行，因此SDK不會嘗試自動轉譯任何內容。 不過，SDK仍會自動擷取符合自動轉譯資格的內容，並會在您想要手動轉譯時提供給您使用。 請注意，每個主張物件都有其 `renderAttempted` 屬性設定為 `false`.

如果您改為設定 `renderDecisions` 選項至 `true` 傳送事件時，SDK會嘗試轉譯任何符合自動轉譯資格的主張（如先前所述）。 因此，每個主張物件都會有其 `renderAttempted` 屬性設定為 `true`. 在此情況下，不需要手動轉譯這些主張。

到目前為止，我們僅討論可自動呈現的個人化內容(亦即在Adobe Target的視覺化體驗撰寫器中或Adobe Journey Optimizer的Web Campaign UI中建立的任何內容)。 擷取任何個人化內容 _not_ 符合自動呈現的條件，您需要透過填入 `decisionScopes` 選項傳送事件。 範圍是字串，可識別您要從伺服器擷取的特定主張。

示例如下：

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

在此範例中，如果在伺服器上找到符合以下條件的建議： `salutation` 或 `discount` 範圍，它們會傳回並包含在 `result.propositions` 陣列。 請注意，符合自動轉譯資格的主張將繼續包含在 `propositions` 陣列，無論您如何設定 `renderDecisions` 或 `decisionScopes` 選項。 此 `propositions` 在此範例中，陣列看起來會類似於以下範例：

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
      "activity": {
        "id": "384456"
      }
    },  
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
      "activity": {
        "id": "384457"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  }
]
```

此時，您可以視需要演算主張內容。 在此範例中，主張符合 `discount` scope是使用Adobe Target的表單式體驗撰寫器建立的HTML主張。 假設您的頁面上有一個元素，其ID為 `daily-special` 並希望從呈現內容 `discount` 中的主張 `daily-special` 元素，請執行下列動作：

1. 從擷取主張 `result` 物件。
1. 循環瀏覽每個主張，尋找具有下列範圍的主張 `discount`.
1. 如果您找到主張，會在主張中的每個專案之間回圈，尋找是HTML內容的專案。 （檢查總比假設要好。）
1. 如果您找到包含HTML內容的專案，請找到 `daily-special` 元素並以個人化內容取代其HTML。
1. 呈現內容後，傳送 `display` 事件。

您的程式碼如下所示：

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['salutation', 'discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  var discountHtml;
  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a signle place to update in the HTML.
        break;  
      }
    }
      // Send a "display" event 
    alloy("sendEvent", {
      xdm: {
        eventType: "decisioning.propositionDisplay",
        _experience: {
          decisioning: {
            propositions: [
              {
                id: discountProposition.id,
                scope: discountProposition.scope,
                scopeDetails: discountProposition.scopeDetails
              }
            ]
          }
        }
      }
    });
  }
});
```


>[!TIP]
>
>如果您使用Adobe Target，領域會對應至伺服器上的mbox，除了它們會一次要求而非個別要求。 一律會傳回全域mbox。

### 管理忽隱忽現情形

SDK提供的設施可供 [管理閃爍](../personalization/manage-flicker.md) 進行個人化程式期間。

## 在單頁應用程式中轉譯主張而不增加量度 {#applypropositions}

此 `applyPropositions` 命令可讓您從以下位置呈現或執行主張陣列： [!DNL Target] 至單頁應用程式，而不增加 [!DNL Analytics] 和 [!DNL Target] 量度。 這樣可提高報表的正確性。

>[!IMPORTANT]
>
>如果 `__view__` 範圍（或網頁表面）已在頁面載入時呈現，其 `renderAttempted` 標幟將設為 `true`. 此 `applyPropositions` 命令不會重新呈現 `__view__` 範圍（或網頁表面）主張具有 `renderAttempted: true` 標幟。

### 使用案例1：重新呈現單頁應用程式檢視主張

下列範例中說明的使用案例會重新呈現先前擷取和轉譯的購物車檢視主張，而不會傳送顯示通知。

在以下範例中， `sendEvent` 命令會在檢視變更時觸發，並將產生的物件儲存為常數。

接下來，當檢視或元件更新時， `applyPropositions` 系統會使用上一個命令中的主張來呼叫命令 `sendEvent` 命令，以重新呈現檢視主張。

```js
var cartPropositions = alloy("sendEvent", {
    renderDecisions: true,
    xdm: {
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
}).then(function(result) {
    var propositions = result.propositions;

    // Collect response tokens, etc.
    return propositions;
});

// Call applyPropositions to re-render the view propositions from the previous sendEvent command.
alloy("applyPropositions", {
    propositions: cartPropositions
});
```

### 使用案例2：沒有選擇器的演算主張

此使用案例適用於透過編寫的活動選件 [!DNL Target Form-based Experience Composer].

您必須在「 」中提供選擇器、動作和範圍 `applyPropositions` 呼叫。

支援 `actionTypes` 為：

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    decisionScopes: ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        propositions: retrievedPropositions,
        metadata: {
            salutation: {
                selector: "#first-form-based-offer",
                actionType: "setHtml"
            },
            discount: {
                selector: "#second-form-based-offer",
                actionType: "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: renderedPropositions
                    }
                }
            }
        });
    });
});
```

如果您沒有為決定範圍提供中繼資料，將不會轉譯關聯的建議。

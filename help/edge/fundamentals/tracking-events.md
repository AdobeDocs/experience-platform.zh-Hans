---
title: 使用Adobe Experience Platform Web SDK追蹤事件
description: 瞭解如何追蹤Adobe Experience Platform Web SDK事件。
keywords: sendEvent；xdm；eventType；datasetId；sendBeacon；傳送信標；documentUnloading；檔案解除安裝；onBeforeEventSend；
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: a6948e3744aa754eda22831a7e68b847eb904e76
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---

# 追蹤事件

若要將事件資料傳送至Adobe Experience Cloud，請使用 `sendEvent` 命令。 此 `sendEvent` 命令是將資料傳送至的主要方式 [!DNL Experience Cloud]，並擷取個人化內容、身分和對象目的地。

傳送至Adobe Experience Cloud的資料分為兩個類別：

* XDM資料
* 非XDM資料

## 傳送XDM資料

XDM資料是一個物件，其內容和結構符合您在Adobe Experience Platform中建立的結構描述。 [進一步瞭解如何建立結構描述。](../../xdm/tutorials/create-schema-ui.md)

任何您想要成為分析、個人化、對象或目的地一部分的XDM資料，都應使用 `xdm` 選項。


```javascript
alloy("sendEvent", {
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

在以下兩種情況之間可能會經過一段時間： `sendEvent` 命令會執行，且當資料傳送至伺服器時（例如，如果Web SDK程式庫尚未完全載入或尚未收到同意）。 如果您要修改任何部分 `xdm` 物件 `sendEvent` 命令，強烈建議您複製 `xdm` 物件 _早於_ 執行 `sendEvent` 命令。 例如：

```javascript
var clone = function(value) {
  return JSON.parse(JSON.stringify(value));
};

var dataLayer = {
  "commerce": {
    "order": {
      "purchaseID": "a8g784hjq1mnp3",
      "purchaseOrderNumber": "VAU3123",
      "currencyCode": "USD",
      "priceTotal": 999.98
    }
  }
};

alloy("sendEvent", {
  "xdm": clone(dataLayer)
});

// This change will not be reflected in the data sent to the 
// server for the prior sendEvent command.
dataLayer.commerce = null;
```

在此範例中，複製資料層的方法是先將資料層序列化為JSON，然後再反序列化。 接著，複製的結果會傳遞至 `sendEvent` 命令。 這麼做可確保 `sendEvent` 命令具有資料層的快照，因為它存在於 `sendEvent` 已執行命令，因此對原始資料層物件的後續修改將不會反映在傳送至伺服器的資料中。 如果您使用事件導向資料層，複製資料可能已自動處理。 例如，如果您使用 [Adobe使用者端資料層](https://github.com/adobe/adobe-client-data-layer/wiki)，則 `getState()` 方法可提供所有先前變更的計算複製快照。 如果您使用Adobe Experience Platform Web SDK標籤擴充功能，系統也會自動處理此專案。

>[!NOTE]
>
>XDM欄位中每個事件可傳送的資料有32 KB的限制。


## 傳送非XDM資料

不符合XDM結構描述的資料應使用 `data` 的選項 `sendEvent` 命令。 Web SDK 2.5.0版及更新版本支援此功能。

如果您需要更新Adobe Target設定檔或傳送Target Recommendations屬性，這將很有用。 [深入瞭解這些Target功能。](../personalization/adobe-target/target-overview.md#single-profile-update)

將來，您可將完整資料層傳送至 `data` 選項並將其對應至XDM伺服器端。

**如何將設定檔和Recommendations屬性傳送至Adobe Target：**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```


### 设置 `eventType` {#event-types}

在XDM ExperienceEvent結構描述中，有一個選填欄位 `eventType` 欄位。 這會保留記錄的主要事件型別。 設定事件型別可協助您區分要傳送的不同事件。 XDM提供數個預先定義的事件型別，您可加以使用，或一律針對使用案例建立自己的自訂事件型別。 請參閱XDM檔案以瞭解 [所有預先定義的事件型別清單](../../xdm/classes/experienceevent.md#eventType).

如果使用標籤擴充功能，這些事件型別將會顯示在下拉式清單中，或者您一律可以傳入而不使用標籤。 它們可作為的一部分傳入 `xdm` 選項。


```javascript
alloy("sendEvent", {
  "xdm": {
    "eventType": "commerce.purchases",
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

或者， `eventType` 可透過以下指令傳遞至事件命令： `type` 選項。 在幕後，這會新增至XDM資料。 擁有 `type` 作為選項，可讓您更輕鬆地設定 `eventType` 而不需要修改XDM裝載。


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 覆寫資料集ID

>[!IMPORTANT]
>
>此 `datasetId` 選項受到支援 `sendEvent` 命令已過時。 若要覆寫資料集ID，請使用 [設定覆寫](../datastreams/overrides.md) 而非。

在某些使用案例中，您可能會想要將事件傳送至設定UI中設定之事件以外的資料集。 為此，您需要將 `datasetId` 上的選項 `sendEvent` 命令：



```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### 新增身分資訊

自訂身分資訊也可以新增到事件中。 另請參閱 [正在擷取Experience CloudID](../identity/overview.md).

## 使用sendBeacon API

在網頁使用者導覽離開之前傳送事件資料可能會很棘手。 如果請求花費太長時間，瀏覽器可能會取消請求。 有些瀏覽器已實作網頁標準API，稱為 `sendBeacon` 以便在此期間更輕鬆地收集資料。 使用時 `sendBeacon`，瀏覽器會在全域瀏覽內容中提出網頁要求。 這表示瀏覽器會在背景提出信標要求，而不會阻擋頁面導覽。 告訴Adobe Experience Platform [!DNL Web SDK] 使用 `sendBeacon`，新增選項 `"documentUnloading": true` 至事件命令。  示例如下：


```javascript
alloy("sendEvent", {
  "documentUnloading": true,
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

瀏覽器已對可傳送的資料量施加限制 `sendBeacon` 一次性。 在許多瀏覽器中，上限為64K。 如果瀏覽器因裝載太大而拒絕事件，則Adobe Experience Platform [!DNL Web SDK] 回覆為使用其一般傳輸方法（例如，擷取）。

## 處理來自事件的回應

如果您想要處理來自事件的回應，可以收到成功或失敗的通知，如下所示：


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
}).then(function(result) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


### 此 `result` 物件

此 `sendEvent` 命令會傳回以解析的Promise `result` 物件。 此 `result` 物件包含下列屬性：

**主張**：訪客符合資格的個人化選件。 [進一步瞭解主張。](../personalization/rendering-personalization-content.md#manually-rendering-content)

**決定**：此屬性已過時。 请改用 `propositions`。

**目的地**：可與外部個人化平台、內容管理系統、廣告伺服器和在客戶網站上執行的其他應用程式共用的Adobe Experience Platform區段。 [進一步瞭解目的地。](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en)

>[!WARNING]
>
>`destinations` 目前為測試版。 檔案和功能可能會有所變更。

## 全域修改事件 {#modifying-events-globally}

如果您想要全域新增、移除或修改事件中的欄位，可以設定 `onBeforeEventSend` callback。  每次傳送事件時，都會呼叫此回呼。  此回呼是在事件物件中傳遞，具有 `xdm` 欄位。  修改 `content.xdm` 以變更隨事件傳送的資料。


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
    // Change existing values
    content.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete content.xdm.web.webReferrer.URL;
    // Or add new values
    content.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` 欄位的設定順序如下：

1. 作為選項傳遞至事件命令的值 `alloy("sendEvent", { xdm: ... });`
2. 自動收集的值。  (請參閱 [自動資訊](../data-collection/automatic-information.md).)
3. 在中進行的變更 `onBeforeEventSend` callback。

關於的一些注意事項 `onBeforeEventSend` 回撥：

* 事件XDM可在回撥期間修改。 傳回callback後，content.xdm和content.data物件的任何修改欄位和值都會隨事件傳送。

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* 如果callback擲回例外狀況，事件的處理作業會中斷，且不會傳送事件。
* 如果callback傳回的布林值 `false`，事件處理作業會停止，不會發生錯誤，且事件不會傳送。 此機制可讓您透過檢查事件資料並傳回，輕鬆忽略某些事件 `false` 是否不應傳送事件。

   >[!NOTE]
   >請務必小心避免在頁面上的第一個事件上傳回false。 在第一個事件中傳回false可能會對個人化產生負面影響。

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

布林值以外的任何傳回值 `false` 將允許事件在回撥後進行處理和傳送。

* 可透過檢查事件型別來篩選事件(請參閱 [事件型別](#event-types).)：

```javascript
    onBeforeEventSend: function(content) {  
      // augments XDM if link click event is to a partner website
      if (
        content.xdm.eventType === "web.webinteraction.linkClicks" &&
        content.xdm.web.webInteraction.URL ===
          "http://example.com/partner-page.html"
      ) {
        content.xdm.partnerWebsiteClick = true;
      }
   }
```

## 潛在的可操作錯誤

傳送事件時，如果傳送的資料太大（完整要求超過32KB），可能會擲回錯誤。 在這種情況下，您需要減少傳送的資料量。

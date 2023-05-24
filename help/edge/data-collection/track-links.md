---
title: 使用Adobe Experience Platform Web SDK追蹤連結
description: 瞭解如何使用Experience Platform Web SDK將連結資料傳送至Adobe Analytics
keywords: adobe analytics；analytics；sendEvent；s.t()；s.tl()；webPageDetails；pageViews；webInteraction；網頁互動；頁面檢視；連結追蹤；連結；追蹤連結；clickCollection；點選集合；
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: 04078a53bc6bdc01d8bfe0f2e262a28bbaf542da
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# 追蹤連結

可以手動設定或追蹤連結 [自動](#automaticLinkTracking). 手動追蹤是透過在底下新增詳細資訊來完成 `web.webInteraction` 結構描述的一部分。 有三個必要的變數：

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value": 1
        },
        "name": "My Custom Link", // Name that shows up in the custom links report
        "URL": "https://myurl.com", // The URL of the link
        "type": "other" // values: other, download, exit
      }
    }
  }
});
```

從2.15.0版開始，Web SDK會擷取 `region` HTML元素的URL編號。 如此可啟用 [Activity Map](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html?lang=zh-Hans) Adobe Analytics的報告功能。

連結型別可以是下列三個值之一：

* **`other`：** 自訂連結
* **`download`：** 下載連結
* **`exit`：** 退出連結

這些值為 [自動對應](adobe-analytics/automatically-mapped-vars.md) 進入Adobe Analytics，如果 [已設定](adobe-analytics/analytics-overview.md) 以達成此目的。

## 自動連結追蹤 {#automaticLinkTracking}

根據預設，Web SDK會擷取、標籤符合條件的連結標籤上的點選次數，並加以記錄。 點按次數會透過擷取 [capture](https://www.w3.org/TR/uievents/#capture-phase) 按一下附加至檔案的事件監聽器。

自動連結追蹤的停用方式如下 [設定](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) Web SDK。

```javascript
clickCollectionEnabled: false
```

### 哪些標籤符合連結追蹤的資格？{#qualifyingLinks}

已完成錨點的自動連結追蹤 `A` 和 `AREA` 標籤之間。 但是，如果這些標籤已附加，則不會考慮用於連結追蹤 `onclick` 處理常式。

### 連結的標籤如何設定？{#labelingLinks}

如果錨點標籤包含下載屬性，或連結結尾是熱門的副檔名，則連結會被標籤為下載連結。 下載連結限定詞可以是 [已設定](../fundamentals/configuring-the-sdk.md) 使用規則運算式：

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

如果連結目標網域與目前不同，則連結會被標籤為退出連結 `window.location.hostname`.

不符合下載或退出連結資格的連結會標示為「其他」。

### 如何篩選連結追蹤值？

透過自動連結追蹤收集的資料，可透過提供 [onBeforeEventSend回呼函式](../fundamentals/tracking-events.md#modifying-events-globally).

為Analytics報表準備資料時，篩選連結追蹤資料會很有用。 自動連結追蹤會擷取連結名稱和連結URL。 在Analytics報表中，連結名稱的優先順序高於連結URL。 如果您想要回報連結URL，則需要移除連結名稱。 下列範例顯示 `onBeforeEventSend` 移除下載連結之連結名稱的函式：

```javascript
alloy("configure", {
  onBeforeEventSend: function(options) {
    if (options
      && options.xdm
      && options.xdm.web
      && options.xdm.web.webInteraction) {
        if (options.xdm.web.webInteraction.type === "download") {
          options.xdm.web.webInteraction.name = undefined;
        }
    }
  }
});
```

從Web SDK 2.15.0版開始，透過自動連結追蹤收集的資料可以透過提供 [onBeforeLinkClickSend回呼函式](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend).

只有在發生自動連結點選事件時，才會執行此回呼函式。

```javascript
alloy("configure", {
  onBeforeLinkClickSend: function(options) {
    if (options.xdm.web.webInteraction.type === "download") {
      options.xdm.web.webInteraction.name = undefined;
    }
  }
});
```

使用篩選連結追蹤事件時 `onBeforeLinkClickSend` 命令，Adobe建議傳回 `false` 不應追蹤的連結點選次數。 任何其他回應都會讓Web SDK將資料傳送至Edge Network。


>[!NOTE]
>
>**當兩個 `onBeforeEventSend` 和 `onBeforeLinkClickSend` 回撥函式已設定，Web SDK會執行 `onBeforeLinkClickSend` 回呼函式以篩選及增強連結點選互動事件，然後按一下 `onBeforeEventSend` 回呼函式。
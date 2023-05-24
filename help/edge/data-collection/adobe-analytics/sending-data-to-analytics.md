---
title: 使用Adobe Experience Platform Web SDK傳送資料至Adobe Analytics
description: 瞭解如何使用Adobe Experience Platform Web SDK將資料傳送至Adobe Analytics。
keywords: adobe analytics；analytics；sendEvent；s.t()；s.tl()；webPageDetails；pageViews；webInteraction；網頁互動；頁面檢視；連結追蹤；連結；追蹤連結；clickCollection；點選集合；
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# 傳送資料至Adobe Analytics

過去，有不同的函式可區分頁面檢視和連結(例如 `s.t(), s.tl()`)，在Web SDK中， `sendEvent` 命令。 您隨事件傳送的資料會決定該資料應該是頁面檢視還是連結。 [進一步瞭解追蹤連結](../track-links.md).

## 傳送頁面檢視

您可以透過設定 `web.webPageDetails.pageViews.value=1` 變數。

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        "pageViews": {
            "value":1
         }
      }
    }
  }
});
```

雖然技術上來說，即使未設定此變數，Analytics仍會記錄頁面檢視，但只要您想要記錄明確在資料中的頁面檢視，且想在未來驗證實作，最佳實務是設定此變數。

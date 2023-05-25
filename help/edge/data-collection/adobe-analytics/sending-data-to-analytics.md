---
title: 使用Adobe Experience Platform Web SDK将数据发送到Adobe Analytics
description: 了解如何使用Adobe Experience Platform Web SDK将数据发送到Adobe Analytics。
keywords: adobe analytics；analytics；sendEvent；s.t()；s.tl()；webPageDetails；pageViews；webInteraction；Web交互；页面查看；链接跟踪；链接；跟踪链接；clickCollection；点击收藏集；
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# 将数据发送到Adobe Analytics

而在过去，区分页面视图和链接有不同的功能(例如， `s.t(), s.tl()`)，在Web SDK中， `sendEvent` 命令。 您通过事件发送的数据决定了它应该是页面查看还是链接。 [了解有关跟踪链接的更多信息](../track-links.md).

## 发送页面查看

您可以通过设置 `web.webPageDetails.pageViews.value=1` 变量。

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

虽然从技术上讲，即使未设置此变量，Analytics也记录一次页面查看，但最佳实践是，当您希望记录明确显示在数据中的页面查看时，设置此变量以在未来验证实施。

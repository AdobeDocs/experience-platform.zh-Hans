---
title: 使用Adobe Experience Platform Web SDK将数据发送到Adobe Analytics
description: 了解如何使用Adobe Experience Platform Web SDK将数据发送到Adobe Analytics。
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction；页面视图；链接跟踪；链接；跟踪链接；clickCollection；单击集合；
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# 向Adobe Analytics发送数据

过去，可以区分页面视图和链接（例如`s.t(), s.tl()`）的函数不同，而在Web SDK中，只有`sendEvent`命令。 您与事件一起发送的数据决定该数据应为页面视图还是链接。 [了解有关跟踪链接的更多信息](../track-links.md)。

## 发送页面视图

可以通过设置`web.webPageDetails.pageViews.value=1`变量来指定页面视图。

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

虽然Analytics在技术上记录了页面视图，即使未设置此变量，但最好在您希望将页面视图记录到数据中并在将来验证您的实施时设置此变量。

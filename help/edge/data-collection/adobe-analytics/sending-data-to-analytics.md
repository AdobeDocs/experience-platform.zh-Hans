---
title: 页面和链接跟踪与Adobe Analytics
seo-title: 使用Adobe Experience PlatformWeb SDK跟踪到Adobe Analytics的链接
description: 了解如何使用Experience PlatformWeb SDK将链接数据发送到Adobe Analytics
seo-description: 了解如何使用Experience PlatformWeb SDK将链接数据发送到Adobe Analytics
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 9e1ad05285b27a9fc8b56db903609add3fef144e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# 向Adobe Analytics发送数据

过去，可以区分页面视图和链接(例如 `s.t(), s.tl()`)的函数不同，在Web SDK中只有命 `sendEvent` 令。 您与事件一起发送的数据决定数据应为页面视图还是链接。 [了解有关跟踪链接的更多信息](../track-links.md)

## 发送页面视图

可以通过设置变量来指定页面视图 `web.webPageDetails.pageViews.value=1` 符。

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

虽然Analytics从技术上记录页面视图，即使未设置此变量，但最好在您希望记录要在数据中明确显示的页面视图以及将来验证您的实施时设置此变量。

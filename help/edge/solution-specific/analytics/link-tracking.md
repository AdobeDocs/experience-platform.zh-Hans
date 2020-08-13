---
title: 页面和链接跟踪与Adobe Analytics
seo-title: 使用Adobe Experience PlatformWeb SDK跟踪到Adobe Analytics的链接
description: 了解如何使用Experience PlatformWeb SDK将链接数据发送到Adobe Analytics
seo-description: 了解如何使用Experience PlatformWeb SDK将链接数据发送到Adobe Analytics
translation-type: tm+mt
source-git-commit: ab73e4d793cf39c29ddca385487bf027002db883
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# 将数据发送到Adobe Analytics

过去，在页面视图和链接(例如， `s.t(), s.tl()`)之间有不同的函数可区分，在Web SDK中只有命 `sendEvent` 令。 您与事件一起发送的数据决定数据应为页面视图还是链接。

## 发送页面视图

可以通过设置变量来指定页面视图 `web.webPageDetails.pageViews.value=1` 符。

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetailsr": {
        "pageViews": {
            "value":1
      }
    }
  }
});
```

虽然分析技术上记录了页面视图，即使未设置此变量，但最好在您希望记录要在数据中明确显示的页面视图并防止将来实施时设置此变量。

## 跟踪链接

链接可通过在模式部分下添加详 `web.webInteraction` 细信息来设置。 有三个必需变量： `web.webInteraction.name`, `web.webInteraction.type` 和 `web.webInteraction.linkClicks.value`。

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value":1
      },
      "name":"My Custom Link", //Name that shows up in the custom links report
      "URL":"https://myurl.com", //the URL of the link
      "type":"other", // values: other, download, exit
    }
  }
});
```

链接类型可以是以下三个值之一：

* **`other`:** 自定义链接
* **`download`:** 下载链接（库可以自动跟踪这些链接）
* **`exit`:** 退出链接

### 自动链接跟踪

Web SDK可通过启用clickCollection自动跟踪所有链接 [点击](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled)。

下载链接会根据常用文件类型自动检测。 可配置下载分类的逻辑。

---
title: 使用Adobe Experience Platform Web SDK跟踪链接
description: 了解如何使用Experience PlatformWeb SDK将链接数据发送到Adobe Analytics
keywords: Adobe Analytics;Analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;Web Interaction；页面查看次数；链接跟踪；链接；跟踪链接；clickCollection；点击收藏集；
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: dac14cd358922b577c71f8d9b7f7c9b7e1b4f87d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 跟踪链接

可以手动设置或跟踪链接 [自动](#automaticLinkTracking). 通过在 `web.webInteraction` 架构的一部分。 有三个必需变量：

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

链接类型可以是以下三个值之一：

* **`other`:** 自定义链接
* **`download`:** 下载链接
* **`exit`:** 退出链接

这些值包括 [自动映射](adobe-analytics/automatically-mapped-vars.md) 进入Adobe Analytics，如果 [已配置](adobe-analytics/analytics-overview.md) 这样做。

## 自动链接跟踪 {#automaticLinkTracking}

默认情况下，Web SDK会捕获、标签和记录对符合条件的链接标记的点击。 通过 [捕获](https://www.w3.org/TR/uievents/#capture-phase) 单击附加到文档的事件侦听器。

自动链接跟踪可通过 [配置](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) Web SDK。

```javascript
clickCollectionEnabled: false
```

### 哪些标记符合链接跟踪的条件？{#qualifyingLinks}

已为锚点完成自动链接跟踪 `A` 和 `AREA` 标记。 但是，如果这些标记附加了 `onclick` 处理程序。

### 链接的标签如何？{#labelingLinks}

如果锚点标记包含下载属性或链接以常用文件扩展名结尾，则将标记为下载链接。 下载链接限定符可以是 [已配置](../fundamentals/configuring-the-sdk.md) 使用正则表达式：

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

如果链接目标域与当前域不同，则会将链接标记为退出链接 `window.location.hostname`.

不符合下载或退出链接资格的链接将标记为“其他”。

### 如何过滤链接跟踪值？

通过提供 [onBeforeEventSend回调函数](../fundamentals/tracking-events.md#modifying-events-globally).

在为Analytics报表准备数据时，过滤链接跟踪数据可能会很有用。 自动链接跟踪可捕获链接名称和链接URL。 在Analytics报表中，链接名称优先于链接URL。 如果您希望报告链接URL，则需要删除链接名称。 以下示例显示了 `onBeforeEventSend` 用于删除下载链接链接名称的函数：

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


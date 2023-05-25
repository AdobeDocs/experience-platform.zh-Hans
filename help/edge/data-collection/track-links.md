---
title: 使用Adobe Experience Platform Web SDK跟踪链接
description: 了解如何使用Experience PlatformWeb SDK将链接数据发送到Adobe Analytics
keywords: adobe analytics；analytics；sendEvent；s.t()；s.tl()；webPageDetails；pageViews；webInteraction；Web交互；页面查看；链接跟踪；链接；跟踪链接；clickCollection；点击收藏集；
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: 04078a53bc6bdc01d8bfe0f2e262a28bbaf542da
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# 跟踪链接

可以手动设置链接或跟踪链接 [自动](#automaticLinkTracking). 手动跟踪可通过在下面添加详细信息来完成 `web.webInteraction` 架构的一部分。 有三个必需变量：

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

从版本2.15.0开始，Web SDK捕获 `region` 点击的HTML元素的URL值。 这样可启用 [Activity Map](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html?lang=zh-Hans) Adobe Analytics中的报表功能。

链接类型可以是以下三个值之一：

* **`other`：** 自定义链接
* **`download`：** 下载链接
* **`exit`：** 退出链接

这些值为 [自动映射](adobe-analytics/automatically-mapped-vars.md) 若为，则进入Adobe Analytics [已配置](adobe-analytics/analytics-overview.md) 才能做到这一点。

## 自动链接跟踪 {#automaticLinkTracking}

默认情况下，Web SDK会捕获、标记和记录符合条件的链接标记的点击次数。 点击量捕获方式 [capture](https://www.w3.org/TR/uievents/#capture-phase) 单击附加到文档的事件侦听器。

可以通过以下方式禁用自动链接跟踪 [配置](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) Web SDK。

```javascript
clickCollectionEnabled: false
```

### 哪些标记符合链接跟踪的条件？{#qualifyingLinks}

对锚点执行自动链接跟踪 `A` 和 `AREA` 标记之间。 但是，如果这些标记具有附件，则不会考虑用于链接跟踪 `onclick` 处理程序。

### 如何标记链接？{#labelingLinks}

如果锚点标记包含下载属性或链接以常用的文件扩展名结尾，则链接被标记为下载链接。 下载链接限定符可以是 [已配置](../fundamentals/configuring-the-sdk.md) 使用正则表达式：

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

如果链接目标域与当前域不同，则链接被标记为退出链接 `window.location.hostname`.

不符合下载或退出链接的条件的链接将标记为“其他”。

### 如何过滤链接跟踪值？

通过自动链接跟踪收集的数据可以通过提供 [onBeforeEventSend回调函数](../fundamentals/tracking-events.md#modifying-events-globally).

在为Analytics报表准备数据时，筛选链接跟踪数据可能很有用。 自动链接跟踪会捕获链接名称和链接URL。 在Analytics报表中，链接名称优先于链接URL。 如果要报告链接URL，则需要删除链接名称。 以下示例显示了 `onBeforeEventSend` 函数中删除下载链接的链接名称：

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

从Web SDK版本2.15.0开始，通过自动链接跟踪收集的数据可以通过提供 [onBeforeLinkClickSend回调函数](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend).

此回调函数仅在发生自动链接点击事件时执行。

```javascript
alloy("configure", {
  onBeforeLinkClickSend: function(options) {
    if (options.xdm.web.webInteraction.type === "download") {
      options.xdm.web.webInteraction.name = undefined;
    }
  }
});
```

使用过滤链接跟踪事件时 `onBeforeLinkClickSend` 命令，Adobe建议返回 `false` 不应跟踪的链接点击量。 任何其他响应都会使Web SDK将数据发送到Edge Network。


>[!NOTE]
>
>**当两个 `onBeforeEventSend` 和 `onBeforeLinkClickSend` 设置了回调函数，Web SDK将运行 `onBeforeLinkClickSend` 用于过滤和增强链接点击交互事件的回调函数，其后跟 `onBeforeEventSend` 回调函数。
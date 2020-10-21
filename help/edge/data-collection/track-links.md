---
title: 链接跟踪与Adobe Analytics
seo-title: 使用Adobe Experience PlatformWeb SDK跟踪到Adobe Analytics的链接
description: 了解如何使用Experience PlatformWeb SDK将链接数据发送到Adobe Analytics
seo-description: 了解如何使用Experience PlatformWeb SDK将链接数据发送到Adobe Analytics
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 2e28fda40a135330054c749d73439448a55db52c
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# 跟踪链接

可以手动设置链接或自动跟踪 [链接](#automaticLinkTracking)。 手动跟踪是通过在模式部分下添加 `web.webInteraction` 详细信息来完成的。 有三个必需变量：

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

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
  }
});
```

链接类型可以是以下三个值之一：

* **`other`:** 自定义链接
* **`download`:** 下载链接
* **`exit`:** 退出链接

## 自动链接跟踪 {#automaticLinkTracking}

默认情况下，Web SDK会捕获、标 [签](#labelingLinks)，并 [单击符](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/webinteraction.schema.md) 合条件的链 [接标](#qualifyingLinks) 记。 单击是通过附加到 [事件](https://www.w3.org/TR/uievents/#capture-phase) 的捕获单击文档监听器捕获的。

可通过配置Web SDK来禁用 [自动](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) 链接跟踪。

```javascript
clickCollectionEnabled: false
```

### 哪些标记可用于链接跟踪？{#qualifyingLinks}

对锚点和标记执行自动 `A` 链接 `AREA` 跟踪。 但是，如果这些标签具有附加的处理函数，则不会考虑这些标签进行链 `onclick` 接跟踪。

### 链接的标签如何？{#labelingLinks}

如果锚点标签包含下载属性或链接以流行的文件扩展名结尾，则链接将标记为下载链接。 下载链接限定符可 [以配置](../fundamentals/configuring-the-sdk.md) ，并设置常规表达式:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

如果链接目标域与当前域不同，则链接将标记为退出链接 `window.location.hostname`。

不符合下载或退出链接条件的链接将标记为“其他”。

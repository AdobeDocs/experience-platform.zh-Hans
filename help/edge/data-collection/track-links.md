---
title: 使用Adobe Experience Platform Web SDK跟踪链接
description: 了解如何使用Experience Platform Web SDK将链接数据发送到Adobe Analytics
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction；页面视图；链接跟踪；链接；跟踪链接；clickCollection；单击集合；
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# 跟踪链接

可以手动设置链接或跟踪[自动](#automaticLinkTracking)。 手动跟踪是通过在模式的`web.webInteraction`部分下添加详细信息来完成的。 有三个必需变量：

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

## 自动链接跟踪{#automaticLinkTracking}

默认情况下，Web SDK捕获、标签和记录对符合条件的链接标记的点击。 单击是通过附加到文档的[capture](https://www.w3.org/TR/uievents/#capture-phase)单击事件侦听器捕获的。

[配置](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) Web SDK可禁用自动链接跟踪。

```javascript
clickCollectionEnabled: false
```

### 哪些标记符合链接跟踪条件？{#qualifyingLinks}

对锚点`A`和`AREA`标记执行自动链接跟踪。 但是，如果这些标签具有附加的`onclick`处理函数，则不会将其考虑用于链接跟踪。

### 链接如何标记？{#labelingLinks}

如果锚点标签包含下载属性或链接以流行的文件扩展名结尾，则链接将标记为下载链接。 下载链接限定符可以[配置为](../fundamentals/configuring-the-sdk.md)，具有常规表达式:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

如果链接目标域与当前`window.location.hostname`不同，则链接将标记为退出链接。

不符合下载或退出链接的链接将标记为“其他”。

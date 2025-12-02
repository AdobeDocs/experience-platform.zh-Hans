---
title: 调试方法
description: 了解如何在Web SDK中切换调试功能。
keywords: 调试web sdk；调试；调试命令；setDebug；debugEnabled；调试
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: aea46e3804d315c1237fc853540771f1b5c2b767
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 调试方法

启用调试后，Web SDK会将消息输出到浏览器控制台，以便帮助您调试实施。 它还支持在使用标记作为实施方法时查看[`_satellite.logger`](../tags/logger.md)条消息的功能。 当您想要了解SDK如何根据您建立的规则和数据元素进行行为时，调试很有价值。

默认情况下，调试处于禁用状态，但可以通过四种不同的方式切换调试。 您可以使用这些方法的任意组合来启用或禁用对开发工作流最方便的调试。

## 在`debugEnabled`命令中使用`configure`

配置扩展时，将`debugEnabled`布尔值设置为true。 此选项通常用于开发环境，因为它可为访问您网站上任何页面的每个人启用调试功能：

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

有关详细信息，请参阅[`debugEnabled`](../js/commands/configure/debugenabled.md)。

## 使用`setDebug`命令

与上述布尔值类似，此命令支持在页面的所有访客中进行调试。

```js
alloy("setDebug", {"enabled": true});
```

有关详细信息，请参阅[`setDebug`](../js/commands/setdebug.md)命令。

## 设置查询字符串参数

可以通过将查询字符串`?alloy_debug=true`添加到任何URL的末尾来启用调试。 例如：

`http://example.com/?alloy_debug=true`

此方法仅适用于您的本地计算机，允许您调试生产网站，而无需为每个人启用调试。 在浏览会话的其余时间或禁用调试之前，均会启用此方式的调试。

## 使用Adobe Experience Platform Debugger

Adobe Experience Platform Debugger是一款功能强大的工具，可检查您的网页并帮助您调试Experience Cloud产品的实施。 您可以从AEP Web SDK部分的配置选项卡启用调试。

![启用调试器](../js/assets/enable-debugging.png)

有关详细信息，请参阅[Adobe Experience Platform Debugger概述](/help/debugger/home.md)。

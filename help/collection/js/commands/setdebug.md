---
title: setDebug
description: 启用或禁用Web SDK调试设置。
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# `setDebug`

`setDebug`命令允许您在Web SDK中进入或退出调试模式。 它是可用于[调试](../../use-cases/debugging.md)的多个选项之一。 Adobe建议在开发环境中或仅在生产环境中的本地计算机上启用调试模式。

调用Web SDK的配置实例时运行`setDebug`命令。 配置对象中的唯一选项是`enabled`，这是一个布尔值，可确定是否启用调试模式。

```js
alloy("setDebug", {"enabled": true});
```

## 使用Web SDK标记扩展设置debug

在实现标记库的页面上的浏览器控制台中调用[`_satellite.setDebug()`](/help/collection/tags/setdebug.md)。 Web SDK标记扩展不提供在标记UI本身中切换调试选项的功能。

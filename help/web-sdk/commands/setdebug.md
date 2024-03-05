---
title: setDebug
description: 启用或禁用Web SDK调试设置。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

此 `setDebug` 命令允许您在Web SDK中进入或退出调试模式。 它是可用于的多个选项之一 [调试](../use-cases/debugging.md). Adobe建议在开发环境中或仅在生产环境中的本地计算机上启用调试模式。

## 使用Web SDK标记扩展设置调试

标记扩展不提供在UI中切换调试选项的功能。 您可以使用JavaScript语法使用自定义代码编辑器，或者在网站上的浏览器控制台中输入JavaScript代码。

## 使用Web SDK JavaScript库设置调试

运行 `setDebug` 命令。 配置对象中的唯一选项是 `enabled`，这是一个布尔值，可确定是否启用调试模式。

```js
alloy("setDebug", {"enabled": true});
```

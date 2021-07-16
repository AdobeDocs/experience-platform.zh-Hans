---
title: Web扩展中的共享模块
description: 了解如何在Adobe Experience Platform中为Web扩展定义共享库模块。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 58%

---

# Web扩展中的共享模块

>[!NOTE]
>
>Adobe Experience Platform Launch正在Experience Platform中被重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../term-updates.md)。

共享模块是一种可用来与其他扩展进行通信的机制。在 JavaScript 实现中，所有共享模块都使用 `turbine` 自由变量提供的 [`getSharedModule`](../turbine.md#shared) 方法进行实例化。

在开发您自己的标记扩展时，您可以定义您希望它提供的任何共享模块。 例如，您可以创建一个以异步方式加载用户 ID 的模块，然后通过 [promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 与其他任何扩展共享用户 ID：

```javascript
var userIdPromise = new Promise(/* load user id, then resolve promise */);
module.exports = userIdPromise;
```

在[扩展清单](../manifest.md)中，必须为此共享模块提供一个名称。如果将其命名为 `user-id-promise`，则其他扩展可以访问此共享模块，如下所示：

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

共享模块可以是您通常能够从 CommonJS 模块导出的任何内容（例如函数、对象、字符串、数字或布尔值）。

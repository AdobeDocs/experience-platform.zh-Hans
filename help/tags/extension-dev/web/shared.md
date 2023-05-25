---
title: Web扩展中的共享模块
description: 了解如何在Adobe Experience Platform中为Web扩展定义共享库模块。
exl-id: ec013a39-966c-43f3-bc36-31198990a17e
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 66%

---

# Web扩展中的共享模块

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

共享模块是一种可用来与其他扩展进行通信的机制。例如，扩展 A 可以异步加载某个数据段，并通过 [promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 将其提供给扩展 B。

在 JavaScript 实现中，所有共享模块都使用 `turbine` 自由变量提供的 [`getSharedModule`](../turbine.md#shared) 方法进行实例化。

即使从未从其他扩展内部调用共享模块，这些共享模块也会包含在标记库中。 为了避免不必要地增加库大小，您应该谨慎公开将作为共享模块的内容。

共享模块没有视图组件。

在开发您自己的标记扩展时，您可以定义您希望它提供的任何共享模块。 例如，您可以创建一个以异步方式加载用户 ID 的模块，然后通过 promise 与其他任何扩展共享用户 ID：

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

在 [扩展清单](../manifest.md)，您必须为此共享模块提供一个名称。 如果将其命名为 `user-id-promise`，则其他扩展可以访问此共享模块，如下所示：

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

共享模块可以是您通常能够从 CommonJS 模块导出的任何内容（例如函数、对象、字符串、数字或布尔值）。

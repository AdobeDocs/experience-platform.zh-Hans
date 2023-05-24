---
title: Web擴充功能中的程式庫模組
description: 瞭解如何在Adobe Experience Platform中為Web擴充功能格式化程式庫模組。
exl-id: 08f2bb01-9071-49c5-a0ff-47d592cc34a5
source-git-commit: b3754c94843f32ba58aa1e020dface1179372de3
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 70%

---

# Web 扩展中的库模块

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

>[!IMPORTANT]
>
>本文档介绍 Web 扩展的库模块格式。如果您正在开发 Edge 扩展，请另外参阅关于[格式化 Edge 扩展模块](../edge/format.md)的指南。

程式庫模組是一段可重複使用的程式碼，由Adobe Experience Platform中的標籤執行階段程式庫內發出的擴充功能所提供。 然後，此程式庫就會在使用者端的網站上執行。 例如，`gesture` 事件类型具有将在客户端网站上运行的库模块，并且可检测用户手势。

库模块的结构为 [CommonJS 模块](https://nodejs.org/api/modules.html#modules-commonjs-modules)。在 CommonJS 模块中，可使用以下变量：

## `require`

您可以使用 `require` 函数来访问：

1. 標籤提供的核心模組。 可以使用 `require('@adobe/reactor-name-of-module')` 来访问这些模块。有关更多信息，请参阅有关可用[核心模块](./core.md)的文档。
1. 扩展中的其他模块。扩展中的任何模块都可以通过相对路径进行访问。相对路径必须以 `./` 或 `../` 开头。

用法示例：

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## `module`

您可以使用一个名为 `module` 的自由变量来导出模块的 API。

用法示例：

```javascript
module.exports = function(…) { … }
```

## `exports` {#exports-variable}

您可以使用一个名为 `exports` 的自由变量来导出模块的 API。

用法示例：

```javascript
exports.sayHello = function(…) { … }
```

这是 `module.exports` 的替代方法，但其用法受到更多限制。请阅读[了解 node.js 中的 module.exports 和 exports](https://www.sitepoint.com/understanding-module-exports-exports-node-js/)，以更好地了解 `module.exports` 和 `exports` 之间的区别，以及使用 `exports` 的相关注意事项。如有疑问，请简化操作并使用 `module.exports` 而不是使用 `exports`。

## 执行和缓存

當標籤執行階段程式庫執行時，會立即「安裝」模組，並快取其匯出。 假设有以下模块：

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` 將會立即記錄，而 `runs when necessary` 只有在標籤引擎呼叫已匯出的函式時，才會記錄。 虽然这对于特定模块而言可能是不必要的，但您可以通过在导出函数之前执行任何必要的设置来利用此功能。

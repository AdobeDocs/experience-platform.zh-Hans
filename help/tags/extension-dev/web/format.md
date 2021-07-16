---
title: Web扩展中的库模块
description: 了解如何在Adobe Experience Platform中设置用于Web扩展的库模块的格式。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 64%

---

# Web 扩展中的库模块

>[!NOTE]
>
>Adobe Experience Platform Launch正在Experience Platform中被重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../term-updates.md)。

>[!IMPORTANT]
>
>本文档介绍 Web 扩展的库模块格式。如果您正在开发 Edge 扩展，请另外参阅关于[格式化 Edge 扩展模块](../edge/format.md)的指南。

库模块是由扩展提供的一段可重用代码，在Adobe Experience Platform的标记运行时库中发出该扩展。 然后，此库在客户端的网站上运行。 例如，`gesture` 事件类型具有将在客户端网站上运行的库模块，并且可检测用户手势。

库模块的结构为 [CommonJS 模块](http://wiki.commonjs.org/wiki/Modules/1.1.1)。在 CommonJS 模块中，可使用以下变量：

## [!DNL require]

您可以使用 `require` 函数来访问：

1. 标记提供的核心模块。 可以使用 `require('@adobe/reactor-name-of-module')` 来访问这些模块。有关更多信息，请参阅有关可用[核心模块](./core.md)的文档。
1. 扩展中的其他模块。扩展中的任何模块都可以通过相对路径进行访问。相对路径必须以 `./` 或 `../` 开头。

用法示例：

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## [!DNL module]

您可以使用一个名为 `module` 的自由变量来导出模块的 API。

用法示例：

```javascript
module.exports = function(…) { … }
```

## [!DNL exports]

您可以使用一个名为 `exports` 的自由变量来导出模块的 API。

用法示例：

```javascript
exports.sayHello = function(…) { … }
```

这是 `module.exports` 的替代方法，但其用法受到更多限制。请阅读[了解 node.js 中的 module.exports 和 exports](https://www.sitepoint.com/understanding-module-exports-exports-node-js/)，以更好地了解 `module.exports` 和 `exports` 之间的区别，以及使用 `exports` 的相关注意事项。如有疑问，请简化操作并使用 `module.exports` 而不是使用 `exports`。

## 执行和缓存

当标记运行时库运行时，将立即“安装”模块并缓存其导出。 假设有以下模块：

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` 将被立即记录，而 `runs when necessary` 则仅在标记引擎调用导出函数后才会被记录。虽然这对于特定模块而言可能是不必要的，但您可以通过在导出函数之前执行任何必要的设置来利用此功能。

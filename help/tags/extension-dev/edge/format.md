---
title: Edge扩展中的库模块
description: Edge属性中标记扩展的格式库模块。
exl-id: 82b98972-6fa2-4143-bcf4-c5dac1ca0e7f
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 80%

---

# Edge 扩展中的库模块

>[!IMPORTANT]
>
>本文档介绍了 Edge 扩展的库模块格式。如果您正在开发 Web 扩展，请另外参阅关于[格式化 Web 扩展模块](../web/format.md)的指南。

库模块是由Adobe Experience Platform（在Edge节点上运行的库）中的标记运行时库内部发出的扩展提供的一段可重用代码。 例如，`sendBeacon` 操作类型将具有一个库模块，该模块将会在 Edge 节点上运行并发送信标。

库模块的结构为 [CommonJS 模块](https://nodejs.org/api/modules.html#modules-commonjs-modules)。在 CommonJS 模块中，可使用以下变量：

## [!DNL require]

`require` 函数可用于访问扩展中的模块。扩展中的任何模块都可以通过相对路径进行访问。相对路径必须以 `./` 或 `../` 开头。

用法示例：

```js
var transformHelper = require('../helpers/transform');
transformHelper.execute({a: 'b'});
```

## [!DNL module]

您可以使用一个名为 `module` 的自由变量来导出模块的 API。

用法示例：

```js
module.exports = (…) => { … }
```

## [!DNL exports]

您可以使用一个名为 `exports` 的自由变量来导出模块的 API。

用法示例：

```js
exports.sayHello = (…) => { … }
```

这是 `module.exports` 的替代方法，但其用法受到更多限制。请阅读[了解 node.js 中的 module.exports 和 exports](https://www.sitepoint.com/understanding-module-exports-exports-node-js/)，以更好地了解 `module.exports` 和 `exports` 之间的区别，以及使用 `exports` 的相关注意事项。如有疑问，请简化操作并使用 `module.exports` 而不是使用 `exports`。

## 服务器端模块签名

由扩展提供的所有模块类型（数据元素、条件或操作）将使用相同的参数进行调用：[context](./context.md)。

```js
exports.sayHello = (context) => { … }
```

---
title: 边缘扩展中的库模块
description: 在边缘属性中为标记扩展设置库模块的格式。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 69%

---

# Edge 扩展中的库模块

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../term-updates.md)。

>[!IMPORTANT]
>
>本文档介绍了 Edge 扩展的库模块格式。如果您正在开发 Web 扩展，请另外参阅关于[格式化 Web 扩展模块](../web/format.md)的指南。

库模块是由Adobe Experience Platform的标记运行时库（在边缘节点上运行的库）内发出的扩展提供的一段可重用代码。 例如，`sendBeacon` 操作类型将具有一个库模块，该模块将会在 Edge 节点上运行并发送信标。

库模块的结构为 [CommonJS 模块](http://wiki.commonjs.org/wiki/Modules/1.1.1)。在 CommonJS 模块中，可使用以下变量：

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

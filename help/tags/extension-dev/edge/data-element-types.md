---
title: 边缘扩展的数据元素类型
description: 了解如何在边缘属性中为标记扩展定义数据元素类型库模块。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 34%

---

# Edge 扩展中的数据元素类型

>[!NOTE]
>
>Adobe Experience Platform Launch正在Experience Platform中被重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../term-updates.md)。

数据元素类型库模块可检索一段数据。模块作者确定如何检索此段数据。 例如，您可以使用数据元素类型来允许Adobe Experience Platform用户从XDM层或其自定义数据层检索一段数据。

>[!IMPORTANT]
>
>本文档介绍 Edge 扩展的数据元素类型。如果您正在开发 Web 扩展，请另外参阅关于 [Web 扩展的数据元素类型](../web/data-element-types.md)的指南。
>
>本文档还假定您熟悉库模块以及它们在标记扩展中的集成方式。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

如果您希望允许用户从自定义数据层检索一段数据，则您的模块可能类似于以下示例。

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

如果要使为数据层返回的数据可由Adobe Experience Platform用户配置，则可以允许用户输入键名称，然后将该名称保存到`settings`对象。 该对象可能如下所示。

```js
{
  keyName: "campaignId"
}
```

要对用户定义的本地存储项名称执行操作，您的模块需要更改为：

```js
module.exports = (context) => {
  const data = context.arc.event.data;
  return data[keyName];
};
```

## 库模块上下文

所有数据元素模块都可以访问在调用模块时提供的 `context` 变量。您可以在[此处](./context.md)了解更多信息。

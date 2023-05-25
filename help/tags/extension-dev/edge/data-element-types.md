---
title: Edge扩展的数据元素类型
description: 了解如何在Edge属性中为标记扩展定义数据元素类型库模块。
exl-id: ddbc3912-1c25-4d21-bde8-e40e583b4278
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 24%

---

# Edge扩展中的数据元素类型

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

在标记中，数据元素是Web或移动页面上数据段的别名，无论数据在服务器收到的事件中的什么位置找到。 数据元素可以被规则引用，并充当访问这些数据段的抽象。当数据的位置在将来发生更改（例如更改包含值的事件键）时，可以重新配置单个数据元素，而引用该数据元素的所有规则都可以保持不变。

数据元素类型由扩展提供，扩展作者可决定如何检索这段数据。 例如，您可以使用数据元素类型，以允许Adobe Experience Platform用户从XDM层或其自定义数据层检索一段数据。

本文档介绍如何在Adobe Experience Platform中为Edge扩展定义数据元素类型。

>[!IMPORTANT]
>
>如果您正在开发Web扩展，请参阅 [Web扩展的数据元素类型](../web/data-element-types.md) 而是。
>
>本文档还假设您熟悉库模块以及库模块在Edge扩展中的集成方式。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

数据元素类型通常包含以下内容：

1. Experience PlatformUI和数据收集UI中显示的视图，允许用户修改数据元素的设置。
2. 在标记运行时库中发出的库模块，用于解释设置并检索数据段。

如果您希望允许用户从自定义数据层检索一段数据，则您的模块可能类似于此示例。

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

如果要让Adobe Experience Platform用户能够配置返回给数据层的数据，则可以允许用户输入键名称，然后将该名称保存到 `settings` 对象。 对象可能如下所示。

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

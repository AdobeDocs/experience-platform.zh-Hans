---
title: Web扩展的数据元素类型
description: 了解如何在Web属性中为标记扩展定义数据元素类型库模块。
exl-id: 3aa79322-2237-492f-82ff-0ba4d4902f70
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 53%

---

# Web扩展的数据元素类型

在数据收集标记中，数据元素本质上是页面上数据段的别名。 此数据可在查询字符串参数、Cookie、DOM元素或其他位置中找到。 数据元素可以被规则引用，并充当访问这些数据段的抽象。

数据元素类型由扩展提供，允许用户配置数据元素，以特定方式访问数据段。 例如，扩展可以提供“本地存储项”数据元素类型，用户可在其中指定本地存储项名称。 当数据元素被规则引用时，扩展将能够使用用户在配置数据元素时提供的本地存储项名称来查找本地存储项值。

本文档介绍如何在Adobe Experience Platform中为Web扩展定义数据元素类型。

>[!IMPORTANT]
>
>如果您正在开发Edge扩展，请另外参阅关于Edge扩展的[数据元素类型](../edge/data-element-types.md)的指南。
>
>本文档还假定您熟悉库模块以及库模块在Web扩展中的集成方式。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

数据元素类型通常包含以下内容：

1. Experience Platform UI和数据收集UI中显示的[视图](./views.md)，允许用户修改数据元素的设置。
2. 在标记运行时库中发出的库模块，用于解释设置并检索数据段。

假设您想要允许用户从名为 `productName` 的本地存储项中检索一段数据。您的模块可能如下所示：

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

如果要让Adobe Experience Platform用户可以配置本地存储项名称，则可以允许用户输入名称，然后将该名称保存到`settings`对象。 该对象可能如下所示：

```js
{
  itemName: "campaignId"
}
```

要对用户定义的本地存储项名称执行操作，您的模块需要更改为：

```js
module.exports = function(settings) {
  return localStorage.getItem(settings.itemName);
}
```

## 默认值支持

请注意，用户可以选择为任何数据元素配置默认值。如果您的数据元素库模块返回值 `undefined` 或 `null`，则它将被自动替换为用户为数据元素配置的默认值。

## 上下文事件数据

如果因为触发了规则而导致检索数据元素（例如数据元素在规则的条件和操作中使用），则会将第二个参数传递给您的模块，其中包含有关触发规则的事件的上下文信息。该参数在某些情况下可能会有所帮助并且可以按如下方式访问：

```js
module.exports = function(settings, event) {
  // event contains information regarding the event that fired the rule
};
```

`event` 对象必须包含以下属性：

| 属性 | 描述 |
| --- | --- |
| `$type` | 描述扩展名称和事件名称的字符串，使用句点连接。例如，`youtube.play`。 |
| `$rule` | 包含有关当前正在执行的规则的信息的对象。该对象必须包含以下子属性：<ul><li>`id`：当前正在执行的规则的 ID。</li><li>`name`：当前正在执行的规则的名称。</li></ul> |

提供触发规则的事件类型的扩展可以选择性地向此 `event` 对象添加任何其他有用信息。

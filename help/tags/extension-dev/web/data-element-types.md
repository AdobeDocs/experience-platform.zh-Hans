---
title: Web扩展的数据元素类型
description: 了解如何在Web属性中为标记扩展定义数据元素类型库模块。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 61%

---

# Edge 扩展的数据元素类型

>[!NOTE]
>
>Adobe Experience Platform Launch正在Experience Platform中被重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../term-updates.md)。

数据元素类型库模块的用途是检索一段数据。 用于此检索的方法是可定制的。 不同的数据元素类型允许Adobe Experience Platform用户从本地存储、Cookie或DOM元素中检索数据。

>[!IMPORTANT]
>
>本文档提供了有关Web扩展的数据元素类型的信息。 如果要开发 Edge 扩展，请另外参阅关于 [Edge 扩展的数据元素类型](../edge/data-element-types.md)的指南。
>
>本文档还假定您熟悉库模块以及它们在标记扩展中的集成方式。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

假设您想要允许用户从名为 `productName` 的本地存储项中检索一段数据。您的模块可能如下所示：

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

如果要使Adobe Experience Platform用户可配置本地存储项名称，则可以允许用户输入名称，然后将该名称保存到`settings`对象。 该对象可能如下所示：

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

---
title: Web扩展的条件类型
description: 了解如何在Web属性中为标记扩展定义条件类型库模块。
exl-id: db504455-858b-4ac8-aa42-de516b0f1d5a
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 57%

---

# Web 扩展的条件类型

在规则的上下文中，会在事件发生后评估条件。 所有条件必须返回 true，规则才会继续处理。例外情况是用户将条件明确放入“例外”存储段中，在这种情况下，该存储段内的所有条件都必须返回false，规则才能继续处理。

例如，扩展可以提供“视区包含”条件类型，用户可在其中指定CSS选择器。 在客户端网站上评估条件时，扩展将能够找到与 CSS 选择器匹配的元素，并返回其中是否有任何元素包含在用户视区中。

本文档介绍如何在Adobe Experience Platform中定义Web扩展的条件类型。

>[!NOTE]
>
>如果您正在开发 Edge 扩展，请另外参阅关于 [Edge 扩展的条件类型](../edge/condition-types.md)的指南。
>
>本文档假设您熟悉库模块以及库模块在Web扩展中的集成方式。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

条件类型通常包含以下内容：

1. Experience Platform UI和数据收集UI中显示的[视图](./views.md)，允许用户修改条件的设置。
2. 在标记运行时库中发出的库模块，用于解释设置并评估条件。

条件类型库模块的一个目标是：评估某些内容是true还是false。 具体评估的内容由您来决定。

例如，如果要评估用户是否位于主机 `example.com` 上，则您的模块可能如下所示：

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

现在，假定您希望可由Adobe Experience Platform用户配置主机名。 您可以允许用户输入主机名，然后将主机名保存到设置对象。该对象可能如下所示：

```js
{
  "hostname": "example.com"
}
```

要对用户定义的主机名执行操作，您的模块需要更改为：

```js
module.exports = function(settings) {
  return document.location.hostname === settings.hostname;
};
```

## 上下文事件数据

第二个参数将传递到您的模块，其中包含与触发规则的事件相关的上下文信息。该参数在某些情况下可能会有所帮助并且可以按如下方式访问：

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

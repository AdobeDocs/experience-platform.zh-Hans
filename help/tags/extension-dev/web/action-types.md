---
title: Web扩展的操作类型
description: 了解如何在Web属性中为标记扩展定义操作类型库模块。
exl-id: d4539132-a72c-40b0-84b6-50cbe3785d2d
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 49%

---

# Web 扩展的操作类型

在数据收集标记的上下文中，操作是在发生规则事件且所有条件都通过评估后执行的操作。

例如，扩展可以提供“显示支持聊天”操作类型，该操作类型可以显示支持聊天对话框，以帮助在注销时可能遇到困难的用户。

本文档介绍如何在Adobe Experience Platform中为Web扩展定义操作类型。

>[!IMPORTANT]
>
>本文档介绍 Web 扩展的操作类型。如果您正在开发 Edge 扩展，请另外参阅关于 [Edge 扩展的操作类型](../edge/action-types.md)的指南。
>
>本文档还假定您熟悉库模块以及库模块在Web扩展中的集成方式。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

操作类型通常包含以下内容：

1. Experience Platform UI和数据收集UI中显示的[视图](./views.md)，允许用户修改操作的设置。
2. 在标记运行时库中发出的库模块，用于解释设置并执行操作。

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

例如，要使Adobe Experience Platform用户可以配置消息，您可以允许用户输入消息并将消息保存到设置对象。 该对象如下所示：

```json
{
  "message": "Thank you for being one of our VIP members!"
}
```

要对用户定义的消息执行操作，您的模块需要更改为：

```js
module.exports = function(settings) {
  alert(settings.message);
}
```

## 上下文事件数据

然后，必须将第二个参数传递到您的模块，其中包含有关触发规则的事件的上下文信息。 该参数在某些情况下可能会有所帮助并且可以按如下方式访问：

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

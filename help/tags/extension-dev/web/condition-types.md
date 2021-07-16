---
title: Web扩展的条件类型
description: 了解如何在Web属性中为标记扩展定义条件类型库模块。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 75%

---

# Web 扩展的条件类型

>[!NOTE]
>
>Adobe Experience Platform Launch正在Experience Platform中被重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../term-updates.md)。

条件类型库模块的一个目标是：评估某件事为 true 还是 false。具体评估的内容由您来决定。

>[!NOTE]
>
>本文档介绍 Web 扩展的条件类型。如果您正在开发 Edge 扩展，请另外参阅关于 [Edge 扩展的条件类型](../edge/condition-types.md)的指南。
>
>本文档还假定您熟悉库模块以及它们在标记扩展中的集成方式。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

例如，如果要评估用户是否位于主机 `example.com` 上，则您的模块可能如下所示：

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

现在，假定您希望可由 Adobe Experience Platform 用户配置主机名。您可以允许用户输入主机名，然后将主机名保存到设置对象。该对象可能如下所示：

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

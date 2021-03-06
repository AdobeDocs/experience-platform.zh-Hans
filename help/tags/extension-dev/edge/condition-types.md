---
title: 边缘扩展的条件类型
description: 了解如何在Adobe Experience Platform中为边缘扩展定义条件类型库模块。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 44%

---

# Edge 扩展的条件类型

>[!NOTE]
>
> Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../term-updates.md)。

在标记规则中，在事件发生后评估条件。 所有条件必须返回 true，规则才会继续处理。条件类型由扩展提供并评估某些内容是true还是false，从而返回布尔值。

例如，扩展可以提供“视区包含”条件类型， 用户可在其中指定 CSS 选择器。在客户端网站上评估条件时，扩展将能够找到与 CSS 选择器匹配的元素，并返回其中是否有任何元素包含在用户视区中。

本文档介绍如何在Adobe Experience Platform中为边缘扩展定义条件类型。

>[!IMPORTANT]
>
>如果您正在开发 Web 扩展，请另外参阅关于 [Web 扩展的条件类型](../web/condition-types.md)的指南。
>
>本文档还假定您熟悉库模块以及它们在边缘扩展中的集成方式。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

条件类型通常包括：

1. 数据收集UI中显示的视图，允许用户修改条件的设置。
2. 标记运行时库中发出的库模块，用于解释设置并评估条件。

例如，如果要评估用户是否位于主机`example.com`上，则您的模块可能如下所示。

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

如果您希望可由用户配置主机名以允许输入主机名并将其保存到设置对象，则该对象可能类似于此示例。

```js
{
  "hostname": "example.com"
}
```

要对用户定义的主机名执行操作，您的模块需要更改为：

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith(settings.hostname);
};
```

## 条件结果

条件模块返回的结果可以是如下内容之一：

1. 布尔值（`true` 或 `false`）。
1. 解析后返回布尔值的 [promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)。

## 库模块上下文

所有条件模块都可以访问在调用模块时提供的 `context` 变量。您可以在[此处](./context.md)了解更多信息。

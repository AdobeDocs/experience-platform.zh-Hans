---
title: 边缘扩展的操作类型
description: 了解如何在边缘属性中为标记扩展定义操作类型库模块。
source-git-commit: 99780f64c8f09acea06e47ebf5cabc762e05cab2
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 36%

---

# Edge 扩展的操作类型

>[!NOTE]
>
>Adobe Experience Platform Launch正在Experience Platform中被重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../term-updates.md)。

在标记规则中，操作是在规则条件通过评估后执行的操作。 操作类型由扩展提供，其效果完全由扩展作者定义。

例如，扩展可以提供“显示支持聊天”操作类型，该操作类型可以显示支持聊天对话框，以帮助在注销时可能遇到困难的用户。

本文档介绍如何在Adobe Experience Platform中为边缘扩展定义操作类型。

>[!IMPORTANT]
>
>如果您正在开发 Web 扩展，请另外参阅关于 [Web 扩展的操作类型](../web/action-types.md)的指南。
>
>本文档还假定您熟悉库模块以及它们在边缘扩展中的集成方式。 如果您需要查看简介，请在返回本指南之前参阅关于[库模块格式](./format.md)的概述。

操作类型通常包括：

1. 数据收集UI中显示的视图，允许用户修改操作的设置。
2. 标记运行时库中发出的库模块，用于解释设置并执行操作。

例如，用于将某些数据转发到第三方端点的模块可能如下所示。

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  return fetch('http://someendpoint.com', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

如果要使用户可配置端点，并允许将端点的输入和持久性添加到模块中的设置对象，则该对象将类似于下面所示。

```json
{
  "endpoint": "http://someendpoint.com"
}
```

要在用户定义的端点上操作，您的模块需要更改为以下示例。

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  const  { endpoint } = settings;
  return fetch(endpoint, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

## 操作结果

操作模块返回的结果可以是任何内容。如果该操作需要执行异步任务，您可以返回一个 [promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)，该 promise 在得到解析后会返回您所需的结果。

操作结果存储在 `ruleStash` 键中，所有模块均可通过 `context` 参数 (`context.arc.ruleStash`) 使用该键。您可以在[此处](./context.md#rulestash)了解关于 `ruleStash` 的更多信息。

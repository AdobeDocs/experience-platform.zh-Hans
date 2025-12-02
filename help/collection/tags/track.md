---
title: track()
description: 触发直接调用规则。
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 2%

---

# `track()`

`_satellite.track()`方法允许您触发[直接调用规则](/help/tags/extensions/client/core/overview.md#direct-call-event)。

>[!IMPORTANT]
>
>Adobe将`_satellite.track()`视为&#x200B;**旧版实现方法**。 虽然现在仍完全支持，但Adobe强烈建议使用更现代的实施实践，例如[Adobe客户端数据层](/help/tags/extensions/client/client-data-layer/overview.md)，这是建议的新实施方法。
>
>如果您选择在您的网站上使用`_satellite.track()`，请&#x200B;**保护每次调用**，以便您的网站不会与标记库紧密耦合。 如果不加保护，则以后删除标记属性会导致对`_satellite`对象的所有引用引发错误。

```ts
_satellite.track(identifier: string, detail?: unknown ): void;
```

当您使用在标记UI中配置的标识符调用`_satellite.track()`时，将立即触发该规则。 调用此方法仅充当规则事件；在执行规则的操作之前，规则的条件仍适用。 多个直接调用规则可以使用相同的标识符，从而允许您使用单个`_satellite.track()`调用同时触发所有这些规则。 即使多个规则共享同一标识符，每个触发的规则仍会在执行操作之前检查其自身的条件。

## 可用字段

`_satellite.track()`方法支持两个参数：

| 名称 | 类型 | 必需 | 描述 |
|---|---|---|---|
| **`identifier`** | `string` | 是 | 直接调用规则标识符。 在标记UI中配置规则时，需要设置此标识符。 |
| **`detail`** | `unknown` | 否 | 包含任何所需信息的可选有效负载。 配置规则时，您可以使用`event.detail` （自定义代码）或`%event.detail%` （支持数据元素表示法的文本字段）访问有效负载。 |

```js
// Trigger rules with the identifier 'example'
if (window._satellite?.track) {
  _satellite.track('example');
}

// Trigger a direct call rule with an optional payload that your tag rule can use
_satellite.track('contact_submit', { name: 'John Doe' });
// When configuring the rule, access the payload field using:
// event.detail.name (custom code block) or
// %event.detail.name% (data element)
```

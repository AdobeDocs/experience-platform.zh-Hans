---
title: 监视器(_M)
description: 添加事件侦听器以调试标记实施。
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# `_monitors`

`_satellite._monitors`对象允许您创建事件侦听器，并在库检测到触发的规则时执行自定义代码。 其主要用途是协助调试实施，以确保规则正确触发。

>[!IMPORTANT]
>
>此对象仅用于调试目的。 请勿将生产逻辑绑定到此对象。 Adobe可随时更改此对象中属性或名称的可用性。

```ts
_satellite._monitors?: {
  ruleTriggered(event: { rule: Rule }): void;
  ruleCompleted(event: { rule: Rule }): void;
  ruleConditionFailed(event: { rule: Rule; condition: Condition }): void;
}[];
```

您可以监听以下事件类型：

## `ruleTriggered`

当事件在处理规则的条件和操作之前触发规则时，将触发此回调函数。 如果此函数触发，则之后不久将触发`ruleCompleted`或`ruleConditionFailed`（互斥）。

## `ruleCompleted`

当规则的条件条件条件成功并且执行了规则的所有操作时，`ruleCompleted`回调函数将在`ruleTriggered`之后触发。

## `ruleConditionFailed`

至少有一个规则条件失败时，`ruleConditionFailed`回调函数会在`ruleTriggered`之后触发。

## `Rule`对象

每个回调函数都公开一个`Rule`对象，该对象提供有关规则本身的信息。

```ts
type Rule = {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}
```

| 名称 | 类型 | 描述 |
|---|---|---|
| **`id`** | `string` | 规则的唯一标识符。 |
| **`name`** | `string` | 规则的友好名称。 |
| **`events`** | `Event[]` | 一个事件数组，您已将其配置为触发规则。 |
| **`conditions`** | `Condition[]` | 您已配置为触发规则的条件数组。 |
| **`actions`** | `Action[]` | 配置为在触发规则时执行的一系列操作。 |

## 示例

在调用标记库加载程序之前，请将以下代码片段添加到`<head>`标记的HTML中：

```html
<script>
  window._satellite ??= {};
  window._satellite._monitors ??= [];
  window._satellite._monitors.push({
    ruleTriggered(event) { console.log('Rule triggered', event.rule);},
    ruleCompleted(event) { console.log('Rule completed', event.rule);},
    ruleConditionFailed(event) { console.log('Rule condition failed', event.rule, event.condition);}
  });
</script>
<script src="https://assets.adobedtm.com/.../launch-EN...js" async></script>
```

由于此时尚未在页面上加载标记库，因此创建了初始`_satellite`对象，并对`_satellite._monitors`上的数组进行了初始化。 然后，该脚本将一个监视器对象添加到该数组。

使用显示器时，请考虑以下提示：

* 请注意，这些调试消息使用`console.log`而不是[`_satellite.logger`](logger.md)，因为挂接是在加载标记库之前创建的。
* 虽然代码示例包含所有三个回调函数，但它们不是必填字段。 在网站上调试规则时，只能包含所需的挂接。
* 允许使用多个监视器，即使对于同一事件也是如此。 如果为单个事件使用多个监视器，则无法保证调用顺序。
* 确保在`_monitors`加载标记库之前创建&#x200B;__。 如果在加载库之后创建这些挂接，则只会捕获从该时间点开始触发的规则。

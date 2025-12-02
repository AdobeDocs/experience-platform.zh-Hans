---
title: getVar()
description: 返回数据元素的值或使用setVar()设置的值。
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---

# `getVar()`

`_satellite.getVar()`方法返回[数据元素](/help/tags/ui/managing-resources/data-elements.md)的当前值或使用[`_satellite.setVar()`](setvar.md)设置的值。 如果数据元素与`setVar()`值共享相同的名称，则数据元素优先。 如果调用的字符串标识符尚不存在，则该方法返回`undefined`。 评估是同步的。

```js
_satellite.getVar(name: string, event?: unknown) => unknown
```

返回值和类型取决于您引用的数据元素类型。 例如，如果调用检索字符串变量的`getVar()`，则返回的类型为`string`。 如果调用返回Web SDK变量数据元素的`getVar()`，则返回的类型是包含该变量中设置的所有属性的`object`。

```js
// Retrieves the value in the `Example` data element
_satellite.getVar('Example');

// Execute custom logic depending on the numeric value in the `cartTotal` data element
const cartValue = Number(_satellite.getVar('cartTotal'));
if (cartValue > 100) {
  _satellite.logger.info('Purchase larger than $100 detected');
}

// Some data elements like Web SDK variables support deeply nested properties
const pageName = _satellite.getVar('Data layer')?.web?.webPageDetails?.name;
if (!pageName) {
  _satellite.logger.warn('Page name is not set');
}

// Custom code data elements support a second argument
// Works in a Launch custom code block where `event` is provided by the rule engine.
const rule = _satellite.getVar('Return event rule', event);
```

## 可用字段

`getVar()`方法支持两个参数。 大多数用例不包含第二个可选参数。

| 名称 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| **`name`** | `string` | 是 | 要检索的数据元素名称。 数据元素名称区分大小写。 |
| **`event`** | `object` | 否 | 触发规则中的事件上下文。 仅用于数据元素使用[自定义代码](/help/tags/ui/managing-resources/data-elements.md#custom-code)或自定义扩展的高级用例。 当事件(例如单击、表单提交或自定义JavaScript调度)触发规则时，此处包含关联的事件对象。 数据元素可以使用此信息返回上下文值，例如已单击元素的详细信息或自定义事件中的属性。 |

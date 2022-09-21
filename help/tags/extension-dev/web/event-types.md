---
title: 适用于Web扩展的事件类型
description: 了解如何在Adobe Experience Platform中为Web扩展定义事件类型库模块。
exl-id: dbdd1c88-5c54-46be-9824-2f15cce3d160
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 30%

---

# Web扩展的事件类型

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

在标记规则中，事件是要使规则触发而必须发生的活动。 例如，Web扩展可以提供“手势”事件类型，用于监控特定鼠标或触摸手势的发生。 一旦该手势发生，事件逻辑就会触发规则。

事件类型库模块旨在检测活动何时发生，然后调用函数以触发关联规则。 检测到的事件是可自定义的。 例如，可以检测用户何时做出特定手势、快速滚动或与某些内容交互。

本文档介绍如何在Adobe Experience Platform中为Web扩展定义事件类型。

>[!NOTE]
>
>本文档假定您熟悉库模块以及它们在Web扩展中的集成方式。 在返回到本指南之前，请参阅关于[库模块格式](./format.md)的概述，以了解实施概况。

事件类型由扩展定义，通常包含以下内容：

1. A [视图](./views.md) 显示在Experience PlatformUI和数据收集UI中，允许用户修改事件的设置。
2. 标记运行时库中发出的库模块，用于解释设置并观看特定活动的发生。

`module.exports` 接受两者 `settings` 和 `trigger` 参数。 这允许自定义事件类型。

```js
module.exports = function(settings, trigger) { … };
```

| 参数 | 描述 |
| --- | --- |
| `settings` | 一个对象，其中包含用户在事件类型视图中配置的任何设置。您对此对象中的内容拥有最终控制权。 |
| `trigger` | 每当应该触发规则时，模块应调用的函数。在 `settings` 对象，a `trigger` 函数和规则。 这意味着您收到的一个规则的触发器函数不能用于触发其他规则。 |

>[!NOTE]
>
>对于每个已配置为使用您的事件类型的规则，都将调用一次导出函数。

以传递5秒的活动为例，5秒后，活动已发生，规则将触发。 模块将类似于此示例。

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

如果要使持续时间可由Adobe Experience Platform用户配置，则需要用于输入并保存设置对象的持续时间的选项。 该对象可能如下所示：

```js
{
  "duration": 25000
}
```

为了在用户定义的持续时间上操作，需要更新模块以包括此功能。

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## 传递上下文事件数据

触发规则时，提供有关所发生事件的更多详细信息通常会非常有用。 创建规则的用户会发现，该信息对于实现特定行为非常有用。例如，如果营销人员想要创建一个规则，即每当用户轻扫屏幕时，都会发送分析信标。 延长期必须提供 `swipe` 事件类型，以便营销人员可以使用此事件类型触发相应的规则。 假设营销人员希望包含信标上发生轻扫的角度，那么在不提供其他信息的情况下，将很难实现这一点。 要提供有关所发生事件的更多信息，请在调用 `trigger` 函数时传递一个对象。例如：

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

接下来，营销人员可通过在文本字段中指定值 `%event.swipeAngle%`，在分析信标中使用该值。另外，他们也可以从其他上下文（例如，自定义代码操作）中访问 `event.swipeAngle`。可以包含其他类型的可选事件信息，这些信息可能会以相同的方式对营销人员有用。

### [!DNL nativeEvent]

如果您的事件类型基于本机事件(例如，如果您的扩展提供了 `click` 事件类型)，建议将 `nativeEvent` 属性，如下所示。

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

这对于尝试从本机事件中访问任何信息（例如，光标的坐标位置）的营销人员会非常有用。

### [!DNL element]

如果元素与发生的事件之间存在紧密联系，则建议将 `element` 属性添加到元素的DOM节点。 例如，如果您的扩展提供 `click` 事件类型，并且您允许营销人员对其进行配置，以便仅在ID为 `herobanner` 中。 在这种情况下，如果用户选择主页横幅，则建议调用 `trigger` 设置 `element` 到主页横幅的DOM节点。

```js
trigger({
  element: element // the value would be the DOM node
});
```

## 遵守规则顺序

标记允许用户对规则进行排序。 例如，用户可能会创建两个规则，这两个规则既使用方向更改事件类型，又自定义规则触发的顺序。 假定Adobe Experience Platform用户指定的订单值为 `2` 规则A中的方向更改事件和顺序值 `1` ，用于规则B中的方向更改事件。这表示当移动设备上的方向发生更改时，规则B应在规则A之前触发（首先触发顺序靠下的规则）。

如前所述，对于每个已配置为使用我们的事件类型的规则，将调用一次我们事件模块中的导出函数。每次调用导出函数时，都会传递一个与特定规则绑定的唯一 `trigger` 函数。在刚才所述的情况中，将使用 `trigger` 函数与规则B绑定，然后再次与 `trigger` 函数绑定到规则A。规则B先于规则A，因为用户为它提供了比规则A更低的顺序值。当我们的库模块检测到方向更改时，务必要将 `trigger` 函数的顺序与提供给库模块的顺序相同。

在下面的示例代码中，请注意当检测到方向更改时，将按照提供给导出函数的相同顺序来调用 trigger 函数：

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  triggers.forEach(function(trigger) {
    trigger();
  });
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

这可以确保遵守用户指定的顺序。

如果实施不当，则会导致以不同的顺序调用 trigger 函数：

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  for (var i = triggers.length - 1; i >= 0; i--) {
    triggers[i]();
  }
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

通常，自然的编程惯例可遵守正确的顺序，但是务必要了解其影响并相应地进行开发。

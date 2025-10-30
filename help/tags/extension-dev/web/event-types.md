---
title: Web扩展的事件类型
description: 了解如何在Adobe Experience Platform中为Web扩展定义事件类型库模块。
exl-id: dbdd1c88-5c54-46be-9824-2f15cce3d160
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 32%

---

# Web扩展的事件类型

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

在标记规则中，事件是指为了让规则触发而必须发生的活动。 例如，Web扩展可以提供“手势”事件类型，用于监视特定鼠标或触摸手势的发生。 一旦该手势发生，事件逻辑就会触发规则。

事件类型库模块可检测活动何时发生，然后调用函数以触发关联的规则。 检测到的事件是可自定义的。 例如，可以检测用户何时做出特定手势、快速滚动或与其他内容交互。

本文档介绍如何在Adobe Experience Platform中为Web扩展定义事件类型。

>[!NOTE]
>
>本文档假设您熟悉库模块以及库模块在Web扩展中的集成方式。 在返回到本指南之前，请参阅关于[库模块格式](./format.md)的概述，以了解实施概况。

事件类型由扩展定义，通常包含以下内容：

1. 在Experience Platform UI和数据收集UI中显示的[视图](./views.md)，允许用户修改事件的设置。
2. 在标记运行时库中发出的库模块，用于解释设置并监视特定活动的发生。

`module.exports`同时接受`settings`和`trigger`参数。 这样可以自定义事件类型。

```js
module.exports = function(settings, trigger) { … };
```

| 参数 | 描述 |
| --- | --- |
| `settings` | 一个对象，其中包含用户在事件类型视图中配置的任何设置。您对此对象中的内容拥有最终控制权。 |
| `trigger` | 每当应该触发规则时，模块应调用的函数。`settings`对象、`trigger`函数和规则之间存在一对一的关系。 这意味着您收到的某个规则的trigger函数不能用于触发其他规则。 |

>[!NOTE]
>
>对于每个已配置为使用您的事件类型的规则，都将调用一次导出函数。

以经过五秒的活动为例，经过五秒后，该活动即会发生，并会触发规则。 该模块将与以下示例类似。

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

如果要让Adobe Experience Platform用户可以配置持续时间，则需要提供用于输入持续时间并将持续时间保存到设置对象的选项。 该对象可能如下所示：

```js
{
  "duration": 25000
}
```

要对用户定义的持续时间执行操作，需要更新模块以包含此持续时间。

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## 传递上下文事件数据

触发规则时，提供有关所发生事件的其他详细信息通常会非常有用。 创建规则的用户会发现，该信息对于实现特定行为非常有用。例如，如果营销人员想要创建一个规则，即每次用户轻扫屏幕时都发送分析信标。 扩展必须提供`swipe`事件类型，以便营销人员可以使用此事件类型触发相应的规则。 假设营销人员希望包含信标上发生轻扫的角度，那么如果不提供更多信息，则很难做到这一点。 要提供有关所发生事件的更多信息，请在调用 `trigger` 函数时传递一个对象。例如：

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

接下来，营销人员可通过在文本字段中指定值 `%event.swipeAngle%`，在分析信标中使用该值。另外，他们也可以从其他上下文（例如，自定义代码操作）中访问 `event.swipeAngle`。可以以相同的方式包括可能对营销人员有用的其他类型的可选事件信息。

### [!DNL nativeEvent]

如果您的事件类型基于本机事件（例如，如果您的扩展提供了`click`事件类型），则建议设置`nativeEvent`属性，如下所示。

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

这对于尝试从本机事件中访问任何信息（例如，光标的坐标位置）的营销人员会非常有用。

### [!DNL element]

如果元素与发生的事件之间存在紧密联系，建议将`element`属性设置为元素的DOM节点。 例如，如果您的扩展提供`click`事件类型，并且您允许营销人员对其进行配置，那么仅在选择ID为`herobanner`的元素时才触发规则。 在这种情况下，如果用户选择主页横幅，则建议调用`trigger`并将`element`设置为主页横幅的DOM节点。

```js
trigger({
  element: element // the value would be the DOM node
});
```

## 遵守规则顺序

标记让用户能够排序规则。 例如，用户可以创建两个规则，这两个规则都使用orientation-change事件类型并自定义触发规则的顺序。 假设Adobe Experience Platform用户在规则A中为方向更改事件指定了顺序值`2`，在规则B中为方向更改事件指定了顺序值`1`。这表示当移动设备上发生方向更改时，规则B应在规则A之前触发（首先触发顺序值较低的规则）。

如前所述，对于每个已配置为使用我们的事件类型的规则，将调用一次我们事件模块中的导出函数。每次调用导出函数时，都会传递一个与特定规则绑定的唯一 `trigger` 函数。在刚才所述的情况中，将调用一次导出函数，其中`trigger`函数与规则B绑定，然后再次调用导出函数，其中`trigger`函数与规则A绑定。规则B先于规则A触发的原因在于用户为它提供了更低的顺序值。当我们的库模块检测到方向更改时，请务必按照提供给库模块的相同顺序调用`trigger`函数。

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

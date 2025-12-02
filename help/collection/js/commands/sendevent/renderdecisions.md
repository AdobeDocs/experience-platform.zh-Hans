---
title: renderDecisions
description: 呈现符合自动呈现条件的个性化内容。
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# `renderDecisions`

`renderDecisions`属性允许您强制Web SDK呈现任何适于自动呈现的个性化内容。

运行`renderDecisions`命令时设置`sendEvent`布尔值。 如果忽略，则此属性默认为`false`。 如果要自动渲染个性化内容，请将此属性设置为`true`。

>[!IMPORTANT]
>
>`renderDecisions`属性与[`documentUnloading`](documentunloading.md)属性不兼容。 避免同时将两个属性设置为`true`。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```

确保将此属性设置为`true`时也包含关联的范围或表面。 这些作用域或表面可以自动请求（例如在页面上的第一个`sendEvent`命令上），也可以显式请求（使用[`personalization.decisionScopes`](personalization.md#personalizationdecisionscopes)或[`personalization.surfaces`](personalization.md#personalizationsurfaces)）。 呈现个性化设置时的一个常见问题是：

1. `sendEvent`命令在页面上提前执行，该命令请求未设置`renderDecisions`的默认个性化（默认为`false`）。 将会获取建议，但不会呈现建议。
1. 稍后在页面上，另一个`sendEvent`触发了`renderDecisions`设置为`true`但不包含任何范围或表面。 由于此第二次调用中没有范围或表面，因此不会呈现任何内容。

您可以通过以下任一方式避免此问题：

* 在第一个`renderDecisions`调用中将`true`设置为`sendEvent`；或
* 将`decisionScopes`设置为`surfaces`时，在后续`sendEvent`调用中显式设置`renderDecisions`或`true`。

## 使用Web SDK标记扩展呈现决策

此属性的Web SDK标记扩展等效项是“[**”操作中的**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields)&#x200B;呈现可视化个性化决策[!UICONTROL Send event]复选框。

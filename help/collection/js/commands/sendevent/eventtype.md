---
title: 事件类型
description: 为sendEvent调用设置事件类型。
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# `eventType`

`eventType`属性允许您定义使用Web SDK发送的事件类型。 此字段最终填充`xdm.eventType`字段。 当您想要区分发送到Adobe的事件类型时，此插件很有价值。

Adobe提供了一些您可以使用的预定义事件类型。 有关预定义值的完整列表，请参阅XDM用户指南中的[的`eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype)可用值。 如果需要，您还可以使用自己的值。

如果在此设置`type`并在`xdm.eventType`对象中设置[`xdm`](xdm.md)，则此字段中的值优先。

运行`eventType`命令时设置`sendEvent`字符串属性。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

## 使用Web SDK标记扩展的事件类型

此属性的Web SDK标记扩展等效项是配置“[**[!UICONTROL Type]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields)”操作时的[!UICONTROL Send event]下拉菜单。

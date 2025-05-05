---
title: 事件类型
description: 为sendEvent调用设置事件类型。
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

`eventType`属性允许您定义使用Web SDK发送的事件类型。 此字段最终填充`xdm.eventType`字段。 当您想要区分发送给Adobe的事件类型时，此插件很有价值。

Adobe提供了一些您可以使用的预定义事件类型。 有关预定义值的完整列表，请参阅XDM用户指南中的`eventType`[&#128279;](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype)的可用值。 如果需要，您还可以使用自己的值。

如果在此设置`type`并在[`xdm`](xdm.md)对象中设置`xdm.eventType`，则此字段中的值优先。

## 使用Web SDK标记扩展配置事件类型

在标记规则的操作中设置&#x200B;**[!UICONTROL Type]**&#x200B;下拉字段。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 规则]**，然后选择所需的规则。
1. 在[!UICONTROL 操作]下，选择现有操作或创建操作。
1. 将[!UICONTROL 扩展]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，并将[!UICONTROL 操作类型]设置为&#x200B;**[!UICONTROL 发送事件]**。
1. 使用&#x200B;**[!UICONTROL 类型]**&#x200B;字段下的下拉列表，或输入您自己的值。
1. 单击&#x200B;**[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库配置事件类型

运行`sendEvent`命令时设置`eventType`字符串属性。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

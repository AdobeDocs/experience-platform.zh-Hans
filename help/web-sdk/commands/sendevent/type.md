---
title: 事件类型
description: 为sendEvent调用设置事件类型。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

此 `eventType` 属性允许您定义使用Web SDK发送的事件类型。 此字段最终填充 `xdm.eventType` 字段。 当您想要区分发送给Adobe的事件类型时，此插件很有价值。

Adobe提供了一些您可以使用的预定义事件类型。 请参阅 [可用的值 `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) ，以获取预定义值的完整列表。 如果需要，您还可以使用自己的值。

如果您同时设置了 `type` 此处和 `xdm.eventType` 在 [`xdm`](xdm.md) 对象，此字段中的值优先。

## 使用Web SDK标记扩展配置事件类型

设置 **[!UICONTROL 类型]** 标记规则操作中的下拉字段。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 规则]**，然后选择所需的规则。
1. 下 [!UICONTROL 操作]，选择现有操作或创建操作。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 操作类型] 到 **[!UICONTROL 发送事件]**.
1. 使用下面的下拉菜单 **[!UICONTROL 类型]** 字段，或输入您自己的值。
1. 单击 **[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库配置事件类型

设置 `eventType` 字符串属性 `sendEvent` 命令。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

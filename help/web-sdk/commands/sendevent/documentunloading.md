---
title: 文档卸载
description: 使用JavaScript sendBeacon API将数据发送到Adobe。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 2%

---

# `documentUnloading`

此 `documentUnloading` 属性允许您使用JavaScript [`sendBeacon`](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/sendBeacon) 将数据发送到Adobe的方法。 如果典型请求花费的时间过长，浏览器可以取消该请求。 您可以告诉Web SDK使用 `sendBeacon` 这样当您离开页面后，请求就会在后台运行。 启用此属性有助于防止卸载时浏览器取消数据请求。

一些浏览器对可以发送的数据量施加了64 KB的限制 `sendBeacon` 一次性。 如果浏览器因有效负载过大而拒绝事件，则Web SDK将回退以使用其常规传输方法。

## 使用Web SDK标记扩展配置文档卸载

启用 **[!UICONTROL 文档将卸载]** 标记规则操作中的复选框。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 规则]**，然后选择所需的规则。
1. 下 [!UICONTROL 操作]，选择现有操作或创建操作。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 操作类型] 到 **[!UICONTROL 发送事件]**.
1. 启用 **[!UICONTROL 文档将卸载]** 中的复选框 [!UICONTROL 数据] 部分。
1. 单击 **[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库配置文档卸载

设置 `documentUnloading` 布尔值 `sendEvent` 命令。 其默认值为 `false`。将此属性设置为 `true` 如果您要使用 `sendBeacon` 将数据发送到Adobe的方法。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
